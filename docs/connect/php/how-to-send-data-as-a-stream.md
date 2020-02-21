---
title: '방법: 데이터를 스트림으로 전송 | Microsoft Docs'
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data
- streaming data
ms.assetid: ab6b95d6-b6e6-4bd7-a18c-50f2918f7532
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d524e7c7f00b08ce636f8a3b7b945f3e8b349af0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936405"
---
# <a name="how-to-send-data-as-a-stream"></a>방법: 데이터를 스트림으로 전송
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] PHP는 대형 개체를 서버로 보내기 위해 PHP 스트림을 활용합니다. 이 항목의 예제에서는 데이터를 스트림으로 전송하는 방법을 보여 줍니다. 첫 번째 예제는 SQLSRV 드라이버를 사용하여 기본 동작을 나타내며 이는 쿼리를 실행할 때 모든 스트림 데이터를 보내기 위한 것입니다. 두 번째 예제는 SQLSRV 드라이버를 사용하여 서버에 한 번에 최대 8킬로바이트(8kB)의 스트림 데이터를 보내는 방법을 보여 줍니다.  
  
세 번째 예제는 PDO_SQLSRV 드라이버를 사용하여 서버에 스트림 데이터를 전송하는 방법을 보여 줍니다.  
  
## <a name="example-sending-stream-data-at-execution"></a>예제: 실행 시 스트림 데이터 전송
다음 예제는 AdventureWorks 데이터베이스의 *Production.ProductReview* 테이블에 한 행을 삽입합니다. 고객의 의견( *$comments*)은 PHP [fopen](https://php.net/manual/en/function.fopen.php) 함수를 통해 스트림으로 열린 다음, 쿼리를 실행할 때 서버에 스트림됩니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 콘솔에 기록됩니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if ($conn === false) {
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$data = 'Insert any lengthy comment here.';
$comments = fopen('data:text/plain,'.urlencode($data), 'r');
$params = array($productID, $name, $date, $email, $rating, $comments);
  
/* Execute the query. All stream data is sent upon execution.*/  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt === false) {
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
} else {
     echo "The query was successfully executed.";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example-sending-stream-data-using-sqlsrv_send_stream_data"></a>예제: sqlsrv_send_stream_data를 사용하여 스트림 데이터 전송
다음 예제는 이전 예제와 동일하지만 실행 시 모든 스트림 데이터를 보내는 기본 동작이 해제됩니다. 이 예제에서는 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md) 를 사용하여 스트림 데이터를 서버에 보냅니다. **sqlsrv_send_stream_data**에 대한 각 호출에서 최대 8킬로바이트(8kB)의 데이터를 전송합니다. 스크립트는 **sqlsrv_send_stream_data** 에서 수행한 호출의 수를 계산해서 해당 횟수를 콘솔에 표시합니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 콘솔에 기록됩니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if ($conn === false) {
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$data = 'Insert any lengthy comment here.';
$comments = fopen('data:text/plain,'.urlencode($data), 'r');
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Turn off the default behavior of sending all stream data at  
execution. */  
$options = array("SendStreamParamsAtExec" => 0);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params, $options);  
if ($stmt === false) {
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while (sqlsrv_send_stream_data($stmt)) {
     echo "$i call(s) made.\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
이 항목의 예제는 문자 데이터를 서버에 보내기는 하지만 모든 형식의 데이터를 스트림을 보낼 수 있습니다. 예를 들어 이 항목에 나타난 기술을 사용하여 이진 형식의 이미지를 스트림을 보낼 수도 있습니다.  
  
## <a name="example-sending-an-image-as-a-stream"></a>예제: 이미지를 스트림으로 전송 
  
```  
<?php  
   $server = "(local)";   
   $database = "Test";  
   $conn = new PDO( "sqlsrv:server=$server;Database = $database", "", "");  
  
   $binary_source = fopen( "data://text/plain,", "r");  
  
   $stmt = $conn->prepare("insert into binaries (imagedata) values (?)");  
   $stmt->bindParam(1, $binary_source, PDO::PARAM_LOB);   
  
   $conn->beginTransaction();  
   $stmt->execute();  
   $conn->commit();  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[데이터 업데이트&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
