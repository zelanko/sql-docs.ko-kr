---
title: 타사 Active Directory 공급자를 사용 하 여 Linux의 SQL Server를 사용 하 여 | Microsoft Docs
description: 이 자습서는 타사 공급자를 사용 하 여 AD 인증을 위한 구성 단계를 제공합니다.
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: 288f46a2084166a1b7164ff8f0c0ef82b81fb16b
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381522"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Linux의 SQL Server를 사용 하 여 타사 Active Directory 공급자를 사용 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서를 구성 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 와 같은 타사 AD 공급자를 사용 하는 경우 AD 인증을 사용 하 여 Linux 호스트 컴퓨터에 [PowerBroker Identity Services (PBI)](https://www.beyondtrust.com/), [Vintela 인증 서비스 (VAS)](https://www.oneidentity.com/products/authentication-services/), 및 [Centrify](https://www.centrify.com/)합니다. 이 가이드는 AD 구성을 확인 하는 단계를 포함 하 고 컴퓨터를 도메인에 조인 하는 방법을 지시 하는 아닙니다. 조인 하는 자세한 지침은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 영역과 SSSD를 사용 하 여 도메인에 호스트를 참조 하십시오 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

AD 인증을 구성 하기 전에 설정 해야 (Windows)는 AD 도메인 컨트롤러를 네트워크에 조인 하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 도메인에 Linux 호스트에서. 사용할 수 있습니다 [PBI](https://www.beyondtrust.com/)하십시오 [VAS](https://www.oneidentity.com/products/authentication-services/), 또는 [Centrify](https://www.centrify.com/)합니다.

> [!NOTE]
>
>이 자습서에서는 "contoso.com" 및 "CONTOSO.COM" 예제 도메인 및 영역 이름으로 각각 합니다. 또한 사용 하 여 "DC1 합니다. CONTOSO.COM "도메인 컨트롤러의 예제에서는 정규화 된 도메인 이름으로 합니다. 사용자 고유의 값을 사용 하 여 이러한 바꿔야 합니다.

## <a name="check-connection-to-domain-controller"></a>도메인 컨트롤러에 연결 되어 있는지 확인

검사 도메인의 단기 및 정규화 된 이름 사용 하 여 도메인 컨트롤러에 연결할 수 있습니다.

   ```bash
   ping contoso

   ping contoso.com
   ```

   이러한 작업에 실패 하면 도메인 검색 목록을 업데이트 합니다.

   - **Ubuntu**:

     편집 된 `/etc/network/interfaces` AD 도메인이 도메인 검색 목록에 있도록 파일: 

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
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   - **RHEL**:

     편집 된 `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일 (또는 다른 인터페이스 구성 적절 하 게 파일)는 AD 도메인이 도메인 검색 목록에서:

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

   도메인 컨트롤러를 ping 할 수 없는 경우 (예: DC1 정규화 된 도메인 이름 찾기. CONTOSO.COM) 도메인 컨트롤러의 IP 주소 및 다음 항목을 추가 합니다. `/etc/hosts`

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

   - **SLES**:

     편집 된 `/etc/sysconfig/network/config` AD 도메인 컨트롤러 IP를 사용 하 여 DNS 쿼리에 대 한 됩니다 하 고 AD 도메인이 도메인 검색 목록에서 파일:

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

## <a name="check-reverse-dns-is-properly-configured"></a>역방향 DNS가 올바르게 구성 확인

다음 명령 (예: SQL Server를 실행 하는 호스트의 정규화 된 도메인 이름이 되돌아가야 합니다. "SqlHost.contoso.com")입니다.

   ```bash
   host **<IP address of SQL Server host>**
   # **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
   ```

   이 호스트의 FQDN을 반환 하지 않는 경우 또는 FQDN을 올바르지 않은 경우에 대 한 역방향 DNS 항목을 추가 하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DNS 서버로 Linux 호스트에서.

## <a name="check-your-krb5-configuration-is-correct"></a>강화 하려면 KRB5 구성이 올바른지 확인 합니다.

확인 프로그램 `/etc/krb5.conf` 올바르게 구성 되어 있습니다. 대부분의 타사 AD 공급자에 대 한이 자동으로 수행 됩니다. 그러나 확인 `/etc/krb5.conf` 모든 향후 문제를 방지 하기 위해 다음 값에 대 한 합니다.

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

구성 하는 방법에 설명 했습니다이 문서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 타사 AD 공급자를 사용 하는 경우 AD 인증을 사용 하 여 Linux 호스트 컴퓨터. 구성을 마치려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 계정을 지원 하기 위해 linux에서 지침을 따릅니다 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.

> [!div class="nextstepaction"]
> [Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 합니다.](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> "AD 도메인에 조인 SQL Server 호스트" 섹션을 건너뛸 수 있습니다 [Linux의 SQL Server를 사용 하 여 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md) 방금 수행한 경우는이 자습서입니다.