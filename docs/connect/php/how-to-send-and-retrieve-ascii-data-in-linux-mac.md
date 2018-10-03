---
title: '방법: Linux 및 macOS (SQL)에서 ASCII 데이터 검색 및 송신 | Microsoft Docs'
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
manager: mbarwin
ms.openlocfilehash: 2fe78cc80cd7ca77f09465fb7d3e92482da7d008
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669981"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>방법: Linux 및 macOS에서 ASCII 데이터 전송 및 검색 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서는 ASCII (비-u t F-8) 로캘을 생성 되거나 Linux 또는 macOS 시스템에 설치 된 가정 합니다. 

보내거나 서버로 ASCII 문자 집합을 검색 합니다.  

1.  원하는 로캘을 시스템 환경의 기본 없는 경우 호출할 수 있는지 확인 `setlocale(LC_ALL, $locale)` 첫 번째 연결 하기 전에 합니다. PHP setlocale() 함수는 현재 스크립트에 대해서만 로캘을 변경 하 고 첫 번째 연결을 적용 한 후 호출 하는 경우 무시 될 수 있습니다.
 
2.  SQLSRV 드라이버를 사용 하는 경우를 지정할 수 있습니다 `'CharacterSet' => SQLSRV_ENC_CHAR` 연결으로 옵션을 사용 하지만이 단계는 선택 사항 기본값 이므로 인코딩.

3.  PDO_SQLSRV 드라이버를 사용 하는 경우에 두 가지가 있습니다. 연결을 만들 때 설정 하는 먼저 `PDO::SQLSRV_ATTR_ENCODING` 에 `PDO::SQLSRV_ENCODING_SYSTEM` (연결 옵션을 설정 하는 예제를 보려면 [pdo:: __construct](../../connect/php/pdo-construct.md)). 성공적으로 연결 후이 줄을 추가 또는 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
연결 리소스 (SQLSRV) 또는 연결 개체 (PDO_SQLSRV) 인코딩을 지정 하는 경우 다른 연결 옵션 문자열이 해당 동일한 인코딩을 사용 하는 드라이버 가정 합니다. 서버 이름 및 쿼리 문자열도 동일한 문자 집합을 사용한다고 가정합니다.  
  
PDO_SQLSRV 드라이버에 대 한 인코딩 기본 점이 SQLSRV 드라이버를 u t F-8 (PDO::SQLSRV_ENCODING_UTF8)입니다. 이러한 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요. 
  
## <a name="example"></a>예제  
다음 예제에서는 SQL Server 용 PHP 드라이버를 사용 하 여 연결 하기 전에 특정 로캘을 지정 하 여 ASCII 데이터를 검색 하는 방법을 보여 줍니다. MacOS의 동일한 로캘을에서 다양 한 Linux 플랫폼의 로캘은 있습니다 다르게 이름이 지정 됩니다. 예를 들어 하는 미국 ISO-8859-1 (라틴어 1) 로캘이 `en_US.ISO-8859-1` macOS에서 이름은 동안 Linux에 `en_US.ISO8859-1`입니다.
  
예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 설치 됩니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
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
[Utf-8 데이터를 작업할](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[데이터를 업데이트 하는 중 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[예제 응용 프로그램&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
