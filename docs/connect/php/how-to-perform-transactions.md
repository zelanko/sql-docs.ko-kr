---
title: '방법: 트랜잭션을 수행 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a2a2d041ba99ded7a8d611620ce288593b341a6
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307662"
---
# <a name="how-to-perform-transactions"></a>방법: 트랜잭션 수행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 SQLSRV 드라이버는 트랜잭션을 수행하기 위해 세 가지 기능을 제공합니다.  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
PDO_SQLSRV 드라이버는 트랜잭션을 수행하기 위해 세 가지 메서드를 제공합니다.  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
예제를 보려면 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 참조하세요.  
  
이 항목의 나머지 부분에서는 SQLSRV 드라이버를 사용하여 트랜잭션을 수행하는 방법을 설명하고 예로 보여 줍니다.  
  
## <a name="remarks"></a>Remarks  
트랜잭션을 실행하는 단계는 다음과 같이 요약할 수 있습니다.  
  
1.  사용 하 여 트랜잭션을 시작 **sqlsrv_begin_transaction**합니다.  
  
2.  트랜잭션의 일부인 각 쿼리의 성공 또는 실패 여부를 확인합니다.  
  
3.  해당하는 경우 **sqlsrv_commit**을 사용하여 트랜잭션을 시작합니다. 그렇지 않으면 **sqlsrv_rollback**을 사용하여 트랜잭션을 시작합니다. 호출한 후 **sqlsrv_commit** 또는 **sqlsrv_rollback**, 드라이버가 자동 커밋 모드로 반환 됩니다.  
  
    기본적으로는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 자동 커밋 모드에 있습니다. 즉, **sqlsrv_begin_transaction**을 사용하여 트랜잭션을 시작합니다.  
  
    명시적 트랜잭션을으로 커밋되지 않는 경우 **sqlsrv_commit**, 연결 또는 스크립트의 종료 시 다시 롤백됩니다.  
  
    포함된 Transact-SQL을 사용하여 트랜잭션을 수행하지 마세요. 예를 들어 트랜잭션을 시작하는 Transact-SQL 쿼리로 "BEGIN TRANSACTION"을 사용하여 문을 실행하지 마세요. 포함된 Transact-SQL을 사용하여 트랜잭션을 수행하는 경우 예상 트랜잭션 동작을 보장할 수 없습니다.  
  
    앞에서 설명한 **sqlsrv** 함수를 사용하여 트랜잭션을 수행해야 합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
다음 예제는 트랜잭션의 일부로 여러 개의 쿼리를 실행합니다. 모든 쿼리가 성공하면 트랜잭션이 커밋됩니다. 쿼리 중 하나라도 실패하면 트랜잭션이 롤백됩니다.  
  
이 예제에서는 *Sales.SalesOrderDetail* 테이블에서 판매 주문을 삭제하고 판매 주문의 각 제품에 대해 *Product.ProductInventory* 테이블에서 제품 재고 수준을 조정합니다. 두 쿼리 모두 성공해야 데이터베이스에 주문 및 제품 가용성 상태가 정확하게 반영되므로 이러한 쿼리가 트랜잭션에 포함되어 있습니다.  
  
예제의 첫 번째 쿼리가 제품 ID 및 지정된 판매 주문 ID의 수량을 검색합니다. 이 쿼리는 트랜잭션의 일부가 아닙니다. 그러나 후속 트랜잭션의 일부인 쿼리를 완료하려면 제품 ID 및 수량이 필요하기 때문에 이 쿼리가 실패하면 스크립트가 종료됩니다.  
  
뒤이은 쿼리(판매 주문의 삭제 또는 제품 재고 수량 업데이트)는 트랜잭션의 일부입니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
### <a name="code"></a>코드  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>주석  
트랜잭션 동작에 중점을 두기 위해 몇 가지 권장 오류 처리 방법은 이전 예제에 포함되지 않았습니다. 프로덕션 응용 프로그램에 대 한 모든 호출에 검사 권장는 **sqlsrv** 오류에 대 한 함수를 그에 따라 처리 합니다.
  
## <a name="see-also"></a>관련 항목  
[데이터 업데이트&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[트랜잭션 (데이터베이스 엔진)](https://msdn.microsoft.com/library/ms190612.aspx)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
