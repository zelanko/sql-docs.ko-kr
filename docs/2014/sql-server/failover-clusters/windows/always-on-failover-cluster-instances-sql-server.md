---
title: Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- high availability [SQL Server], failover clustering
- virtual servers [SQL Server], about virtual servers
- clusters [SQL Server]
- servers [SQL Server], failover clustering
- resource groups [SQL Server]
- availability [SQL Server]
- failover clustering [SQL Server]
- AlwaysOn [SQL Server], see failover clustering [SQL Server]
ms.assetid: 86a15b33-4d03-4549-8ea2-b45e4f1baad7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff76632459f25981041e5585cd9cbb3dbcf906c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62520490"
---
# <a name="always-on-failover-cluster-instances-sql-server"></a>Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always On 제품을 위해 Always On 장애 조치(failover) 클러스터 인스턴스는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 기능을 사용하여 FCI(*장애 조치(failover) 클러스터 인스턴스*)라고 부르는 서버 인스턴스 수준의 중복성을 통해 로컬 고가용성을 제공합니다. FCI는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드 및 다중 서브넷 간에 설치되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 단일 인스턴스입니다. 네트워크에서 FCI는 단일 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스처럼 보이지만 현재 노드를 사용할 수 없을 경우 FCI가 하나의 WSFC 노드에서 다른 노드로 장애 조치(failover) 기능을 제공합니다.  
  
 FCI는 [AlwaysOn 가용성 그룹](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)을 활용하여 데이터베이스 수준에서 원격 재해 복구 기능을 제공할 수 있습니다. 자세한 내용은 [장애 조치(Failover) 클러스터링 및 AlwaysOn 가용성 그룹(SQL Server)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 Always On 장애 조치(failover) 클러스터 인스턴스는 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 및 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 모두에서 CSV(클러스터 공유 볼륨)를 지원합니다. CSV에 대한 자세한 내용은 [장애 조치(Failover) 클러스터에서 클러스터 공유 볼륨 이해](https://technet.microsoft.com/library/dd759255.aspx)를 참조하세요.  
  
 **항목 내용:**  
  
-   [이점](#Benefits)  
  
-   [권장 사항](#Recommendations)  
  
-   [장애 조치(Failover) 클러스터 인스턴스 개요](#Overview)  
  
-   [장애 조치(Failover) 클러스터 인스턴스의 요소](#FCIelements)  
  
-   [SQL Server 장애 조치(Failover) 개념 및 태스크](#ConceptsAndTasks)  
  
-   [관련 항목](#RelatedTopics)  
  
##  <a name="Benefits"></a> 장애 조치(Failover) 클러스터 인스턴스의 이점  
 서버에 하드웨어 또는 소프트웨어 오류가 있을 경우 서버에 연결하는 애플리케이션이나 클라이언트에서 작동 중단이 발생합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 독립형 인스턴스가 아니라 FCI로 구성된 경우, 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 고가용성은 FCI에 있는 중복된 노드를 통해 보호됩니다. FCI에 있는 여러 노드 중에서 WSFC 리소스 그룹을 소유하는 노드는 한 번에 하나뿐입니다. 오류(하드웨어 오류, 운영 체제 오류, 애플리케이션 또는 서비스 오류)가 발생하거나 계획된 업그레이드가 수행될 경우에는 리소스 그룹의 소유권이 다른 WSFC 노드로 넘어갑니다. 이 프로세스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 연결하는 클라이언트나 애플리케이션에 투명하게 수행되며, 오류 중 애플리케이션이나 클라이언트에 발생하는 작동 중단 시간을 최소화합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스가 제공하는 몇 가지 주요 이점은 다음과 같습니다.  
  
-   중복을 통한 인스턴스 수준의 보호  
  
-   오류(하드웨어 오류, 운영 체제 오류, 애플리케이션 또는 서비스 오류) 발생 시 자동 장애 조치(Failover)  
  
    > [!IMPORTANT]  
    >  Always On 가용성 그룹에서는 FCI에서 해당 가용성 그룹 내의 다른 노드로의 자동 장애 조치(failover)가 지원되지 않습니다. 즉, 고가용성 솔루션에서 자동 장애 조치(failover)가 중요한 구성 요소일 경우 하나의 가용성 그룹 내에 FCI와 독립형 노드를 함께 연결해서는 안됩니다. 그러나 *재해 복구* 솔루션에 대해서는 이러한 연결이 가능합니다.  
  
-   WSFC 클러스터 디스크(iSCSI, 파이버 채널 등) 및 SMB(서버 메시지 블록) 파일 공유와 같은 다양한 스토리지 솔루션 지원  
  
-   다중 서브넷 FCI를 사용하거나 Always On 가용성 그룹 내에서 FCI가 호스트하는 데이터베이스를 실행하는 재해 복구 솔루션. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]의 새로운 다중 서브넷 지원 덕분에 다중 서브넷 FCI에는 더 이상 가상 LAN이 필요하지 않으며 다중 서브넷 FCI에 대한 관리 및 보안 성능이 향상되었습니다.  
  
-   장애 조치(failover) 중 애플리케이션 및 클라이언트를 재구성할 필요 없음  
  
-   자동 장애 조치(failover)를 위해 세부적인 트리거 이벤트에 대한 유연한 장애 조치(failover) 정책  
  
-   전용 및 영구 연결을 사용하는 정기적이고 세부적인 상태 검색을 통한 안정적인 장애 조치(failover)  
  
-   간접 백그라운드 검사점을 통해 장애 조치(failover) 시간에 대한 구성 및 예측 가능  
  
-   장애 조치(failover) 중 리소스 사용 조절  
  
##  <a name="Recommendations"></a> 권장 사항  
 프로덕션 환경에서 장애 조치(Failover) 클러스터 인스턴스의 가상 IP 주소와 함께 고정 IP 주소를 사용하는 것이 좋습니다.  DHCP는 프로덕션 환경에서 사용하지 않는 것이 좋습니다. 작동이 중단하고 DHCP IP 임대가 만료된 경우 DNS 이름과 연결된 새 DHCP IP 주소를 다시 등록하는 데 시간이 추가로 소요됩니다.  
  
##  <a name="Overview"></a> 장애 조치(Failover) 클러스터 인스턴스 개요  
 FCI는 WSFC 노드가 하나 이상 포함된 WSFC 리소스 그룹에서 실행됩니다. FCI가 시작되면 노드 중 하나가 리소스 그룹의 소유권을 갖고 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 온라인으로 설정합니다. 이 노드가 소유하는 리소스는 다음과 같습니다.  
  
-   네트워크 이름  
  
-   IP 주소  
  
-   공유 디스크  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 엔진 서비스  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Services 서비스(설치된 경우)  
  
-   파일 공유 리소스 하나(FILESTREAM 기능이 설치된 경우)  
  
 리소스 그룹에서 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 실행하는 노드는 언제라도 해당 리소스 그룹 소유자뿐이며 FCI의 다른 노드는 서비스를 실행할 수 없습니다. 장애 조치(failover)가 수행되면 자동 장애 조치(failover) 또는 계획된 장애 조치(failover)인지 여부에 따라 다음과 같은 순서로 이벤트가 발생합니다.  
  
1.  하드웨어 또는 시스템 오류가 발생하지 않은 한 버퍼 캐시에 있는 모든 더티 페이지가 디스크에 기록됩니다.  
  
2.  리소스 그룹의 모든 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 현재 노드에서 중지됩니다.  
  
3.  리소스 그룹 소유권은 FCI의 다른 노드로 전송됩니다.  
  
4.  새 리소스 그룹 소유자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 시작합니다.  
  
5.  클라이언트 애플리케이션 연결 요청이 동일한 VNN(가상 네트워크 이름)을 사용하여 새 현재 노드에 자동으로 연결됩니다.  
  
 FCI는 기본 WSFC 클러스터의 쿼럼 상태가 올바른 한(대부분의 쿼럼 WSFC 노드를 자동 장애 조치(failover) 대상으로 사용할 수 있는 경우) 온라인 상태로 유지됩니다. WSFC 클러스터가 쿼럼을 잃으면, 그 원인이 하드웨어, 소프트웨어, 네트워크 오류인지 아니면 부적절한 쿼럼 구성으로 인한 것인지에 따라 해당 FCI와 함께 전체 WSFC 클러스터가 오프라인으로 설정됩니다. 이러한 계획되지 않은 장애 조치(failover) 시나리오에서는 WSFC 클러스터 및 FCI를 다시 온라인으로 설정하기 위해 사용 가능한 남은 노드에서 쿼럼을 다시 설정하도록 수동 개입이 필요합니다. 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성(SQL Server)](wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
### <a name="predictable-failover-time"></a>예측 가능한 장애 조치(Failover) 시간  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 검사점 작업을 마지막으로 언제 수행했는지에 따라 버퍼 캐시에 더티 페이지가 대량으로 남아 있을 수 있습니다. 따라서 남은 더티 페이지를 디스크에 기록하기 위한 시간만큼 장애 조치(failover)가 지속되어 장애 조치(failover) 시간이 오래 걸리고 예측할 수 없게 될 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 FCI가 간접 검사점을 사용하여 버퍼 캐시에 남은 더티 페이지의 양을 조절할 수 있습니다. 이러한 방식은 일반적인 작업의 경우 추가 리소스를 소비하지만 장애 조치(failover) 시간을 보다 예측 가능하도록 만들고 구성할 수도 있게 해줍니다. 이 기능은 조직 내 서비스 수준 계약에 따라 고가용성 솔루션에 대한 RTO(복구 시간 목표)가 지정된 경우에 매우 유용합니다. 간접 검사점에 대한 자세한 내용은 [Indirect Checkpoints](../../../relational-databases/logs/database-checkpoints-sql-server.md#IndirectChkpt)을 참조하세요.  
  
### <a name="reliable-health-monitoring-and-flexible-failover-policy"></a>안정적인 상태 모니터링 및 유연한 장애 조치(Failover) 정책  
 FCI가 성공적으로 시작된 다음에는 WSFC 서비스가 기본 WSFC 클러스터의 상태뿐만 아니라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 상태를 모두 모니터링합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터 WSFC 서비스는 시스템 저장 프로시저를 통한 자세한 구성 요소 진단을 위해 전용 연결을 사용하여 현재 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 폴링합니다. 이 방식은 세 가지 의미를 갖습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 전용 연결을 통해 FCI의 부하가 높더라도 항상 구성 요소 진단을 위해 폴링을 안정적으로 수행할 수 있습니다. 부하가 높은 시스템과 실제로 오류 조건이 있는 시스템을 구분할 수 있으므로 잘못된 장애 조치(failover)와 같은 문제를 방지할 수 있습니다.  
  
-   자세한 구성 요소 진단을 통해 보다 유연한 장애 조치(failover) 정책을 구성할 수 있으며, 이러한 정책에서 장애 조치(failover)를 일으키는 오류 조건과 그렇지 않은 오류 조건을 선택할 수 있습니다.  
  
-   또한 자세한 구성 요소 진단은 자동 장애 조치(failover)에 대한 소급적인 문제 해결에도 도움을 줍니다. 진단 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 로그와 함께 배치되는 로그 파일에 저장됩니다. 로그 파일을 로그 파일 뷰어에 로드해서 장애 조치(failover)를 일으킨 구성 요소 상태를 검사하여 해당 장애 조치(failover)가 발생한 원인을 확인할 수 있습니다.  
  
 자세한 내용은 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)를 참조하세요.  
  
##  <a name="FCIelements"></a> 장애 조치(Failover) 클러스터 인스턴스의 요소  
 FCI는 운영 체제 버전과 패치 수준 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전과 패치 수준, 구성 요소 및 인스턴스 이름을 포함하는 동일 소프트웨어 구성뿐만 아니라 비슷한 하드웨어 구성을 포함하는 물리적 서버(노드) 집합으로 구성됩니다. 노드간 장애 조치(failover)를 수행할 때 FCI가 완전히 작동할 수 있도록 하려면 소프트웨어 구성이 동일해야 합니다.  
  
 WSFC 리소스 그룹  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI는 WSFC 리소스 그룹에서 실행됩니다. 리소스 그룹의 각 노드는 동기화된 구성 설정 복사본과 검사 기준 레지스트리 키를 유지하여 장애 조치(failover) 후 FCI가 완전히 작동하고 클러스터의 노드 중 한 번에 하나의 노드만 리소스 그룹을 소유하도록 보장합니다. WSFC 서비스는 FCI의 VNN 및 가상 IP 주소뿐만 아니라 서버 클러스터, 쿼럼 구성, 장애 조치(failover) 정책 및 장애 조치(failover) 작업을 관리합니다. 오류(하드웨어 오류, 운영 체제 오류, 애플리케이션 또는 서비스 오류)가 발생하거나 계획된 업그레이드가 수행될 경우에는 리소스 그룹의 소유권이 FCI의 다른 노드로 넘어갑니다. WSFC 리소스 그룹에서 지원되는 노드 수는 사용자의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다. 또한 CPU, 메모리 및 디스크 수와 같은 하드웨어 용량에 따라 동일한 WSFC 클러스터가 여러 FCI(다중 리소스 그룹)를 실행할 수 있습니다.  
  
 SQL Server 바이너리  
 제품 바이너리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 독립형 설치와 비슷하게 FCI의 각 노드에 로컬로 설치됩니다. 하지만 노드를 시작할 때 서비스가 자동으로 시작되지는 않으며, WSFC에서 관리됩니다.  
  
 스토리지  
 Always On 가용성 그룹과 달리 FCI는 데이터베이스 및 로그 스토리지를 위해 FCI의 모든 노드 간에 공유 스토리지를 사용해야 합니다. 공유 스토리지는 WSFC 클러스터 디스크, SAN 디스크 또는 SMB의 파일 공유 형식일 수 있습니다. 이러한 방식으로 장애 조치(failover)가 발생할 때마다 FCI의 모든 노드가 동일한 인스턴스 데이터를 사용할 수 있습니다. 하지만 잠재적으로 공유 스토리지가 단일 장애 지점이 될 가능성은 없으며, FCI는 기본 스토리지 솔루션을 사용하여 데이터 보호를 보장합니다.  
  
 네트워크 이름  
 FCI의 VNN은 FCI에 대한 통합 연결 지점을 제공합니다. 따라서 현재 노드가 무엇인지 확인할 필요 없이 애플리케이션이 VNN에 연결할 수 있습니다. 장애 조치(failover)가 발생하면 새 현재 노드가 시작된 후 이 노드에 VNN이 등록됩니다. 이 프로세스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 연결하는 클라이언트나 애플리케이션에 투명하게 수행되며, 오류 중 애플리케이션이나 클라이언트에 발생하는 작동 중단 시간을 최소화합니다.  
  
 가상 IP  
 다중 서브넷 FCI의 경우 FCI의 각 서브넷에 가상 IP 주소가 할당됩니다. 그리고 장애 조치(failover)가 발생하면 해당 서브넷의 가상 IP 주소를 가리키도록 DNS 서버에서 VNN이 업데이트됩니다. 그런 다음에는 다중 서브넷 장애 조치(failover) 후에도 애플리케이션 및 클라이언트가 동일한 VNN을 사용하여 FCI에 연결할 수 있습니다.  
  
##  <a name="ConceptsAndTasks"></a> SQL Server 장애 조치(Failover) 개념 및 태스크  
  
|개념 및 태스크|항목|  
|------------------------|-----------|  
|오류 검색 메커니즘과 유연한 장애 조치(failover) 정책에 대해 설명합니다.|[장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](failover-policy-for-failover-cluster-instances.md)|  
|FCI 관리 및 유지 관리에 대한 개념을 설명합니다.|[장애 조치(failover) 클러스터 인스턴스 관리 및 유지 관리](failover-cluster-instance-administration-and-maintenance.md)|  
|다중 서브넷 구성 및 개념 설명|[SQL Server 다중 서브넷 클러스터링 ( SQL Server);](sql-server-multi-subnet-clustering-sql-server.md)|  
  
##  <a name="RelatedTopics"></a> 관련 항목  
  
|**항목 설명**|**항목**|  
|----------------------------|---------------|  
|새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI를 설치하는 방법을 설명합니다.|[새 SQL Server 장애 조치 클러스터를 만듭니다 ( 설치 프로그램).](../install/create-a-new-sql-server-failover-cluster-setup.md)|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 장애 조치(failover) 클러스터를 업그레이드하는 방법을 설명합니다.|[SQL Server 장애 조치(Failover) 클러스터 업그레이드](upgrade-a-sql-server-failover-cluster-instance.md)|  
|Windows 장애 조치(Failover) 클러스터링 개념을 설명하고 Windows 장애 조치(Failover) 클러스터링에 관련된 태스크의 링크를 제공합니다.|[!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]: [장애 조치 클러스터 개요](https://go.microsoft.com/fwlink/?LinkId=177878)<br /><br /> [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] R2: [장애 조치 클러스터 개요](https://go.microsoft.com/fwlink/?LinkId=177879)|  
|FCI의 노드와 가용성 그룹 내 복제본 간의 개념적인 차이를 설명하고 FCI를 사용하여 가용성 그룹을 위한 복제본을 호스팅할 때 고려해야 할 사항에 대해 설명합니다.|[장애 조치 클러스터링 및 Always On 가용성 그룹 (SQL Server)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)|  
  
  
