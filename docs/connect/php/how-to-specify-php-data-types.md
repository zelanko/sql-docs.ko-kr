---
title: '방법: PHP 데이터 형식 지정 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8453b2cd2db36ed2c69b8ada941bcde0050a0759
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915809"
---
# <a name="how-to-specify-php-data-types"></a>방법: PHP 데이터 형식 지정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 드라이버를 사용하는 경우 서버에서 데이터를 검색할 때 PDOStatement::bindColumn 및 PDOStatement::bindParam을 사용하여 PHP 데이터 형식을 지정할 수 있습니다. 자세한 내용은 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 및 [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) 를 참조하세요.  
  
다음 단계에서는 SQLSRV 드라이버를 사용하여 서버에서 데이터를 검색할 때 PHP 데이터 형식을 지정하는 방법을 간략하게 설명합니다.  
  
1.  [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 조합을 사용하여 Transact-SQL 쿼리를 설정하고 실행합니다.  
  
2.  데이터 행을 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)에서 읽을 수 있도록 만듭니다.  
  
3.  원하는 PHP 데이터 형식을 선택적인 세 번째 매개 변수로 지정한 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 를 사용하여 반환된 행에서 필드 데이터를 검색합니다. 선택적인 세 번째 매개 변수를 지정하지 않으면 데이터가 기본 PHP 형식에 따라 반환됩니다. 기본 PHP 반환 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요.  
  
    PHP 데이터 형식을 지정하는 데 사용하는 상수에 대한 자세한 내용은 [상수(Microsoft Drivers for PHP for SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)의 PHPTYPE 섹션을 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스의 *Production.ProductReview* 테이블에서 행을 검색합니다. 반환된 각 행에서 *ReviewDate* 필드는 문자열로 검색되고 *Comments* 필드는 스트림으로 검색됩니다. 스트림 데이터는 PHP [fpassthru](https://php.net/manual/en/function.fpassthru.php) 함수를 사용하여 표시됩니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
예제에서 두 번째 필드*ReviewDate*를 문자열로 검색하면 SQL Server DATETIME 데이터 형식의 밀리초 정확도가 유지됩니다. 기본적으로 SQL Server DATETIME 데이터 형식은 밀리초 정확도가 떨어지는 PHP DateTime 개체로 검색됩니다.  
  
네 번째 필드*Comments*를 스트림으로 검색하는 것은 예시용입니다. 기본적으로 SQL Server 데이터 형식 nvarchar(3850)은 문자열로 검색되며 이는 대부분의 경우에 허용됩니다.  
  
> [!NOTE]  
> [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) 함수는 쿼리를 실행하기 전에 형식 정보를 포함하여 필드 정보를 얻는 방법을 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)

[방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[방법: SQLSRV 드라이버를 사용하여 입력 및 출력 매개 변수 검색](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
