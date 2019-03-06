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
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 8664c2452a650e1ce572651afeece2a4ab7ca4ca
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56828053"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD)는 대 안으로 작동 하는 중앙 사용자 ID 관리 기술 [SQL Server 인증](../../connect/php/how-to-connect-using-sql-server-authentication.md)합니다. Azure AD 허용 사용자 이름 및 암호, Windows 통합 인증 또는 Azure AD 액세스 토큰을 사용 하 여 Azure AD에서 페더레이션된 id 사용 하 여 Microsoft Azure SQL Database 및 SQL Data Warehouse에 연결 합니다. SQL Server 용 PHP 드라이버에는 이러한 기능에 대 한 부분 지원을 제공합니다.

Azure AD를 사용 하려면 사용 합니다 **인증** 또는 **AccessToken** 키워드 (이러한 상호 배타적인)를 표에 표시 된 것 처럼 합니다. 자세한 기술 정보를 참조 [를 사용 하 여 Azure Active Directory와 ODBC 드라이버](../../connect/odbc/using-azure-active-directory.md)합니다.

|키워드|값|설명|
|-|-|-|
|**AccessToken**|(기본값)을 설정 하지|다른 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||바이트 문자열|Azure AD 액세스 토큰을 OAuth JSON 응답에서 추출 합니다. 연결 문자열에는 사용자 ID, 암호 또는 인증 키워드가 없어야 (필요한 ODBC 드라이버 버전 17 이상 Linux 또는 macOS에서). |
|**인증**|(기본값)을 설정 하지|다른 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||`SqlPassword`|(Azure 인스턴스 수 있음)는 SQL Server 인스턴스를 직접 인증할 사용자 이름 및 암호를 사용 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 해야 합니다 **UID** 하 고 **PWD** 키워드입니다. |
||`ActiveDirectoryPassword`|사용자 이름 및 암호를 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 해야 합니다 **UID** 하 고 **PWD** 키워드입니다. |
||`ActiveDirectoryMsi`|시스템 할당 된 관리 되는 id 또는 사용자 할당 관리 id를 사용 하 여 인증 (ODBC 드라이버 버전 17.3.1.1 필요 이상). 개요 및 자습서를 참조 하세요 [Azure 리소스에 대 한 관리 되는 id 란?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)합니다.|

합니다 **인증** 키워드 연결 보안 설정에 영향을 줍니다. 기본적으로 다음 연결 문자열에 설정 된 경우는 **Encrypt** 키워드를 클라이언트에 암호화를 요청 합니다 즉 true로 설정 합니다. 또한 서버 인증서 유효성을 검사할 암호화 설정에 관계 없이 경우가 아니면 **TrustServerCertificate** 설정 된 true (**false** 기본적으로). 이 기능은 보안 로그인 메서드는 서버 인증서의 유효성 검사 암호화 연결 문자열에 특별히 요청 될 경우에 덜 이전에서 구분 됩니다.

PHP 드라이버를 사용 하 여 Azure AD를 사용 하 여 Windows에서 SQL server, 설치를 묻는 메시지가 표시 될 수 있습니다 합니다 [Microsoft Online Services 로그인 도우미](https://www.microsoft.com/download/details.aspx?id=41950) (17 + ODBC에 대 한 필요 없음).

#### <a name="limitations"></a>제한 사항

Windows에 기본 ODBC 드라이버 지원에 대 한 하나 더 많은 가치를 **인증** 키워드 **ActiveDirectoryIntegrated**, 하지만 PHP 드라이버를 모든 플랫폼에서이 값을 지원 하지 않습니다.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>예제-SqlPassword 및 ActiveDirectoryPassword를 사용 하 여 연결

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

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>예제-PDO_SQLSRV 드라이버를 사용 하 여 연결

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

## <a name="example---connect-using-azure-ad-access-token"></a>예제-Azure AD 액세스 토큰을 사용 하 여 연결

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

### <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>예제-관리 되는 id를 사용 하 여 Azure 리소스에 대 한 연결

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>SQLSRV 드라이버를 사용 하 여 관리 되는 시스템 할당 id를 사용 하 여

관리 되는 id 시스템 할당을 사용 하 여 연결 하는 중, 하는 경우 UID 또는 PWD 옵션을 사용 하지 마십시오.

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버를 사용 하 여 사용자 할당 관리 되는 id를 사용 하 여

사용자 할당 관리 id는 독립 실행형 Azure 리소스 생성 됩니다. Azure에서 사용 중인 구독에서 신뢰할 수 있는 Azure AD 테 넌 트 id를 만듭니다. Id를 만든 후 하나 이상의 Azure 서비스 인스턴스에 id는 할당할 수 있습니다. 복사를 `Object ID` 연결 문자열에 이름을 사용자로는이 id 및 집합입니다. 

따라서 관리 되는 id 사용자 할당을 사용 하 여 연결 하는 중에 사용자 이름으로 개체 ID를 제공 하지만 암호를 생략 합니다.

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

[Azure 리소스에 대 한 관리 되는 id 란?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
