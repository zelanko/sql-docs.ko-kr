---
title: Active Directory에는 Linux에서 SQL 서버 연결
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
manager: jroth
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4cee4ca0edcc5a49a34b6c352ae0121bed3b40ca
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834438"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>SQL Server Linux 호스트는 Active Directory 도메인에 가입

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 SQL Server Linux 호스트 컴퓨터는 Active Directory (AD) 도메인에 가입 하는 방법은 일반 지침을 제공 합니다. 두 가지 방법이 있습니다: 기본 제공 SSSD 패키지를 사용 하거나 제 3 자 Active Directory 공급자를 사용 합니다. 타사 도메인 조인 제품의 예로 [PowerBroker Identity Services (PBI)](https://www.beyondtrust.com/)를 [하나의 Id](https://www.oneidentity.com/products/authentication-services/), 및 [Centrify](https://www.centrify.com/)합니다. 이 가이드는 Active Directory 구성을 확인 하는 단계를 포함 합니다. 그러나 것은 아닙니다 타사 유틸리티를 사용 하는 경우 컴퓨터를 도메인에 가입 하는 방법에 지침을 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

Active Directory 인증을 구성 하기 전에 Active Directory 도메인 컨트롤러를, Windows, 네트워크에서 설정 해야 합니다. 그런 다음 SQL Server Linux 호스트는 Active Directory 도메인에 가입.

> [!IMPORTANT]
> 이 문서에 설명 된 샘플 단계를 참조용 으로만 됩니다. 실제 단계는 환경의 전반적인 환경을 구성 하는 방법에 따라 약간 달라질 수 있습니다. 특정 구성, 사용자 지정 및 문제 해결 하는 데 필요한 모든 환경에 대 한 시스템 이름과 도메인 관리자를 참여 합니다.

## <a name="check-the-connection-to-a-domain-controller"></a>도메인 컨트롤러에 대 한 연결 확인

도메인의 단기 및 정규화 된 이름이 있는 도메인 컨트롤러에 연결할 수 있는지 확인 합니다.

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> 이 자습서에서는 **contoso.com** 하 고 **CONTOSO.COM** 예제 도메인 및 영역 이름으로 각각. 또한 사용 하 여 **DC1 합니다. CONTOSO.COM** 예제에서는 정규화 된 도메인 컨트롤러의 도메인 이름으로 합니다. 사용자 고유의 값을 사용 하 여 이러한 이름을 바꿔야 합니다.

이러한 이름 검사 중 실패 하는 경우 도메인 검색 목록을 업데이트 합니다. 다음 섹션에서는 각각 Ubuntu, Red Hat Enterprise Linux (RHEL), 및 SUSE Linux Enterprise Server (SLES)에 대 한 지침을 제공합니다.

### <a name="ubuntu"></a>Ubuntu

1. 편집 된 **/etc/network/interfaces** Active Directory 도메인은 도메인 검색 목록에 있도록 파일:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > 네트워크 인터페이스 `eth0`, 서로 다른 컴퓨터에 대 한 다를 수 있습니다. 사용 하는 어떤 것을 확인 하려면 실행 **ifconfig**합니다. 인터페이스에 IP 주소 및 전송 및 수신 바이트를 복사 합니다.

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 다음으로 확인 하 **/etc/resolv.conf** 다음과 같이 줄을 포함 하는 파일:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. 편집 된 **/etc/sysconfig/network-scripts/ifcfg-eth0** 파일, Active Directory 도메인은 도메인 검색 목록에 있도록 합니다. 또는 적절 하 게 다른 인터페이스 구성 파일을 편집 합니다.

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart network
   ```

1. 이제 확인 프로그램 **/etc/resolv.conf** 다음과 같이 줄을 포함 하는 파일:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. 도메인 컨트롤러를 ping 할 수 없는 경우에 정규화 된 도메인 이름 및 도메인 컨트롤러의 IP 주소를 찾습니다. 예제 도메인 이름은 **DC1 합니다. CONTOSO.COM**합니다. 다음 항목을 추가 **등은 / 호스트**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. 편집 된 **/etc/sysconfig/network/config** DNS 쿼리에 대 한 Active Directory 도메인 컨트롤러 IP가 사용 되며 Active Directory 도메인 도메인 검색 목록에 있도록 파일:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. 이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart network
   ```

1. 다음으로 확인 하 **/etc/resolv.conf** 다음과 같이 줄을 포함 하는 파일:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>AD 도메인에 가입

기본 구성 및 도메인 컨트롤러와의 연결을 확인 한 후 가지 Active Directory 도메인 컨트롤러를 사용 하 여 SQL Server Linux 호스트 컴퓨터를 조인 하는 데 두 가지 옵션이 있습니다.

- [옵션 1: SSSD 패키지 사용](#option1)
- [옵션 2: 타사 openldap 공급자 유틸리티를 사용 합니다.](#option2)

### <a id="option1"></a> 옵션 1: SSSD 패키지를 사용 하 여 AD 도메인에 가입

이 메서드는 SQL Server 호스트를 사용 하 여 AD 도메인 조인 **realmd** 하 고 **sssd** 패키지 있습니다.

> [!NOTE]
> 이 AD 도메인 컨트롤러에 Linux 호스트를 조인 하는 기본 방법입니다.

SQL Server 호스트는 Active Directory 도메인에 가입 하려면 다음 단계를 사용 합니다.

1. 사용 하 여 [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) AD 도메인에 호스트 컴퓨터를 가입 합니다. 둘 다를 먼저 설치 해야 합니다 **realmd** 및 Linux 배포판의 패키지 관리자를 사용 하 여 SQL Server 호스트 컴퓨터에서 Kerberos 클라이언트 패키지:

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

1. Kerberos 클라이언트 패키지 설치 요청 영역 이름, 도메인 이름을 대문자로 입력 합니다.

1. DNS가 올바르게 구성 되었는지 확인 하 고 나면 다음 명령을 실행 하 여 도메인에 가입 합니다. 새 컴퓨터를 도메인에 가입 AD에 충분 한 권한이 있는 AD 계정을 사용 하 여 인증 해야 합니다. 이 명령은 AD에서 새 컴퓨터 계정을 만들고, 만듭니다는 **/etc/krb5.keytab** keytab 파일을 호스트를 도메인에 구성 **/etc/sssd/sssd.conf**, 및 업데이트 **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   메시지를 표시 해야 `Successfully enrolled machine in realm`합니다.

   다음 표에서 일부 받을 수 있는 오류 메시지 및 해결 하는 방법과 권장 사항을 나열 합니다.

   | 오류 메시지 | 권장 |
   |---|---|
   | `Necessary packages are not installed` | Linux 배포판의 패키지 관리자를 사용 하 여 영역 조인 명령을 다시 실행 하기 전에 해당 패키지를 설치 합니다. |
   | `Insufficient permissions to join the domain` | 도메인 관리자를 사용 하 여 Linux 컴퓨터를 도메인에 가입 하면 충분 한 권한이 있는지 확인 합니다. |
   | `KDC reply did not match expectations` | 사용자에 대 한 올바른 영역 이름의 지정 하지 않을 수 있습니다. 영역 이름 대/소문자 구분 및 대문자로 일반적으로 명령 영역을 사용 하 여 식별할 수 있습니다 contoso.com을 검색 합니다. |

   SQL Server 사용자 계정 및 그룹 보안 식별자 (Sid)에 매핑하기 위한 SSSD 및 NSS를 사용 합니다. SSSD 구성 하 고 SQL server 로그인을 만들려면 AD 성공적으로 실행 해야 합니다. **realmd** 일반적으로이 위해 자동으로 경우도 있지만 도메인에 가입 하는 과정에서 변경 해야 할 개별적으로 합니다.

   자세한 내용은 참조 하는 방법 [SSSD를 수동으로 구성](https://access.redhat.com/articles/3023951), 및 [SSSD 작업할 NSS 구성](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. 도메인에서 사용자에 대 한 정보를 수집할 이제 수 및 해당 사용자로 Kerberos 티켓을 얻을 수 있습니다는 확인 합니다. 다음 예제에서는 **id**를 [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html), 및 [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) 이 대 한 명령입니다.

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
   > - 하는 경우 **id user@contoso.com**  반환 `No such user`, SSSD 서비스 명령을 실행 하 여 성공적으로 시작 되도록 `sudo systemctl status sssd`합니다. 서비스가 실행 되는 오류가 계속 표시 하 고 SSSD에 대 한 자세한 정보 로깅을 사용 하도록 설정 하십시오. 자세한 내용은 Red Hat 설명서를 참조 [문제 해결 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)합니다.
   >
   > - 하는 경우 **kinit user@CONTOSO.COM**  반환 `KDC reply did not match expectations while getting initial credentials`, 대문자로 영역을 지정 했는지 확인 합니다.

자세한 내용은 Red Hat 설명서를 참조 [Discovering 및 Id 도메인이 가입](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)합니다.

### <a id="option2"></a> 옵션 2: 타사 openldap 공급자 유틸리티를 사용 합니다.

와 같은 타사 유틸리티를 사용할 수 있습니다 [PBI](https://www.beyondtrust.com/)하십시오 [VAS](https://www.oneidentity.com/products/authentication-services/), 또는 [Centrify](https://www.centrify.com/)합니다. 이 문서는 각 개별 유틸리티에 대 한 단계를 다루지 않습니다. 앞으로 계속 하기 전에 SQL Server에 대 한 Linux 호스트를 도메인에 가입 하려면 다음이 유틸리티 중 하나를 먼저 사용 해야 합니다.  

SQL Server AD와 관련 된 모든 쿼리에 대 한 타사 통합자 코드 또는 라이브러리를 사용 하지 않습니다. SQL Server는 항상이 설치 프로그램에서 직접 openldap 라이브러리 호출을 사용 하 여 AD를 쿼리 합니다. 타사 통합은 Linux 호스트에 AD 도메인에 가입 하는 데만 사용 됩니다 하 고 이러한 유틸리티와 직접 통신을 SQL Server에 없습니다.

> [!IMPORTANT]
> 사용에 대 한 권장 사항을 참조 하세요 합니다 **mssql conf** `network.disablesssd` 구성 옵션에는 **추가 구성 옵션** 문서의 섹션 [사용 하 여 활성 Linux의 SQL Server를 사용 하 여 디렉터리 인증](sql-server-linux-active-directory-authentication.md#additionalconfig)합니다.

확인 프로그램 **/etc/krb5.conf** 올바르게 구성 되어 있습니다. 대부분의 타사 Active Directory 공급자에 대 한이 구성은 자동으로 수행 됩니다. 그러나 체크 **/etc/krb5.conf** 모든 향후 문제를 방지 하기 위해 다음 값에 대 한 합니다.

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>역방향 DNS가 올바르게 구성 되었는지 확인

다음 명령은 SQL Server를 실행 하는 호스트의 정규화 된 도메인 이름 (FQDN)을 반환 해야 합니다. 예로 **SqlHost.contoso.com**합니다.

```bash
host **<IP address of SQL Server host>**
```

이 명령의 출력은 같은 형태가 됩니다 `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`합니다. 이 명령은 호스트의 FQDN을 반환 하지 않는 경우 또는 FQDN 올바르지 않으면 DNS 서버에 Linux 호스트에서 SQL Server에 대 한 역방향 DNS 항목을 추가 합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 Active Directory 인증을 사용 하 여 Linux 호스트 컴퓨터에서 SQL Server를 구성 하는 방법의 필수 구성 요소에 설명 합니다. Active Directory 계정을 지원 하기 위해 Linux에서 SQL Server 구성을 완료 하려면의 지침을 따르세요 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.