---
title: '방법: SQLSRV 드라이버를 사용하여 스트림으로 이진 데이터 검색 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f77439f2369d7fbf4e27603bcbf8c8a2f8d8399
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993483"
---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 스트림으로 이진 데이터 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

스트림으로 데이터 검색은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 SQLSRV 드라이버에서만 사용 가능하고 PDO_SQLSRV 드라이버에서는 사용할 수 없습니다.  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 PHP 스트림을 활용하여 서버로부터 대용량 이진 데이터를 검색합니다. 이 항목에서는 스트림으로 이진 데이터를 검색하는 방법을 보여 줍니다.  
  
스트림을 사용하여 이미지와 같은 이진 데이터를 검색하고, 전체 개체를 스크립트 메모리로 로드하는 대신 데이터 청크를 검색하여 스크립트 메모리를 절약합니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스의 *Production.ProductPhoto* 테이블에서 이진 데이터(이 경우 이미지)를 검색합니다. 이미지는 스트림으로 가져와서 브라우저에 표시됩니다.  
  
스트림으로 이미지 데이터를 검색하려면 이진 스트림으로 지정된 반환 형식의 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 및 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 를 사용합니다. 반환 형식은 상수 **SQLSRV_PHPTYPE_STREAM**을 사용하여 지정합니다. **sqlsrv** 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
예제에서 반환 형식을 지정하여 PHP 반환 형식을 이진 스트림으로 지정하는 방법을 보여 줍니다. 기술적으로 볼 때, *LargePhoto* 필드에는 SQL Server 형식 varbinary(max)가 있어 기본적으로 이진 스트림으로 반환되므로 이 예제에서는 필요하지 않습니다. 기본 PHP 데이터 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요. PHP 반환 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
