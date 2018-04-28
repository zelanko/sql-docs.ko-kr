---
title: 커서 유형 (SQLSRV 드라이버) | Microsoft Docs
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
ms.topic: article
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c95beace96484b53d6786f8df24b55878a1ab8e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-types-sqlsrv-driver"></a>커서 유형 (SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 드라이버를 사용 하면 커서 유형에 따라 어떤 순서로 액세스할 수 있는 행이 있는 결과 집합을 만들 수 있습니다.  클라이언트 쪽 (버퍼 됨) 및 서버 쪽 (버퍼링 안 됨)이이 항목을 설명 합니다 커서입니다.  
  
## <a name="cursor-types"></a>커서 유형  
결과 집합을 만들 때 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)을 커서의 유형을 지정할 수 있습니다. 기본적으로 결과 결과 집합의 끝에 도달할 때까지 집합의 첫 번째 행에서 시작 하는 한 번에 한 행을 이동할 수 있는 정방향 전용 커서가 사용 됩니다.  
  
결과 집합을 순서에 관계 없이 결과 집합에 있는 모든 행에 액세스할 수 있는 스크롤 가능 커서를 만들 수 있습니다. 에 전달 될 수 있는 값을 나열 하는 다음 표에 **Scrollable** sqlsrv_query 또는 sqlsrv_prepare 옵션입니다.  
  
|옵션|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|결과 결과 집합의 끝에 도달할 때까지 집합의 첫 번째 행에서 시작 하는 한 번에 한 행을 이동할 수 있습니다.<br /><br />이것이 기본 커서 유형을입니다.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 이 커서 유형과 함께 만들어진 결과 집합에는 오류를 반환 합니다.<br /><br />**앞으로** 은 SQLSRV_CURSOR_FORWARD의 간략된 한 형태입니다.|  
|SQLSRV_CURSOR_STATIC|있습니다 순서에 관계 없이 행에 액세스 하지만 데이터베이스에 변경 내용이 반영 되지 것입니다.<br /><br />**정적** 은 SQLSRV_CURSOR_STATIC의 간략된 한 형태입니다.|  
|SQLSRV_CURSOR_DYNAMIC|있습니다 순서에 관계 없이 행에 액세스 하 고 데이터베이스에 변경 내용이 반영 됩니다.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 이 커서 유형과 함께 만들어진 결과 집합에는 오류를 반환 합니다.<br /><br />**동적** 은 SQLSRV_CURSOR_DYNAMIC의 간략된 한 형태입니다.|  
|SQLSRV_CURSOR_KEYSET|있습니다 순서에 관계 없이 행에 액세스할 수 있습니다. 그러나 키 집합 커서 (삭제 된 행 값이 반환 값이 없는) 테이블에서 행이 삭제 하는 경우 행 개수를 업데이트 하지 않습니다.<br /><br />**키 집합** SQLSRV_CURSOR_KEYSET의 간략된 한 형태는 합니다.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|있습니다 순서에 관계 없이 행에 액세스할 수 있습니다. 클라이언트 쪽 커서 쿼리를 만듭니다.<br /><br />**버퍼링** SQLSRV_CURSOR_CLIENT_BUFFERED의 간략된 한 형태 됩니다.|  
  
쿼리에서 여러 결과 집합을 생성 하는 경우는 **Scrollable** 옵션은 모든 결과 집합에 적용 됩니다.  
  
## <a name="selecting-rows-in-a-result-set"></a>결과 집합의 행 선택  
결과 집합을 만든 후 사용할 수 있습니다 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md), 또는 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) 행을 지정 하려면.  
  
다음 표에서 값을 지정할 수 있습니다는 *행* 매개 변수입니다.  
  
|매개 변수|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|다음 행을 지정합니다. 이 기본값을 지정 하지 않는 경우는 *행* 스크롤 가능한 결과 집합에 대 한 매개 변수입니다.|  
|SQLSRV_SCROLL_PRIOR|현재 행 앞에 있는 행을 지정합니다.|  
|SQLSRV_SCROLL_FIRST|결과 집합의 첫 번째 행을 지정합니다.|  
|SQLSRV_SCROLL_LAST|결과 집합의 마지막 행을 지정합니다.|  
|SQLSRV_SCROLL_ABSOLUTE|지정 된 행을 지정 된 *오프셋* 매개 변수입니다.|  
|SQLSRV_SCROLL_RELATIVE|지정 된 행을 지정 된 *오프셋* 현재 행에서 매개 변수입니다.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>서버 쪽 커서 및 SQLSRV 드라이버  
다음 예제에서는 다양 한 커서의 결과 보여 줍니다. 이 예제에서는 줄 33에 다른 커서를 지정 하는 세 가지 쿼리 문 처음을 볼 수 있습니다.  두 쿼리 문의 주석 처리 합니다. 프로그램을 실행할 때마다 다른 커서 유형을 사용 하 여 47 줄에는 데이터베이스 업데이트의 영향을 확인할 수 있습니다.  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>클라이언트 쪽 커서 및 SQLSRV 드라이버  
클라이언트 쪽 커서의 버전 3.0에서에서 추가 된 기능에는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 을 전체 결과 집합을 메모리를 캐시할 수 있습니다. 클라이언트 쪽 커서를 사용 하는 경우 쿼리가 실행 된 후 행 개수를 사용할 수 있습니다.  
  
소규모-결과 집합에 대 한 클라이언트 쪽 커서를 사용 해야 합니다. 큰 결과 집합에 대 한 서버 쪽 커서를 사용 합니다.  
  
쿼리는 버퍼가 전체 결과 집합을 보유할 수 있을 만큼 큰 경우 false를 반환 합니다. 최대 PHP 메모리 제한의 버퍼 크기를 늘릴 수 있습니다.  
  
SQLSRV 드라이버를 사용 하 여 결과 대 한 ClientBufferMaxKBSize 설정을 사용 하 여 집합을 보유 하는 버퍼의 크기를 구성할 수 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)합니다. [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) ClientBufferMaxKBSize의 값을 반환 합니다. Sqlsrv와 php.ini 파일에서 최대 버퍼 크기를 설정할 수도 있습니다. ClientBufferMaxKBSize (예를 들어 sqlsrv 합니다. ClientBufferMaxKBSize = 1024)입니다.  
  
다음 샘플에서는 다음을 보여 줍니다.  
  
-   행 개수는 항상 클라이언트 쪽 커서와 함께 사용할 수 있습니다.  
  
-   클라이언트 쪽 커서 및 일괄 처리 문 사용 합니다.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
다음 샘플은 사용 하 여 클라이언트 쪽 커서 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)합니다.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable"=>SQLSRV_CURSOR_CLIENT_BUFFERED));  
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
