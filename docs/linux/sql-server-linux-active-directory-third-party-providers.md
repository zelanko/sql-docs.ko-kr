---
title: 타사 Active Directory 공급자를 사용 하 여 Linux의 SQL Server를 사용 하 여 | Microsoft Docs
description: 이 자습서는 타사 공급자를 사용 하 여 Active Directory 인증에 대 한 구성 단계를 제공합니다.
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: 0ffe146de3a842f9c273b4dbba2a9fe4d9ff7ff5
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757998"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Linux의 SQL Server를 사용 하 여 타사 Active Directory 공급자를 사용 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서를 구성 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 타사 Active Directory 공급자를 사용 하는 경우 Active Directory 인증을 사용 하 여 Linux 호스트 컴퓨터에서. 예로 [PowerBroker Identity Services (PBI)](https://www.beyondtrust.com/)를 [하나의 Id](https://www.oneidentity.com/products/authentication-services/), 및 [Centrify](https://www.centrify.com/)합니다. 이 가이드는 Active Directory 구성을 확인 하는 단계를 포함 합니다. 컴퓨터를 도메인에 조인 하는 방법을 지시에 없습니다. 조인에 관한 자세한 지침을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] realmd 및 SSSD 사용 하 여 도메인에 호스트를 참조 하십시오 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>필수 구성 요소

Active Directory 인증을 구성 하기 전에 Active Directory 도메인 컨트롤러를, Windows, 네트워크에서 설정 해야 합니다. 그런 다음 조인에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Active Directory 도메인에 Linux 호스트에서. 사용할 수 있습니다 [PBI](https://www.beyondtrust.com/)하십시오 [VAS](https://www.oneidentity.com/products/authentication-services/), 또는 [Centrify](https://www.centrify.com/)합니다.

> [!NOTE]
>
>이 자습서에서는 **`contoso.com`** 하 고 **`CONTOSO.COM`** 예제 도메인 및 영역 이름으로 각각. 또한 사용 하 여 **`DC1.CONTOSO.COM`** 예제에서는 정규화 된 도메인 컨트롤러의 도메인 이름으로 합니다. 이러한 이름은 고유한 값으로 대체 해야 합니다.

## <a name="check-the-connection-to-a-domain-controller"></a>도메인 컨트롤러에 대 한 연결 확인

도메인의 단기 및 정규화 된 이름이 있는 도메인 컨트롤러에 연결할 수 있는지 확인 합니다.

```bash
ping contoso

ping contoso.com
```

이러한 이름 검사 중 실패 하는 경우 업데이트 도메인 검색 목록:

- **Ubuntu**

  편집 된 `/etc/network/interfaces` Active Directory 도메인은 도메인 검색 목록에 있도록 파일: 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > 네트워크 인터페이스 **eth0**, 서로 다른 컴퓨터에 대 한 다를 수 있습니다. 사용 하는 어떤 것을 확인 하려면 실행 **ifconfig**합니다. 인터페이스에 IP 주소 및 전송 및 수신 바이트를 복사 합니다.

  이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  편집 된 `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일, Active Directory 도메인은 도메인 검색 목록에 있도록 합니다. 또는 적절 하 게 다른 인터페이스 구성 파일을 편집 합니다.

  ```/etc/sysconfig/network-scripts/ifcfg-eth0
  <...>
  PEERDNS=no
  DNS1=**<AD domain controller IP address>**
  DOMAIN="contoso.com com"
  ```

  이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

  ```bash
  sudo systemctl restart network
  ```

  이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

  도메인 컨트롤러를 ping 할 수 없는 경우에 정규화 된 도메인 이름 및 도메인 컨트롤러의 IP 주소를 찾습니다. 예제 도메인 이름은 `DC1.CONTOSO.COM`합니다. 다음 항목을 추가 `/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  편집 된 `/etc/sysconfig/network/config` DNS 쿼리에 대 한 Active Directory 도메인 컨트롤러 IP가 사용 되며 Active Directory 도메인 도메인 검색 목록에 있도록 파일:

  ```/etc/sysconfig/network/config
  <...>
  NETCONFIG_DNS_STATIC_SEARCHLIST=""
  NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
  ```

  이 파일을 편집한 후 네트워크 서비스를 다시 시작 합니다.

  ```bash
  sudo systemctl restart network
  ```

  이제 확인 프로그램 `/etc/resolv.conf` 다음과 같이 줄을 포함 하는 파일:

  ```/etc/resolv.conf
  search contoso.com com
  nameserver **<AD domain controller IP address>**
  ```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>역방향 DNS가 올바르게 구성 되었는지 확인

다음 명령은 SQL Server를 실행 하는 호스트의 정규화 된 도메인 이름을 반환 해야 합니다. 예로 **`SqlHost.contoso.com`** 합니다.

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

이 명령은 호스트의 FQDN을 반환 하지 않는 경우 또는 FQDN을 올바르지 않은 경우는 대 한 역방향 DNS 항목을 추가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DNS 서버로 Linux 호스트에서.

## <a name="check-that-your-krb5-configuration-is-correct"></a>강화 하려면 KRB5 구성에 정확한 지 확인

확인 프로그램 `/etc/krb5.conf` 올바르게 구성 되어 있습니다. 대부분의 타사 Active Directory 공급자에 대 한이 구성은 자동으로 수행 됩니다. 그러나 확인 `/etc/krb5.conf` 모든 향후 문제를 방지 하기 위해 다음 값에 대 한 합니다.

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

## <a name="next-steps"></a>다음 단계

이 문서에서는 구성 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 타사 Active Directory 공급자를 사용 하는 경우 Active Directory 인증을 사용 하 여 Linux 호스트 컴퓨터에서. 구성을 마치려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Active Directory 계정을 지원 하기 위해 linux에서 지침을 따릅니다 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.

> [!div class="nextstepaction"]
> [Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 합니다.](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> 건너뛸 수 있습니다 합니다 **Active Directory 도메인에 가입 하는 SQL Server 호스트** 섹션 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md) 방금 수행한는이 자습서에 따라 합니다.
