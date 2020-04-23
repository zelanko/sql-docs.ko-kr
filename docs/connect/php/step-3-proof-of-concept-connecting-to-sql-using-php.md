---
title: '3단계: PHP를 사용하여 SQL에 연결'
description: 3단계는 PHP를 사용하여 SQL Server에 연결할 수 있는 방법을 보여 주는 개념 증명입니다. 기본 예제에서는 데이터를 선택하고 삽입하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a7451a85-18e5-4fd0-bbcb-2f15a1117290
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69c8b1ec58dbb40ab6e4463d343720e02e583ac8
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528587"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-php"></a>3단계: PHP를 사용하여 SQL에 연결하는 개념 증명
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="step-1--connect"></a>1단계:  연결  
  
  
이 **OpenConnection** 함수는 이어지는 모든 함수의 거의 최상위에서 호출됩니다.  
  
  
```php 
    function OpenConnection()  
    {  
        try  
        {  
            $serverName = "tcp:myserver.database.windows.net,1433";  
            $connectionOptions = array("Database"=>"AdventureWorks",  
                "Uid"=>"MyUser", "PWD"=>"MyPassword");  
            $conn = sqlsrv_connect($serverName, $connectionOptions);  
            if($conn == false)  
                die(FormatErrors(sqlsrv_errors()));  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="step-2--execute-query"></a>2단계:  쿼리 실행  
  
[sqlsrv_query()](https://php.net/manual/en/function.sqlsrv-query.php) 함수를 사용하여 SQL Database에 대한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 본질적으로 모든 쿼리 및 연결 개체를 허용하며, [sqlsrv_fetch_array()](https://php.net/manual/en/function.sqlsrv-fetch-array.php)를 사용하여 반복될 수 있는 결과 집합을 반환합니다.  
  
```php  
    function ReadData()  
    {  
        try  
        {  
            $conn = OpenConnection();  
            $tsql = "SELECT [CompanyName] FROM SalesLT.Customer";  
            $getProducts = sqlsrv_query($conn, $tsql);  
            if ($getProducts == FALSE)  
                die(FormatErrors(sqlsrv_errors()));  
            $productCount = 0;  
            while($row = sqlsrv_fetch_array($getProducts, SQLSRV_FETCH_ASSOC))  
            {  
                echo($row['CompanyName']);  
                echo("<br/>");  
                $productCount++;  
            }  
            sqlsrv_free_stmt($getProducts);  
            sqlsrv_close($conn);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
  
## <a name="step-3--insert-a-row"></a>3단계:  행 삽입  
  
이 예에서는 [INSERT](../../t-sql/statements/insert-transact-sql.md) 문을 안전하게 실행하고 매개 변수를 전달하는 방법을 확인합니다. 매개 변수 값이 [SQL 삽입](../../relational-databases/tables/primary-and-foreign-key-constraints.md)으로부터 애플리케이션을 보호합니다.
  
```php 
    function InsertData()  
    {  
        try  
        {  
            $conn = OpenConnection();  
  
            $tsql = "INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT            INSERTED.ProductID VALUES ('SQL Server 1', 'SQL Server 2', 0, 0, getdate())";  
            //Insert query  
            $insertReview = sqlsrv_query($conn, $tsql);  
            if($insertReview == FALSE)  
                die(FormatErrors( sqlsrv_errors()));  
            echo "Product Key inserted is :";  
            while($row = sqlsrv_fetch_array($insertReview, SQLSRV_FETCH_ASSOC))  
            {     
                echo($row['ProductID']);  
            }  
            sqlsrv_free_stmt($insertReview);  
            sqlsrv_close($conn);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="step-4--roll-back-a-transaction"></a>4단계:  트랜잭션 롤백  
  
  
이 코드 예제는 다음과 같은 트랜잭션의 사용법을 보여줍니다.  
  
-트랜잭션 시작  
  
-데이터의 행 삽입, 데이터의 다른 행 업데이트  
  
-삽입 및 업데이트가 성공한 경우 트랜잭션 커미트, 둘 중 하나가 성공하지 못한 경우 트랜잭션 롤백  
  
  
```php 
    function Transactions()  
    {  
        try  
        {  
            $conn = OpenConnection();  
  
            if (sqlsrv_begin_transaction($conn) == FALSE)  
                die(FormatErrors(sqlsrv_errors()));  
  
            $tsql1 = "INSERT INTO SalesLT.SalesOrderDetail (SalesOrderID,OrderQty,ProductID,UnitPrice)  
            VALUES (71774, 22, 709, 33)";  
            $stmt1 = sqlsrv_query($conn, $tsql1);  
  
            /* Set up and execute the second query. */  
            $tsql2 = "UPDATE SalesLT.SalesOrderDetail SET OrderQty = (OrderQty + 1) WHERE ProductID = 709";  
            $stmt2 = sqlsrv_query( $conn, $tsql2);  
  
            /* If both queries were successful, commit the transaction. */  
            /* Otherwise, rollback the transaction. */  
            if($stmt1 && $stmt2)  
            {  
                   sqlsrv_commit($conn);  
                   echo("Transaction was commited");  
            }  
            else  
            {  
                sqlsrv_rollback($conn);  
                echo "Transaction was rolled back.\n";  
            }  
            /* Free statement and connection resources. */  
            sqlsrv_free_stmt( $stmt1);  
            sqlsrv_free_stmt( $stmt2);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="additional-examples"></a>추가 예  
  
[예제 애플리케이션(SQLSRV 드라이버)](../../connect/php/example-application-sqlsrv-driver.md)  

[예제 애플리케이션(PDO_SQLSRV 드라이버)](../../connect/php/example-application-pdo-sqlsrv-driver.md)
