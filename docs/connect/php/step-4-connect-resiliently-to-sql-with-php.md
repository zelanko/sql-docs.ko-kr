---
title: '4 단계: PHP를 사용 하 여 탄력적으로를 SQL에 연결 | Microsoft Docs'
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8013474f-48e9-43d5-ab89-7b0504044468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b32bbb0df1c5977e814eecca7a1e6d1ddee5eca4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992632"
---
# <a name="step-4-connect-resiliently-to-sql-with-php"></a>4단계: PHP를 사용하여 탄력적으로 SQL에 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  
데모 프로그램은 연결 시도를 시도 하는 동안 일시적인 오류 (이 [부록](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-a-odbc-error-codes)에 나열 된 접두사 ' 08 '이 포함 된 오류 코드)가 다시 시도 될 수 있도록 설계 되었습니다. 그러나 쿼리 명령을 실행 하는 동안 일시적인 오류가 발생 하면 프로그램에서 연결을 삭제 하 고 새 연결을 만든 다음 쿼리 명령을 다시 시도 합니다. 이 디자인을 선택 하지 않는 것이 좋습니다. 데모 프로그램은 사용자에 게 제공 되는 몇 가지 디자인 유연성을 보여 줍니다.  
  
이 코드 샘플의 길이는 주로 예외 catch 논리로 인해 발생 합니다.   
  
[Sqlsrv_query ()](../../connect/php/sqlsrv-query.md) 함수를 사용 하 여 SQL Database에 대 한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 기본적으로 모든 쿼리 및 연결 개체를 허용 하 고 [sqlsrv_fetch_array ()](../../connect/php/sqlsrv-fetch-array.md)를 사용 하 여 반복 될 수 있는 결과 집합을 반환 합니다. 
  
```php

    <?php  
        // Variables to tune the retry logic.    
        $connectionTimeoutSeconds = 30;  // Default of 15 seconds is too short over the Internet, sometimes.  
        $maxCountTriesConnectAndQuery = 3;  // You can adjust the various retry count values.  
        $secondsBetweenRetries = 4;  // Simple retry strategy.  
        $errNo = 0;  
        $serverName = "tcp:yourdatabase.database.windows.net,1433";  
        $connectionOptions = array("Database"=>"AdventureWorks",  
           "Uid"=>"yourusername", "PWD"=>"yourpassword", "LoginTimeout" => $connectionTimeoutSeconds);  
        $conn = null;  
        $arrayOfTransientErrors = array('08001', '08002', '08003', '08004', '08007', '08S01'); 
        for ($cc = 1; $cc <= $maxCountTriesConnectAndQuery; $cc++) {  
            // [A.2] Connect, which proceeds to issue a query command.  
            $conn = sqlsrv_connect($serverName, $connectionOptions);    
            if ($conn === true) {  
                echo "Connection was established";  
                echo "<br>";  
  
                $tsql = "SELECT Name FROM Production.ProductCategory";  
                $stmt = sqlsrv_query($conn, $tsql);  
                if ($stmt === false) {
                    echo "Error in query execution";  
                    echo "<br>";  
                    die(print_r(sqlsrv_errors(), true));  
                }
                while($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {     
                    echo $row['Name'] . "<br/>" ;
                }  
                sqlsrv_free_stmt($stmt);  
                sqlsrv_close( $conn); 
                break;  
            } else {    
                // [A.4] Check whether the error code is on the whitelist of transients.  
                $isTransientError = false;  
                $errorCode = '';
                if (($errors = sqlsrv_errors()) != null) {
                    foreach ($errors as $error) {  
                        $errorCode = $error['code'];
                        $isTransientError = in_array($errorCode, $arrayOfTransientErrors);
                        if ($isTransientError) {
                            break;
                        }
                    }
                }  
                if (!$isTransientError) { 
                    // it is a static persistent error...
                    echo("Persistent error suffered with error code = $errorCode. Program will terminate.");  
                    echo "<br>";  
                    // [A.5] Either the connection attempt or the query command attempt suffered a persistent error condition.  
                    // Break the loop, let the hopeless program end.  
                    exit(0);  
                }  
                // [A.6] It is a transient error from an attempt to issue a query command.  
                // So let this method reloop and try again. However, we recommend that the new query  
                // attempt should start at the beginning and establish a new connection.  
                if ($cc >= $maxCountTriesConnectAndQuery) {  
                    echo "Transient errors suffered in too many retries - $cc. Program will terminate.";  
                    echo "<br>";  
                    exit(0);  
                }  
                echo("Transient error encountered with error code = $errorCode. Program might retry by itself.");    
                echo "<br>";  
                echo "$cc attempts so far. Might retry.";  
                echo "<br>";  
                // A very simple retry strategy, a brief pause before looping.  
                sleep(1*$secondsBetweenRetries);  
            }  
            // [A.3] All has gone well, so let the program end.  
        }  
    ?>
```
