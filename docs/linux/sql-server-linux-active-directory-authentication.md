---
title: '자습서: SQL Server on Linux에 AD 인증 사용'
titleSuffix: SQL Server
description: 이 자습서에서는 SQL Server on Linux의 AD(Active Directory) 인증 구성 단계를 제공합니다.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 12/18/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 7c93711eae4a6a2eea397940811089f366e47829
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896960"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>자습서: SQL Server on Linux와 Active Directory 인증 사용

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 자습서에서는 통합 인증이라고도 하는 AD(Active Directory) 인증을 지원하도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux를 구성하는 방법을 설명합니다. 개요에 대해서는 [Linux의 SQL Server에 대한 Active Directory 인증](sql-server-linux-active-directory-auth-overview.md)을 참조하세요.

이 자습서는 다음 작업으로 구성됩니다.

> [!div class="checklist"]
> * AD 도메인에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 가입
> * [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 AD 사용자 만들기 및 SPN 설정
> * [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 keytab 구성
> * Keytab 파일 보호
> * Kerberos 인증에 keytab 파일을 사용하도록 SQL Server 구성
> * Transact-SQL에서 AD 기반 로그인 만들기
> * AD 인증을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결

## <a name="prerequisites"></a>사전 요구 사항

AD 인증을 구성하기 전에 다음을 수행해야 합니다.

* 네트워크에서 AD 도메인 컨트롤러(Windows) 설정  
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치
  * [Red Hat Enterprise Linux(RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server(SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a name="join-ssnoversion-host-to-ad-domain"></a><a id="join"></a> AD 도메인에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 가입

SQL Server Linux 호스트를 Active Directory 도메인 컨트롤러에 연결합니다. Active Directory 도메인을 가입시키는 방법에 대한 자세한 내용은 [Linux 호스트의 SQL Server를 Active Directory 도메인에 가입](sql-server-linux-active-directory-join-domain.md)을 참조하세요.

## <a name="create-ad-user-or-msa-for-ssnoversion-and-set-spn"></a><a id="createuser"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 AD 사용자(또는 MSA) 만들기 및 SPN 설정

> [!NOTE]
> 다음 단계에서는 [정규화된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)을 사용합니다. **Azure**에서 계속하기 전에 **[AD 사용자를 만들어야](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 합니다.

1. 도메인 컨트롤러에서 [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 명령을 실행하여 만료하지 않는 암호를 사용하여 새 AD 사용자를 만듭니다. 다음 예제에서는 계정의 이름을 `mssql`로 지정하지만 계정 이름은 원하는 대로 지정할 수 있습니다. 계정의 새 암호를 입력하라는 메시지가 표시됩니다.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > SQL Server의 전용 AD 계정을 사용하는 것이 보안 모범 사례이므로, SQL Server의 자격 증명은 동일한 계정을 사용하는 다른 서비스와 공유되지 않습니다. 그러나 계정 암호(다음 단계에서 keytab 파일을 생성하는 데 필요함)를 알고 있는 경우 필요에 따라 기존 AD 계정을 다시 사용할 수 있습니다. 또한 사용자 계정에서 128비트 및 256비트 Kerberos AES 암호화(**msDS-SupportedEncryptionTypes** 특성)를 지원하도록 계정을 활성화해야 합니다.

2. **setspn.exe** 도구를 사용하여 이 계정의 SPN(서비스 사용자 이름)을 설정합니다. SPN은 다음 예제에 지정된 대로 정확하게 형식을 지정해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트에서 `hostname --all-fqdns`를 실행하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 머신의 정규화된 도메인 이름을 찾을 수 있습니다. 다른 포트 번호를 사용하도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 구성한 경우가 아니면 TCP 포트는 1433이어야 합니다.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > `Insufficient access rights` 오류가 표시되면 도메인 관리자와 함께 이 계정의 SPN을 설정할 권한이 있는지 확인합니다. SPN을 등록하는 데 사용되는 계정에 **servicePrincipalName 쓰기** 권한이 있어야 합니다. 자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.
   >
   > 나중에 TCP 포트를 변경하는 경우 새 포트 번호를 사용하여 **setspn** 명령을 다시 실행해야 합니다. 다음 섹션의 단계에 따라 SQL Server 서비스 keytab에 새 SPN을 추가해야 합니다.

자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.

## <a name="configure-ssnoversion-service-keytab"></a><a id="configurekeytab"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 keytab 구성

SQL Server on Linux에 AD 인증을 구성하려면 이전 섹션에서 만든 AD 계정(MSA 또는 AD 사용자 계정)과 SPN이 필요합니다.

> [!IMPORTANT]
> AD 계정의 암호를 변경했거나 SPN이 할당된 계정의 암호를 변경한 경우 새 암호와 KVNO(키 버전 번호)를 사용하여 keytab을 업데이트해야 합니다. 일부 서비스에서는 암호를 자동으로 순환시킬 수도 있습니다. 해당하는 계정에 대한 암호 순환 정책을 검토하고 예기치 않은 가동 중지 시간을 방지하기 위해 예약된 유지 관리 작업에 맞게 조정합니다.

### <a name="spn-keytab-entries"></a><a id="spn"></a> SPN keytab 항목

1. 이전 단계에서 만든 AD 계정의 KVNO(키 버전 번호)를 확인합니다. 일반적으로 2이지만, 계정 암호를 여러 번 변경한 경우에는 다른 정수일 수 있습니다. SQL Server 호스트 머신에서 다음 명령을 실행합니다.

    - 아래 예제에서는 `user`가 `@CONTOSO.COM` 도메인에 있다고 가정합니다. 사용자 및 도메인 이름을 해당 사용자 및 도메인 이름으로 수정합니다.

   ```bash
   kinit user@CONTOSO.COM
   kvno user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > SPN은 도메인을 통해 전파되는 데 몇 분 정도 걸릴 수 있습니다(특히 도메인이 클 경우). `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM` 오류가 표시되면 몇 분 정도 기다린 후 다시 시도하세요.</br></br> 위 명령은 이전 섹션에서 설명한 것처럼 서버가 AD 도메인에 가입된 경우에만 작동합니다.

1. [**ktpass**](/windows-server/administration/windows-commands/ktpass)를 사용하여 Windows 머신 명령 프롬프트에서 다음 명령을 통해 각 SPN의 keytab 항목을 추가합니다.

    - `<DomainName>\<UserName>` - MSA 또는 AD 사용자 계정일 수 있습니다.
    - `@CONTOSO.COM` - 해당 도메인 이름을 사용합니다.
    - `/kvno <#>` - `<#>`을 이전 단계에서 가져온 KVNO로 바꿉니다.
    - `<StrongPassword>` - 강력한 암호를 사용합니다.

   ```bash
   ktpass /princ MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<netbios name of the host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<netbios name of the host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ <UserName>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ <UserName>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>
   ```

   > [!NOTE]
   > 위 명령은 AD 인증에 AES 및 RC4 암호화 암호를 모두 허용합니다. RC4는 이전 암호화 암호이며, 더 높은 수준의 보안이 필요한 경우 AES 암호화 암호로만 keytab 항목을 만들도록 선택할 수 있습니다.
   > 마지막 두 `UserName` 항목은 소문자여야 합니다. 그렇지 않으면 권한 인증에 실패할 수 있습니다.

1. 위 명령을 실행하면 mssql.keytab이라는 keytab 파일이 생성됩니다. SQL Server 머신의 `/var/opt/mssql/secrets` 폴더에 파일을 복사합니다.

1. keytab 파일을 보호합니다.

    이 keytab 파일에 액세스할 수 있는 사용자는 도메인에서 SQL Server를 가장할 수 있으므로 mssql 계정에만 읽기 액세스 권한이 있도록 파일에 대한 액세스를 제한해야 합니다.

    ```bash
    sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
    sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
    ```

1. **mssql-conf** 도구로 다음 구성 옵션을 설정하여 keytab 파일에 액세스하는 동안 사용할 계정을 지정해야 합니다.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <username>
   ```

   > [!NOTE]
   > 사용자 이름만 포함하고 domainname\username 또는 username@domain을 사용하지 않습니다. SQL Server에서 사용 시 필요한 경우 이 사용자 이름과 함께 도메인 이름을 내부적으로 추가합니다.

1. 다음 단계를 사용하여 Kerberos 인증에 keytab 파일을 사용하도록 SQL Server를 구성합니다.

    ```bash
    sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
    sudo systemctl restart mssql-server
    ```

    > [!TIP]
    > 필요에 따라 도메인 컨트롤러에 대한 UDP 연결을 사용하지 않도록 설정하여 성능을 향상합니다. 대부분의 경우 도메인 컨트롤러에 연결할 때 UDP 연결이 지속적으로 실패하므로 **/etc/krb5.conf**에서 구성 옵션을 설정하여 UDP 호출을 건너뛸 수 있습니다. **/etc/krb5.conf**를 편집하고 다음 옵션을 설정합니다.
    > ```bash
    > /etc/krb5.conf
    > [libdefaults]
    > udp_preference_limit=0
    > ```

이제 SQL Server에서 AD 기반 로그인을 사용할 수 있습니다.

## <a name="create-ad-based-logins-in-transact-sql"></a><a id="createsqllogins"></a> Transact-SQL에서 AD 기반 로그인 만들기

1. SQL Server에 연결하고 새 AD 기반 로그인을 만듭니다.

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 이제 로그인이 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 시스템 카탈로그 뷰에 나열되는지 확인합니다.

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a name="connect-to-sql-server-using-ad-authentication"></a><a id="connect"></a> AD 인증을 사용하여 SQL Server에 연결

도메인 자격 증명을 사용하여 클라이언트 머신에 로그인합니다. 이제 AD 인증을 사용하여 암호를 다시 입력하지 않고 SQL Server에 연결할 수 있습니다. AD 그룹에 대한 로그인을 만드는 경우 해당 그룹의 멤버인 모든 AD 사용자는 동일한 방식으로 연결할 수 있습니다.

AD 인증을 사용할 클라이언트의 특정 연결 문자열 매개 변수는 사용 중인 드라이버에 따라 달라집니다. 다음 섹션의 예제를 살펴보세요.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>도메인에 가입된 Linux 클라이언트의 sqlcmd

**ssh** 및 도메인 자격 증명을 사용하여 도메인에 가입된 Linux 클라이언트에 로그인합니다.

```bash
ssh -l user@contoso.com client.contoso.com
```

[mssql-tools](sql-server-linux-setup-tools.md) 패키지를 설치했는지 확인한 다음, 자격 증명을 지정하지 않고 **sqlcmd**를 사용하여 연결합니다.

```bash
sqlcmd -S mssql-host.contoso.com
```
SQL Windows와 달리 Kerberos 인증은 SQL Linux의 로컬 연결에서 작동합니다. 그러나 SQL Linux 호스트의 FQDN을 제공해야 하며 ‘.’, ‘localhost’, ‘127.0.0.1’ 등에 연결하려고 하면 AD 인증이 작동하지 않습니다.

### <a name="ssms-on-a-domain-joined-windows-client"></a>도메인에 가입된 Windows 클라이언트의 SSMS

도메인 자격 증명을 사용하여 도메인에 가입된 Windows 클라이언트에 로그인합니다. SQL Server Management Studio가 설치되어 있는지 확인한 다음 **서버에 연결** 대화 상자에서 **Windows 인증**을 지정하여 SQL Server 인스턴스(예: `mssql-host.contoso.com`)에 연결합니다.

### <a name="ad-authentication-using-other-client-drivers"></a>다른 클라이언트 드라이버를 사용하는 AD 인증

다음 표에서는 다른 클라이언트 드라이버에 대한 권장 사항을 설명합니다.

| 클라이언트 드라이버 | 권장 |
|---|---|
| **JDBC** | Kerberos 통합 인증을 사용하여 SQL Server 연결 |
| **ODBC** | 통합 인증을 사용합니다. |
| **ADO.NET** | 연결 문자열 구문입니다. |

## <a name="additional-configuration-options"></a><a id="additionalconfig"></a> 추가 구성 옵션

[PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) 또는 [Centrify](https://www.centrify.com/)와 같은 타사 유틸리티를 사용하여 Linux 호스트를 AD 도메인에 가입시키며 openldap 라이브러리를 직접 사용할 때 SQL Server를 강제 실행하려는 경우 다음과 같이 **mssql-conf**를 사용하여 **disablesssd** 옵션을 구성할 수 있습니다.

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> SSSD를 설정하는 **realmd**와 같은 유틸리티가 있지만, PBIS, VAS 및 Centrify와 같은 다른 도구는 SSSD를 설정하지 않습니다. AD 도메인에 가입하는 데 사용되는 유틸리티가 SSSD를 설정하지 않는 경우 **disablesssd** 옵션을 `true`로 구성하는 것이 좋습니다. SQL Server는 openldap 메커니즘으로 대체되기 전에 AD에 SSSD를 사용하려고 시도하므로 이 구성이 필요하지 않지만, 이와 같이 구성하면 SQL Server가 직접 openldap를 호출하여 SSSD 메커니즘을 무시하므로 성능이 향상됩니다.

도메인 컨트롤러에서 LDAPS를 지원하는 경우 SQL Server에서 도메인 컨트롤러로 모든 연결이 LDAPS를 통해 수행되도록 할 수 있습니다. 클라이언트에서 ldaps를 통해 도메인 컨트롤러에 연결할 수 있는지 확인하려면 bash 명령 `ldapsearch -H ldaps://contoso.com:3269`를 실행합니다. LDAPS만 사용하도록 SQL Server를 설정하려면 다음을 실행합니다.

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

호스트의 AD 도메인 가입이 SSSD 패키지를 통해 수행되었고 **disablesssd**가 true로 설정되지 않은 경우에는 여기에는 SSSD를 통해 LDAPS가 사용됩니다. **disablesssd**가 true로 설정되고 **forcesecureldap**가 true로 설정된 경우에는 SQL Server에서 수행된 openldap 라이브러리 호출을 통해 LDAPS 프로토콜이 사용됩니다.

### <a name="post-sql-server-2017-cu14"></a>Post SQL Server 2017 CU14

SQL Server 2017 CU14부터, SQL Server가 타사 공급자를 사용하여 AD 도메인 컨트롤러에 가입되었고 **disablesssd**를 true로 설정하여 일반적인 AD 조회에 openldap 호출을 사용하도록 구성된 경우에는 **enablekdcfromkrb5** 옵션을 사용하여 SQL Server에서 KDC 서버에 대한 역방향 DNS 조회 대신에 krb5 라이브러리를 KDC 조회에 사용하도록 할 수 있습니다.

이 방법은 SQL Server가 통신을 시도하는 도메인 컨트롤러를 수동으로 구성하려는 시나리오에 유용할 수 있습니다. 또한 **krb5.conf**에서 KDC 목록을 사용하여 openldap 라이브러리 메커니즘을 사용합니다.

먼저 **disablesssd** 및 **enablekdcfromkrb5conf**를 true로 설정한 다음, SQL Server를 다시 시작합니다.

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

그런 다음, **/etc/krb5.conf**에서 다음과 같이 KDC 목록을 구성합니다.

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 권장하지는 않지만 SQL Server가 Active Directory 관련 호출에 SSSD 대신에 openldap 호출을 사용하도록 **disablesssd**를 true로 구성하면서 Linux 호스트를 도메인에 가입시키는 동안 SSSD를 설정하는 **realmd**와 같은 유틸리티를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 SQL Server on Linux를 사용하여 Active Directory 인증을 설정하는 방법을 살펴보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * AD 도메인에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 가입
> * [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 AD 사용자 만들기 및 SPN 설정
> * [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 keytab 구성
> * Transact-SQL에서 AD 기반 로그인 만들기
> * AD 인증을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결

다음에는 SQL Server on Linux의 다른 보안 시나리오를 살펴보겠습니다.

> [!div class="nextstepaction"]
> [SQL Server on Linux에 대한 연결 암호화](sql-server-linux-encrypted-connections.md)
