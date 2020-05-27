---
title: '방법: SQLSRV 드라이버를 사용하여 SQL Server 데이터 형식 지정 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b9ddb359c34e929247357713c5c48035a3eed9a9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993361"
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 SQL Server 데이터 형식 지정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 SQLSRV 드라이버를 사용하여 서버에 전송되는 데이터에 대한 SQL Server 데이터 형식을 지정하는 방법을 보여 줍니다. PDO_SQLSRV 드라이버를 사용하는 경우에는 이 항목이 적용되지 않습니다.  
  
SQL Server 데이터 형식을 지정하려면 데이터를 삽입하거나 업데이트하는 쿼리를 준비 또는 실행할 때 선택적 *$params* 배열을 사용해야 합니다. *$params* 배열의 구조체와 구문에 대한 자세한 내용은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)를 참조하세요.  
  
다음 단계는 서버에 데이터를 보낼 때 SQL Server 데이터 형식을 지정하는 방법을 요약합니다.  
  
> [!NOTE]  
> SQL Server 데이터 형식이 지정되지 않으면 기본 형식이 사용됩니다. 기본 SQL Server 데이터 형식에 대한 자세한 내용은 [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md)을 참조하세요.  
  
1.  데이터를 삽입하거나 업데이트하는 Transact-SQL 쿼리를 정의합니다. 쿼리에서 매개 변수 값에 대한 자리 표시자로 물음표(?)를 사용합니다.  
  
2.  Transact-SQL 쿼리의 자리 표시자에 해당하는 PHP 변수를 초기화하거나 업데이트합니다.  
  
3.  쿼리를 준비하거나 실행할 때 사용되는 *$params* 배열을 생성합니다. 또한 *$params* 배열의 각 요소는 SQL Server 데이터 형식을 지정할 때 배열이어야 합니다.  
  
4.  *$params* 배열의 각 하위 배열에서 네 번째 매개 변수로 적절한 **SQLSRV_SQLTYPE_&#42;** 상수를 사용하여 원하는 SQL Server 데이터 형식을 지정합니다. **SQLSRV_SQLTYPE_&#42;** 상수의 전체 목록은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)의 SQLTYPE 섹션을 참조하세요. 예를 들어 아래 코드에서 *$changeDate*, *$rate*및 *$payFrequency* 는 **$params**배열에서 SQL Server 형식 **datetime**, **money** 및 *tinyint* 로 각각 지정됩니다. *$employeeId* 에 대해 SQL Server 형식이 지정되지 않고 정수로 초기화되었기 때문에 기본 SQL Server 형식 **정수** 가 사용됩니다.  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스의 *HumanResources.EmployeePayHistory* 테이블에 데이터를 삽입합니다. *$changeDate*, *$rate*및 *$payFrequency* 매개 변수에 대해 SQL Server 형식이 지정됩니다. 기본 SQL Server 형식이 *$employeeId* 매개 변수에 사용됩니다. 데이터가 성공적으로 삽입된 것을 확인하기 위해 동일한 데이터가 검색되고 표시됩니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)

[방법: PHP 데이터 형식 지정](../../connect/php/how-to-specify-php-data-types.md)

[데이터 형식 변환](../../connect/php/converting-data-types.md)

[방법: 기본 제공 UTF-8 지원을 사용하여 UTF-8 데이터 보내기 및 검색](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
