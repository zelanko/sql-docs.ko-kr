---
title: sqlsrv_cancel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
apiname:
- sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85f6770a745eaefa4d97ffcb1ff4f0a941ca2d25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문을 취소합니다. 즉, 문에 대해 보류 중인 결과가 삭제됩니다. 이 함수가 호출 된 후 문을 다시 실행할 수 있습니다으로 준비 된 경우 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)합니다. 문과 연결된 모든 결과가 사용되는 경우에는 이 함수를 호출할 필요가 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 취소할 문입니다.  
  
## <a name="return-value"></a>반환 값  
부울 값: 작업이 성공하면 **true** 입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="example"></a>예제  
다음 예에서는 대상은 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 쿼리를 실행 하는 데이터베이스를 선택한 다음 사용 하 고 변수 될 때까지 결과 계산 *$salesTotal* 지정된 된 양에 도달할 합니다. 나머지 쿼리 결과는 삭제됩니다. 이 예제에서는 SQL Server 및 AdventureWorks 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>설명  
준비 되 고의 조합을 사용 하 여 실행 하는 문을 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 및 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 여 다시 실행 될 수 **sqlsrv_execute** 를호출한후**sqlsrv_cancel**합니다. 로 실행 되는 문 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 호출한 후에 다시 실행할 수 없습니다 **sqlsrv_cancel**합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[서버에 연결](../../connect/php/connecting-to-the-server.md)

[데이터 검색](../../connect/php/retrieving-data.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)

  
