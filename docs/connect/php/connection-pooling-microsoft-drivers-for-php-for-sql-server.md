---
title: 연결 풀링(Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e1075cd25fa352543837afa31ff2a3d540704f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015126"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>연결 풀링(Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

다음은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 연결 풀링에 대해 유의할 중요한 사항입니다.  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 ODBC 연결 풀링을 사용합니다.  
  
-   기본적으로 Windows에서는 연결 풀링이 사용하도록 설정되어 있습니다. Linux 및 macOS에서 연결은 ODBC에 대해 연결 풀링을 사용 하도록 설정 된 경우에만 풀링 됩니다 ( [연결 풀링 사용/사용 안 함](#enablingdisabling-connection-pooling)참조). 연결 풀링을 사용 하도록 설정 하 고 서버에 연결 하는 경우 드라이버는 새 연결을 만들기 전에 풀링된 연결을 사용 하려고 시도 합니다. 해당 연결이 풀에 없는 경우 새 연결이 만들어지고 풀에 추가됩니다. 드라이버가 연결 문자열을 비교하여 연결이 동일한지 여부를 확인합니다.  
  
-   풀에서 연결이 사용되는 경우 연결 상태가 재설정됩니다.  
  
-   연결을 닫으면 풀에 대한 연결을 반환합니다.  
  
연결 풀링에 대한 자세한 내용은 [Driver Manager Connection Pooling](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)(드라이버 관리자 연결 풀링)을 참조하세요.  
  
## <a name="enablingdisabling-connection-pooling"></a>연결 풀링 사용/사용 안 함
### <a name="windows"></a>Windows
연결 풀에서 동일한 연결을 찾지 않고 연결 문자열의 *ConnectionPooling* 특성 값을 **false**(또는 0)로 설정하여 드라이버에서 새 연결을 강제로 만들 수 있습니다.  
  
*ConnectionPooling* 특성이 연결 문자열에서 생략되거나 **true**(또는 1)로 설정되면 동등한 연결이 연결 풀에 존재하지 않는 경우에만 드라이버가 새 연결을 만듭니다.  
  
다른 연결 특성에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
### <a name="linux-and-macos"></a>Linux 및 macOS
*Connectionpooling* 특성은 연결 풀링을 사용 하거나 사용 하지 않도록 설정 하는 데 사용할 수 없습니다. 

Odbcinst.ini 구성 파일을 편집 하 여 연결 풀링을 사용/사용 하지 않도록 설정할 수 있습니다. 변경 내용을 적용 하려면 드라이버를 다시 로드 해야 합니다.

을 `Pooling` 로 `Yes` 설정 하 고 `CPTimeout` odbcinst.ini 파일에서 양수 값을 설정 하면 연결 풀링이 가능 합니다. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
최소한 odbcinst.ini 파일은 다음 예제와 같이 표시 되어야 합니다.

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

Odbcinst.ini `Pooling` 파일 `No` 에서를로 설정 하면 드라이버가 새 연결을 강제로 만듭니다.
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Remarks
- Linux 또는 macOS에서는 odbcinst.ini 파일에서 풀링이 사용 되는 경우 모든 연결이 풀링되지 않습니다. 즉, ConnectionPooling 연결 옵션이 적용 되지 않습니다. 풀링을 사용 하지 않도록 설정 하려면 odbcinst.ini 파일에서 Pooling = No를 설정 하 고 드라이버를 다시 로드 합니다.
  - 2\.3.4 (Linux 및 macOS)는 오류 메시지, 경고 및 정보 메시지와 같은 적절 한 진단 정보를 반환 하지 않을 수 있습니다. <
  - 따라서 SQLSRV 및 PDO_SQLSRV 드라이버는 long 데이터 (예: xml, 이진)를 문자열로 제대로 인출 하지 못할 수 있습니다. Long 데이터를 해결 방법으로 스트림으로 페치할 수 있습니다. 아래의 SQLSRV 예제를 참조하세요.

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>참고 항목  
[방법: Windows 인증을 사용하여 연결](../../connect/php/how-to-connect-using-windows-authentication.md)

[방법: SQL Server 인증을 사용하여 연결](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
