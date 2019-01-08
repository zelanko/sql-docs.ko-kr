---
title: '자습서: Linux의 SQL Server에 대 한 active Directory 인증'
titleSuffix: SQL Server
description: 이 자습서에서는 Linux의 SQL Server에 대 한 AAD 인증에 대 한 구성 단계를 제공 합니다.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 237924a1bc4309b4e4d686076d1e0862ea3afe92
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160610"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>자습서: Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서를 구성 하는 방법에 설명 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 라고도 통합된 인증, Active Directory (AD) 인증을 지원 하기 위한 linux. 개요를 보려면 [Linux의 SQL Server에 대 한 Active Directory 인증](sql-server-linux-active-directory-auth-overview.md)합니다.

이 자습서는 다음 작업으로 이루어집니다.

> [!div class="checklist"]
> * 조인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 호스트
> * AD 사용자에 대 한 만들기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SPN 설정
> * 구성 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 키
> * TRANSACT-SQL에서 AD 기반 로그인 만들기
> * 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 인증을 사용 하 여

> [!NOTE]
>
> 구성 하려는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 타사 AD 공급자를 사용 하도록 linux에서 하세요 [타사 Active Directory 공급자를 사용 하 여 Linux의 SQL Server를 사용 하 여](./sql-server-linux-active-directory-third-party-providers.md)입니다.

## <a name="prerequisites"></a>사전 요구 사항

AD 인증을 구성 하기 전에 해야 합니다.

* 네트워크에서 AD 도메인 컨트롤러 (Windows)를 설정  
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 조인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 호스트

다음 단계를 사용 하 여 연결할는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Active Directory 도메인에 호스트 합니다.

1. 사용 하 여 **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** AD 도메인에 호스트 컴퓨터를 가입 합니다. 이미 않았다면에 realmd와 Kerberos 클라이언트 패키지가 설치 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux 배포판의 패키지 관리자를 사용 하 여 호스트 컴퓨터:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Kerberos 클라이언트 패키지 설치 요청 영역 이름, 도메인 이름을 대문자로 입력 합니다.

   > [!NOTE]
   > 이 연습에서는 "contoso.com" 및 "CONTOSO.COM" 예제 도메인 및 영역 이름으로 각각 합니다. 사용자 고유의 값을 사용 하 여 이러한 바꿔야 합니다. 이러한 명령은 대/소문자, 따라서 반드시 사용할 대문자이 연습에서 사용 될 때마다 합니다.

1. 구성 프로그램 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 컴퓨터는 DNS 이름 서버를 AD 도메인 컨트롤러의 IP 주소를 사용 합니다. 

   - **Ubuntu**:

      편집 된 `/etc/network/interfaces` 파일에 AD 도메인 컨트롤러의 IP 주소를 dns 이름 서버 목록이 표시 됩니다. 예를 들어: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auto eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > 네트워크 인터페이스 (eth0)는 서로 다른 컴퓨터에 대 한 다 수 있습니다. 사용 하는 어떤 것을 알아보려면 ifconfig를 실행 하 고 인터페이스에 IP 주소 및 전송 및 수신 바이트를 복사 합니다.

      이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:  

      ```/etc/resolv.conf
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     편집 된 `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일 (또는 다른 인터페이스 구성 파일을 적절 하 게) AD 도메인 컨트롤러의 IP 주소를 DNS 서버로 나열 됩니다.

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

     ```bash
     sudo systemctl restart network
     ```

     이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:  

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

   - **SLES**:

     편집 된 `/etc/sysconfig/network/config` AD 도메인 컨트롤러 IP가 DNS 쿼리에 사용할 수 있도록 파일 및 AD 도메인이 도메인 검색 목록에는:

     ```/etc/sysconfig/network/config
     <...>
     NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
     ```

     이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

     ```bash
     sudo systemctl restart network
     ```

     이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

1. 도메인에 가입

   DNS가 올바르게 구성 되었는지 확인 하 고 나면 다음 명령을 실행 하 여 도메인에 가입 합니다. 새 컴퓨터를 도메인에 가입 AD에 충분 한 권한이 있는 AD 계정을 사용 하 여 인증 해야 합니다.

   특히,이 명령은 AD에서 새 컴퓨터 계정을 만듭니다, 만들 합니다 `/etc/krb5.keytab` keytab 파일을 호스트 하 고 도메인에 구성 `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > 오류가 표시, "필요한 패키지가 설치 되지 않은" 경우 실행 하기 전에 Linux 배포판의 패키지 관리자를 사용 하 여 이러한 패키지를 설치 해야 합니다 `realm join` 명령을 다시 합니다.
   >
   > "권한 부족"는 도메인에 가입 하는 오류가 표시 되 면 Linux 컴퓨터를 도메인에 가입 하면 충분 한 권한이 있는지 도메인 관리자를 사용 하 여 확인 해야 합니다.
   >
   > "KDC 회신을 기대를 일치 하지 않습니다" 오류가 표시 다음 수 없습니다 지정 되어 있는지 사용자에 대 한 올바른 영역 이름입니다. 영역 이름 대/소문자, 대문자 일반적으로, 및 명령을 사용 하 여 식별할 수 있습니다 `realm discover contoso.com`합니다.
   
   > SQL Server 사용자 계정 및 그룹 보안 식별자 (SID)에 매핑하기 위한 SSSD 및 NSS를 사용 합니다. SSSD 구성 하 고 AD 로그인을 성공적으로 만들려면 SQL Server에 대 한 순서 대로 실행 해야 합니다. Realmd 일반적으로이 도메인에 가입의 일부로 자동으로 않지만 일부 경우에 이렇게 해야 별도로 있습니다.
   >
   > 구성 하려면 다음을 확인 [SSSD 수동으로](https://access.redhat.com/articles/3023951), 및 [SSSD 작업할 NSS 구성](https://access.redhat.com/documentation/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. 도메인에서 사용자에 대 한 정보를 수집할 이제 수 및 해당 사용자로 Kerberos 티켓을 얻을 수 있습니다는 확인 합니다.

   다음 예제에서는 **id**를  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, 및 **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** 이 대 한 명령입니다.

   ```bash
   id user@contoso.com
   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM
   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   <...>
   ```

   > [!NOTE]
   > 하는 경우 `id user@contoso.com` 반환 되는 경우 "사용자를" 명령을 실행 하 여 SSSD 서비스를 성공적으로 시작 되었는지 확인 `sudo systemctl status sssd`합니다. 서비스가 실행 되는 경우 "사용자" 오류가 계속 표시 SSSD에 대 한 자세한 정보 로깅을 사용 하도록 설정 하십시오. 자세한 내용은 Red Hat 설명서를 참조 [문제 해결 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)합니다.
   >
   > 경우 `kinit user@CONTOSO.COM` 반환 되는 경우 "KDC 회신 일치 하지 않습니다 기대 초기 자격 증명을 가져오는 동안" 대문자로 영역을 지정 했는지 확인 합니다.

자세한 내용은 Red Hat 설명서를 참조 [Discovering 및 Id 도메인이 가입](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)합니다. 

## <a id="createuser"></a> AD 사용자에 대 한 만들기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SPN 설정

  > [!NOTE]
  > 다음 단계를 사용 하 여 사용자 [정규화 된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)합니다. 있는 경우 **Azure**, 해야 **[만드십시오](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 계속 진행 하기 전에 합니다.

1. 도메인 컨트롤러에서 실행 합니다 [New-aduser](https://technet.microsoft.com/library/ee617253.aspx) 만료 되지 않는 암호를 사용 하 여 새 AD 사용자를 만들려면 PowerShell 명령입니다. 이 예에서는 "mssql," 계정 이름을 있지만 계정 이름을 원하는 대로 수 있습니다. 계정의 새 암호를 입력 하 라는 메시지가 표시 됩니다.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 것이 전용 AD 계정이 SQL Server에 대 한 보안 모범 사례에 동일한 계정을 사용 하 여 다른 서비스를 사용 하 여 SQL Server 자격 증명이 공유 되지 않도록 합니다. 그러나 다시 사용할 수 있습니다 기존 AD 계정을 원한다 면 (다음 단계에서 keytab 파일을 생성 하는 데 필요) 하는 계정의 암호를 알고 있는 경우.

2. 사용 하 여이 계정에 대 한 ServicePrincipalName (SPN)을 설정 합니다 `setspn.exe` 도구입니다. SPN은 다음 예제에서 지정 된 대로 포맷 되어야 합니다. 정규화 된 도메인 이름을 찾을 수 있습니다는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 하 여 호스트 컴퓨터 `hostname --all-fqdns` 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 및 TCP 포트를 구성 하지 않으면 1433를 이어야 합니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다른 포트 번호를 사용 하도록 합니다.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > "액세스 권한이 부족 합니다" 오류가 표시 되 면 다음 해야 수 있는 충분 한 권한이이 계정에 SPN을 설정 하는 도메인 관리자를 사용 하 여 확인 합니다.
   >
   > 나중에 TCP 포트를 변경한 경우 새 포트 번호를 사용 하 여 setspn 명령을 다시 실행 해야 합니다. 다음 섹션의 단계를 수행 하 여 SQL Server 서비스 키를 새 SPN을 추가 해야 합니다.

3. 자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.

## <a id="configurekeytab"></a> 구성 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 키

1. 이전 단계에서 만든 AD 계정에 대 한 키 버전 번호 (kvno)를 확인 합니다. 일반적으로 2, 있지만 여러 번 계정의 암호를 변경 하는 경우 다른 정수 수 있습니다. 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 호스트 컴퓨터에 다음을 실행 합니다.

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > Spn은 도메인이 큰 경우에 도메인을 통해 전파 되는 데 몇 분 정도 걸릴 수 있습니다. 오류를 수신 하는 경우 "kvno: MSSQLSvc에 대 한 자격 증명을 가져오는 동안 Kerberos 데이터베이스에서 발견 되지 않았음 /\*\*\<호스트 컴퓨터의 정규화 된 도메인 이름\>\*\*:\* \* \< tcp 포트\>\*\*\@CONTOSO.COM ", 몇 분 정도 기다렸다가 다시 시도 하십시오.

2. 사용 하 여 keytab 파일을 만듭니다 **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** 이전 단계에서 만든 AD 사용자에 대 한 합니다. 메시지가 표시 되 면 해당 AD 계정의 암호를 입력 합니다.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > Ktutil 도구 암호의 유효성을 검사 하지 않습니다 이므로 올바르게 입력 해야 합니다.

3. 컴퓨터 계정을 사용 하 여 키에 추가할  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** 합니다. (UPN) 컴퓨터 계정에 있으면 `/etc/krb5.keytab` 형태로 "\<hostname\>$\@\<realm.com\>" (예: sqlhost$\@CONTOSO.COM). 이러한 항목에서 복사 됩니다 `/etc/krb5.keytab` 에 `mssql.keytab`입니다.

   ```bash
   sudo ktutil

   # Read all entries from /etc/krb5.keytab
   ktutil: rkt /etc/krb5.keytab

   # List all entries
   ktutil: list

   # Delete all entries by their slot number which are not the UPN one at a
   # time.
   # Warning: when an entry is deleted (e.g. slot 1), all values slide up by
   # one to take its place (e.g. the entry in slot 2 moves to slot 1 when slot
   # 1's entry is deleted)
   ktutil: delent <slot num>
   ktutil: delent <slot num>
   ...

   # List all entries to ensure only UPN entries are left
   ktutil: list

   # When only UPN entries are left, append these values to mssql.keytab
   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

4. 이에 대 한 액세스를 사용 하 여 누구나 `keytab` 파일 가장할 수 있습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도메인에서 그러므로 이러한 파일에 대 한 액세스를 제한는 유일한는 `mssql` 계정에 대 한 읽기 액세스:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

5. 구성할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 사용 하도록 `keytab` Kerberos 인증에 대 한 파일:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

6. 선택 사항: 성능 향상을 위해 도메인 컨트롤러에 대 한 UDP 연결을 사용 하지 않도록 설정 합니다. 대부분의 경우에서 UDP 연결에 항상 실패 구성 옵션을 설정할 수 있는 도메인 컨트롤러에 연결할 때 `/etc/krb5.conf` 건너뛸 UDP 호출 합니다. 편집 `/etc/krb5.conf` 다음 옵션을 설정 합니다.

   ```/etc/krb5.conf
   [libdefaults]
   udp_preference_limit=0
   ```

## <a id="createsqllogins"></a> TRANSACT-SQL에서 AD 기반 로그인 만들기

1. 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 새, AD 기반 로그인을 만듭니다.

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. 로그인에 이제 나열 되어 있는지 확인 합니다 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 시스템 카탈로그 뷰:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 인증을 사용 하 여

도메인 자격 증명을 사용 하 여 클라이언트 컴퓨터에 로그인 합니다. 에 연결할 수 있습니다 이제 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 인증을 사용 하 여 암호를 다시 입력 하지 않고도 합니다. AD 그룹에 대 한 로그인을 만들면 해당 그룹의 구성원 인 모든 AD 사용자는 동일한 방식으로 연결할 수 있습니다.

AD 인증을 사용 하는 클라이언트에 대 한 특정 연결 문자열 매개 변수는 사용 중인 드라이버에 따라 다릅니다. 다음 예를 살펴봅니다.

* `sqlcmd` 도메인에 가입 된 Linux 클라이언트에서

   도메인에 가입 된 Linux 클라이언트를 사용 하 여 로그인 `ssh` 및 도메인 자격 증명:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   이전에 설치한 있는지 확인 합니다 [mssql 도구](sql-server-linux-setup-tools.md) 패키지를 사용 하 여 연결 `sqlcmd` 자격 증명을 지정 하지 않고:

   ```bash
   sqlcmd -S mssql-host.contoso.com
   ```

* 도메인에 가입 된 Windows 클라이언트에서 SSMS

   도메인 자격 증명을 사용 하는 도메인에 가입 된 Windows 클라이언트에 로그인 합니다. 있는지 확인 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 가 설치 되어 다음에 연결 하 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 (예: "mssql-host.contoso.com")을 지정 하 여 **Windows 인증** 에 **서버에 연결** 대화 합니다.

* 다른 클라이언트 드라이버를 사용 하 여 AD 인증

  * JDBC: [Kerberos 통합된 인증을 사용 하 여 SQL Server에 연결할](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [통합 인증 사용](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [연결 문자열 구문](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)

## <a name="performance-improvements"></a>성능 향상
AD 계정 조회 시간이 걸리고 있습니다 체크 표시 하는 경우 AD 구성의 단계를 사용 하 여 유효 [타사 AD 공급자를 통해 Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 하 여](sql-server-linux-active-directory-third-party-providers.md)를 추가할 수 있습니다는 줄 아래 `/var/opt/mssql/mssql.conf` 을 SSSD 호출을 건너뛰고 직접 LDAP 호출을 사용 합니다.

```/var/opt/mssql/mssql.conf
[network]
disablesssd = true
```

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
>[Linux의 SQL Server에 대 한 연결 암호화](sql-server-linux-encrypted-connections.md)
