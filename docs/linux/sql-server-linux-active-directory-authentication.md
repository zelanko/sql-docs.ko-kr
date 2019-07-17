---
title: '자습서: Linux의 SQL Server에 대 한 AD 인증을 사용 합니다.'
titleSuffix: SQL Server
description: 이 자습서에서는 Linux의 SQL Server에 대 한 AD 인증에 대 한 구성 단계를 제공 합니다.
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027334"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>자습서: Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서를 구성 하는 방법에 설명 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 라고도 통합된 인증, Active Directory (AD) 인증을 지원 하기 위한 linux. 개요를 보려면 [Linux의 SQL Server에 대 한 Active Directory 인증](sql-server-linux-active-directory-auth-overview.md)합니다.

이 자습서는 다음 작업으로 이루어집니다.

> [!div class="checklist"]
> * 조인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 호스트
> * AD 사용자에 대 한 만들기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SPN 설정
> * 구성 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 키
> * Keytab 파일을 보호
> * Kerberos 인증에 대 한 키 파일을 사용 하도록 SQL Server 구성
> * TRANSACT-SQL에서 AD 기반 로그인 만들기
> * 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 인증을 사용 하 여

## <a name="prerequisites"></a>사전 요구 사항

AD 인증을 구성 하기 전에 해야 합니다.

* 네트워크에서 AD 도메인 컨트롤러 (Windows)를 설정  
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치
  * [Red Hat Enterprise Linux(RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server(SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 조인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 호스트

Active Directory 도메인 컨트롤러를 사용 하 여 SQL Server Linux 호스트를 조인 해야 합니다. Active directory 도메인에 가입 시키는 방법에 대 한 내용은 참조 하세요 [Active Directory 도메인에 Linux 호스트에서 SQL Server 조인](sql-server-linux-active-directory-join-domain.md)합니다.

## <a id="createuser"></a> AD 사용자 (또는 MSA)에 대 한 만들기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SPN 설정

> [!NOTE]
> 다음 단계를 사용 하 여 사용자 [정규화 된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)합니다. 있는 경우 **Azure**, 해야 **[만드십시오](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 계속 진행 하기 전에 합니다.

1. 도메인 컨트롤러에서 실행 합니다 [New-aduser](https://technet.microsoft.com/library/ee617253.aspx) 만료 되지 않는 암호를 사용 하 여 새 AD 사용자를 만들려면 PowerShell 명령입니다. 다음 예제에서는 계정 이름을 `mssql`, 있지만 계정 이름을 원하는 대로 수 있습니다. 계정의 새 암호를 입력 하 라는 메시지가 표시 됩니다.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 것이 전용 AD 계정이 SQL Server에 대 한 보안 모범 사례에 동일한 계정을 사용 하 여 다른 서비스를 사용 하 여 SQL Server 자격 증명이 공유 되지 않도록 합니다. 그러나 필요에 따라 다시 사용할 수 있습니다 기존 AD 계정 (다음 단계에서 keytab 파일을 생성 하려면 필요)이 표시 되는 계정의 암호를 알고 있는 경우.

2. 사용 하 여이 계정에 대 한 ServicePrincipalName (SPN)을 설정 합니다 **setspn.exe** 도구입니다. SPN은 다음 예제에서 지정 된 대로 포맷 되어야 합니다. 정규화 된 도메인 이름을 찾을 수 있습니다 합니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 하 여 호스트 컴퓨터 `hostname --all-fqdns` 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 합니다. 구성 하지 않으면 TCP 포트 1433 해야 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다른 포트 번호를 사용 하도록 합니다.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 오류가 나타나면 `Insufficient access rights`, 충분 한 권한이이 계정에 SPN을 설정할 수 있는 도메인 관리자에 게 문의 하십시오.
   >
   > 나중에 TCP 포트를 변경한 경우에 실행 해야 합니다 **setspn** 새 포트 번호를 사용 하 여 다시 명령을 합니다. 다음 섹션의 단계를 수행 하 여 SQL Server 서비스 키를 새 SPN을 추가 해야 합니다.

자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.

## <a id="configurekeytab"></a> 구성 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 키

두 가지 다른 SQL Server 서비스 keytab 파일을 구성 해야 합니다. 첫 번째 옵션 keytab 구성에서 두 번째 옵션을 관리 되는 서비스 계정 (MSA)을 사용 하는 동안 컴퓨터 계정 (UPN)를 사용 하는 것입니다. 두 메커니즘 모두 동일 하 게 작동 되며 사용자 환경에 가장 적합 한 방법을 선택할 수 있습니다.

두 경우 모두 이전 단계에서 만든 SPN이 필요 하 고는 keytab에서 SPN을 등록 해야 합니다.

SQL Server 서비스 keytab 파일을 구성 합니다.

1. 구성 합니다 [SPN keytab 항목](#spn) 다음 섹션에 있습니다.

1. 다음 중 하나 [UPN을 추가](#upn) (옵션 1) 또는 [MSA](#msa) (옵션 2) 항목 keytab 파일에서 각 섹션의 단계를 수행 합니다.

> [!IMPORTANT]
> UPN/MSA에 대 한 암호 변경 또는 Spn에 할당 되는 계정의 암호가 변경 된 경우에 새 암호 및 키 버전 번호 (KVNO) 사용 하 여는 keytab를 업데이트 해야 합니다. 일부 서비스는 암호를 자동으로 회전도 않을 수 있습니다. 해당 계정에 대 한 모든 암호 회전 정책을 검토 하 고 예기치 않은 가동 중지 시간을 방지 하려면 예약 된 유지 관리 작업을 사용 하 여 따르도록 합니다.

### <a id="spn"></a> SPN keytab 항목

1. 이전 단계에서 만든 AD 계정에 대 한 키 버전 번호 (KVNO)를 확인 합니다. 일반적으로 2, 있지만 여러 번 계정의 암호를 변경 하는 경우 다른 정수 수 있습니다. SQL Server 호스트 컴퓨터에서 다음 명령을 실행 합니다.

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > Spn은 도메인이 큰 경우에 도메인을 통해 전파 되는 데 몇 분 정도 걸릴 수 있습니다. 오류가 표시 되 면 `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, 몇 분 정도 기다렸다가 다시 시도 하십시오.  

1. 시작 **ktutil**:

   ```bash
   sudo ktutil
   ```

1. 다음 명령을 사용 하 여 각 SPN에 대 한 키 항목을 추가 합니다.

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. keytab 파일에 쓸 및 다음 ktutil를 종료 합니다.

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > 합니다 **ktutil** 하므로 반드시 입력 해야 해당 올바르게 메시지가 표시 되 면, 도구는 암호를 확인 하지 않습니다.

### <a id="upn"></a> 옵션 1: UPN을 사용 하 여 키를 구성 하려면

컴퓨터 계정을 사용 하 여 키에 추가할 **ktutil**합니다. (UPN) 컴퓨터 계정에 있으면 **/etc/krb5.keytab** 형태로 `<hostname>$@<realm.com>` (예를 들어 `sqlhost$@CONTOSO.COM`). 이러한 항목을 복사할 **/etc/krb5.keytab** 하 **mssql.keytab**합니다.

1. 시작 **ktuil** 다음 명령을 사용 하 여:

   ```bash
   sudo ktutil
   ```

1. 사용 된 **rkt** 모두에서 항목을 읽을 수 명령 **/etc/krb5.keytab**합니다.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 그런 다음 항목을 나열 합니다.

   ```bash
   list
   ```

1. 슬롯 번호로 UPN 없는 모든 항목을 삭제 합니다. 다음 명령을 반복 하 여 한 번에이 하나만이 수행 합니다.

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 경우 슬롯 1에 해당 위치로 이동 하 여 모든 값 슬라이드를 같은 항목이 삭제 됩니다. 즉, 슬롯 1의 항목이 삭제 될 때 슬롯 1에 슬롯 2에서에서 항목을 이동 합니다.

1. 항목을 다시까지 나열 UPN 항목만 유지 됩니다.

   ```bash
   list
   ```

1. UPN 항목만 유지 하는 경우 이러한 값을 추가 **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Quit **ktutil**합니다.

   ```bash
   quit
   ```

### <a id="msa"></a> 옵션 2:  MSA를 사용 하 여 키를 구성 하려면

MSA 옵션에 대 한 SQL Server의 Kerberos keytab을 만들어야 합니다. 모든 것이 있어야 합니다 [첫 번째 단계에서 등록 된 Spn](#spn) 및 Spn은 등록 되는 MSA에 대 한 자격 증명입니다. 

1. SPN keytab 후 다음 명령을 실행 하는 도메인에 가입 되어 있는 Linux 컴퓨터에서 항목이 생성 됩니다.

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   이 단계는 SPN 소유권을 할당 하는 사용자 계정의 KVNO를 표시 합니다. 작동 하려면이 단계에 대 한 SPN 해야에 할당 된 MSA 계정을 만드는 동안. SPN을 MSA를 할당 하지 않은 경우 현재 SPN 소유자 계정의 표시 KVNO 되어 올바른 구성에 사용할 수 없습니다.  

1. 시작 **ktutil**:

   ```bash
   sudo ktutil
   ```

1. 다음 두 명령 사용 하 여 MSA를 추가 합니다.

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. keytab 파일에 쓸 및 다음 ktutil를 종료 합니다.

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. 구성 옵션을 사용 하 여 설정 해야 MSA 접근 방식을 사용 하는 경우는 **mssql conf** keytab 파일에 액세스 하는 동안 사용할 MSA를 지정 하는 도구입니다. 아래 값은 보장 **/var/opt/mssql/mssql.conf**합니다.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > MSA 이름 및 도메인 \ 계정 이름이 아니라만 포함 됩니다.

## <a id="securekeytab"></a> Keytab 파일을 보호

이 keytab 파일에 대 한 액세스를 사용 하 여 모든 사용자가 도메인에 대해 SQL Server 가장을 mssql 계정에만 읽기 액세스 권한이 있도록 파일에 액세스를 제한 하 고 있는지 확인:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Kerberos 인증에 대 한 키 파일을 사용 하도록 SQL Server 구성

Kerberos 인증에 대 한 키 파일을 사용 하려면 SQL Server를 구성 하려면 다음 단계를 사용 합니다.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

필요에 따라 성능 향상을 위해 도메인 컨트롤러에 대 한 UDP 연결을 사용 하지 않도록 합니다. 대부분의 경우에서 UDP 연결 일관 되 게 실패 구성 옵션을 설정할 수 있는 도메인 컨트롤러에 연결할 때 **/etc/krb5.conf** 건너뛸 UDP 호출 합니다. 편집할 **/etc/krb5.conf** 다음 옵션을 설정 합니다.

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

이 시점에서 SQL Server에 다음과 같이 AD 기반 로그인을 사용할 준비가 되었습니다.

## <a id="createsqllogins"></a> TRANSACT-SQL에서 AD 기반 로그인 만들기

1. SQL Server에 연결 하 고 새 AD 기반 로그인을 만듭니다.

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 로그인에 이제 나열 되어 있는지 확인 합니다 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 시스템 카탈로그 뷰:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> AD 인증을 사용 하 여 SQL Server에 연결

도메인 자격 증명을 사용 하 여 클라이언트 컴퓨터에 로그인 합니다. 이제 AD 인증을 사용 하 여 암호를 다시 입력 하지 않고도 SQL Server에 연결할 수 있습니다. AD 그룹에 대 한 로그인을 만들면 해당 그룹의 구성원 인 모든 AD 사용자는 동일한 방식으로 연결할 수 있습니다.

AD 인증을 사용 하는 클라이언트에 대 한 특정 연결 문자열 매개 변수는 사용 중인 드라이버에 따라 다릅니다. 다음 섹션의 예제를 고려해 야 합니다.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>도메인에 가입 된 Linux 클라이언트에서 sqlcmd

사용 하 여 도메인에 가입 된 Linux 클라이언트에 로그인 **ssh** 및 도메인 자격 증명:

```bash
ssh -l user@contoso.com client.contoso.com
```

이전에 설치한 있는지 확인 합니다 [mssql 도구](sql-server-linux-setup-tools.md) 패키지를 사용 하 여 연결 **sqlcmd** 자격 증명을 지정 하지 않고:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>도메인에 가입 된 Windows 클라이언트에서 SSMS

도메인 자격 증명을 사용 하는 도메인에 가입 된 Windows 클라이언트에 로그인 합니다. SQL Server Management Studio가 설치 되었는지 확인 한 다음 SQL Server 인스턴스에 연결할 (예를 들어 `mssql-host.contoso.com`)를 지정 하 여 **Windows 인증** 에 **서버에 연결** 대화 합니다.

### <a name="ad-authentication-using-other-client-drivers"></a>다른 클라이언트 드라이버를 사용 하 여 AD 인증

다음 표에서 다른 클라이언트 드라이버에 대 한 권장 사항을 설명합니다.

| 클라이언트 드라이버 | 권장 |
|---|---|
| **JDBC** | SQL Server에 연결할 Kerberos 통합된 인증을 사용 합니다. |
| **ODBC** | 통합된 인증을 사용 합니다. |
| **ADO.NET** | 연결 문자열 구문입니다. |

## <a id="additionalconfig"></a> 추가 구성 옵션

와 같은 타사 유틸리티를 사용 하는 경우 [PBI](https://www.beyondtrust.com/)하십시오 [VAS](https://www.oneidentity.com/products/authentication-services/), 또는 [Centrify](https://www.centrify.com/) AD Linux 호스트에 연결할 도메인을 하려고 합니다 openldap를 사용 하 여 SQL server 요구 라이브러리를 직접 구성할 수 있습니다 합니다 **disablesssd** 옵션을 **mssql conf** 다음과 같습니다.

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> 와 같은 유틸리티는 **realmd** 는 SSSD, 다른 도구는 동안 같은 대로 설정 PBI, VAS 및 Centrify SSSD 설치 되지 않습니다. 구성에 권장 되는 AD 도메인에 가입 하는 데 사용 하는 유틸리티 SSSD 설치 하지 않습니다 하는 경우 **disablesssd** 옵션을 `true`입니다. 아니지만 필수 SQL Server는 SSSD openldap 메커니즘으로 대체 하기 전에 AD에 대 한 사용 하려고 하는 대로, 뛰어난 SQL Server 호출 openldap SSSD 메커니즘을 우회 하 여 직접 않도록 구성 됩니다.

도메인 컨트롤러 LDAPS를 지 원하는 경우 LDAPS를 통해 되도록 도메인 컨트롤러에 SQL Server에서 모든 연결을 강제할 수 있습니다. 클라이언트 ldaps의 경우 다음 bash 명령을 실행을 통해 도메인 컨트롤러에 연결할 수를 확인 하려면 `ldapsearch -H ldaps://contoso.com:3269`합니다. SQL Server만 LDAPS를 사용 하도록 설정 하려면 다음을 실행 합니다.

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

이 사용 하 여 LDAPS SSSD AD 도메인에 가입 하는 경우 호스트는 SSSD 패키지가 통해 수행 됨 및 **disablesssd** 설정 되어 있지 않으면 true로 합니다. 하는 경우 **disablesssd** 로 설정 되어 함께 true **forcesecureldap** 을 true로 설정 되 고 SQL Server가 수행한 openldap 라이브러리 호출을 통해 LDAPS 프로토콜을 사용 합니다.

### <a name="post-sql-server-2017-cu14"></a>Post SQL Server 2017 CU14

타사 공급자를 사용 하 여 AD 도메인 컨트롤러에 가입 된 SQL Server 설정 하 여 일반 AD 조회를 위해 openldap 호출을 사용 하도록 구성 된 경우 SQL Server 2017 CU14부터 **disablesssd** 에 true를 이용할 수 있습니다 **enablekdcfromkrb5** KDC 서버에 대 한 역방향 DNS 조회 하는 대신 KDC 조회에 대 한 강화 하려면 krb5 라이브러리를 사용 하도록 SQL Server에 적용할 옵션입니다.

이 SQL Server와 통신 하려고 하는 도메인 컨트롤러를 수동으로 구성 하려는 시나리오에 유용할 수 있습니다. Openldap 라이브러리 메커니즘을 사용 하 여 KDC 목록을 사용 하 여 **krb5.conf**합니다.

먼저 설정 **disablessd** 하 고 **enablekdcfromkrb5conf** true 및 다음 SQL Server를 다시 시작 하려면:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

KDC 목록에서 구성한 **/etc/krb5.conf** 다음과 같습니다.

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 와 같은 유틸리티를 사용할 수 있기 권장 되지는 않지만 **realmd**, SSSD 구성 하는 동안 Linux 호스트를 도메인에 가입 하는 동안 설정 된 **disablesssd** SQL Server 사용 되도록 true openldap 호출 대신 Active Directory에 대 한 SSSD의 관련 호출 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Linux의 SQL Server를 사용 하 여 Active Directory 인증을 설정 하는 방법을 단계별로 안내 합니다. 방법을 배웠습니다에:
> [!div class="checklist"]
> * 조인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 호스트
> * AD 사용자에 대 한 만들기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SPN 설정
> * 구성 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 키
> * TRANSACT-SQL에서 AD 기반 로그인 만들기
> * 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 인증을 사용 하 여

다음으로, Linux에서 SQL Server에 대 한 다른 보안 시나리오를 탐색 합니다.

> [!div class="nextstepaction"]
> [Linux의 SQL Server에 대 한 연결 암호화](sql-server-linux-encrypted-connections.md)
