---
title: 커서 형식(SQLSRV 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac090ad8831397bf31c0911ab8a8db21486528db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015108"
---
# <a name="cursor-types-sqlsrv-driver"></a>커서 형식(SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 드라이버를 사용하면 커서 유형에 따라 어떤 순서로든지 액세스할 수 있는 행이 있는 결과 집합을 만들 수 있습니다.  이 항목에서는 클라이언트 쪽(버퍼링됨)과 서버 쪽(버퍼링되지 않음) 커서를 설명합니다.  
  
## <a name="cursor-types"></a>커서 유형  
커서 형식은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)로 결과 집합을 만들 때 지정할 수 있습니다. 기본적으로는 정방향 전용 커서가 사용되므로 결과 집합의 첫 번째 행부터 결과 집합의 끝에 도달할 때까지 한 번에 한 행씩 이동할 수 있습니다.  
  
스크롤 가능한 커서로 결과 집합을 만들면 임의의 순서로 결과 집합의 모든 행에 액세스할 수 있습니다. 다음 표에서는 sqlsrv_query 또는 sqlsrv_prepare에서 **스크롤 가능한** 옵션으로 전달될 수 있는 값을 나열합니다.  
  
|옵션|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|결과 집합의 첫 번째 행부터 결과 집합의 끝에 도달할 때까지 한 번에 한 행씩 이동할 수 있습니다.<br /><br />이는 기본적인 커서 형식입니다.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)는 이 커서 형식을 사용하여 만들어진 결과 집합에 대한 오류를 반환합니다.<br /><br />**forward**는 SQLSRV_CURSOR_FORWARD의 약어 형식입니다.|  
|SQLSRV_CURSOR_STATIC|순서에 관계없이 행에 액세스할 수 있지만 데이터베이스에 변경 내용은 반영되지 않습니다.<br /><br />**static**은 SQLSRV_CURSOR_STATIC의 약어 형식입니다.|  
|SQLSRV_CURSOR_DYNAMIC|순서에 관계없이 행에 액세스할 수 있으며 데이터베이스에 변경 내용이 반영됩니다.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)는 이 커서 형식을 사용하여 만들어진 결과 집합에 대한 오류를 반환합니다.<br /><br />**dynamic**은 SQLSRV_CURSOR_DYNAMIC의 약어 형식입니다.|  
|SQLSRV_CURSOR_KEYSET|순서에 관계없이 행에 액세스할 수 있습니다. 그러나 행이 테이블에서 삭제되는 경우(값이 없는 삭제된 행은 반환됨) 키 집합 커서가 행 개수를 업데이트하지 않습니다.<br /><br />**keyset**는 SQLSRV_CURSOR_KEYSET의 약어 형식입니다.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|순서에 관계없이 행에 액세스할 수 있습니다. 클라이언트 쪽 커서 쿼리를 만듭니다.<br /><br />**buffered**는 SQLSRV_CURSOR_CLIENT_BUFFERED의 약어 형식입니다.|  
  
쿼리가 여러 결과 집합을 생성하는 경우 **스크롤 가능** 옵션이 모든 결과 집합에 적용됩니다.  
  
## <a name="selecting-rows-in-a-result-set"></a>결과 집합의 행 선택  
결과 집합을 만든 다음에는 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) 또는 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)를 사용하여 행을 지정할 수 있습니다.  
  
다음 표에서는 *행* 매개 변수에 지정할 수 있는 값을 설명합니다.  
  
|매개 변수|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|다음 행을 지정합니다. 스크롤 가능 결과 집합의 *행* 매개 변수를 지정하지 않으면 이 값이 기본값입니다.|  
|SQLSRV_SCROLL_PRIOR|현재 행 앞의 행을 지정합니다.|  
|SQLSRV_SCROLL_FIRST|결과 집합에서 첫 번째 행을 지정합니다.|  
|SQLSRV_SCROLL_LAST|결과 집합에서 마지막 행을 지정합니다.|  
|SQLSRV_SCROLL_ABSOLUTE|*오프셋* 매개 변수로 지정된 행을 지정합니다.|  
|SQLSRV_SCROLL_RELATIVE|현재 행에서 *오프셋* 매개 변수로 지정된 행을 지정합니다.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>서버 쪽 커서 및 SQLSRV 드라이버  
다음 예제에서는 다양한 커서의 효과를 보여줍니다. 예제의 33번째 줄에는 다른 커서를 지정하는 세 쿼리 문 중 첫 번째가 표시됩니다.  쿼리 문 중 둘은 주석 처리됩니다. 프로그램을 실행할 때마다 다른 커서 형식을 사용하여 47번째 줄의 데이터베이스 업데이트가 어떤 영향을 미치는지 확인합니다.  
  
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
클라이언트 쪽 커서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 3.0에서 추가된 기능으로, 이 기능으로 전체 결과 집합을 메모리에 캐시할 수 있습니다. 행 수는 클라이언트 쪽 커서 사용 시 쿼리가 실행된 다음에 사용할 수 있습니다.  
  
클라이언트 쪽 커서는 중소 규모의 결과 집합에 사용해야 합니다. 대규모 결과 집합에는 서버 쪽 커서를 사용합니다.  
  
버퍼가 전체 결과 집합을 저장할 만큼 크지 않으면 쿼리에서 false가 반환됩니다. PHP 메모리 한도까지 버퍼 크기를 늘릴 수 있습니다.  
  
사용자는 SQLSRV 드라이버를 사용하여 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)에 대해 ClientBufferMaxKBSize 설정으로 결과 집합을 보유하는 버퍼의 크기를 구성할 수 있습니다. [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)는 ClientBufferMaxKBSize의 값을 반환합니다. sqlsrv.ClientBufferMaxKBSize를 사용하여 php.ini 파일의 최대 버퍼 크기를 설정할 수도 있습니다(예: sqlsrv.ClientBufferMaxKBSize = 1024).  
  
다음 샘플은 다음과 같은 내용을 보여 줍니다.  
  
-   행 수는 항상 클라이언트 쪽 커서로 사용할 수 있습니다.  
  
-   클라이언트 쪽 커서와 일괄 처리 문 사용.  
  
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
  
다음 샘플에서는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)를 사용하는 클라이언트 쪽 커서와 다른 클라이언트의 버퍼 크기를 보여 줍니다.
  
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
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
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
  
## <a name="see-also"></a>참고 항목  
[커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
