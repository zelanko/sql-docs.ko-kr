---
title: '자습서: SQL Server on Linux에 AD 인증 사용'
titleSuffix: SQL Server
description: 이 자습서에서는 SQL Server on Linux의 AD 인증에 대한 구성 단계를 제공합니다.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027334"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>자습서: SQL Server on Linux와 Active Directory 인증 사용

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

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

## <a id="join"></a> AD 도메인에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 가입

SQL Server Linux 호스트를 Active Directory 도메인 컨트롤러에 가입시켜야 합니다. Active Directory 도메인을 가입시키는 방법에 대한 자세한 내용은 [Linux 호스트의 SQL Server를 Active Directory 도메인에 가입](sql-server-linux-active-directory-join-domain.md)을 참조하세요.

## <a id="createuser"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 AD 사용자(또는 MSA) 만들기 및 SPN 설정

> [!NOTE]
> 다음 단계에서는 [정규화된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)을 사용합니다. **Azure**에서 계속하기 전에 **[AD 사용자를 만들어야](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 합니다.

1. 도메인 컨트롤러에서 [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 명령을 실행하여 만료하지 않는 암호를 사용하여 새 AD 사용자를 만듭니다. 다음 예제에서는 계정의 이름을 `mssql`로 지정하지만 계정 이름은 원하는 대로 지정할 수 있습니다. 계정의 새 암호를 입력하라는 메시지가 표시됩니다.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > SQL Server의 전용 AD 계정을 사용하는 것이 보안 모범 사례이므로, SQL Server의 자격 증명은 동일한 계정을 사용하는 다른 서비스와 공유되지 않습니다. 그러나 계정 암호(다음 단계에서 keytab 파일을 생성하는 데 필요함)를 알고 있는 경우 필요에 따라 기존 AD 계정을 다시 사용할 수 있습니다.

2. **setspn.exe** 도구를 사용하여 이 계정의 SPN(서비스 사용자 이름)을 설정합니다. SPN은 다음 예제에 지정된 대로 정확하게 형식을 지정해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트에서 `hostname --all-fqdns`를 실행하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 머신의 정규화된 도메인 이름을 찾을 수 있습니다. 다른 포트 번호를 사용하도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 구성한 경우가 아니면 TCP 포트는 1433이어야 합니다.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > `Insufficient access rights` 오류가 표시되면 도메인 관리자와 함께 이 계정의 SPN을 설정할 권한이 있는지 확인합니다.
   >
   > 나중에 TCP 포트를 변경하는 경우 새 포트 번호를 사용하여 **setspn** 명령을 다시 실행해야 합니다. 다음 섹션의 단계에 따라 SQL Server 서비스 keytab에 새 SPN을 추가해야 합니다.

자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.

## <a id="configurekeytab"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 keytab 구성

SQL Server 서비스 keytab 파일은 두 가지 방법으로 구성할 수 있습니다. 첫 번째 옵션은 UPN(머신 계정)을 사용하는 것이지만, 두 번째 옵션은 keytab 구성에서 MSA(관리 서비스 계정)를 사용하는 것입니다. 두 메커니즘은 모두 동일하게 작동하며 환경에 가장 적합한 방법을 선택할 수 있습니다.

두 경우에 모두, 이전 단계에서 만든 SPN이 필요하며 SPN을 keytab에 등록해야 합니다.

SQL Server 서비스 keytab 파일을 구성하려면:

1. 다음 섹션에서 [SPN keytab 항목](#spn)을 구성합니다.

1. 그런 다음, 각 섹션의 단계에 따라 keytab 파일에서 [UPN](#upn)(옵션 1) 또는 [MSA](#msa)(옵션 2) 항목을 추가합니다.

> [!IMPORTANT]
> UPN/MSA의 암호가 변경되거나 SPN이 할당된 계정의 암호가 변경된 경우 새 암호 및 KVNO(키 버전 번호)를 사용하여 keytab을 업데이트해야 합니다. 일부 서비스에서는 암호를 자동으로 순환시킬 수도 있습니다. 해당하는 계정에 대한 암호 순환 정책을 검토하고 예기치 않은 가동 중지 시간을 방지하기 위해 예약된 유지 관리 작업에 맞게 조정합니다.

### <a id="spn"></a> SPN keytab 항목

1. 이전 단계에서 만든 AD 계정의 KVNO(키 버전 번호)를 확인합니다. 일반적으로 2이지만, 계정 암호를 여러 번 변경한 경우에는 다른 정수일 수 있습니다. SQL Server 호스트 머신에서 다음 명령을 실행합니다.

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > SPN은 도메인을 통해 전파되는 데 몇 분 정도 걸릴 수 있습니다(특히 도메인이 클 경우). `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM` 오류가 표시되면 몇 분 정도 기다린 후 다시 시도하세요.  

1. **ktutil**을 시작합니다.

   ```bash
   sudo ktutil
   ```

1. 다음 명령을 사용하여 각 SPN의 keytab 항목을 추가합니다.

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Keytab을 파일에 쓴 다음, ktutil를 종료합니다.

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > **ktutil** 도구는 암호의 유효성을 검사하지 않으므로 메시지가 표시되면 암호를 올바르게 입력했는지 확인합니다.

### <a id="upn"></a> 옵션 1: UPN을 사용하여 keytab 구성

**ktutil**을 사용하여 keytab에 머신 계정을 추가합니다. 머신 계정(UPN이라고도 함)은 `<hostname>$@<realm.com>` 형식(예: `sqlhost$@CONTOSO.COM`)으로 **/etc/krb5.keytab**에 있어야 합니다. 이 항목을 **/etc/krb5.keytab**에서 **mssql.keytab**으로 복사합니다.

1. 다음 명령을 사용하여 **ktuil**을 시작합니다.

   ```bash
   sudo ktutil
   ```

1. **rkt** 명령을 사용하여 **/etc/krb5.keytab**에서 모든 항목을 읽습니다.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 다음으로, 항목을 나열합니다.

   ```bash
   list
   ```

1. UPN이 아닌 슬롯 번호로 모든 항목을 삭제합니다. 다음 명령을 반복하여 한 번에 하나씩 이 항목을 삭제합니다.

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 슬롯 1과 같은 항목을 삭제하면 모든 값이 1씩 위로 이동하여 배치됩니다. 즉, 슬롯 1의 항목이 삭제되면 슬롯 2의 항목이 슬롯 1로 이동합니다.

1. UPN 항목만 남을 때까지 항목을 다시 나열합니다.

   ```bash
   list
   ```

1. UPN 항목만 남아 있으면 **mssql.keytab**에 다음 값을 추가합니다.

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. **ktutil**을 종료합니다.

   ```bash
   quit
   ```

### <a id="msa"></a> 옵션 2:  MSA를 사용하여 keytab 구성

MSA 옵션의 경우 SQL Server의 Kerberos keytab을 만들어야 합니다. [첫 번째 단계에서 등록된 SPN](#spn) 및 SPN이 등록된 MSA의 자격 증명을 모두 포함해야 합니다. 

1. SPN keytab 항목을 만든 후 도메인에 가입된 Linux 머신에서 다음 명령을 실행합니다.

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   이 단계에서는 SPN 소유권이 할당된 사용자 계정의 KVNO를 표시합니다. 이 단계가 작동하려면 SPN이 생성되는 동안 MSA 계정에 할당되었어야 합니다. SPN이 MSA에 할당되지 않은 경우 현재 SPN 소유자 계정의 KVNO가 표시되며 이 KVNO는 구성에 사용할 수 없습니다.  

1. **ktutil**을 시작합니다.

   ```bash
   sudo ktutil
   ```

1. 다음 두 명령을 사용하여 MSA를 추가합니다.

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Keytab을 파일에 쓴 다음, ktutil를 종료합니다.

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. MSA 방법을 사용하는 경우 keytab 파일에 액세스하는 동안 사용할 MSA를 지정하려면 **mssql-conf** 도구를 사용하여 구성 옵션을 설정해야 합니다. 아래 값이 **/var/opt/mssql/mssql.conf**에 있는지 확인합니다.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > MSA 이름만 포함하고 도메인\계정 이름을 포함하지 않습니다.

## <a id="securekeytab"></a> Keytab 파일 보호

이 keytab 파일에 액세스할 수 있는 사용자는 도메인에서 SQL Server를 가장할 수 있으므로 mssql 계정에만 읽기 액세스 권한이 있도록 파일에 대한 액세스를 제한해야 합니다.

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Kerberos 인증에 keytab 파일을 사용하도록 SQL Server 구성

다음 단계를 사용하여 Kerberos 인증에 keytab 파일을 사용하기 시작하도록 SQL Server를 구성합니다.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

필요에 따라 도메인 컨트롤러에 대한 UDP 연결을 사용하지 않도록 설정하여 성능을 향상합니다. 대부분의 경우 도메인 컨트롤러에 연결할 때 UDP 연결이 지속적으로 실패하므로 **/etc/krb5.conf**에서 구성 옵션을 설정하여 UDP 호출을 건너뛸 수 있습니다. **/etc/krb5.conf**를 편집하고 다음 옵션을 설정합니다.

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

이제 다음과 같이 SQL Server에서 AD 기반 로그인을 사용할 수 있습니다.

## <a id="createsqllogins"></a> Transact-SQL에서 AD 기반 로그인 만들기

1. SQL Server에 연결하고 새 AD 기반 로그인을 만듭니다.

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 이제 로그인이 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 시스템 카탈로그 뷰에 나열되는지 확인합니다.

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> AD 인증을 사용하여 SQL Server에 연결

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

### <a name="ssms-on-a-domain-joined-windows-client"></a>도메인에 가입된 Windows 클라이언트의 SSMS

도메인 자격 증명을 사용하여 도메인에 가입된 Windows 클라이언트에 로그인합니다. SQL Server Management Studio가 설치되어 있는지 확인한 다음 **서버에 연결** 대화 상자에서 **Windows 인증**을 지정하여 SQL Server 인스턴스(예: `mssql-host.contoso.com`)에 연결합니다.

### <a name="ad-authentication-using-other-client-drivers"></a>다른 클라이언트 드라이버를 사용하는 AD 인증

다음 표에서는 다른 클라이언트 드라이버에 대한 권장 사항을 설명합니다.

| 클라이언트 드라이버 | 권장 |
|---|---|
| **JDBC** | Kerberos 통합 인증을 사용하여 SQL Server 연결 |
| **ODBC** | 통합 인증을 사용합니다. |
| **ADO.NET** | 연결 문자열 구문입니다. |

## <a id="additionalconfig"></a> 추가 구성 옵션

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

먼저, **disablessd** 및 **enablekdcfromkrb5conf**를 true로 설정한 다음, SQL Server를 다시 시작합니다.

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
