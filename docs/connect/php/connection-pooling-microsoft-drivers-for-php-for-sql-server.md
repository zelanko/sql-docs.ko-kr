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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714a3436cc79f3568e14c5e2609e16fd408f288e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80900989"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>연결 풀링(Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

다음은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 연결 풀링에 대해 유의할 중요한 사항입니다.  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 ODBC 연결 풀링을 사용합니다.  
  
-   기본적으로 Windows에서는 연결 풀링이 사용하도록 설정되어 있습니다. Linux 및 macOS에서 연결은 ODBC에 대해 연결 풀링을 사용하도록 설정된 경우에만 풀링됩니다([연결 풀링 사용/사용 안 함](#enablingdisabling-connection-pooling) 참조). 연결 풀링을 사용하도록 설정하고 서버에 연결하면 드라이버는 새 연결을 만들기 전에 풀링된 연결을 사용하려고 시도합니다. 해당 연결이 풀에 없는 경우 새 연결이 만들어지고 풀에 추가됩니다. 드라이버가 연결 문자열을 비교하여 연결이 동일한지 여부를 확인합니다.  
  
-   풀에서 연결이 사용되는 경우 연결 상태가 재설정됩니다.  
  
-   연결을 닫으면 풀에 대한 연결을 반환합니다.  
  
연결 풀링에 대한 자세한 내용은 [Driver Manager Connection Pooling](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)(드라이버 관리자 연결 풀링)을 참조하세요.  
  
## <a name="enablingdisabling-connection-pooling"></a>연결 풀링 사용/사용 안 함
### <a name="windows"></a>Windows
연결 풀에서 동일한 연결을 찾지 않고 연결 문자열의 *ConnectionPooling* 특성 값을 **false**(또는 0)로 설정하여 드라이버에서 새 연결을 강제로 만들 수 있습니다.  
  
*ConnectionPooling* 특성이 연결 문자열에서 생략되거나 **true**(또는 1)로 설정되면 동등한 연결이 연결 풀에 존재하지 않는 경우에만 드라이버가 새 연결을 만듭니다.  
  
다른 연결 특성에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
### <a name="linux-and-macos"></a>Linux 및 macOS
연결 풀링을 사용하거나 사용하지 않도록 설정하는 데 *ConnectionPooling* 특성을 사용할 수 없습니다. 

odbcinst.ini 구성 파일을 편집하여 연결 풀링을 사용/사용하지 않도록 설정할 수 있습니다. 변경 내용을 적용하려면 드라이버를 다시 로드해야 합니다.

`Pooling`을 `Yes`로 설정하고 odbcinst.ini 파일에서 양의 `CPTimeout` 값을 설정하면 연결 풀링을 사용할 수 있습니다. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
최소한 odbcinst.ini 파일은 다음 예제와 비슷해야 합니다.

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

odbcinst.ini 파일에서 `Pooling`를 `No`로 설정하면 드라이버가 강제로 새 연결을 만듭니다.
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>설명
- Linux 또는 macOS에서는 odbcinst.ini 파일에서 풀링이 사용하도록 설정된 경우 모든 연결이 풀링됩니다. 즉, ConnectionPooling 연결 옵션이 적용되지 않습니다. 풀링을 사용하지 않도록 설정하려면 odbcinst.ini 파일에서 Pooling=No를 설정하고 드라이버를 다시 로드합니다.
  - 2\.3.4 이하 unixODBC(Linux 및 macOS)는 오류 메시지, 경고 및 정보 메시지와 같은 적절한 진단 정보를 반환하지 않을 수 있습니다.
  - 따라서 SQLSRV 및 PDO_SQLSRV 드라이버는 긴 데이터(예: xml, 이진)를 문자열로 제대로 페치하지 못할 수 있습니다. 해결 방법으로 긴 데이터를 스트림으로 페치할 수 있습니다. 아래의 SQLSRV 예제를 참조하세요.

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
  
