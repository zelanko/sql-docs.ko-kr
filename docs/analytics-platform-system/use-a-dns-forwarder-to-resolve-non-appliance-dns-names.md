---
title: DNS 전달자를 사용 하 여 분석 플랫폼 시스템에 | Microsoft Docs "
description: Analytics Platform System에서 비 어플라이언스 DNS 이름을 확인 하려면 DNS 전달자를 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6ce978d7b05382b1a02018f3d5022b0f8bfaf585
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243785"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>DNS 전달자를 사용 하 여 분석 플랫폼 시스템에 비 어플라이언스 DNS 이름을 확인 하려면
Active Directory Domain Services 노드에서 DNS 전달자를 구성할 수 있습니다 (**_어플라이언스\_도메인_-AD01** 하 고  **_어플라이언스\_ 도메인_-AD02**) 스크립트 및 소프트웨어 응용 프로그램을 외부 서버에 액세스를 허용 하기 위해 분석 플랫폼 시스템 어플라이언스입니다.  
  
## <a name="ResolveDNS"></a>DNS 전달자를 사용 하 여  
Analytics Platform System appliance 기기에 있지 않은 서버의 DNS 이름 확인을 방지 하도록 구성 됩니다. 같은 Windows Software Update Services (WSUS), 일부 프로세스는 어플라이언스 외부 서버에 액세스 해야 합니다. 이 사용 시나리오는 분석 플랫폼 시스템 DNS를 지원 하기 위해 Analytics Platform System 호스트 및 가상 머신 (Vm) 어플라이언스 외부 이름을 확인 하기 위해 외부 DNS 서버를 사용할 수 있는 외부 이름이 전달자를 지원 하도록 구성할 수 있습니다. DNS 접미사의 사용자 지정 구성을 사용할 수 없습니다, 즉, 비 어플라이언스 서버 이름을 확인 하려면 정규화 된 도메인 이름을 사용 해야 합니다.  
  
**DNS GUI를 사용 하 여 DNS 전달자를 만들려면**  
  
1.  에 로그온 합니다  **_어플라이언스\_도메인_-AD01** 노드.  
  
2.  DNS 관리자를 엽니다 (**dnsmgmt.msc**).  
  
3.  서버의 이름을 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
4.  에 **고급** 탭을 선택 취소 합니다 **재귀 (전달자도 사용 하지 않도록 설정)를 사용 하지 않도록 설정** 옵션을 선택한 다음 클릭 **적용**.)  
  
5.  클릭 합니다 **전달자** 탭을 클릭 한 다음 **편집**합니다.  
  
6.  이름 확인을 제공 하는 외부 DNS 서버의 IP 주소를 입력 합니다. Vm 및 어플라이언스에서 (호스트) 서버는 정규화 된 도메인 이름을 사용 하 여 외부 서버에 연결 됩니다.  
  
7.  1-6 단계를 반복 합니다  **_어플라이언스\_도메인_-AD02** 노드  
  
**Windows PowerShell을 사용 하 여 DNS 전달자를 만들려면**  
  
1.  에 로그온 합니다  **_어플라이언스\_도메인_-AD01**노드.  
  
2.  다음 Windows PowerShell 스크립트를 실행 합니다  **_어플라이언스\_도메인_-AD01** 노드. Windows PowerShell 스크립트를 실행 하기 전에 비 어플라이언스 DNS 서버의 IP 주소를 사용 하 여 IP 주소를 바꿉니다.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  동일한 명령을 실행 합니다  **_어플라이언스\_도메인_-AD02** 노드.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>WSUS에 대 한 DNS 확인 구성  
SQL Server PDW 2012 통합 서비스 및 패치 기능을 제공 합니다. SQL Server PDW는 Microsoft 업데이트 및 다른 Microsoft 기술과 서비스를 사용 합니다. 어플라이언스는 Microsoft 공용 WSUS 리포지토리 또는 회사 WSUS 리포지토리에 연결할 수 있어야 합니다. 업데이트할 수 있도록 합니다.  
  
Microsoft 공용 WSUS 리포지토리에서 업데이트를 찾도록 어플라이언스를 구성 하도록 선택 하는 고객의 경우 다음 지침을 어플라이언스에서 적절 한 구성 세부 정보를 설정 합니다.  
  
> [!NOTE]  
> 고객 네트워크 관리자에서 이름을 확인할 수 있는 회사 DNS 서버에 대 한 IP 주소를 제공 해야 합니다 **Microsoft.com**합니다.  
  
1.  VMM VM에 로그온 하는 원격 데스크톱을 사용 하 여 (<fabric domain>VMM) fabric 도메인 관리자 계정을 사용 합니다.  
  
2.  제어판을 열고, 클릭 **네트워크 및 인터넷**를 클릭 하 고 **네트워크 및 공유 센터**합니다.  
  
3.  연결 목록에서 클릭 **VMSEthernet**를 클릭 하 고 **속성**합니다.  
  
4.  선택 **인터넷 프로토콜 버전 4 (Tcp/ipv4)** 를 클릭 하 고 **속성**합니다.  
  
5.  에 **대체 DNS 서버** 상자에서 고객 네트워크 관리자가 제공한 IP 주소를 추가 합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
