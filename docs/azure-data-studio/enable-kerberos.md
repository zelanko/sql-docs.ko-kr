---
title: Active Directory 인증 사용 (Kerberos)
titleSuffix: Azure Data Studio
description: Azure Data Studio에 대 한 Active Directory 인증을 사용 하는 Kerberos를 사용 하는 방법 알아보기
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
ms.openlocfilehash: 5c8fae6bf1333742b40e9c8aae4ee575736058cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959660"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>연결 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Kerberos Windows 인증을 사용 하 여 SQL server 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] Kerberos를 사용 하 여 SQL Server에 연결을 지원 합니다.

MacOS 또는 Linux에서 통합 인증 (Windows 인증)을 사용 하려면 설정 해야는 **Kerberos 티켓** Windows 도메인 계정에 현재 사용자를 연결 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- Kerberos 도메인 컨트롤러를 쿼리 하기 위해 Windows 도메인에 가입 된 컴퓨터에 액세스 합니다.
- SQL Server는 Kerberos 인증을 허용 하도록 구성 되어야 합니다. 클라이언트 드라이버의 Unix에서 실행 되는 경우 통합된 인증 에서만 지원 됩니다 Kerberos를 사용 하 여. Kerberos를 사용 하 여 인증 하도록 Sql Server를 설정 하는 방법은 찾을 수 있습니다 [여기](https://support.microsoft.com/help/319723/how-to-use-kerberos-authentication-in-sql-server)합니다. 에 연결 하려는 Sql Server의 각 인스턴스에 대해 등록 된 Spn이 있어야 합니다. SQL Server Spn의 형식에 대 한 자세한 내용은 [여기](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Sql Server가 Kerberos 설정 하는 경우 확인

Sql Server의 호스트 컴퓨터에 로그인 합니다. Windows 명령 프롬프트에서 사용 된 `setspn -L %COMPUTERNAME%` 호스트에 대 한 모든 서비스 주체 이름을 나열 합니다. 즉, Sql Server가 SPN을 등록 하 고 Kerberos 인증을 받을 준비가 되었음을 MSSQLSvc/HostName.Domain.com로 시작 하는 항목이 표시 됩니다. 
- Sql Server의 호스트에 액세스할 수 없는 경우 원하는 다른 Windows OS에서 동일한 Active Directory에 가입 된, 명령을 사용할 수 있습니다 `setspn -L <SQLSERVER_NETBIOS>` 여기서 < SQLSERVER_NETBIOS >은 Sql Server의 호스트의 컴퓨터 이름입니다.


## <a name="get-the-kerberos-key-distribution-center"></a>Kerberos 키 배포 센터 가져오기

Kerberos KDC (키 배포 센터) 구성 값을 찾습니다. Active Directory 도메인에 가입 된 Windows 컴퓨터에서 다음 명령을 실행 합니다. 

시작 `cmd.exe` 실행 `nltest`합니다.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
이 경우 dc 33.domain.company.com에 필요한 KDC 구성 값이 DC 이름을 복사합니다

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Active Directory 도메인 컨트롤러에 OS를 가입

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

편집 된 `/etc/network/interfaces` 파일에 AD 도메인 컨트롤러의 IP 주소를 dns 이름 서버 목록이 표시 됩니다. 예를 들어: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
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

이제 확인 프로그램 `/etc/resolv.conf` 다음과 같은 줄을 포함 하는 파일:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

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

이제 확인 프로그램 `/etc/resolv.conf` 다음과 같은 줄을 포함 하는 파일:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 다음이 단계를 수행 하 여 Active Directory 도메인 컨트롤러에 macOS를 참여:



## <a name="configure-kdc-in-krb5conf"></a>Krb5.conf에서 KDC 구성

편집 된 `/etc/krb5.conf` 원하는 편집기에서. 다음 키 구성

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

그런 다음, krb5.conf 파일 및 종료

> [!NOTE]
> 도메인은 모두 대문자로에 있어야 합니다.


## <a name="test-the-ticket-granting-ticket-retrieval"></a>티켓 부여 티켓 검색 테스트

KDC에서 Granting을 Ticket (TGT)을 가져옵니다.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Klist를 사용 하 여 사용 가능한 티켓을 봅니다. Kinit를 성공적으로 수행 되었으면 티켓을 표시 됩니다. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>사용 하 여 연결 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* 새 연결 프로필을 만들려면

* 선택할 **Windows 인증** 인증 유형으로

* 연결 프로필을 작성, 클릭 **연결**

성공적으로 연결 되 면 서버에 표시 합니다 *서버* 보충 합니다.
