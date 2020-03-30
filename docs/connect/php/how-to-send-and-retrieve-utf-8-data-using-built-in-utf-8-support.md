---
title: '방법: 기본 제공 UTF-8 지원을 사용하여 UTF-8 데이터 보내기 및 검색 | Microsoft Docs'
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, UTF-8 encoded data
- converting data types
- updating data
ms.assetid: 366c57cf-352f-4202-8074-6ddce44880d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74d64aa0a5a93587997bc66d064d0c5c47ffb132
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993376"
---
# <a name="how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support"></a>기본 제공 UTF-8 지원을 사용하여 UTF-8 데이터를 보내고 검색하는 방법
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 드라이버를 사용하는 경우 PDO::SQLSRV_ATTR_ENCODING 특성으로 인코딩을 지정할 수 있습니다. 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.  
  
이 항목의 나머지 부분에서는 SQLSRV 드라이버를 사용하는 인코딩을 설명합니다.  
  
서버에 UTF-8로 인코드된 데이터를 보내고 검색하려면  
  
1.  원본 열 또는 대상 열이 **nchar** 형식인지 또는 **nvarchar**형식인지 확인합니다.  
  
2.  매개 변수 배열에서 `SQLSRV_PHPTYPE_STRING('UTF-8')` 으로 PHP 형식을 지정합니다. 또는 연결 옵션으로 `"CharacterSet" => "UTF-8"` 을 지정합니다.  
  
    연결 옵션의 일부로 문자 집합을 지정하는 경우 드라이버는 다른 연결 옵션 문자열이 동일한 문자 집합을 사용한다고 가정합니다. 서버 이름 및 쿼리 문자열도 동일한 문자 집합을 사용한다고 가정합니다.  
  
**CharacterSet**에 UTF-8 또는 SQLSRV_ENC_CHAR을 전달할 수 있습니다(그러나 SQLSRV_ENC_BINARY는 전달할 수 없음). 기본 인코딩은 SQLSRV_ENC_CHAR입니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 연결 시 UTF-8 문자 집합을 지정하여 UTF-8로 인코드된 데이터를 보내고 검색하는 방법을 보여 줍니다. 이 예제는 지정된 검토 ID에 대한 Production.ProductReview 테이블의 주석 열을 업데이트합니다. 또한 새로 업데이트된 데이터를 검색하고 표시합니다. 주석 열은 **nvarchar(3850)** 형식입니다. 또한 서버에 데이터를 보내기 전에 PHP **utf8_encode** 함수를 사용하여 UTF-8 인코딩으로 변환됩니다. 이는 예시용으로만 수행됩니다. 실제 애플리케이션 시나리오에서는 UTF-8 인코드된 데이터로 시작합니다.  
  
이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치되어 있다고 가정합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "CharacterSet" => "UTF-8");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing 1, 2, 3, 4.  Testing.");  
$params1 = array(  
                  array( $comments, null ),  
                  array( $reviewID, null )  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field( $stmt2, 0 );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
유니코드 데이터 저장에 대한 정보는 [유니코드 데이터로 작업](https://msdn.microsoft.com/library/ms175180.aspx)을 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 첫 번째 예제와 유사하지만 연결에서 UTF-8 문자 집합 대신 열에서 UTF-8 문자 집합을 지정하는 방법을 보여 줍니다.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing");  
$params1 = array(  
                  array($comments,  
                        SQLSRV_PARAM_IN,  
                        SQLSRV_PHPTYPE_STRING('UTF-8')  
                  ),  
                  array($reviewID)  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field($stmt2,   
                            0,   
                            SQLSRV_PHPTYPE_STRING('UTF-8')  
                           );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[비 Windows에서 ASCII 데이터 사용](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)

[데이터 업데이트&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[예제 애플리케이션&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
