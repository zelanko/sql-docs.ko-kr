---
title: 분석 플랫폼 시스템에는 DNS 전달자를 사용 하 여 | "Microsoft Docs
description: 분석 플랫폼 시스템의 비 어플라이언스 DNS 이름을 확인 하는 DNS 전달자를 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f707d4c681c695105daf23d5fc640279bb83658
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544945"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>분석 플랫폼 시스템에 비 어플라이언스 DNS 이름을 확인 하기 위해 DNS 전달자를 사용 합니다.
Active Directory 도메인 서비스 노드에서 DNS 전달자를 구성할 수 있습니다 (***appliance_domain *-AD01** 및 ***appliance_domain *-AD02**) 수 있도록 분석 플랫폼 시스템 어플라이언스의 스크립트와 소프트웨어 응용 프로그램 외부 서버에 액세스할 수 있습니다.  
  
## <a name="ResolveDNS"></a>DNS 전달자를 사용 하 여  
분석 플랫폼 시스템 어플라이언스 어플라이언스에 없는 서버의 DNS 이름 확인을 방지 하도록 구성 됩니다. 예: 소프트웨어 업데이트 서비스 WSUS (Windows), 일부 프로세스 어플라이언스에 외부 서버에 액세스 해야 합니다. 분석 플랫폼 시스템 DNS이 사용 시나리오를 지원 하기 위해 분석 플랫폼 시스템 호스트 및 가상 컴퓨터 (Vm) 어플라이언스에 외부 이름을 확인 하기 위해 외부 DNS 서버를 사용할 수 있는 외부 이름 전달자를 지원 하도록 구성할 수 있습니다. 사용자 지정 DNS 접미사의 구성할 수 없습니다, 즉, 비 어플라이언스 서버의 이름을 확인 하려면 정규화 된 도메인 이름을 사용 해야 합니다.  
  
**DNS GUI를 사용 하 여 DNS 전달자를 만들려면**  
  
1.  로그온 하는 ***appliance_domain *-AD01** 노드.  
  
2.  DNS 관리자를 엽니다 (**dnsmgmt.msc**).  
  
3.  서버 이름을 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
4.  에 **고급** 탭을 선택 취소 합니다.는 **재귀 (전달자도 사용 하지 않도록 설정) 사용 하지 않도록** 옵션을 선택한 다음 클릭 **적용**.)  
  
5.  클릭는 **전달자** 탭을 클릭 한 다음 **편집**합니다.  
  
6.  이름 확인을 제공 하는 외부 DNS 서버에 대 한 IP 주소를 입력 합니다. Vm 및 기기에서 (호스트) 서버는 정규화 된 도메인 이름을 사용 하 여 외부 서버에 연결 됩니다.  
  
7.  1-6 단계를 반복은 ***appliance_domain *-AD02** 노드  
  
**Windows PowerShell을 사용 하 여 DNS 전달자를 만들려면**  
  
1.  로그온 하는 ***appliance_domain *-AD01**노드.  
  
2.  다음 Windows PowerShell 스크립트를 실행 하는 ***appliance_domain *-AD01** 노드. Windows PowerShell 스크립트를 실행 하기 전에 비 어플라이언스 DNS 서버의 IP 주소와 IP 주소를 대체 합니다.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  동일한 명령을 실행 하는 ***appliance_domain *-AD02** 노드.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>WSUS에 대 한 DNS 확인 구성  
SQL Server PDW 2012 통합 서비스 및 패치 기능을 제공 합니다. SQL Server PDW Microsoft Update와 다른 Microsoft 서비스 기술을 사용 합니다. 업데이트할 수 있도록 어플라이언스에 Microsoft 공용 WSUS 리포지토리 또는 회사 WSUS 저장소에 연결할 수 있어야 합니다.  
  
Microsoft 공용 WSUS 저장소에서 업데이트를 찾도록 어플라이언스를 구성 하도록 선택 하는 고객에 대 한 다음 지침에서는 어플라이언스에서 적절 한 구성 세부 정보를 설정 합니다.  
  
> [!NOTE]  
> 고객 네트워크 관리자에서 이름을 확인할 수 있는 회사 DNS 서버에 대 한 IP 주소를 제공 해야 **Microsoft.com**합니다.  
  
1.  VMM VM에 로그온 하는 원격 데스크톱을 사용 하 여 (<fabric domain>VMM) 패브릭 도메인 관리자 계정을 사용 합니다.  
  
2.  제어판을 열고 **네트워크 및 인터넷**, 클릭 하 고 **네트워크 및 공유 센터**합니다.  
  
3.  연결 목록에서 클릭 **VMSEthernet**, 클릭 하 고 **속성**합니다.  
  
4.  선택 **인터넷 프로토콜 버전 4 (TCP/IPv4)**, 클릭 하 고 **속성**합니다.  
  
5.  에 **보조 DNS 서버** 상자 고객 네트워크 관리자가 제공 되는 IP 주소를 추가 합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
