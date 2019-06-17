---
title: '3단계: PHP를 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a7451a85-18e5-4fd0-bbcb-2f15a1117290
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f4828be81914eddbbb5c26b5a6f65cd8b81d85df
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801442"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-php"></a>3단계: PHP를 사용하는 SQL과 연결된 개념 증명
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="step-1--connect"></a>1 단계: 연결  
  
  
이렇게 **OpenConnection** 위쪽을 따르는 함수의 모든 함수를 호출 합니다.  
  
  
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
  
## <a name="step-2--execute-query"></a>2 단계: 쿼리를 실행 합니다.  
  
합니다 [sqlsrv_query ()](https://php.net/manual/en/function.sqlsrv-query.php) 결과 SQL Database에 대해 쿼리에서 집합을 검색 하는 함수를 사용할 수 있습니다. 이 함수에서 기본적으로 모든 쿼리 및 연결 개체를 수락 하 고 사용 하 여 반복 될 수 있는 결과 집합을 반환 합니다 [sqlsrv_fetch_array ()](https://php.net/manual/en/function.sqlsrv-fetch-array.php)합니다.  
  
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
  
  
## <a name="step-3--insert-a-row"></a>3 단계: 행 삽입  
  
이 예제에서는 실행 하는 방법에에서는 [삽입](../../t-sql/statements/insert-transact-sql.md) 에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 하는 문을 [SQL 주입](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값입니다.    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>4 단계: Rollback 트랜잭션  
  
  
이 코드 예제는 트랜잭션의 사용을 보여 줍니다. 있습니다.  
  
-트랜잭션 시작  
  
-데이터 행을 삽입, 데이터의 다른 행 업데이트  
  
-커밋 트랜잭션 롤백하고 고 삽입 및 업데이트가 성공한 경우 트랜잭션 중 하나, 없는 경우  
  
  
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
