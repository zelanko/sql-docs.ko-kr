---
title: sqlsrv_rollback | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_rollback
apitype: NA
helpviewer_keywords:
- transaction support
- API Reference, sqlsrv_rollback
- sqlsrv_rollback
ms.assetid: 6e6bac39-45af-428c-bc32-f773482562ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8475944b4167184a6a2ef4a71d8751b2cd320fe1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68014965"
---
# <a name="sqlsrv_rollback"></a>sqlsrv_rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

지정된 연결에서 현재 트랜잭션을 롤백하고 자동 커밋 모드에 대한 연결을 반환합니다. 현재 트랜잭션은 [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md) 호출 후 및 **sqlsrv_rollback** 또는 [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)호출 전에 실행된 지정된 연결에 대한 모든 문을 포함합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 기본적으로 자동 커밋 모드입니다. 즉, **sqlsrv_begin_transaction**을 사용하여 트랜잭션을 시작합니다.  
  
> [!NOTE]  
> 활성 트랜잭션에 없고 **sqlsrv_rollback** transaction **sqlsrv_begin_transaction**이 호출된 경우 **false** 를 반환하고 *트랜잭션에 없음* 오류가 오류 수집에 추가됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_rollback( resource $conn)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: 트랜잭션이 활성화된 연결입니다.  
  
## <a name="return-value"></a>Return Value  
부울 값: 트랜잭션이 성공적으로 롤백되면 **true** 이고, 그렇지 않으면 **false**입니다.  
  
## <a name="example"></a>예제  
다음 예제는 트랜잭션의 일부로 두 개의 쿼리를 실행합니다. 두 쿼리 모두 성공하면 트랜잭션이 커밋됩니다. 쿼리 중 하나(또는 둘 다)가 실패하면 트랜잭션이 롤백됩니다.  
  
예제의 첫 번째 쿼리는 AdventureWorks 데이터베이스의 *Sales.SalesOrderDetail* 테이블에 새 판매 주문을 삽입합니다. 주문은 제품 ID가 709인 제품 5단위에 대한 것입니다. 두 번째 쿼리는 제품 ID가 709인 제품의 재고 수량을 5단위 줄입니다. 두 쿼리 모두 성공해야 데이터베이스에 주문 및 제품 가용성 상태가 정확하게 반영되므로 이러한 쿼리가 트랜잭션에 포함되어 있습니다.  
  
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
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and executee the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
트랜잭션 동작에 중점을 두기 위해 몇 가지 권장 오류 처리 방법은 위의 예제에 포함되지 않았습니다. 프로덕션 애플리케이션에서는 **sqlsrv** 함수 호출에 오류가 있는지 확인하여 적절하게 처리하는 것이 좋습니다.  
  
> [!NOTE]  
> 포함된 Transact-SQL을 사용하여 트랜잭션을 수행하지 마세요. 예를 들어 트랜잭션을 시작하는 Transact-SQL 쿼리로 "BEGIN TRANSACTION"을 사용하여 문을 실행하지 마세요. 포함된 Transact-SQL을 사용하여 트랜잭션을 수행하는 경우 예상 트랜잭션 동작을 보장할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[방법: 트랜잭션 수행](../../connect/php/how-to-perform-transactions.md)

[Microsoft Drivers for PHP for SQL Server 개요](../../connect/php/overview-of-the-php-sql-driver.md) 
  
