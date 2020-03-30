---
title: '방법: Linux 및 macOS(SQL)에서 ASCII 데이터 전송 및 검색 | Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68251900"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>방법: Linux 및 macOS에서 ASCII 데이터 전송 및 검색 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서에서는 Linux 또는 macOS 시스템에 ASCII(비 UTF-8) 로캘이 생성 또는 설치된 것으로 가정합니다. 

서버에 ASCII 문자 집합을 보내거나 검색하려면 다음을 수행합니다.  

1.  원하는 로캘이 시스템 환경에서 기본값이 아닌 경우 첫 번째 연결을 만들기 전에 `setlocale(LC_ALL, $locale)`을 호출해야 합니다. PHP setlocale() 함수는 현재 스크립트에 대해서만 로캘을 변경하며, 첫 번째 연결을 만든 후에 호출하는 경우 무시될 수 있습니다.
 
2.  SQLSRV 드라이버를 사용하는 경우 `'CharacterSet' => SQLSRV_ENC_CHAR`을 연결 옵션으로서 지정할 수 있지만 이 단계는 기본 인코딩이므로 선택 사항일 뿐입니다.

3.  PDO_SQLSRV 드라이버를 사용하는 경우 두 가지 방법이 있습니다. 먼저 연결을 만들 때 `PDO::SQLSRV_ATTR_ENCODING`을 `PDO::SQLSRV_ENCODING_SYSTEM`으로 설정합니다(연결 옵션 설정 예제는 [PDO::__construct](../../connect/php/pdo-construct.md) 참조). 또는 성공적으로 연결된 후에 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 줄을 추가합니다. 
  
연결 리소스(SQLSRV) 또는 연결 개체(PDO_SQLSRV)의 인코딩을 지정하는 경우 드라이버는 다른 연결 옵션 문자열이 동일한 인코딩을 사용한다고 가정합니다. 서버 이름 및 쿼리 문자열도 동일한 문자 집합을 사용한다고 가정합니다.  
  
PDO_SQLSRV 드라이버의 기본 인코딩은 SQLSRV 드라이버와 달리 UTF-8(PDO::SQLSRV_ENCODING_UTF8)입니다. 이러한 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요. 
  
## <a name="example"></a>예제  
다음 예제에서는 연결 설정 전에 특정 로캘을 지정하여 SQL Server용 PHP 드라이버를 사용하여 ASCII 데이터를 보내고 검색하는 방법을 보여줍니다. 다양한 Linux 플랫폼의 로캘은 macOS의 동일한 로캘과 다른 이름이 지정될 수 있습니다. 예를 들어 US ISO-8859-1(라틴어 1) 로캘은 Linux에서 `en_US.ISO-8859-1`이고 macOS에서는 이름이 `en_US.ISO8859-1`로 지정됩니다.
  
이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 서버에 설치되어 있다고 가정합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)  
[UTF-8 데이터 작업](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[&#40;Microsoft Drivers for PHP for SQL Server 데이터 업데이트&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[예제 애플리케이션&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
