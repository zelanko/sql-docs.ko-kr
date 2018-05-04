---
title: '방법: 매개 변수가 있는 쿼리를 수행 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4f6500c630cf7962654654646a1d21bda711c17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-perform-parameterized-queries"></a>방법: 매개 변수가 있는 쿼리 수행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 를 사용하여 매개 변수가 있는 쿼리를 수행하는 방법을 요약하여 보여 줍니다.  
  
매개 변수가 있는 쿼리를 수행하는 단계는 네 단계로 요약할 수 있습니다.  
  
1.  실행할 쿼리인 Transact-SQL 문자열의 매개 변수 자리 표시자로 물음표(?)를 넣습니다.  
  
2.  Transact-SQL 쿼리의 자리 표시자에 해당하는 PHP 변수를 초기화하거나 업데이트합니다.  
  
3.  2 단계의 PHP 변수를 사용 하 여 만들거나 TRANSACT-SQL 문자열의 매개 변수 자리 표시자에 해당 하는 매개 변수 값의 배열을 업데이트 합니다. 배열에 매개 변수 값을 나타내기 위한 자리 표시자와 동일한 순서로 이어야 합니다.
  
4.  다음 쿼리를 실행합니다.  
  
    -   SQLSRV 드라이버를 사용하는 경우 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)를 사용합니다.  
  
    -   PDO_SQLSRV 드라이버를 사용 하는 경우로 쿼리를 실행 [pdo:: prepare](../../connect/php/pdo-prepare.md) 및 [pdostatement:: Execute](../../connect/php/pdostatement-execute.md)합니다. [PDO::prepare](../../connect/php/pdo-prepare.md) 및 [PDOStatement::execute](../../connect/php/pdostatement-execute.md) 에 대한 항목에 코드 예제가 있습니다.  
  
이 항목의 나머지 부분에서는 SQLSRV 드라이버를 사용하여 매개 변수가 있는 쿼리를 설명합니다.  
  
> [!NOTE]  
> 매개 변수는 **sqlsrv_prepare**를 사용합니다. 즉, 매개 변수가 있는 쿼리가 **sqlsrv_prepare** 를 사용하여 준비되고 매개 변수 배열의 값이 업데이트되는 경우 다음 쿼리 실행 시 업데이트된 값이 사용됩니다. 자세한 내용은 이 항목의 두 번째 예제를 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스 *Production.ProductInventory* 테이블의 지정된 제품 ID 수량을 업데이트합니다. 수량 및 제품 ID는 UPDATE 쿼리의 매개 변수입니다.  
  
다음 예제에서는 데이터베이스를 쿼리하여 수량이 올바르게 업데이트되었는지 확인합니다. 제품 ID는 SELECT 쿼리의 매개 변수입니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
이전 예제에서는 쿼리를 실행하기 위해 **sqlsrv_query** 함수를 사용했습니다. 이 함수는 문을 준비하고 실행하므로 일회성 쿼리를 실행할 때 유용합니다. 조합의 **sqlsrv_prepare**/**sqlsrv_execute** 다른 매개 변수 값으로 쿼리를 다시 실행에 가장 적합 합니다. 다른 매개 변수 값으로 쿼리를 다시 실행하는 예제를 확인하려면 다음 예제를 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 **sqlsrv_prepare** 함수를 사용할 때 변수의 암시적 바인딩을 보여 줍니다. 예제에서는 *Sales.SalesOrderDetail* 테이블에 여러 개의 판매 주문을 삽입합니다. *$params* 배열 문에 바인딩된 (*$stmt*) 때 **sqlsrv_prepare** 호출 됩니다. 테이블에 새 판매 주문을 삽입하는 각 쿼리를 실행하기 전에 *$params* 배열이 판매 주문 세부 사항에 해당하는 새 값으로 업데이트됩니다. 후속 쿼리를 실행할 때는 새 매개 변수 값을 사용합니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[데이터 형식 변환](../../connect/php/converting-data-types.md)

[보안 고려 사항 Microsoft Drivers for PHP for SQL Server](../../connect/php/security-considerations-for-php-sql-driver.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
