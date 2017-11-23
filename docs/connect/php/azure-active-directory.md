---
title: Azure Active Directory | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology: drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.openlocfilehash: eb13c1a57c63ce013a3b546572994106b8b1ffc0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용 하 여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (Azure AD)는 하는 대신 작동 하는 중앙 사용자 ID 관리 기술 [SQL Server 인증](../../connect/php/how-to-connect-using-sql-server-authentication.md)합니다. Azure AD 연결을 허용 Microsoft Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스 페더레이션된 id와 Azure AD에서 사용자 이름 및 암호, Windows 통합 인증 또는 Azure AD 액세스 토큰을 사용 하 여 SQL Server 용 PHP 드라이버에는 이러한 기능에 대 한 부분 지원을 제공합니다.

Azure AD를 사용 하려면 사용 된 **인증** 키워드입니다. 값은 **인증** 걸릴 수 있습니다에 다음 표에 설명 되어 있습니다.

|키워드|값|Description|
|-|-|-|
|**인증**|(기본값)을 설정 하지|다른 모든 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||`SqlPassword`|(수도 있음 Azure 인스턴스)는 SQL Server 인스턴스를 직접 인증할 사용자 이름 및 암호를 사용 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 되어야 합니다는 **UID** 및 **PWD** 키워드입니다. |
||`ActiveDirectoryPassword`|사용자 이름 및 암호를 사용 하 여 Azure Active Directory id로 인증 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 되어야 합니다는 **UID** 및 **PWD** 키워드입니다. |

**인증** 키워드 연결 보안 설정에 영향을 줍니다. 기본적으로 다음 연결 문자열에 설정 된 경우는 **Encrypt** 키워드 true로 설정 되어 있으므로 클라이언트는 암호화를 요청 합니다. 또한 서버 인증서 유효성을 검사할 암호화 설정에 관계 없이 하지 않는 한 **TrustServerCertificate** 설정을 true로 합니다. 이 이전에서와 없는 서버 인증서 유효성이 검사 되지 않습니다 암호화 연결 문자열에 특별히 요청 될 하지 않는 한 보안 로그인 방법을 낮은 구분 됩니다.

Azure AD는 PHP 드라이버와 함께 for SQL Server를 사용 하기 전에 설치 했는지 확인는 [Microsoft Online Services 로그인 도우미](https://www.microsoft.com/download/details.aspx?id=41950) (Linux와 MacOS에 대 한 필요 없음).

#### <a name="limitations"></a>제한 사항

Windows에서는 기본 ODBC 드라이버 지원에 대 한 더 많은 값을 하나는 **인증** 키워드를 **ActiveDirectoryIntegrated**, 되지만 PHP 드라이버를 사용 하는 모든 플랫폼에서이 값을 지원 하지 않습니다 및이 따른도 Azure AD 토큰 기반 인증을 지원 하지 않습니다.

## <a name="example"></a>예제

다음 예제를 사용 하 여 연결 하는 방법을 보여 줍니다 **SqlPassword** 및 **ActiveDirectoryPassword**합니다.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

다음 예제와 동일 하 게 위에서 PDO_SQLSRV 드라이버를 수행합니다.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>관련 항목:  
[Azure Active Directory를 사용 하 여 ODBC 드라이버](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)
