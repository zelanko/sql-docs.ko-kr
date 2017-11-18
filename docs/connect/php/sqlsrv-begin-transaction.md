---
title: sqlsrv_begin_transaction | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_begin_transaction
apitype: NA
helpviewer_keywords:
- sqlsrv_begin_transaction
- transaction support
- API Reference, sqlsrv_begin_transaction
ms.assetid: 0b223bc8-4047-4329-9cbf-d350ab0fb886
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b28185f3e858f30a9ff67c73381b0b9c4f07a028
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvbegintransaction"></a>sqlsrv_begin_transaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

지정된 연결에서 트랜잭션을 시작합니다. 현재 트랜잭션에는 **sqlsrv_begin_transaction** 을 호출한 후와 [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) 또는 [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)을 호출하기 전에 실행된 지정된 연결에 대한 모든 문이 포함됩니다.  
  
> [!NOTE]  
> [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 기본적으로 자동 커밋 모드에 있습니다. 즉, **sqlsrv_begin_transaction**을 사용하여 트랜잭션을 시작합니다.  
  
> [!NOTE]  
> 경우 **sqlsrv_begin_transaction** 트랜잭션이 이미 후 호출 되는 연결에서 시작 되었지만 호출 하 여 완료 되지 **sqlsrv_commit** 또는 **sqlsrv_rollback**, 호출이 반환 **false** 및 *Already in Transaction* 오류가 오류 수집에 추가 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_begin_transaction( resource $conn)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: 트랜잭션과 관련된 연결입니다.  
  
## <a name="return-value"></a>반환 값  
부울 값: 트랜잭션이 성공적으로 시작하면 **true** 입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="example"></a>예제  
아래 예제는 트랜잭션의 일부로 두 개의 쿼리를 실행합니다. 두 쿼리 모두 성공하면 트랜잭션이 커밋됩니다. 쿼리 중 하나(또는 둘 다)가 실패하면 트랜잭션이 롤백됩니다.  
  
예제의 첫 번째 쿼리는 AdventureWorks 데이터베이스의 *Sales.SalesOrderDetail* 테이블에 새 판매 주문을 삽입합니다. 주문은 제품 ID가 709인 제품 5단위에 대한 것입니다. 두 번째 쿼리는 제품 ID가 709인 제품의 재고 수량을 5단위 줄입니다. 두 쿼리 모두 성공해야 데이터베이스에 주문 및 제품 가용성 상태가 정확하게 반영되므로 이러한 쿼리가 트랜잭션에 포함되어 있습니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
if ( sqlsrv_begin_transaction( $conn ) === false )  
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
  
/* Set up and execute the second query. */  
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
  
트랜잭션 동작에 중점을 두기 위해 몇 가지 권장 오류 처리 방법은 위의 예제에 포함되지 않았습니다. 프로덕션 응용 프로그램에서는 **sqlsrv** 함수 호출에 오류가 있는지 확인하여 적절하게 처리하는 것이 좋습니다.  
  
> [!NOTE]  
> 포함된 Transact-SQL을 사용하여 트랜잭션을 수행하지 마세요. 예를 들어 트랜잭션을 시작하는 Transact-SQL 쿼리로 "BEGIN TRANSACTION"을 사용하여 문을 실행하지 마세요. 포함된 Transact-SQL을 사용하여 트랜잭션을 수행하는 경우 예상 트랜잭션 동작을 보장할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[방법: 트랜잭션 수행](../../connect/php/how-to-perform-transactions.md)  
[PHP SQL 드라이버 개요](../../connect/php/overview-of-the-php-sql-driver.md) 
  

