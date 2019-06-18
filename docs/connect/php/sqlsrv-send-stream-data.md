---
title: sqlsrv_send_stream_data | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_send_stream_data
apitype: NA
helpviewer_keywords:
- sqlsrv_send_stream_data
- API Reference, sqlsrv_send_stream_data
- streaming data
ms.assetid: 826c2d45-694f-42b8-b12b-cd4523a31883
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d20cba8eb5e6b9cd5a6c30142ac3b06d2ad57af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782764"
---
# <a name="sqlsrvsendstreamdata"></a>sqlsrv_send_stream_data
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

매개 변수 스트림에서 서버로 데이터를 보냅니다. **sqlsrv_send_stream_data**에 대한 각 호출에서 최대 8킬로바이트(8K)의 데이터를 전송합니다.  
  
> [!NOTE]  
> 기본적으로 쿼리가 실행될 때 모든 스트림 데이터를 서버에 보냅니다. 이 기본 동작이 변경되지 않은 경우 스트림 데이터를 서버에 보내기 위해 **sqlsrv_send_stream_data** 를 사용할 필요가 없습니다. 기본 동작 변경에 대한 내용은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)의 매개 변수 섹션을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_send_stream_data( resource $stmt)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 실행된 문에 해당하는 문 리소스입니다.  
  
## <a name="return-value"></a>반환 값  
부울: 보낼 데이터가 더 있는 경우 **true** 입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 제품 검토를 스트림으로 열고 서버에 보냅니다. 실행 시 모든 스트림 데이터를 보내는 기본 동작이 사용하지 않도록 설정됩니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Define the query. */  
$tsql = "UPDATE Production.ProductReview   
         SET Comments = (?)   
         WHERE ProductReviewID = 3";  
  
/* Open parameter data as a stream and put it in the $params array. */
$data = 'Insert any lengthy comment here.';
$comment = fopen('data:text/plain,'.urlencode($data), 'r');
$params = array(&$comment);
  
/* Prepare the statement. Use the $options array to turn off the  
default behavior, which is to send all stream data at the time of query  
execution. */  
$options = array("SendStreamParamsAtExec"=>0);  
$stmt = sqlsrv_prepare($conn, $tsql, $params, $options);
  
/* Execute the statement. */  
sqlsrv_execute( $stmt);  
  
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
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[데이터 업데이트&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
