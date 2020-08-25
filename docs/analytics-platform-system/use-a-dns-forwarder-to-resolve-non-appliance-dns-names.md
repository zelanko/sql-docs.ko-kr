---
title: DNS 전달자 사용
description: DNS 전달자를 사용 하 여 분석 플랫폼 시스템에서 비-어플라이언스 DNS 이름을 확인 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399428"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 DNS 전달자를 사용 하 여 비 어플라이언스 DNS 이름 확인
스크립트 및 소프트웨어 응용 프로그램이 외부 서버에 액세스할 수 있도록 분석 플랫폼 시스템 어플라이언스의 Active Directory Domain Services 노드 (**_어플라이언스 \_ 도메인_-AD01** 및 ** _어플라이언스 \_ _AD02**)에서 DNS 전달자를 구성할 수 있습니다.  
  
## <a name="using-a-dns-forwarder"></a><a name="ResolveDNS"></a>DNS 전달자 사용  
분석 플랫폼 시스템 어플라이언스는 어플라이언스에 없는 서버의 DNS 이름을 확인 하지 않도록 구성 되어 있습니다. WSUS (Windows Software Update Services)와 같은 일부 프로세스는 어플라이언스 외부의 서버에 액세스 해야 합니다. 이 사용 시나리오를 지원 하려면 분석 플랫폼 시스템 DNS가 외부 DNS 서버를 사용 하 여 어플라이언스 외부에서 이름을 확인할 수 있도록 하 Virtual Machines는 외부 이름 전달자를 지원 하도록 분석 플랫폼 시스템 DNS를 구성할 수 있습니다. DNS 접미사의 사용자 지정 구성은 지원 되지 않습니다. 즉, 정규화 된 도메인 이름을 사용 하 여 비-어플라이언스 서버 이름을 확인 해야 합니다.  
  
**DNS GUI를 사용 하 여 DNS 전달자를 만들려면**  
  
1.  ** _어플라이언스 \_ 도메인_-AD01** 노드에 로그온 합니다.  
  
2.  DNS 관리자 (**dnsmgmt.msc**)를 엽니다.  
  
3.  서버 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
4.  **고급** 탭에서 **재귀 사용 안 함 (전달자도 사용 안 함)** 옵션을 선택 취소 한 다음 **적용**을 클릭 합니다.  
  
5.  **전달자** 탭을 클릭 한 다음 **편집**을 클릭 합니다.  
  
6.  이름 확인을 제공 하는 외부 DNS 서버의 IP 주소를 입력 합니다. 어플라이언스의 Vm 및 서버 (호스트)는 정규화 된 도메인 이름을 사용 하 여 외부 서버에 연결 합니다.  
  
7.  ** _어플라이언스 \_ 도메인_AD02** 노드에서 1-6 단계를 반복 합니다.  
  
**Windows PowerShell을 사용 하 여 DNS 전달자를 만들려면**  
  
1.  ** _어플라이언스 \_ 도메인_-AD01**노드에 로그온 합니다.  
  
2.  ** _어플라이언스 \_ 도메인_-AD01** 노드에서 다음 Windows PowerShell 스크립트를 실행 합니다. Windows PowerShell 스크립트를 실행 하기 전에 IP 주소를 비 어플라이언스 DNS 서버의 IP 주소로 바꿉니다.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  ** _어플라이언스 \_ 도메인_-AD02** 노드에서 동일한 명령을 실행 합니다.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>WSUS에 대 한 DNS 확인 구성  
SQL Server PDW 2012는 통합 서비스 및 패치 기능을 제공 합니다. SQL Server PDW에는 Microsoft 업데이트 및 기타 Microsoft 서비스 기술이 사용 됩니다. 업데이트를 사용 하도록 설정 하려면 어플라이언스는 회사 WSUS 리포지토리 또는 Microsoft 공용 WSUS 리포지토리에 연결할 수 있어야 합니다.  
  
Microsoft 공용 WSUS 리포지토리에서 업데이트를 찾도록 어플라이언스를 구성 하도록 선택 하는 고객의 경우 다음 지침에 따라 어플라이언스에서 적절 한 구성 세부 정보를 설정 합니다.  
  
> [!NOTE]  
> 고객 네트워크 관리자는 **Microsoft.com**에서 이름을 확인할 수 있는 회사 DNS 서버의 IP 주소를 제공 해야 합니다.  
  
1.  원격 데스크톱을 사용 하 여 <fabric domain> 패브릭 도메인 관리자 계정을 사용 하 여 VMM VM (-vmm)에 로그온 합니다.  
  
2.  제어판을 열고 **네트워크 및 인터넷**을 클릭 한 다음 **네트워크 및 공유 센터**를 클릭 합니다.  
  
3.  연결 목록에서 **Vmsethernet**을 클릭 한 다음 **속성**을 클릭 합니다.  
  
4.  **인터넷 프로토콜 버전 4(TCP/IPv4)** 를 선택하고 **속성**을 클릭합니다.  
  
5.  **대체 DNS 서버** 상자에 고객 네트워크 관리자가 제공한 IP 주소를 추가 합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
