---
title: "Linux에서 SQL Server와 active Directory 인증 | Microsoft Docs"
description: "Linux에서 SQL Server에 대 한 AAD 인증에 대 한 구성 단계"
author: tmullaney
ms.date: 07/17/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, AAD authentication
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e6d1afdfa7b7d4ef1bfec4461badca746651c44
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="active-directory-authentication-with-sql-server-on-linux"></a>Linux에서 SQL Server와 active Directory 인증  
[!INCLUDE[tsql-appliesto-sslinx-only_md](../../docs/includes/tsql-appliesto-sslinx-only_md.md)]


이 문서에서는 구성 하는 방법에 설명 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] linux Active Directory (AD) 인증, 라고도 통합된 인증을 지원 하도록 합니다. AD 인증을 통해 인증 하는 데 Windows 또는 Linux에서 도메인에 가입 된 클라이언트 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 해당 도메인 자격 증명 및 Kerberos 프로토콜을 사용 하 여 합니다. AD 인증을 통해 다음과 같은 이점을 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 인증:  
• 사용자가 암호를 입력 하지 않고 single sign-on을 통해 인증 합니다.   
AD 그룹에 대 한 로그인을 만들어 •를 액세스 및 권한을 관리할 수 있습니다 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] AD 그룹 멤버 자격을 사용 하 여 합니다.  
• 각 사용자 id를 가진 단일 조직 전체에서 추적할 수는 없는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 사람에 해당 하는 로그인입니다.   
• AD를 사용 하면 조직 전체에서 중앙 집중화 된 암호 정책을 적용할 수 있습니다.   

## <a name="prerequisites"></a>필수 구성 요소
AD 인증을 구성 하기 전에 해야 합니다.
- 네트워크에서 AD 도메인 컨트롤러 (Windows) 설정  
- [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 설치
  - [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  - [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  - [Ubuntu](quickstart-install-connect-ubuntu.md)

>  [!IMPORTANT]  
>   이 경우 데이터베이스 미러링 끝점에 지원 되는 유일한 인증 방법에는 인증서입니다. 이후 버전에서 WINDOWS 인증 방법을 설정 됩니다.

## <a name="step-1-join-includessnoversiondocsincludesssnoversion-mdmd-host-to-ad-domain"></a>1 단계: 조인 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] AD 도메인에 호스트
참가할 수 있도록 있는 다양 한 도구는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] AD 도메인에 호스트 컴퓨터. 이 연습에서는  **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)**, 인기 있는 오픈 소스 패키지 합니다. 아직 하지 않는 경우에 realmd와 Kerberos 클라이언트 패키지가 설치는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Linux 배포판의 패키지 관리자를 사용 하 여 호스트 컴퓨터:  
```bash  
# RHEL
sudo yum install realmd krb5-workstation

# SUSE
sudo zypper install realmd krb5-client

# Ubuntu
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```  

Kerberos 클라이언트 패키지 설치 영역 이름을 요청 하는 경우 도메인 이름을 대문자로 입력 합니다.  

>  [!NOTE]  
>  이 연습에서는 "contoso.com" 및 "CONTOSO.COM" 예제 도메인 및 영역 이름으로 각각 사용 됩니다. 이러한 고유한 값으로 바꿔야 합니다. 이러한 명령은 대/소문자, 하므로 반드시 사용 대문자이 연습에서 사용 될 때마다 합니다.  

확인 하려면 다음 명령을 실행 하는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 컴퓨터와 DNS 이름 서버에 대 한 AD 도메인 컨트롤러를 사용 하도록 구성 된:
```bash  
sudo realm discover contoso.com -v
```  
구성 해야 하는 도메인이 없는 경우 프로그램 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 컴퓨터를 AD 도메인 컨트롤러의 IP 주소는 DNS 이름 서버를 사용 합니다. 이렇게 하려면 특정 단계는 네트워크 장치 구성, 도메인 구성 및 Linux 배포 사항에 따라 달라 집니다. 다음은 몇 가지 예제 방식을입니다.

### <a name="example-dns-configuration-ubuntu"></a>DNS 구성의 예: Ubuntu
편집 된 `/etc/network/interfaces` 파일 AD 도메인 컨트롤러의 IP 주소는 dns 이름 서버 목록이 표시 됩니다. 예를 들어 
 
```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```  
>  [!NOTE]  
>  다른 컴퓨터에 대 한 네트워크 인터페이스 (eth0) 다를 수 있습니다. 사용 하는 어떤 것을 알아보려면 ifconfig를 실행 하 고 인터페이스에는 IP 주소와 전송 및 수신한 바이트를 복사 합니다.

이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.
```bash
sudo ifdown eth0 && sudo ifup eth0
```
이제 있는지 여부를 확인 하면 `/etc/resolv.conf` 파일에 다음과 같은 줄이 포함 되어 있습니다.  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="example-dns-configuration-rhel"></a>DNS 구성의 예: RHEL
편집의 `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일 (또는 다른 인터페이스 구성 파일을 적절 하 게)를 AD 도메인 컨트롤러의 IP 주소는 DNS 서버 목록이 표시 됩니다.

 ```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```
이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.
```bash
sudo systemctl restart network
```
이제 있는지 여부를 확인 하면 `/etc/resolv.conf` 파일에 다음과 같은 줄이 포함 되어 있습니다.  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="join-the-domain"></a>도메인에 가입
DNS가 올바르게 구성 되었는지 확인 하 고 나면 아래 명령을 실행 하 여 도메인에 가입 합니다. 새 컴퓨터를 도메인에 가입 하는 AD에 충분 한 권한을 가진 AD 계정을 사용 하 여 인증 해야 합니다. 이 명령은 AD에서 새 컴퓨터 계정을 만들를 만들기는 특히는 `/etc/krb5.keytab` keytab 파일을 호스트 하 고 있는 도메인의 구성 `/etc/sssd/sssd.conf`:
```bash                                     
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
 * Successfully enrolled machine in realm
```    

>  [!NOTE]  
>   오류 표시, "필요한 패키지가 설치 되지 않은" 경우 실행 하기 전에 Linux 배포판의 패키지 관리자를 사용 하 여 이러한 패키지를 설치 해야는 `realm join` 명령을 다시 합니다. 
>  
>  "에 도메인 가입 권한이" 오류가 발생 하는 경우 Linux 컴퓨터를 도메인에 연결 하려면 충분 한 권한이 있는지 도메인 관리자와 함께 확인 해야 합니다.

 
도메인에서 사용자에 대 한 정보를 수집할 이제 수 및 해당 사용자로 Kerberos 티켓을 얻을 수 있습니다를 확인 합니다. 

We will use **id**, **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)** and **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** commands for this.

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

>  [!NOTE]  
>   경우 `id user@contoso.com` 반환, "사용자," 명령을 실행 하 여 SSSD 서비스가 성공적으로 시작 되었는지 확인 `sudo systemctl status sssd`합니다. 서비스를 실행 하는 경우 "사용자" 오류가 표시 SSSD에 대 한 자세한 정보 로깅을 사용 하도록 설정 하십시오. 자세한 내용은 Red Hat 설명서를 참조 [문제 해결 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)합니다.  
>  
>  경우 `kinit user@CONTOSO.COM` "KDC 회신 일치 하지 않습니다 기대 초기 자격 증명을 가져오는 동안" 반환 대문자로 표시 영역을 지정 했는지 확인 합니다.

자세한 내용은 Red Hat 설명서를 참조 [Discovering 및 Id 도메인이 가입](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)합니다. 

## <a name="step-2-create-ad-user-for-includessnoversiondocsincludesssnoversion-mdmd-and-set-spn"></a>2 단계: AD 사용자에 대 한 만들기 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] SPN을 설정 하 고  

>  [!NOTE]  
>  다음 단계는 사용 하면 [정규화 된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)합니다. 사용 중인 **Azure**, ´ ë ç  **[만드세요](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)**  계속 진행 하기 전에. 

도메인 컨트롤러에서 실행 하는 [New-aduser](https://technet.microsoft.com/library/ee617253.aspx) 만료 되지 않는 암호를 사용 하 여 새 AD 사용자를 만들려면 PowerShell 명령입니다. 이 예에서는 "mssql," 계정 이름이 되지만 필요 하면 계정 이름이 될 수 있습니다. 계정의 새 암호를 입력 하 라는 메시지가 표시 됩니다.  
```PowerShell   
Import-Module ActiveDirectory

New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
```   

>  [!NOTE]  
>  전용 AD 계정이 SQL Server에 대 한 보안 모범 사례는 하는 SQL Server 자격 증명 동일한 계정을 사용 하 여 다른 서비스와 공유 되지 않도록 합니다. 그러나 재사용할 수 있습니다 기존 AD 계정 원하는 경우 (다음 단계에서는 keytab 파일을 생성 하는 데 필요) 계정의 암호를 알고 있는 경우.

지금 사용 하 여이 계정에 대 한 서비스 사용자 이름 (SPN) 설정에서 `setspn.exe` 도구입니다. SPN은 다음 예제에 지정 된 대로 형식 이어야 합니다:의 정규화 된 도메인 이름을 찾을 수 있습니다는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 컴퓨터를 실행 하 여 `hostname --all-fqdns` 에 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 및 TCP 포트는 1433 이어야 함 구성 하지 않으면 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 다른 포트 번호를 사용 하도록 합니다.  
```PowerShell   
setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
```   

>  [!NOTE]  
>  "액세스 권한이 부족 합니다" 오류가 발생 하는 경우 수 있는 충분 한 권한이이 계정에 SPN을 설정할 수는 도메인 관리자와 함께 확인 해야 합니다.
>  
>  나중에 TCP 포트를 변경 하면 새 포트 번호로 setspn 명령을 다시 실행 해야 합니다. 다음 섹션의 단계를 수행 하 여 SQL Server 서비스 keytab에 새 SPN을 추가 해야 합니다.

자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.  

## <a name="step-3-configure-includessnoversiondocsincludesssnoversion-mdmd-service-keytab"></a>3 단계: 구성 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 서비스 keytab  
먼저, 이전 단계에서 만든 AD 계정에 대 한 키 버전 번호 (kvno)를 확인 합니다. 일반적으로 2, 됩니다 이지만 여러 번 계정의 암호를 변경 하는 경우 다른 정수 수도 있습니다. 에 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 컴퓨터를 다음을 실행 합니다.

```bash
kinit user@CONTOSO.COM

kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
```

이제 이전 단계에서 만든 AD 사용자는 keytab 파일을 만듭니다. 사용 하 여 그렇게 하려면  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**합니다. 메시지가 표시 되 면 해당 AD 계정의 암호를 입력 합니다. 
```bash  
sudo ktutil

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

quit
```  

>  [!NOTE]  
>  Ktutil 도구 암호의 유효성을 검사 하지는 않으므로 올바르게 입력 있는지를 확인 합니다.

이에 액세스할 수 있는 모든 사용자 `keytab` 파일을 가장할 수 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 도메인에 있으므로 해야 이러한 파일에 대 한 액세스는 유일한는 `mssql` 계정에 대 한 읽기 액세스:  
```bash  
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```  
다음으로 구성 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 이 하 `keytab` Kerberos 인증에 대 한 파일:  
```bash  
sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```  

## <a name="step-4-create-ad-based-logins-in-transact-sql"></a>4 단계: transact-sql에서 AD 기반 로그인 만들기  
연결할 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 새, AD 기반 로그인을 만듭니다.  
```Transact-SQL  
CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
```   

로그인에 이제 나열 되어 있는지 확인 하십시오.는 [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql.mc) 시스템 카탈로그 뷰:  
```Transact-SQL  
SELECT name FROM sys.server_principals;
```  

## <a name="step-5-connect-to-includessnoversiondocsincludesssnoversion-mdmd-using-ad-authentication"></a>5 단계: 연결할 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] AD 인증을 사용 하 여  
도메인 자격 증명을 사용 하는 클라이언트 컴퓨터에 로그인 합니다. 에 연결할 수 이제 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] AD 인증을 사용 하 여 암호를 다시 입력 하지 않고도 합니다. AD 그룹에 대 한 로그인을 만들면 해당 그룹의 구성원 인 모든 AD 사용자는 동일한 방식으로 연결할 수 있습니다.  
AD 인증을 사용 하는 클라이언트에 대 한 특정 연결 문자열 매개 변수는 사용 중인 드라이버에 따라 다릅니다. 몇 가지 예는 다음과 같습니다.  

## <a name="examples"></a>예  
### <a name="example-1-sqlcmd-on-a-domain-joined-linux-client"></a>예제 1: `sqlcmd` 도메인에 가입 된 Linux 클라이언트에서  
사용 하 여 도메인에 가입 된 Linux 클라이언트에 로그인 `ssh` 및 도메인 자격 증명:  
```bash  
ssh -l user@contoso.com client.contoso.com
```  

이전에 설치한 있는지 확인은 [mssql 도구](sql-server-linux-setup-tools.md) 패키지 하 고, 다음 사용 하 여 연결 `sqlcmd` 자격 증명을 지정 하지 않고:  
```bash  
sqlcmd -S mssql.contoso.com
```  

### <a name="example-2-ssms-on-a-domain-joined-windows-client"></a>도메인에 가입 된 Windows 클라이언트에서 예 2: SSMS  
도메인 자격 증명을 사용 하는 도메인에 가입 된 Windows 클라이언트에 로그인 합니다. 있는지 확인 [!INCLUDE[ssmanstudiofull-md](../../docs/includes/ssmanstudiofull-md.md)] 설치 된 다음에 연결 하면 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 인스턴스를 지정 하 여 **Windows 인증** 에 **서버에 연결** 대화 합니다.  

### <a name="ad-authentication-using-other-client-drivers"></a>다른 클라이언트 드라이버를 사용 하 여 AD 인증  
• JDBC: [Kerberos를 사용 하 여 통합 인증을 SQL 서버에 연결 하려면](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server])  
• ODBC: [통합된 인증을 사용 하 여](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)  
• ADO.NET: [연결 문자열 구문](https://msdn.microsoft.com/library/ms254500.aspx)   


