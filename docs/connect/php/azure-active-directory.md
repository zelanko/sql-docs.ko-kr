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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265185"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD)는 [SQL Server 인증](../../connect/php/how-to-connect-using-sql-server-authentication.md)에 대 한 대 안으로 작동 하는 중앙 사용자 ID 관리 기술입니다. Azure AD는 사용자 이름 및 암호, Windows 통합 인증 또는 Azure AD 액세스 토큰을 사용 하 여 Azure AD에서 페더레이션 id로 Microsoft Azure SQL Database 및 SQL Data Warehouse에 대 한 연결을 허용 합니다. SQL Server 용 PHP 드라이버는 이러한 기능을 부분적으로 지원 합니다.

Azure AD를 사용 하려면 다음 표에 나와 있는 것 처럼 **인증** 또는 **AccessToken** 키워드 (함께 사용할 수 없음)를 사용 합니다. 자세한 기술 정보는 [ODBC 드라이버를 사용 하 여 Azure Active Directory 사용](../../connect/odbc/using-azure-active-directory.md)을 참조 하세요.

|키워드|값|설명|
|-|-|-|
|**AccessToken**|설정 안 함 (기본값)|다른 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||바이트 문자열입니다.|OAuth JSON 응답에서 추출 된 Azure AD 액세스 토큰입니다. 연결 문자열에는 사용자 ID, 암호 또는 인증 키워드가 포함 되지 않아야 합니다 (Linux 또는 macOS에서 ODBC 드라이버 버전 17 이상이 필요 함). |
|**인증**|설정 안 함 (기본값)|다른 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||`SqlPassword`|사용자 이름 및 암호를 사용 하 여 SQL Server 인스턴스 (Azure 인스턴스 일 수 있음)에 직접 인증 합니다. **UID** 및 **PWD** 키워드를 사용 하 여 연결 문자열에 사용자 이름 및 암호를 전달 해야 합니다. |
||`ActiveDirectoryPassword`|사용자 이름 및 암호를 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다. **UID** 및 **PWD** 키워드를 사용 하 여 연결 문자열에 사용자 이름 및 암호를 전달 해야 합니다. |
||`ActiveDirectoryMsi`|시스템 할당 관리 id 또는 사용자 할당 관리 id 중 하나를 사용 하 여 인증 합니다 (ODBC 드라이버 버전 17.3.1.1 이상 필요). 개요 및 자습서는 [Azure 리소스에 대 한 관리 되는 id 란?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)을 참조 하세요.|

**Authentication** 키워드는 연결 보안 설정에 영향을 줍니다. 연결 문자열에 설정 된 경우 기본적으로 **Encrypt** 키워드가 true로 설정 됩니다. 즉, 클라이언트가 암호화를 요청 합니다. 또한 **Trustservercertificate** 가 true로 설정 되어 있지 않으면 (기본적으로**false** ) 암호화 설정에 관계 없이 서버 인증서의 유효성이 검사 됩니다. 이 기능은 연결 문자열에서 암호화가 구체적으로 요청 된 경우에만 서버 인증서의 유효성을 검사 하는 이전의 낮은 보안 로그인 방법과 구별 됩니다.

Windows에서 SQL Server 용 PHP 드라이버와 함께 Azure AD를 사용 하는 경우 [Microsoft Online Services 로그인 도우미](https://www.microsoft.com/download/details.aspx?id=41950) 를 설치 하 라는 메시지가 표시 될 수 있습니다 (ODBC 17 이상에서는 필요 없음).

#### <a name="limitations"></a>제한 사항

Windows에서 기본 ODBC 드라이버는 **인증** 키워드 **ActiveDirectoryIntegrated**에 대해 하나 이상의 값을 지원 하지만 PHP 드라이버는 모든 플랫폼에서이 값을 지원 하지 않습니다.

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>예제-Azure 리소스에 대해 관리 되는 id를 사용 하 여 연결

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>SQLSRV 드라이버를 사용 하 여 시스템 할당 관리 id 사용

시스템 할당 관리 id를 사용 하 여 연결 하는 경우 UID 또는 PWD 옵션을 사용 하지 마십시오.

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>PDO_SQLSRV driver와 함께 사용자 할당 관리 id 사용

사용자 할당 관리 id는 독립 실행형 Azure 리소스로 생성 됩니다. Azure는 사용 중인 구독에서 신뢰할 수 있는 Azure AD 테 넌 트에 id를 만듭니다. Id를 만든 후에는 하나 이상의 Azure 서비스 인스턴스에 id를 할당할 수 있습니다. 이 id `Object ID` 의를 복사 하 고 연결 문자열의 사용자 이름으로 설정 합니다. 

따라서 사용자 할당 관리 id를 사용 하 여 연결 하는 경우에는 개체 ID를 사용자 이름으로 제공 하 고 암호는 생략 합니다.

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
