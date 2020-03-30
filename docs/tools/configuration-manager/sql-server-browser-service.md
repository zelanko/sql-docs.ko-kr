---
title: SQL Server Browser 서비스
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.browseservers.local.f1
- sql13.swb.browseservers.network.f1
helpviewer_keywords:
- services [SQL Server], security
- SQL Browser service (See SQL Server Browser Service)
- Browser Service
- SQL Server Browser service
ms.assetid: 3cc00d3a-487c-4cd9-a155-655f02485fa0
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ba9a8f2af9b703b64ffadb597d9eda2edb28a0b8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307086"
---
# <a name="sql-server-browser-service"></a>SQL Server Browser 서비스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 프로그램은 Windows 서비스로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에 대해 들어오는 요청을 수신 대기하고 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정보를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 사용할 수 있습니다.  
  
-   사용할 수 있는 서버 목록 찾아보기  
  
-   올바른 서버 인스턴스에 연결  
  
-   DAC(관리자 전용 연결) 엔드포인트에 연결  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Browser 서비스(sqlbrowser)는 [!INCLUDE[ssAS](../../includes/ssas-md.md)]및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 각 인스턴스에 대해 인스턴스 이름과 버전 번호를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 설치됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 구성하거나 설치 중에 구성할 수 있습니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 자동으로 시작됩니다.  
  
-   설치를 업그레이드하는 경우  
  
-   클러스터에 설치하는 경우  
  
-   SQL Server Express의 모든 인스턴스를 포함한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 명명된 인스턴스를 설치하는 경우  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 명명된 인스턴스를 설치하는 경우  
  
## <a name="background"></a>배경  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]이전에는 컴퓨터 한 대에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 하나만 설치할 수 있었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 공식 IANA(Internet Assigned Numbers Authority)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 할당한 포트 1433을 통해 들어오는 요청을 수신했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 하나만 포트를 사용할 수 있으므로 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 에서 처음으로 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 지원하게 되자 UDP 포트 1434로 수신하기 위해 SSRP( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol)가 개발되었습니다. 이 수신기 서비스는 설치된 인스턴스 이름과 인스턴스에 사용되는 포트나 명명된 파이프를 사용하여 클라이언트 요청에 응답합니다. SSRP 시스템의 제한을 해결하기 위해 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Browser 서비스가 SSRP를 대신하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 도입되었습니다.  
  
## <a name="how-sql-server-browser-works"></a>SQL Server Browser 작동 방법  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 TCP/IP 프로토콜이 설정되면 서버에 TCP/IP 포트가 할당됩니다. 명명된 파이프 프로토콜을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 특정 명명된 파이프에서 수신합니다. 이 포트 또는 "파이프"는 클라이언트 애플리케이션과 데이터를 교환하기 위해 특정 인스턴스에 사용됩니다. 설치하는 동안 TCP 포트 1433과 파이프 `\sql\query` 가 기본 인스턴스에 할당되지만 나중에 서버 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 하나에서만 포트나 파이프를 사용할 수 있으므로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 비롯한 명명된 인스턴스에는 다른 포트 번호와 파이프 이름이 할당됩니다. 기본적으로 설정되어 있는 명명된 인스턴스와 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 둘 다 동적 포트를 사용하도록 구성되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때 사용 가능한 포트가 할당됩니다. 필요할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 특정 포트를 할당할 수 있습니다. 연결할 때 클라이언트가 특정 포트를 지정할 수 있지만 포트가 동적으로 할당될 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 시작되면 언제든지 포트 변호가 달라질 수 있어 클라이언트는 정확한 포트 번호를 알지 못합니다.  
  
 시작하자마자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 시작되어 UDP 포트 1434를 요청합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 레지스트리를 읽어 컴퓨터에 있는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 식별하여 사용되는 포트와 명명된 파이프를 기록합니다. 서버에 네트워크 카드가 두 개 이상 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용할 수 있는 포트 중 처음 발견된 포트를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 ipv6과 ipv4를 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스를 요청하면 클라이언트 네트워크 라이브러리에서 포트 1434를 사용하여 서버로 UDP 메시지를 보냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에서는 요청된 인스턴스의 TCP/IP 포트나 명명된 파이프를 사용하여 응답합니다. 그러면 클라이언트 애플리케이션 네트워크 라이브러리가 원하는 인스턴스의 포트나 명명된 파이프를 사용하여 서버로 요청을 보내 연결을 완료합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 시작 및 중지하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
## <a name="using-sql-server-browser"></a>SQL Server Browser 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행되고 있지 않아도 올바른 포트 번호나 명명된 파이프를 제공하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 수 있습니다. 예를 들어 포트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스가 포트 1433에서 실행 중이면 TCP/IP로 이 인스턴스에 연결할 수 있습니다.  
  
 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행되고 있지 않으면 다음 연결은 작동하지 않습니다.  
  
-   TCP/IP 포트나 명명된 파이프와 같은 모든 매개 변수를 완전히 지정하지 않고 명명된 인스턴스에 연결하려고 하는 구성 요소  
  
-   다시 연결하기 위해 다른 구성 요소에서 나중에 사용할 수 있는 server\instance 정보를 생성하거나 전달하는 구성 요소  
  
-   포트 번호나 파이프를 제공하지 않고 명명된 인스턴스에 연결  
  
-   TCP/IP 포트 1433을 사용하지 않을 경우 명명된 인스턴스나 기본 인스턴스에 대한 DAC  
  
-   OLAP 리디렉터 서비스  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 엔터프라이즈 관리자 또는 쿼리 분석기에 서버 열거  
  
 애플리케이션이 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 액세스하는 경우처럼 클라이언트-서버 시나리오에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 중지하거나 해제하면 각 인스턴스에 특정 포트 번호를 할당하고 해당 포트 번호를 항상 사용하도록 클라이언트 애플리케이션 코드를 작성해야 합니다. 이 방법에는 다음과 같은 문제점이 있습니다.  
  
-   애플리케이션 코드를 업데이트하고 유지 관리하여 올바른 포트에 연결하도록 해야 합니다.  
  
-   각 인스턴스에 대해 선택한 포트를 서버의 다른 서비스나 애플리케이션에서 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용할 수 없게 됩니다.  
  
## <a name="clustering"></a>Clustering  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 클러스터형 리소스가 아니며 클러스터 노드 간 장애 조치(Failover)를 지원하지 않으므로 클러스터의 경우 클러스터의 노드마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 설치하고 튜닝해야 합니다. 클러스터에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 IP_ANY에서 수신합니다.  
  
> [!NOTE]  
>  IP_ANY에서 수신할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 처음 발견되는 IP/포트 쌍을 반환하므로 사용자가 IP마다 같은 TCP 포트를 구성해야 하는 특정 IP에서 수신하도록 설정할 수 있습니다.  
  
## <a name="installing-uninstalling-and-running-from-the-command-line"></a>명령줄에서 설치, 제거 및 실행  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 프로그램은 C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe에 설치됩니다.  
  
 마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제거될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스도 제거됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 **-c** 스위치를 사용하여 명령 프롬프트에서 시작하여 문제를 해결할 수 있습니다.  
  
```  
<drive>\<path>\sqlbrowser.exe -c  
```  
  
## <a name="security"></a>보안  
  
### <a name="account-privileges"></a>계정 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 UDP 포트에서 수신하고 SSRP( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol)를 사용하여 인증되지 않은 요청을 허용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 실행해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 로그온 계정을 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser의 최소 사용자 권한은 다음과 같습니다.  
  
-   네트워크에서 이 컴퓨터 액세스 거부  
  
-   로컬 로그온 거부  
  
-   일괄 작업으로 로그온 거부  
  
-   터미널 서비스를 통한 로그온 거부  
  
-   서비스로 로그온  
  
-   네트워크 통신(포트 및 파이프) 관련 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 레지스트리 키 읽기 및 쓰기  
  
### <a name="default-account"></a>기본 계정  
 설치하는 동안 서비스에 대해 선택한 계정을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 구성합니다. 사용할 수 있는 다른 계정은 다음과 같습니다.  
  
-   모든 **domain\local** 계정  
  
-   **로컬 서비스** 계정  
  
-   **로컬 시스템** 계정(불필요한 권한이 있으면 권장되지 않음)  
  
### <a name="hiding-sql-server"></a>SQL Server 숨기기  
 숨겨진 인스턴스는 공유 메모리 연결만 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 `HideInstance` 플래그를 설정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에서 이 서버 인스턴스에 대한 정보를 사용하여 응답할 수 없음을 나타내십시오.  
  
### <a name="using-a-firewall"></a>방화벽 사용  
 방화벽이 설치된 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스와 통신하려면 UDP 포트 1434 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용되는 1433 등의 TCP 포트를 여십시오. 방화벽 작업 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 “방법: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스를 허용하도록 방화벽 구성”을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로토콜 및 네트워크 라이브러리](../../sql-server/install/network-protocols-and-network-libraries.md)  
  
  
