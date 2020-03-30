---
title: Azure Active Directory | Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68265185"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)(Azure Active Directory)는 [SQL Server 인증](../../connect/php/how-to-connect-using-sql-server-authentication.md) 대신 사용 가능한 중앙 사용자 ID 관리 기술입니다. Azure AD는 Azure AD의 페더레이션 ID로 사용자 이름과 암호, Windows 통합 인증, 또는 Azure AD 액세스 토큰을 사용하여 Microsoft Azure SQL Database 및 SQL Data Warehouse에 대한 연결을 허용합니다. SQL Server의 PHP 드라이버는 이 기능을 부분적으로 지원합니다.

Azure AD를 사용하려면 다음 표에 나와 있는 것처럼 **인증** 또는 **AccessToken** 키워드를 사용합니다(함께 사용할 수 없음). 자세한 기술 정보는 [ODBC 드라이버에서 Azure Active Directory 사용](../../connect/odbc/using-azure-active-directory.md)을 참조하세요.

|키워드|값|Description|
|-|-|-|
|**AccessToken**|미설정(기본값)|다른 키워드에 의해 결정되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||바이트 문자열|OAuth JSON 응답에서 추출된 Azure AD 액세스 토큰입니다. 연결 문자열에는 사용자 ID, 암호 또는 인증 키워드가 포함되지 않아야 합니다(Linux 또는 macOS에서 ODBC 드라이버 버전 17 이상 필요). |
|**인증**|미설정(기본값)|다른 키워드에 의해 결정되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||`SqlPassword`|사용자 이름과 암호로 SQL Server 인스턴스(Azure 인스턴스일 수 있음)에 직접 인증합니다. **UID** 및 **PWD** 키워드로 사용자 이름과 암호를 연결 문자열에 전달해야 합니다. |
||`ActiveDirectoryPassword`|Azure Active Directory ID로 사용자 이름 및 암호를 사용하여 인증합니다. **UID** 및 **PWD** 키워드로 사용자 이름과 암호를 연결 문자열에 전달해야 합니다. |
||`ActiveDirectoryMsi`|시스템 할당 관리 ID 또는 사용자 할당 관리 ID 중 하나로 인증합니다(ODBC 드라이버 버전 17.3.1.1 이상 필요). 개요와 자습서는 [Azure 리소스에 대한 관리 ID란?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)을 참조하세요.|

**인증** 키워드는 연결 보안 설정에 영향을 줍니다. 연결 문자열에 설정된 경우 **암호화** 키워드는 기본적으로 true로 설정되며, 따라서 클라이언트가 암호화를 요청합니다. 또한 **TrustServerCertificate**의 설정이 true가 아니면(**false**로 기본 설정 시) 암호화 설정과 관계없이 서버 인증서의 유효성이 검사됩니다. 이 기능은 연결 문자열에서 암호화가 구체적으로 요청된 경우에만 서버 인증서의 유효성을 검사하는 방식 때문에 보안성이 비교적 떨어지던 이전의 로그인 방법과 구별됩니다.

Windows에서 SQL Server용 PHP 드라이버로 Azure AD를 사용하는 경우 [Microsoft Online Services 로그인 도우미](https://www.microsoft.com/download/details.aspx?id=41950)를 설치하라는 메시지가 표시될 수 있습니다(ODBC 17 이상에서는 필요 없음).

#### <a name="limitations"></a>제한 사항

Windows에서 기본 ODBC 드라이버는 **인증** 키워드 **ActiveDirectoryIntegrated**에 대해 하나 이상의 값을 지원하지만 PHP 드라이버는 모든 플랫폼에서 이 값을 지원하지 않습니다.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>예제 - SqlPassword 및 ActiveDirectoryPassword를 사용하여 연결

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdo_sqlsrv-driver"></a>예제 - PDO_SQLSRV 드라이버를 사용하여 연결

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>예제 - Azure AD 액세스 토큰을 사용하여 연결

### <a name="sqlsrv-driver"></a>SQLSRV 드라이버

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdo_sqlsrv-driver"></a>PDO_SQLSRV 드라이버

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>예제 - Azure 리소스에 대한 관리 ID를 사용하여 로그인

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>SQLSRV 드라이버를 사용하여 시스템 할당 관리 ID 사용

시스템 할당 관리 ID를 사용하여 연결할 때는 UID 또는 PWD 옵션을 사용하지 말아야 합니다.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdo_sqlsrv-driver"></a>PDO_SQLSRV 드라이버를 사용하여 사용자 할당 관리 ID 사용

사용자 할당 관리 ID는 독립 실행형 Azure 리소스로 생성됩니다. Azure는 사용 중인 구독에서 신뢰하는 Azure AD 테넌트에 ID를 만듭니다. 생성된 ID는 하나 이상의 Azure 서비스 인스턴스에 할당할 수 있습니다. 이 ID의 `Object ID`를 복사하여 연결 문자열에서 사용자 이름으로 설정합니다. 

따라서 사용자 할당 관리 ID를 사용하여 연결할 때는 개체 ID를 사용자 이름으로서 제공하고 암호는 생략합니다.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>참고 항목
[ODBC 드라이버에서 Azure Active Directory 사용](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[Azure 리소스용 관리 ID란?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
