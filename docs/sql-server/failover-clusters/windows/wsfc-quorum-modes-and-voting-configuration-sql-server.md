---
title: WSFC 쿼럼 모드 및 투표 구성(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: ca0d59ef-25f0-4047-9130-e2282d058283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cb85a4e0f209fd5589c55e0392393c61a57e6fe7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835931"
---
# <a name="wsfc-quorum-modes-and-voting-configuration-sql-server"></a>WSFC 쿼럼 모드 및 투표 구성(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 Always On FCI(장애 조치(failover) 클러스터 인스턴스)는 모두 WSFC(Windows Server 장애 조치(failover) 클러스터링)를 플랫폼 기술로 활용합니다.  WSFC는 쿼럼 기반 방식을 사용하여 전반적인 클러스터 상태를 모니터링하고 노드 수준의 내결함성을 극대화합니다. Always On 고가용성 및 재해 복구 솔루션을 디자인하고 운영하고 문제를 해결하기 위해서는 WSFC 쿼럼 모드 및 노드 투표 구성의 기초를 이해하는 것이 매우 중요합니다.  
  
 **항목 내용**  
  
-   [쿼럼을 기준으로 클러스터 상태 검색](#ClusterHealthDetectionbyQuorum)  
  
-   [쿼럼 모드](#QuorumModes)  
  
-   [투표 및 비투표 노드](#VotingandNonVotingNodes)  
  
-   [쿼럼 투표에 권장되는 조정](#RecommendedAdjustmentstoQuorumVoting)  
  
-   [관련 작업](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="ClusterHealthDetectionbyQuorum"></a> 쿼럼을 기준으로 클러스터 상태 검색  
 WSFC 클러스터의 각 노드는 주기적 하트비트 통신에 참여하여 노드의 상태를 다른 노드와 공유합니다. 응답하지 않는 노드는 오류 상태에 있는 것으로 간주됩니다.  
  
 WSFC 클러스터에서 *쿼럼* 노드 집합은 대부분의 투표 노드 및 미러링 모니터입니다. WSFC 클러스터의 전반적인 상태는 주기적 *쿼럼 득표*에 의해 결정됩니다.  쿼럼이 있으면 클러스터가 양호한 상태이고 노드 수준의 내결함성을 제공할 수 있음을 의미합니다.  
  
 쿼럼이 없으면 클러스터 상태가 정상이 아님을 의미합니다.  장애 조치(failover)를 수행하는 주 노드에 대해 정상 상태의 보조 노드를 사용할 수 있는지 확인하려면 전반적인 WSFC 클러스터 상태가 유지 관리되어야 합니다.  쿼럼 득표에 실패하면 WSFC 클러스터가 예방 조치로 오프라인으로 설정됩니다.  이 경우 클러스터에 등록된 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 중지될 수도 있습니다.  
  
> [!IMPORTANT]  
>  쿼럼 실패로 인해 WSFC 클러스터가 오프라인으로 설정된 경우 다시 온라인으로 설정하려면 수동으로 설정해야 합니다.  
>   
>  자세한 내용은 [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)에 의해 결정됩니다.  
  
##  <a name="QuorumModes"></a> 쿼럼 모드  
 *쿼럼 모드* 는 쿼럼 투표에 사용되는 방법을 지시하는 WSFC 클러스터 수준에서 구성됩니다.  장애 조치(Failover) 클러스터 관리자 유틸리티는 클러스터의 노드 수에 따라 쿼럼 모드를 추천합니다.  
  
 다음 쿼럼 모드는 득표 쿼럼을 구성하는 요소를 결정하는 데 사용할 수 있습니다.  
  
-   **노드 과반수.** 클러스터의 상태가 정상이 되려면 클러스터에 있는 투표 노드의 절반 이상이 찬성해야 합니다.  
  
-   **노드 및 파일 공유 과반수.** 노드 과반수 쿼럼 모드와 유사하지만 원격 파일 공유도 투표 미러링 모니터로 구성되며 노드에서 해당 공유로의 연결도 찬성으로 계산된다는 점이 다릅니다.  클러스터의 상태가 정상이 되려면 가능한 투표 수의 절반 이상이 찬성이어야 합니다.  
  
     미러링 모니터 파일 공유는 클러스터의 노드에 있지 않고 클러스터의 모든 노드에 표시되는 것이 좋습니다.  
  
-   **노드 및 디스크 과반수.** 노드 과반수 쿼럼 모드와 유사하지만 공유 디스크 클러스터 리소스도 투표 미러링 모니터로 지정되며 노드에서 해당 공유 디스크로의 연결도 찬성으로 계산된다는 점이 다릅니다.  클러스터의 상태가 정상이 되려면 가능한 투표 수의 절반 이상이 찬성이어야 합니다.  
  
-   **디스크만** 공유 디스크 클러스터 리소스가 미러링 모니터로 지정되며 노드에서 해당 공유 디스크로의 연결이 찬성으로 계산됩니다.  
  
> [!TIP]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대해 비대칭 저장소 구성을 사용할 때는 일반적으로 투표 노드의 수가 홀수인 경우 노드 과반수 쿼럼 모드를 사용하고 투표 노드의 수가 짝수인 경우 노드 및 파일 공유 과반수 쿼럼 모드를 사용해야 합니다.  
  
##  <a name="VotingandNonVotingNodes"></a> 투표 및 비투표 노드  
 기본적으로 WSFC 클러스터의 각 노드는 클러스터 쿼럼의 멤버로 포함됩니다. 각 노드는 전반적인 클러스터 상태를 결정하는 데 하나의 투표권이 있으며 지속적으로 쿼럼을 설정하려고 합니다.  이 시점까지 쿼럼 토론은 클러스터 상태에 대해 투표하는 WSFC 클러스터 노드 집합을 *투표 노드*로 간주합니다.  
  
 WSFC 클러스터에는 전체 클러스터가 정상 상태인지 아닌지를 명확하게 결정할 수 있는 개별 노드가 없습니다.  모든 지정된 시점에서 다른 일부 노드는 각 노드의 큐브 뷰에서 오프라인으로 표시되거나, 장애 조치(failover)가 진행 중인 것으로 표시되거나, 네트워크 통신 오류로 인해 응답하지 않는 것으로 표시될 수 있습니다.  쿼럼 투표의 주요 기능은 WSFC 클러스터의 각 노드 표시 상태가 해당 노드의 실제 상태인지 여부를 결정하는 것입니다.  
  
 '디스크에만 해당'을 제외한 모든 쿼럼 모델의 경우 쿼럼 투표의 효과는 클러스터의 모든 투표 노드 간 안정적인 통신에 따라 달라집니다. 동일한 물리적 서브넷에 있는 노드 간 네트워크 통신은 안정적인 것으로 간주되어야 하며 쿼럼 투표를 신뢰할 수 있어야 합니다.  
  
 그러나 다른 서브넷에 있는 노드가 쿼럼 투표에 응답하지 않는 것으로 표시되지만 실제로 온라인 상태이고 정상 상태이면 이는 서브넷 사이에 네트워크 통신 오류가 발생했기 때문일 확률이 높습니다.  클러스터 토폴로지, 쿼럼 모드 및 장애 조치(Failover) 정책 구성에 따라 해당 네트워크 통신 오류는 사실상 두 개 이상의 투표 노드 집합(또는 하위 집합)을 만들 수 있습니다.  
  
 두 개 이상의 투표 노드 하위 집합이 자체적으로 쿼럼을 설정할 수 있는 경우 이를 *분리 장애(split-brain) 시나리오*라고 합니다.  이러한 시나리오에서는 별도의 쿼럼에 있는 노드가 다른 노드와 다르게 동작하고 충돌할 수 있습니다.  
  
> [!NOTE]  
>  분리 장애(split-brain) 시나리오는 시스템 관리자가 수동으로 쿼럼 작업이나 흔치 않게 장애 조치(Failover)를 강제로 수행하여 쿼럼 노드 집합을 명시적으로 분할하는 경우에만 가능합니다.  
  
 쿼럼 구성을 단순화하고 실행 시간을 늘리려면 노드의 투표가 쿼럼으로 계산되지 않도록 각 노드의 *NodeWeight* 설정을 조정해야 할 수 있습니다.  
  
> [!IMPORTANT]  
>  NodeWeight 설정을 사용하려면 WSFC 클러스터의 모든 서버에 다음 핫픽스를 적용해야 합니다.  
>   
>  [KB2494036](http://support.microsoft.com/kb/2494036): [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
##  <a name="RecommendedAdjustmentstoQuorumVoting"></a> 쿼럼 투표에 권장되는 조정  
 지정된 WSFC 노드의 투표를 사용하거나 사용하지 않도록 설정하는 경우 다음 지침을 따르세요.  
  
-   **기본적으로 투표가 없습니다.** 각 노드에서 명시적인 이유 없이 투표하지 않는 것으로 가정합니다.  
  
-   **모든 주 복제본을 포함합니다.** 가용성 그룹 주 복제본을 호스팅하거나 FCI의 기본 설정 소유자인 각 WSFC 노드에는 투표가 있어야 합니다.  
  
-   **가능한 자동 장애 조치(Failover) 소유자를 포함합니다.** 자동 가용성 그룹 장애 조치(Failover) 또는 FCI 장애 조치(Failover)로 인해 주 복제본을 호스팅할 수 있었던 각 노드에는 투표가 있어야 합니다. WSFC 클러스터에 가용성 그룹이 하나만 있고 가용성 복제본이 독립 실행형 인스턴스에서만 호스팅되는 경우 이 규칙에는 자동 장애 조치(Failover) 대상인 보조 복제본만 포함되어야 합니다.  
  
-   **보조 사이트 노드를 제외합니다.** 일반적으로 보조 재해 복구 사이트에 있는 WSFC 노드에는 투표를 제공하지 마세요.  주 사이트에 아무런 문제가 없는 경우 보조 사이트의 노드가 클러스터를 오프라인으로 전환하는 의사 결정에 영향을 주어서는 안 됩니다.  
  
-   **홀수 투표 수** 필요한 경우 미러링 모니터 파일 공유, 미러링 모니터 노드 또는 미러링 모니터 디스크를 클러스터에 추가하고 쿼럼 투표가 동률이 되지 않도록 쿼럼 모드를 조정합니다.  
  
-   **투표 할당 사후 장애 조치(Post-failover)를 다시 평가합니다.** 정상 상태의 쿼럼을 지원하지 않는 클러스터 구성에 대해 장애 조치(Failover)를 수행해서는 안 됩니다.  
  
> [!IMPORTANT]  
>  WSFC 쿼럼 득표 구성의 유효성을 검사할 때 다음 조건 중 하나가 충족되는 경우 Always On 가용성 그룹 마법사에 경고가 표시됩니다.  
>   
>  -   주 복제본을 호스팅하는 클러스터 노드에 투표가 없습니다.  
> -   보조 복제본이 자동 장애 조치(Failover)용으로 구성되고 해당 클러스터 노드에 투표가 없습니다.  
> -   가용성 복제본을 호스팅하는 모든 클러스터 노드에[KB2494036](http://support.microsoft.com/kb/2494036) 이 설치되어 있지 않습니다. 멀티 사이트 배포에 클러스터 노드에 대한 투표를 추가하거나 제거하려면 이 패치가 필요합니다. 그러나 단일 사이트 배포에서는 주로 요구되지 않으며 경고를 무시해도 괜찮습니다.  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 WSFC 클러스터 구성 및 노드 쿼럼 투표에 관련된 설정을 관리하는 데 도움이 되는 몇 가지 시스템 DMV(동적 관리 뷰)를 표시합니다.  
>   
>  자세한 내용은  [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md), [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md), [sys.dm_os_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md), [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [클러스터 쿼럼 NodeWeight 설정 보기](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 구성](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Always On 가용성 그룹 마법사의 쿼럼 투표 구성 검사](https://blogs.msdn.microsoft.com/sqlalwayson/2012/03/13/quorum-vote-configuration-check-in-alwayson-availability-group-wizards-andy-jing/)  
  
-   [Windows Server 기술: 장애 조치(failover) 클러스터](http://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [장애 조치(Failover) 클러스터 단계별 가이드: 장애 조치 클러스터에서 쿼럼 구성](http://technet.microsoft.com/library/cc770620\(WS.10\).aspx)  
  
## <a name="see-also"></a>참고 항목  
 [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
