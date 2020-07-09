---
title: SQL Server on Linux를 Active Directory에 가입
titleSuffix: SQL Server
description: 이 문서에서는 SQL Server Linux 호스트 머신을 AD 도메인에 연결하기 위한 가이드를 제공합니다. 기본 제공 SSSD 패키지를 사용하거나 타사 AD 공급자를 사용할 수 있습니다.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ff058b2e326399fa6d04503d984d540fba8efc1b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896973"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Linux 호스트의 SQL Server를 Active Directory 도메인에 가입

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server Linux 호스트 머신을 AD(Active Directory) 도메인에 가입시키는 방법에 관한 일반 지침을 제공합니다. 기본 제공 SSSD 패키지를 사용하거나 타사 Active Directory 공급자를 사용하는 두 가지 방법이 있습니다. 타사 도메인 가입 제품의 예로는 [PBIS(PowerBroker Identity Services)](https://www.beyondtrust.com/), [One Identity](https://www.oneidentity.com/products/authentication-services/) 및 [Centrify](https://www.centrify.com/)가 있습니다. 이 가이드에는 Active Directory 구성을 확인하는 단계가 포함되어 있습니다. 그러나 타사 유틸리티를 사용할 때 머신을 도메인에 가입시키는 방법을 설명하지 않습니다.

## <a name="prerequisites"></a>사전 요구 사항

Active Directory 인증을 구성하려면 먼저 네트워크에서 Active Directory 도메인 컨트롤러인 Windows를 설정해야 합니다. 그런 다음 SQL Server on Linux 호스트를 Active Directory 도메인에 가입시킵니다.

> [!IMPORTANT]
> 이 아티클에서 설명하는 샘플 단계는 지침을 제공하기 위한 것이며 Ubuntu 16.04, RHEL(Red Hat Enterprise Linux) 7.x 및 SLES(SUSE Enterprise Linux) 12 운영 체제를 참조합니다. 실제 단계는 전체 환경이 구성된 방식 및 운영 체제 버전에 따라 사용자 환경에서 약간 다를 수 있습니다. 예를 들어 Ubuntu 18.04에서는 netplan을 사용하는 반면, RHEL(Red Hat Enterprise Linux) 8.x에서는 다른 도구 중 nmcli를 사용하여 네트워크를 관리하고 구성합니다. 특정 도구, 구성, 사용자 지정 및 필요한 문제 해결 관련 정보는 사용자 환경의 시스템 및 도메인 관리자에게 문의하는 것이 좋습니다.

## <a name="check-the-connection-to-a-domain-controller"></a>도메인 컨트롤러의 연결 확인

도메인의 약식 이름과 정규화된 이름을 모두 사용하여 도메인 컨트롤러에 연결할 수 있는지 확인합니다.

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> 이 자습서에서는 예제 도메인과 영역 이름으로 각각 **contoso.com** 및 **CONTOSO.COM**을 사용합니다. 또한 **DC1.CONTOSO.COM**을 도메인 컨트롤러의 정규화된 도메인 이름 예제로 사용합니다. 이러한 이름을 사용자 고유의 값으로 바꾸어야 합니다.

이러한 이름 확인 중 하나라도 실패하면 도메인 검색 목록을 업데이트합니다. 다음 섹션에서는 각각 Ubuntu, RHEL(Red Hat Enterprise Linux) 및 SLES(SUSE Linux Enterprise Server)에 관한 지침을 제공합니다.

### <a name="ubuntu-1604"></a>Ubuntu 16.04

1. Active Directory 도메인이 도메인 검색 목록에 있도록 **/etc/network/interfaces** 파일을 편집합니다.

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > 네트워크 인터페이스 `eth0`은 머신마다 다를 수 있습니다. 사용 중인 인터페이스를 확인하려면 **ifconfig**를 실행합니다. 그런 다음 IP 주소와 전송 및 수신된 바이트가 있는 인터페이스를 복사합니다.

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작합니다.

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 다음으로 **/etc/resolv.conf** 파일에 다음 예제와 같은 줄이 포함되어 있는지 확인합니다.

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel-7x"></a>RHEL 7.x

1. Active Directory 도메인이 도메인 검색 목록에 있도록 **/etc/sysconfig/network-scripts/ifcfg-eth0** 파일을 편집합니다. 또는 다른 인터페이스 구성 파일을 적절하게 편집합니다.

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart network
   ```

1. 이제 **/etc/resolv.conf** 파일에 다음 예제와 같은 줄이 포함되어 있는지 확인합니다.

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. 여전히 도메인 컨트롤러를 ping할 수 없으면 도메인 컨트롤러의 정규화된 도메인 이름 및 IP 주소를 찾습니다. 예제 도메인 이름은 **DC1.CONTOSO.COM**입니다. **/etc/hosts**에 다음 항목을 추가합니다.

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles-12"></a>SLES 12

1. Active Directory 도메인 컨트롤러 IP가 DNS 쿼리에 사용되고 Active Directory 도메인이 도메인 검색 목록에 있도록 **/etc/sysconfig/network/config** 파일을 편집합니다.

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart network
   ```

1. 다음으로 **/etc/resolv.conf** 파일에 다음 예제와 같은 줄이 포함되어 있는지 확인합니다.

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>AD 도메인에 조인

기본 구성 및 도메인 컨트롤러와의 연결이 확인된 후에는 두 가지 옵션을 통해 SQL Server Linux 호스트 머신을 Active Directory 도메인 컨트롤러에 조인할 수 있습니다.

- [옵션 1: SSSD 패키지 사용](#option1)
- [옵션 2: 타사 openldap 공급자 유틸리티 사용](#option2)

### <a name="option-1-use-sssd-package-to-join-ad-domain"></a><a id="option1"></a> 옵션 1: SSSD 패키지를 사용하여 AD 도메인 조인

이 방법에서는 **realmd** 및 **sssd** 패키지를 사용하여 SQL Server 호스트를 AD 도메인에 연결합니다.

> [!NOTE]
> Linux 호스트를 AD 도메인 컨트롤러에 조인할 때 기본적으로 사용하는 방법입니다.

다음 단계에 따라 SQL Server 호스트를 Active Directory 도메인에 조인합니다.

1. [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join)를 사용하여 호스트 머신을 AD 도메인에 조인합니다. 먼저 Linux 배포판의 패키지 관리자를 사용하여 SQL Server 호스트 머신에 **realmd** 및 Kerberos 클라이언트 패키지를 모두 설치해야 합니다.

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Kerberos 클라이언트 패키지 설치에서 영역 이름을 입력하라는 메시지가 표시되면 도메인 이름을 대문자로 입력합니다.

1. DNS가 올바르게 구성되어 있는지 확인한 후 다음 명령을 실행하여 도메인을 조인합니다. AD에서 도메인에 새 머신을 조인할 수 있는 권한이 있는 AD 계정을 사용하여 인증해야 합니다. 이 명령은 AD에서 새 컴퓨터 계정을 만들고 **/etc/krb5.keytab** 호스트 keytab 파일을 만들고, **/etc/sssd/sssd.conf**에서 도메인을 구성하고, **/etc/krb5.conf**를 업데이트합니다.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   `Successfully enrolled machine in realm` 메시지가 표시됩니다.

   다음 표에서는 표시될 수 있는 몇 가지 오류 메시지를 나열하고 해결하는 방법을 제안합니다.

   | 오류 메시지 | 권장 |
   |---|---|
   | `Necessary packages are not installed` | 영역 조인 명령을 다시 실행하기 전에 Linux 배포판의 패키지 관리자를 사용하여 패키지를 설치합니다. |
   | `Insufficient permissions to join the domain` | Linux 머신을 도메인에 조인할 수 있는 권한이 있는지 도메인 관리자에게 확인합니다. |
   | `KDC reply did not match expectations` | 사용자의 올바른 영역 이름을 지정하지 않았을 수 있습니다. 영역 이름은 대/소문자를 구분하고 대개 대문자이며 명령 영역 검색 contoso.com을 사용하여 식별할 수 있습니다. |

   SQL Server는 SSSD 및 NSS를 사용하여 사용자 계정 및 그룹을 SID(보안 식별자)에 매핑합니다. SSSD가 구성되어 실행 중이어야 SQL Server가 AD 로그인을 성공적으로 만들 수 있습니다. **realmd** 는 일반적으로 도메인 조인을 하는 중인 이 작업을 자동으로 수행하지만 경우에 따라 이 작업을 별도로 수행해야 합니다.

   자세한 내용은 [SSSD를 수동으로 구성](https://access.redhat.com/articles/3023951)하는 방법과 [SSSD를 사용하도록 NSS를 구성](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)하는 방법을 참조하세요.

1. 이제 도메인에서 사용자에 관한 정보를 수집할 수 있고 해당 사용자로 Kerberos 티켓을 가져올 수 있는지 확인합니다. 다음 예제에서는 이를 위해 **id**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) 및 [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) 명령을 사용합니다.

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - **id user\@contoso.com**에서 `No such user`를 반환하는 경우 `sudo systemctl status sssd` 명령을 실행하여 SSSD 서비스가 시작되었는지 확인하세요. SSSD 서비스가 실행 중인데도 오류가 계속 표시되는 경우에는 SSSD의 자세한 정보 로깅을 사용하도록 설정해 보세요. 자세한 내용은 Red Hat 설명서에서 [Troubleshooting SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)(SSSD 문제 해결)에 관한 내용을 참조하세요.
   >
   > - **kinit user\@CONTOSO.COM**을 반환하는 경우에는 `KDC reply did not match expectations while getting initial credentials`, 대문자로 영역을 지정했는지 확인합니다.

자세한 내용은 Red Hat 설명서에서 [Discovering and Joining Identity Domains](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)(ID 도메인 검색 및 조인)에 관한 내용을 참조하세요.

### <a name="option-2-use-third-party-openldap-provider-utilities"></a><a id="option2"></a> 옵션 2: 타사 openldap 공급자 유틸리티 사용

[PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) 또는 [Centrify](https://www.centrify.com/)와 같은 타사 유틸리티를 사용할 수 있습니다. 이 문서에서는 각 개별 유틸리티에 관한 단계는 다루지 않습니다. 계속하기 전에 먼저 이러한 유틸리티 중 하나를 사용하여 SQL Server의 Linux 호스트를 도메인에 조인해야 합니다.  

SQL Server는 AD 관련 쿼리에 타사 통합자의 코드 또는 라이브러리를 사용하지 않습니다. SQL Server는 항상 이 설치 프로그램에서 직접 openldap library 호출을 사용하여 AD를 쿼리합니다. 타사 통합자는 Linux 호스트를 AD 도메인에 조인하는 데만 사용되며 SQL Server는 이러한 유틸리티와 직접 통신하지 않습니다.

> [!IMPORTANT]
> **mssql-conf** `network.disablesssd` 구성 옵션 사용에 관한 권장 사항은 [SQL Server on Linux에서 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md#additionalconfig) 문서의 **추가 구성 옵션** 섹션을 참조하세요.

**/etc/krb5.conf**가 올바르게 구성되어 있는지 확인합니다. 타사 Active Directory 공급자 대부분의 경우 이 구성이 자동으로 수행됩니다. 그러나 이후 문제를 방지하기 위해 **/etc/krb5.conf**에서 다음 값을 확인하세요.

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>역방향 DNS가 제대로 구성되어 있는지 확인합니다.

다음 명령은 SQL Server를 실행하는 호스트의 FQDN(정규화된 도메인 이름)을 반환해야 합니다. 예를 들어 **SqlHost.contoso.com**을 반환해야 합니다.

```bash
host **<IP address of SQL Server host>**
```

이 명령의 출력은 `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`과 비슷해야 합니다. 이 명령이 호스트의 FQDN을 반환하지 않거나 FQDN이 잘못된 경우 SQL Server on Linux 호스트의 역방향 DNS 항목을 DNS 서버에 추가합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 Active Directory 인증을 사용하여 Linux 호스트 머신에서 SQL Server를 구성하는 방법에 관한 필수 조건을 설명합니다. SQL Server on Linux에서 Active Directory 계정을 지원하도록 구성을 마무리하려면 [Use Active Directory authentication with SQL Server on Linux](sql-server-linux-active-directory-authentication.md)(SQL Server on Linux에서 Active Directory 인증 사용)의 지침을 따르세요.
