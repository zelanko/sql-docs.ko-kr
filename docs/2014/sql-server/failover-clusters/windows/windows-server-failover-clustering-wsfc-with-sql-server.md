---
title: SQL Server의 WSFC(Windows Server 장애 조치(Failover) 클러스터링) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Windows Server Failover Clustering (WSFC), with SQL Server
- WSFC, with SQL Server
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 79d2ea5a-edd8-4b3b-9502-96202057b01a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f39911901b6ab729382c2e08b34c3452d4ec65cd
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367055"
---
# <a name="windows-server-failover-clustering-wsfc-with-sql-server"></a>SQL Server의 WSFC(Windows Server 장애 조치(Failover) 클러스터링)
  WSFC( *Windows Server 장애 조치(failover) 클러스터링* ) 클러스터는 애플리케이션 및 서비스의 가용성 향상을 위해 함께 작동하는 독립 서버 그룹입니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서는 WSFC 서비스와 기능을 활용하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 지원합니다.  
  
 
  
##  <a name="TermsAndDefs"></a> 용어 및 정의  
 WSFC 클러스터  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터는 애플리케이션 및 서비스의 가용성 향상을 위해 함께 작동하는 독립 서버 그룹입니다.  
  
 장애 조치(Failover) 클러스터 인스턴스  
 하나 이상의 애플리케이션 또는 서비스를 실행하는 데 필요한 IP 주소 리소스, 네트워크 이름 리소스 및 추가 리소스를 관리하는 Windows 서비스 인스턴스입니다. 클라이언트는 네트워크 이름을 사용하여 그룹의 리소스에 액세스할 수 있습니다. 이는 컴퓨터 이름을 사용하여 실제 서버의 서비스에 액세스하는 것과 비슷합니다. 그러나 장애 조치(Failover) 클러스터 인스턴스는 그룹이기 때문에 기본 이름 또는 주소에 영향을 주지 않고 다른 노드에 장애 조치될 수 있습니다.  
  
 노드  
 서버 클러스터의 활성 또는 비활성 멤버인 Microsoft Windows Server 시스템입니다.  
  
 클러스터 리소스  
 노드에서 소유하고, 온라인 또는 오프라인으로 전환하고, 노드 간에 이동하고, 클러스터 개체로 관리할 수 있는 물리적 엔터티 또는 논리적 엔터티입니다. 클러스터 리소스는 항상 하나의 노드에서만 소유할 수 있습니다.  
  
 리소스 그룹  
 단일 클러스터 개체로 관리되는 클러스터 리소스 모음입니다. 일반적으로 리소스 그룹은 특정 애플리케이션이나 서비스를 실행하는 데 필요한 모든 클러스터 리소스를 포함합니다. 장애 조치(Failover) 및 장애 복구(failback)는 리소스 그룹에만 적용됩니다.  
  
 리소스 종속성  
 다른 리소스에 종속되는 리소스입니다. 리소스 A가 리소스 B에 종속하는 경우 B는 A의 종속성입니다.  
  
 네트워크 이름 리소스  
 클러스터 리소스로 관리되는 논리 서버 이름입니다. 네트워크 이름 리소스는 IP 주소 리소스와 함께 사용해야 합니다.  
  
 기본 설정 소유자  
 리소스 그룹이 실행되는 노드입니다. 각 리소스 그룹은 기본 설정의 순서대로 정렬된 기본 설정 소유자 목록에 연결됩니다. 자동 장애 조치(Failover) 중에 리소스 그룹은 기본 설정 소유자 목록의 다음 기본 설정 노드로 이동됩니다.  
  
 가능한 소유자  
 리소스가 실행될 수 있는 보조 노드입니다. 각 리소스 그룹은 가능한 소유자 목록에 연결됩니다. 리소스 그룹은 가능한 소유자 목록에 있는 노드에만 장애 조치될 수 있습니다.  
  
 쿼럼 모드  
 클러스터에서 유지할 수 있는 노드 실패 수를 결정하는 장애 조치(Failover) 클러스터의 쿼럼 구성입니다.  
  
 강제 쿼럼  
 쿼럼에 필요한 요소 중 일부만 통신 중이더라도 클러스터를 시작하는 프로세스입니다.  
  
 참조 항목: [장애 조치 클러스터 용어 설명](/previous-versions/windows/desktop/MsCS/server-cluster-glossary)  
  
##  <a name="Overview"></a> Windows Server 장애 조치(Failover) 클러스터링 개요  
 Windows Server 장애 조치(Failover) 클러스터링은 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , Microsoft Exchange 등의 호스팅된 서버 애플리케이션의 고가용성 및 재해 복구 시나리오를 지원하는 인프라 기능을 제공합니다. 클러스터 노드 또는 서비스가 실패하면 해당 노드에 호스팅된 서비스는 *장애 조치(Failover)* 라는 프로세스를 통해 사용 가능한 다른 노드에 자동으로 전송되거나 수동으로 전송할 수 있습니다.  
  
 WSFC 클러스터의 노드가 함께 작동하여 다음과 같은 기능을 제공합니다.  
  
-   **분산된 메타데이터 및 알림.** WSFC 서비스와 호스팅된 애플리케이션 메타데이터가 클러스터의 각 노드에서 유지 관리됩니다. 이 메타데이터에는 WSFC 구성 및 상태와 호스팅된 애플리케이션 설정이 포함됩니다. 노드의 메타데이터 또는 상태에 대한 변경 내용은 클러스터의 다른 노드에 자동으로 전파됩니다.  
  
-   **리소스 관리.** 클러스터의 개별 노드는 직접 연결된 저장소, 네트워크 인터페이스, 공유 디스크 저장소에 대한 액세스 등의 실제 리소스를 제공합니다. 호스팅된 애플리케이션은 클러스터 리소스로 등록되며 다른 리소스에 대한 시작 및 상태 종속성을 구성할 수 있습니다.  
  
-   **상태 모니터링.** 노드 간 상태 검색 및 주 노드 상태 검색은 하트비트 스타일 네트워크 통신과 리소스 모니터링의 조합을 통해 수행됩니다. 클러스터의 전반적인 상태는 클러스터에서 노드의 쿼럼 투표에 의해 결정됩니다.  
  
-   **장애 조치(Failover) 조정.** 각 리소스는 주 노드에 호스팅되도록 구성되며, 하나 이상의 보조 노드에 자동 또는 수동으로 전송될 수 있습니다. 상태 기반 장애 조치(Failover) 정책은 노드 간의 리소스 소유권 자동 전송을 제어합니다. 장애 조치(Failover)가 발생할 경우 적절히 대응할 수 있도록 노드 및 호스팅된 애플리케이션에 알림을 제공합니다.  
  
 참조 항목: [Windows Server 2008 R2의 장애 조치(Failover) 클러스터](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
##  <a name="AlwaysOnWsfcTech"></a> SQL Server AlwaysOn 기술 및 WSFC  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] *AlwaysOn* 새 높은 가용성 및 재해 복구 솔루션을 WSFC를 활용 하는 합니다. AlwaysOn은 애플리케이션 가용성을 높이고 하드웨어에 대한 ROI(투자 수익률)를 향상시키고 고가용성 배포 및 관리를 간소화하는 유연한 통합 솔루션입니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스는 WSFC를 플랫폼 기술로 사용하고 구성 요소를 WSFC 클러스터 리소스로 등록합니다.  관련 리소스는 *리소스 그룹*에 결합되므로 다른 WSFC 클러스터 리소스에 종속될 수 있습니다. WSFC 클러스터 서비스에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 하는지 감지하여 신호를 보내거나 WSFC 클러스터의 다른 서버 노드에 자동으로 장애 조치합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 기술을 최대한 활용하려면 여러 WSFC 관련 사전 요구 사항을 적용해야 합니다.  
>   
>  참조 항목: [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
### <a name="instance-level-high-availability-with-alwayson-failover-cluster-instances"></a>AlwaysOn 장애 조치(Failover) 클러스터 인스턴스가 있는 인스턴스 수준 고가용성  
 *AlwaysOn FCI(장애 조치(Failover) 클러스터 인스턴스* )는 WSFC 클러스터에서 노드를 통해 설치되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스입니다. 이 유형의 인스턴스는 공유 디스크 저장소(파이버 채널 또는 iSCSI SAN 사용) 및 가상 네트워크 이름에 대한 리소스 종속성이 있습니다. 가상 네트워크 이름은 서로 다른 서브넷에 있는 하나 이상의 가상 IP 주소에 대한 리소스 종속성이 있습니다. SQL Server 서비스와 SQL Server 에이전트 서비스는 리소스로 등록되고 가상 네트워크 이름 리소스에 종속됩니다.  
  
 장애 조치(Failover)가 발생하면 WSFC 서비스는 인스턴스 리소스의 소유권을 지정된 장애 조치(Failover) 노드에 전송합니다. 그러면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 장애 조치 노드(Failover)에서 다시 시작되고 데이터베이스는 복구됩니다. 모든 지정된 시점에서 클러스터의 노드 중 하나만 FCI 및 기본 리소스를 호스팅할 수 있습니다.  
  
> [!NOTE]  
>  AlwaysOn 장애 조치(Failover) 클러스터 인스턴스는 SAN(Storage Area Network) 또는 SMB 파일 공유와 같은 대칭 공유 디스크 저장소가 필요합니다.  공유 디스크 저장소 볼륨은 WSFC 클러스터의 모든 잠재적인 장애 조치(Failover) 노드에서 사용할 수 있어야 합니다.  
  
 참조 항목: [AlwaysOn 장애 조치 클러스터 인스턴스](always-on-failover-cluster-instances-sql-server.md)  
  
### <a name="database-level-high-availability-with-includesshadrincludessshadr-mdmd"></a>다음이 있는 데이터베이스 수준 고가용성 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  
 *가용성 그룹* 은 함께 장애 조치되는 사용자 데이터베이스 집합입니다. 가용성 그룹은 주 *가용성 복제본* 과 공유 저장소를 필요로 하지 않고 데이터 보호를 위해 SQL Server 로그 기반 데이터 이동을 통해 유지 관리되는 1-4개의 보조 복제본으로 구성됩니다. 각 복제본은 WSFC 클러스터의 서로 다른 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 의해 호스팅됩니다. 가용성 그룹과 해당 가상 네트워크 이름은 WSFC 클러스터에 리소스로 등록됩니다.  
  
 주 복제본 노드의 *가용성 그룹 수신기* 는 가상 네트워크 이름에 연결하기 위한 들어오는 클라이언트 요청에 응답하고 연결 문자열의 특성을 기반으로 각 요청을 적절한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 리디렉션합니다.  
  
 장애 조치(Failover) 중에 공유되는 실제 리소스의 소유권을 다른 노드로 전송하는 대신 WSFC를 활용하여 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 보조 복제본을 가용성 그룹의 주 복제본으로 다시 구성합니다. 그러면 가용성 그룹의 가상 네트워크 이름 리소스가 해당 인스턴스로 전송됩니다.  
  
 항상 단일 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스만 가용성 그룹 데이터베이스의 주 복제본을 호스팅할 수 있고 모든 연결된 보조 복제본은 각각 별도의 인스턴스에 위치해야 하며 각 인스턴스는 별도의 실제 노드에 있어야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]은 장애 조치(Failover) 클러스터 인스턴스를 배포하거나 대칭 공유 저장소(SAN 또는 SMB)를 사용할 필요가 없습니다.  
>   
>  FCI(장애 조치(Failover) 클러스터 인스턴스)를 가용성 그룹과 함께 사용하여 가용성 복제본의 가용성을 높일 수 있습니다. 그러나 WSFC 클러스터에서 잠재적 경합 상태를 방지하기 위해 FCI에 호스팅된 가용성 복제본을 원본 또는 대상으로 하는 가용성 그룹 자동 장애 조치(Failover)는 지원되지 않습니다.  
  
 참조 항목: [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
##  <a name="AlwaysOnWsfcHealth"></a> WSFC 상태 모니터링 및 장애 조치(Failover)  
 AlwaysOn 솔루션에 대한 고가용성을 위해서는 물리/논리적 WSFC 클러스터 리소스의 상태를 사전에 모니터링하고 중복 하드웨어를 자동으로 장애 조치하고 다시 구성해야 합니다.  또한 시스템 관리자는 가용성 그룹 또는 *인스턴스를 다른 노드로* 수동 장애 조치(Failover) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 할 수 있습니다.  
  
### <a name="failover-policies-for-nodes-failover-cluster-instances-and-availability-groups"></a>노드, 장애 조치(Failover) 클러스터 인스턴스 및 가용성 그룹에 대한 장애 조치(Failover) 정책  
 *장애 조치(failover) 정책* 은 WSFC 클러스터 노드, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(failover) 클러스터 인스턴스) 및 가용성 그룹 수준으로 구성됩니다.  이러한 정책에서는 비정상 클러스터 리소스 상태 및 노드 응답의 심각도, 기간 및 빈도를 기반으로 서비스를 다시 시작하거나 클러스터 리소스를 다른 노드로 *자동 장애 조치(Failover)* 할 수 있습니다. 또는 가용성 그룹 주 복제본을 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 이동할 수 있습니다.  
  
 가용성 그룹 복제본에 대한 장애 조치(Failover)는 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 영향을 주지 않습니다.  FCI를 장애 조치하면 호스팅된 가용성 그룹 복제본이 인스턴스와 함께 이동합니다.  
  
 참조 항목: [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](failover-policy-for-failover-cluster-instances.md)  
  
### <a name="wsfc-resource-health-detection"></a>WSFC 리소스 상태 검색  
 WSFC 클러스터 노드의 각 리소스는 요청이 있을 때나 정기적으로 상태를 보고할 수 있습니다. 정전, 디스크 또는 메모리 오류, 네트워크 통신 오류, 응답하지 않는 서비스 등, 다양한 경우에 리소스 오류가 발생할 수 있습니다.  
  
 네트워크, 저장소 또는 서비스와 같은 WSFC 클러스터 리소스는 서로 종속될 수 있습니다. 리소스의 누적 상태는 각 리소스 종속성의 상태를 연속적으로 롤업하여 결정됩니다.  
  
### <a name="wsfc-inter-node-health-detection-and-quorum-voting"></a>WSFC 노드 간 상태 검색 및 쿼럼 투표  
 WSFC 클러스터의 각 노드는 주기적 하트비트 통신에 참여하여 노드의 상태를 다른 노드와 공유합니다. 응답하지 않는 노드는 오류 상태에 있는 것으로 간주됩니다.  
  
 WSFC 클러스터에서 *쿼럼* 노드 집합은 대부분의 투표 노드 및 미러링 모니터입니다. WSFC 클러스터의 전반적인 상태는 주기적 *쿼럼 득표*에 의해 결정됩니다. 쿼럼이 있으면 클러스터가 양호한 상태이고 노드 수준의 내결함성을 제공할 수 있음을 의미합니다.  
  
 *쿼럼 모드* 는 쿼럼 투표에 사용되는 방법과 자동 장애 조치(Failover)를 수행하거나 클러스터를 오프라인으로 전환할 시기를 나타내는 WSFC 클러스터 수준에서 구성됩니다.  
  
> [!TIP]  
>  WSFC 클러스터 내에서 쿼럼 투표 수를 항상 홀수로 유지하는 것이 좋습니다.  쿼럼 투표를 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 클러스터의 모든 노드에 설치할 필요는 없습니다. 추가 서버가 쿼럼 멤버 역할을 하거나 원격 파일 공유를 결정 기준으로 사용하도록 WSFC 쿼럼 모델을 구성할 수 있습니다.  
>   
>  참조 항목: [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)  
  
### <a name="disaster-recovery-through-forced-quorum"></a>쿼럼 강제를 통해 재해 복구  
 운영 방법과 WSFC 클러스터 구성에 따라 자동 장애 조치(Failover)와 수동 장애 조치(Failover)를 모두 수행할 수 있으며 내결함성이 있는 강력한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 솔루션을 유지 관리할 수 있습니다. 그러나 WSFC 클러스터의 적격한 투표 노드 쿼럼에서 노드 간에 통신할 수 없거나 WSFC 클러스터에서 상태 검증에 실패할 경우 WSFC 클러스터가 오프라인으로 전환될 수 있습니다.  
  
 계획되지 않은 재해나 영구적인 하드웨어 또는 통신 장애로 인해 WSFC 클러스터가 오프라인으로 전환된 경우 수동 관리 작업을 통해 *강제 쿼럼* 을 수행하고 내결함성이 없는 구성에서 활성 클러스터 노드를 다시 온라인으로 전환해야 합니다.  
  
 그런 다음 일련의 단계를 수행하여 WSFC 클러스터를 다시 구성하고, 영향을 받는 데이터베이스 복제본을 복구하고, 새 쿼럼을 다시 설정해야 합니다.  
  
 참조 항목: [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="AlwaysOnWsfcRelationship"></a> SQL Server AlwaysOn 구성 요소와 WSFC의 관계  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn과 WSFC의 기능 및 구성 요소 간에 여러 계층의 관계가 존재합니다.  
  
 AlwaysOn 가용성 그룹이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 호스팅됩니다.  
 논리적 가용성 그룹 수신기 네트워크를 지정하여 주 데이터베이스 또는 보조 데이터베이스에 연결하는 클라이언트 요청은 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)의 적절한 인스턴스 네트워크 이름에 리디렉션됩니다.  
  
 SQL Server 인스턴스는 단일 노드에 활성 상태로 호스팅됩니다.  
 독립 실행형 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스(있는 경우)는 항상 단일 노드에 정적 인스턴스 네트워크 이름으로 존재합니다.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(있는 경우)는 두 개 이상의 가능한 장애 조치(Failover) 노드 중 하나에 단일의 가상 인스턴스 네트워크 이름으로 활성화됩니다.  
  
 노드는 WSFC 클러스터의 멤버입니다.  
 모든 노드에 대한 WSFC 구성 메타데이터와 상태는 각 노드에 저장됩니다. 각 서버는 사용자 또는 시스템 데이터베이스에 대한 비대칭 저장소 또는 공유 저장소(SAN) 볼륨을 제공할 수 있습니다. 각 서버는 하나 이상의 IP 서브넷에 적어도 하나의 실제 네트워크 인터페이스가 있습니다.  
  
 WSFC 서비스는 상태를 모니터링하고 서버 그룹에 대한 구성을 관리합니다.  
 WSFC(Windows Server 장애 조치(Failover) 클러스터) 서비스는 WSFC 구성 메타데이터 및 상태 변경 사항을 클러스터의 모든 노드에 전파합니다. 메타데이터와 상태가 WSFC 쿼럼 감시 원격 파일 공유에 부분적으로 저장될 수 있습니다. 두 개 이상의 활성 노드 또는 미러링 모니터 서버가 WSFC 클러스터 상태에 대한 쿼럼 투표를 구성합니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 레지스트리 키는 WSFC 클러스터의 하위 키입니다.  
 WSFC 클러스터를 삭제한 다음 다시 만들려는 경우 원본 WSFC 클러스터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 사용할 수 있도록 설정한 각 서버 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 사용하지 않도록 설정한 후 다시 사용하도록 설정해야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
 ![SQL Server AlwaysOn 구성 요소 컨텍스트 다이어그램](../../../database-engine/media/alwaysoncomponentcontextdiagram.gif "SQL Server AlwaysOn 구성 요소 컨텍스트 다이어그램")  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [클러스터 쿼럼 NodeWeight 설정 보기](view-cluster-quorum-nodeweight-settings.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 구성](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [쿼럼 없이 WSFC 클러스터 강제 시작](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [Windows Server 기술:  장애 조치 클러스터](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Windows Server 2008 R2의 장애 조치(Failover) 클러스터](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
-   [장애 조치(Failover) 클러스터에 대한 이벤트 및 로그 보기](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 장애 조치(Failover) 클러스터 Cmdlet](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 장애 조치 클러스터 인스턴스 (SQL Server)](always-on-failover-cluster-instances-sql-server.md)   
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](failover-policy-for-failover-cluster-instances.md)   
 [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
