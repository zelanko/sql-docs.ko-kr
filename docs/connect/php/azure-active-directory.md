---
title: Azure Active Directory | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 71e6b3b4556621b6bc8a8a4c7996cfdb47a12849
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979445"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD)는 대 안으로 작동 하는 중앙 사용자 ID 관리 기술 [SQL Server 인증](../../connect/php/how-to-connect-using-sql-server-authentication.md)합니다. Azure AD 연결을 허용 Microsoft Azure SQL Database 및 SQL Data Warehouse 페더레이션된 id 사용 하 여 Azure AD의 사용자 이름 및 암호, Windows 통합 인증 또는 Azure AD 액세스 토큰을;를 사용 하 여 SQL Server 용 PHP 드라이버에는 이러한 기능에 대 한 부분 지원을 제공합니다.

Azure AD를 사용 하려면 사용 합니다 **인증** 키워드입니다. 값입니다 **인증** 걸릴 수 있습니다에 다음 표에 설명 되어 있습니다.

|키워드|값|설명|
|-|-|-|
|**인증**|(기본값)을 설정 하지|다른 키워드에 의해 결정 되는 인증 모드입니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. |
||`SqlPassword`|(Azure 인스턴스 수 있음)는 SQL Server 인스턴스를 직접 인증할 사용자 이름 및 암호를 사용 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 해야 합니다 **UID** 하 고 **PWD** 키워드입니다. |
||`ActiveDirectoryPassword`|사용자 이름 및 암호를 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다. 사용자 이름 및 암호를 사용 하 여 연결 문자열에 전달 해야 합니다 **UID** 하 고 **PWD** 키워드입니다. |

합니다 **인증** 키워드 연결 보안 설정에 영향을 줍니다. 기본적으로 다음 연결 문자열에 설정 된 경우는 **Encrypt** 키워드를 true로 설정 되어 있으므로 클라이언트에서 암호화를 요청 합니다. 또한 서버 인증서 유효성을 검사할 암호화 설정에 관계 없이 경우가 아니면 **TrustServerCertificate** 설정을 true로 합니다. 이는 서버 인증서 유효성이 검사 되지 않습니다 암호화 연결 문자열에 특별히 요청 될 하지 않는 한 보안 로그인 메서드를 줄이고 이전, 구분 됩니다.

Windows에서 SQL Server 용 PHP 드라이버를 사용 하 여 Azure AD 사용 하기 전에 설치를 확인 합니다 [Microsoft Online Services 로그인 도우미](https://www.microsoft.com/download/details.aspx?id=41950) (Linux 및 MacOS에 대 한 필요 없음).

#### <a name="limitations"></a>제한 사항

Windows에 기본 ODBC 드라이버 지원에 대 한 하나 더 많은 가치를 **인증** 키워드 **ActiveDirectoryIntegrated**, 하지만 PHP 드라이버를 모든 플랫폼에서이 값을 지원 하지 않습니다 이므로 Azure AD 토큰 기반 인증을 지원 하지 않습니다.

## <a name="example"></a>예제

다음 예제에서는 사용 하 여 연결 하는 방법을 보여 줍니다 **SqlPassword** 하 고 **ActiveDirectoryPassword**합니다.

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

다음 예에서는 동일 위에 PDO_SQLSRV 드라이버를 사용 하 여 수행합니다.

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
## <a name="see-also"></a>참고 항목  
[ODBC 드라이버에서 Azure Active Directory 사용](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)
