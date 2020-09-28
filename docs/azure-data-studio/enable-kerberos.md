---
title: Windows 인증을 사용하여 SQL Server 인스턴스 연결(Kerberos)
description: Microsoft Kerberos 통합 인증을 사용하여 Azure Data Studio를 SQL Server 인스턴스에 연결하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 7acc55d55afc3d994230a529243c26d5e1a626be
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364110"
---
# <a name="connect-azure-data-studio-to-sql-server-using-windows-authentication---kerberos"></a>Windows 인증을 사용하여 Azure Data Studio를 SQL Server에 연결 - Kerberos

Azure Data Studio는 Kerberos를 사용하여 SQL Server에 연결할 수 있도록 지원합니다.

macOS 또는 Linux에서 통합 인증(Windows 인증)을 사용하려면 현재 사용자를 Windows 도메인 계정에 연결하는 *Kerberos 티켓*을 설정해야 합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작하려면 다음이 필요합니다.

- Kerberos 도메인 컨트롤러를 쿼리하기 위해 Windows 도메인에 조인된 머신에 액세스할 수 있어야 합니다.
- Kerberos 인증을 허용하도록 SQL Server가 구성되어 있어야 합니다. Unix에서 실행되는 클라이언트 드라이버의 경우 Kerberos를 통해서만 통합 인증이 지원됩니다. 자세한 내용은 [Kerberos 통합 인증을 사용하여 SQL Server에 연결](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)을 참조하세요. 연결하려는 SQL Server의 각 인스턴스에 대해 SPN(서비스 사용자 이름)이 등록되어 있어야 합니다. 자세한 내용은 [서비스 사용자 이름 등록](/previous-versions/sql/sql-server-2008-r2/ms191153(v=sql.105)#SPN%20Formats)을 참조하세요.


## <a name="check-if-sql-server-has-a-kerberos-setup"></a>SQL Server에 Kerberos 설정이 있는지 확인

SQL Server의 호스트 머신에 로그인합니다. Windows 명령 프롬프트에서 `setspn -L %COMPUTERNAME%`을 사용하여 호스트의 모든 SPN을 나열합니다. MSSQLSvc/HostName.Domain.com으로 시작하는 항목이 표시되어야 합니다. 항목이 표시되면 SQL Server가 SPN을 등록했으며 Kerberos 인증을 수락할 준비가 되었음을 나타냅니다.

SQL Server 인스턴스 호스트에 대한 액세스 권한이 없는 경우 동일한 Active Directory에 조인된 다른 Windows OS에서 `setspn -L <SQLSERVER_NETBIOS>` 명령을 사용할 수 있습니다. 여기서 *<SQLSERVER_NETBIOS>* 는 SQL Server 인스턴스 호스트의 컴퓨터 이름입니다.


## <a name="get-the-kerberos-key-distribution-center"></a>Kerberos 키 배포 센터 가져오기

Kerberos KDC(키 배포 센터) 구성 값을 찾습니다. Active Directory 도메인에 조인된 Windows 컴퓨터에서 다음 명령을 실행합니다.

`cmd.exe`를 시작하고 `nltest`를 실행합니다.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
필수 KDC 구성 값인 DC 이름을 복사합니다. 이 경우 dc-33.domain.company.com입니다.

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Active Directory 도메인 컨트롤러에 OS 조인

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Active Directory 도메인 컨트롤러의 IP 주소가 dns-nameserver로 나열되도록 `/etc/network/interfaces` 파일을 편집합니다. 예를 들면 다음과 같습니다.

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 네트워크 인터페이스(eth0)는 머신마다 다를 수 있습니다. 사용 중인 인터페이스를 확인하려면 ifconfig를 실행하고 IP 주소와 전송 및 수신된 바이트가 있는 인터페이스를 복사합니다.

이 파일을 편집한 후 네트워크 서비스를 다시 시작합니다.

```bash
sudo ifdown eth0 && sudo ifup eth0
```

이제 `/etc/resolv.conf` 파일에 다음과 같은 줄이 포함되어 있는지 확인합니다.

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

Active Directory 도메인 컨트롤러의 IP 주소가 DNS 서버로 나열되도록 `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일(또는 다른 적절한 인터페이스 구성 파일)을 편집합니다.

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

이 파일을 편집한 후 네트워크 서비스를 다시 시작합니다.

```bash
sudo systemctl restart network
```

이제 `/etc/resolv.conf` 파일에 다음과 같은 줄이 포함되어 있는지 확인합니다.  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

다음 단계를 수행하여 macOS를 Active Directory 도메인 컨트롤러에 조인합니다.

## <a name="configure-kdc-in-krb5conf"></a>krb5.conf에서 KDC 구성

선택한 편집기에서 `/etc/krb5.conf` 파일을 편집합니다. 다음 키를 구성합니다.

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

그런 다음, krb5.conf 파일을 저장하고 종료합니다.

> [!NOTE]
> 도메인은 모두 대문자여야 합니다.


## <a name="test-the-ticket-granting-ticket-retrieval"></a>허용 티켓 검색 테스트

KDC에서 TGT(허용 티켓)를 가져옵니다.

```bash
kinit username@DOMAIN.COMPANY.COM
```

klist를 사용하여 사용 가능한 티켓을 봅니다. kinit가 성공적으로 완료되면 티켓이 표시됩니다.

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-by-using-azure-data-studio"></a>Azure Data Studio를 사용하여 연결

1. 새 연결 프로필을 만듭니다.

1. 인증 유형으로 **Windows 인증**을 선택합니다.

1. 연결 프로필을 완료하고 **연결**을 선택합니다.

성공적으로 연결되면 서버가 **서버** 사이드바에 표시됩니다.
