---
title: SQLSRV 드라이버를 사용하여 스트림으로 문자 데이터 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 026160c3e65255321691ec24fc331f8c7ab09b5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803179"
---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 스트림으로 문자 데이터 가져오기
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

스트림으로 데이터 검색은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 SQLSRV 드라이버에서만 사용 가능하고 PDO_SQLSRV 드라이버에서는 사용할 수 없습니다.  
  
SQLSRV 드라이버는 PHP 스트림을 활용하여 서버로부터 용량이 큰 데이터를 가져옵니다. 이 항목의 예제에서는 문자 데이터를 스트림으로 검색하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스의 *Production.ProductReview* 테이블에서 행을 검색합니다. 반환된 행의 *Comments* 필드는 스트림으로 검색되고 PHP [fpassthru](https://php.net/manual/function.fpassthru.php) 함수를 사용하여 표시됩니다.  
  
스트림으로 데이터를 검색하려면 문자 스트림으로 지정되는 반환 형식으로 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 및 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 를 사용합니다. 반환 형식은 상수 **SQLSRV_PHPTYPE_STREAM**을 사용하여 지정합니다. **sqlsrv** 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.  
  
이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치되어 있다고 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
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
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
처음 세 개의 필드에 대해 PHP 반환 형식이 지정되지 않았기 때문에 해당 기본 PHP 형식에 따라 각 필드가 반환됩니다. 기본 PHP 데이터 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요. PHP 반환 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
