---
title: '방법: Linux와 macOS (SQL)에서 ASCII 데이터 검색 및 보내기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 32599ca0facc7a35877f6d59573b27209ce68d31
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307682"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>방법: Send 및 Linux와 macOS에서 ASCII 데이터 검색 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서는 ASCII (비-u t F-8) 로캘을 생성 되거나 Linux 또는 macOS 시스템에 설치를 가정 합니다. 

보내고 서버에 ASCII 문자 집합을 검색 하려면:  

1.  원하는 로캘 시스템 환경에서 기본 없으면 호출 했는지 확인 `setlocale(LC_ALL, $locale)` 첫 번째 연결 하기 전에. PHP setlocale() 함수는 현재 스크립트에 대 한 로캘을 변경 하 고 첫 번째 연결한 후 호출 하는 경우 무시 될 수 있습니다.
 
2.  SQLSRV 드라이버를 사용 하 여 지정할 수 `'CharacterSet' => SQLSRV_ENC_CHAR` 연결으로 옵션을 하지만이 단계는 선택 사항이 기본 인코딩입니다.

3.  PDO_SQLSRV 드라이버를 사용 하는 경우에 두 가지가 있습니다. 먼저, 연결을 만들 때 설정 `PDO::SQLSRV_ATTR_ENCODING` 를 `PDO::SQLSRV_ENCODING_SYSTEM` (연결 옵션을 설정할 때의 예제를 보려면 [:: __construct](../../connect/php/pdo-construct.md)). 성공적으로 연결이 줄을 추가 또는 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
연결 리소스 (SQLSRV) 또는 연결 개체 (PDO_SQLSRV)의 인코딩을 지정 하면 다른 연결 옵션 문자열이 동일한이 인코딩을 사용 하는 드라이버 가정 합니다. 서버 이름 및 쿼리 문자열도 동일한 문자 집합을 사용한다고 가정합니다.  
  
PDO_SQLSRV 드라이버에 대 한 인코딩을 u t F-8 (pdo:: SQLSRV_ENCODING_UTF8), SQLSRV 드라이버와 달리 이러한 상수에 대 한 자세한 내용은 참조 [상수 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)합니다. 
  
## <a name="example"></a>예제  
다음 예에서는 보내고 연결 하기 전에 특정 로캘을 지정 하 여 SQL Server 용 PHP 드라이버를 사용 하 여 ASCII 데이터를 검색 하는 방법을 보여 줍니다. 다양 한 Linux 플랫폼에는 로캘은 macOS에서 동일한 로캘을에서 다르게 이름을 지정할 수 있습니다. 예를 들어 미국 iso-8859-1 (라틴어 1) 로캘은 `en_US.ISO-8859-1` macOS 이름은 동안 Linux에서 `en_US.ISO8859-1`합니다.
  
예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 서버에 설치 합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록 됩니다.  
  
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

## <a name="see-also"></a>관련 항목  
[데이터 검색](../../connect/php/retrieving-data.md)  
[U t F-8 데이터로 작업](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[데이터 업데이트 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[예제 응용 프로그램&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
