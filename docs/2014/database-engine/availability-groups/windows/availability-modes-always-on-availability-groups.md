---
title: 가용성 모드(Always On 가용성 그룹) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], asynchronous commit
- synchronous-commit availability mode
- Availability Groups [SQL Server], synchronous commit
- asynchronous-commit availability mode
- Availability Groups [SQL Server], availability modes
ms.assetid: 10e7bac7-4121-48c2-be01-10083a8c65af
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 924708dabd2cfe4fa94eb6f726e29613d6917d86
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172251"
---
# <a name="availability-modes-always-on-availability-groups"></a>가용성 모드(Always On 가용성 그룹)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 *가용성 모드* 는 지정된 가용성 복제본을 동기 커밋 모드에서 실행할 수 있는지 여부를 결정하는 복제본 속성입니다. 각 가용성 복제본에 대해 가용성 모드를 동기 커밋 모드나 비동기 커밋 모드로 구성해야 합니다.  주 복제본이 *비동기 커밋 모드*로 구성된 경우 주 복제본에서는 보조 복제본이 들어오는 트랜잭션 로그 레코드를 디스크에 기록( *로그 확정*)할 때까지 기다리지 않습니다. 특정 보조 복제본이 비동기 커밋 모드로 구성된 경우 주 복제본은 해당 보조 복제본이 로그를 확정할 때까지 기다리지 않습니다. 주 복제본과 특정 보조 복제본이 모두 *동기 커밋 모드*로 구성된 경우에는 보조 복제본이 주 복제본의 *세션 제한 시간*내에 주 복제본을 ping하는 데 실패하지 않은 한 주 복제본은 보조 복제본이 로그를 확정했음을 확인할 때까지 기다립니다.  
  
> [!NOTE]  
>  보조 복제본이 주 복제본의 세션 제한 시간을 초과할 경우 주 복제본은 일시적으로 해당 보조 복제본에 대해 비동기 커밋 모드로 전환합니다. 보조 복제본이 주 복제본에 다시 연결할 때는 동기 커밋 모드가 다시 시작됩니다.  
  
  
##  <a name="SupportedAvModes"></a> 지원되는 가용성 모드  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 아래 설명되어 있는 비동기-커밋 모드 및 동기-커밋 모드라는 두 가지 가용성 모드를 지원합니다.  
  
-   *비동기-커밋 모드* 는 여러 가용성 복제본이 상당한 거리를 두고 분산되어 있는 경우에 적합한 재해 복구 솔루션입니다. 모든 보조 복제본이 비동기-커밋 모드로 실행될 경우 주 복제본은 보조 복제본이 로그를 확정할 때까지 기다리지 않습니다. 대신 주 복제본은 로그 레코드를 로컬 로그 파일에 쓴 후 곧바로 트랜잭션 확인을 클라이언트로 보냅니다. 주 복제본은 비동기-커밋 모드로 구성된 보조 복제본에 비해 최소한의 트랜잭션 대기 시간으로 실행됩니다.  현재 주 복제본이 비동기 커밋 가용성 모드로 구성되어 있는 경우 주 복제본은 보조 복제본 각각의 가용성 모드 설정에 관계없이 모든 보조 복제본에 대해 비동기로 트랜잭션을 커밋합니다.  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [비동기-커밋 가용성 모드](#AsyncCommitAvMode)를 참조하세요.  
  
-   *동기-커밋 모드* 는 트랜잭션 대기 시간이 증가하더라도 성능에 비해 고가용성을 강조합니다. 동기-커밋 모드에서는 보조 복제본이 로그를 디스크에 확정할 때까지 트랜잭션이 트랜잭션 확정을 클라이언트에 보내기를 기다립니다. 보조 데이터베이스에서 데이터 동기화가 시작되면 보조 복제본은 해당 주 데이터베이스로부터 들어오는 로그 레코드를 적용하기 시작합니다. 모든 로그 레코드가 확정되면 보조 데이터베이스가 곧바로 SYNCHRONIZED 상태로 전환됩니다. 이후부터 모든 새 트랜잭션은 보조 복제본에 의해 확정된 후 로그 레코드가 로컬 로그 파일에 작성됩니다. 지정된 보조 복제본의 모든 보조 데이터베이스가 동기화된 경우 동기-커밋 모드에서는 수동 장애 조치(Failover)와 필요한 경우 자동 장애 조치를 지원합니다.  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [동기-커밋 가용성 모드](#SyncCommitAvMode)를 참조하세요.  
  
 다음 그림에서는 5개의 가용성 복제본이 있는 가용성 그룹을 보여 줍니다. 주 복제본 및 하나의 보조 복제본이 자동 장애 조치를 사용하여 동기-커밋 모드에 대해 구성됩니다. 또한 다른 보조 복제본이 계획된 수동 장애 조치만 사용하여 동기-커밋 모드에 대해 구성되고, 두 개의 보조 복제본이 비동기-커밋 모드에 대해 구성됩니다(강제 수동 장애 조치만 지원함, 일반적으로 *강제 장애 조치 작업*이라고 함).  
  
 ![복제본의 가용성 및 장애 조치 모드](../../media/aoag-availabilityandfailovermodes.gif "복제본의 가용성 및 장애 조치 모드")  
  
 두 가용성 복제본 간의 동기화와 장애 조치(failover) 동작은 두 복제본의 가용성 모드에 따라 다릅니다. 예를 들어 발생할 동기 커밋의 경우 동기 커밋에 대해 현재 주 복제본 및 보조 복제본을 모두 구성해야 합니다. 이와 마찬가지로 발생할 자동 장애 조치(Failover)의 경우 자동 장애 조치(Failover)에 대해 두 복제본을 모두 구성해야 합니다. 따라서 위에서 그림에 표시된 배포 시나리오 동작은 다음 표로 요약될 수 있으며 이 표에서는 각 잠재 주 복제본과 함께 동작을 설명합니다.  
  
|현재 주 복제본|자동 장애 조치(Failover) 대상|동기-커밋 모드 다음에 대한 동작|비동기-커밋 모드 다음에 대한 동작|자동 장애 조치(Failover) 가능 여부|  
|-----------------------------|--------------------------------|--------------------------------------------|---------------------------------------------|---------------------------------|  
|01|02|02 및 03|04|예|  
|02|01|01 및 03|04|예|  
|03||01 및 02|04|아니요|  
|04|||01, 02 및 03|아니요|  
  
 일반적으로 노드 04는 비동기 커밋 복제본으로서 재해 복구 사이트에 배포됩니다. 노드 04에 대한 장애 조치(Failover)를 수행한 후 노드 01, 02, 03은 비동기 커밋 모드로 유지된다는 점에서 두 사이트 간의 긴 네트워크 지연 시간으로 인해 가용성 그룹의 잠재적 성능이 저하되는 것을 방지할 수 있습니다.  
  
##  <a name="AsyncCommitAvMode"></a> Asynchronous-Commit Availability Mode  
 *비동기-커밋 모드*에서는 보조 복제본이 주 복제본과 동기화되지 않습니다. 지정된 보조 데이터베이스가 해당 주 데이터베이스를 따라 잡더라도 보조 데이터베이스는 언제든지 뒤쳐질 수 있습니다. 비동기 커밋 모드는 주 복제본과 보조 복제본이 상당한 거리를 두고 떨어져 있으며 사소한 오류로 인해 주 복제본이 영향을 받지 않도록 하려는 경우나 동기화된 데이터 보호보다 성능을 중요시하는 경우의 재해 복구 시나리오에서 유용합니다. 또한 주 복제본이 보조 복제본의 승인을 기다리지 않기 때문에 보조 복제본의 문제가 주 복제본에 영향을 주지 않습니다.  
  
 비동기 커밋 보조 복제본은 주 복제본으로부터 받은 로그 레코드를 따라잡으려고 합니다. 그러나 비동기 커밋 보조 데이터베이스는 항상 동기화되지 않은 상태로 있으며 해당 주 데이터베이스보다 뒤쳐질 수 있습니다. 일반적으로 비동기 커밋 보조 데이터베이스와 해당 주 데이터베이스 간의 시간차는 작은 편입니다. 그러나 보조 복제본을 호스팅하는 서버가 과부화되거나 네트워크 속도가 느린 경우에는 이 시간차가 상당히 커질 수 있습니다.  
  
 비동기-커밋 모드에서 지원되는 유일한 형태의 장애 조치는 강제 장애 조치(데이터가 손실될 수 있음)입니다. 강제 장애 조치는 현재 주 복제본을 상당 기간 사용할 수 없으며 데이터 손실의 위험보다 주 데이터베이스 가용성이 더 중요한 경우에만 최후의 수단으로 사용해야 합니다. 장애 조치(Failover) 대상은 역할이 SECONDARY 또는 RESOLVING 상태인 복제본이어야 합니다. 이때 장애 조치(Failover) 대상은 주 역할로 전환되고 해당 데이터베이스 복사본이 주 데이터베이스가 됩니다. 나머지 보조 데이터베이스(사용 가능하게 된 경우)는 이전 주 데이터베이스와 함께 사용자가 수동으로 개별 데이터베이스를 다시 시작할 때까지 일시 중지됩니다. 비동기 커밋 모드에서는 원래 주 복제본이 이전의 보조 복제본으로 아직 보내지지 않은 트랜잭션 로그가 손실됩니다. 즉, 최근에 커밋된 트랜잭션이 새로운 주 데이터베이스의 일부 또는 모두에 없을 수도 있습니다. 강제 장애 조치 작동 방법 및 사용에 대 한 모범 사례에 자세한 내용은 참조 하십시오. [장애 조치 및 장애 조치 모드 &#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)합니다.  
  
##  <a name="SyncCommitAvMode"></a> Synchronous-Commit Availability Mode  
 동기-커밋 가용성 모드(*동기-커밋 모드*)에서는 보조 데이터베이스가 가용성 그룹에 조인한 후에 해당 주 데이터베이스를 따라잡고 SYNCHRONIZED 상태로 전환됩니다. 보조 데이터베이스는 데이터 동기화가 계속되는 한 SYNCHRONIZED로 유지됩니다. 그러면 지정된 주 데이터베이스에서 커밋된 모든 트랜잭션이 해당 보조 데이터베이스에서도 커밋됩니다. 지정된 보조 복제본의 모든 보조 데이터베이스가 동기화되면 보조 복제본 전체의 동기화 상태가 HEALTHY가 됩니다.  
  
  
###  <a name="DisruptSync"></a> 데이터 동기화를 방해하는 요인  
 모든 데이터베이스가 동기화되면 보조 복제본이 HEALTHY 상태가 됩니다. 다음 중 하나가 발생하지 않는 한 동기화된 보조 복제본은 정상으로 유지됩니다.  
  
-   네트워크/컴퓨터 지연 또는 결함으로 인해 보조 복제본과 주 복제본 간의 세션 제한 시간이 만료됩니다.  
  
    > [!NOTE]  
    >  가용성 복제본의 세션-시간 속성에 대 한 정보를 참조 하십시오. [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)합니다.  
  
-   보조 복제본에서 보조 데이터베이스를 일시 중지합니다. 보조 복제본이 더 이상 동기화되지 않고 해당 동기화 상태가 NOT_HEALTHY로 표시됩니다. 일시 중지된 보조 데이터베이스가 다시 시작되고 다시 동기화되거나 가용성 그룹에서 제거될 때까지 해당 보조 복제본은 다시 정상이 될 수 없습니다.  
  
-   가용성 그룹에 주 데이터베이스를 추가합니다. 이전에 동기화된 보조 복제본은 NOT_HEALTHY 동기화 상태가 됩니다. 이 상태는 하나 이상의 데이터베이스가 NOT SYNCHRONIZING 동기화 상태임을 나타냅니다. 지정된 보조 복제본은 복제본에서 해당 보조 데이터베이스가 준비되고, 가용성 그룹에 조인하고, 새로운 주 데이터베이스와 동기화될 때까지 다시 HEALTHY가 될 수 없습니다.  
  
-   주 복제본 또는 보조 복제본을 동기-커밋 가용성 모드로 변경합니다. 보조 복제본은 동기-커밋 모드로 변경된 후 데이터 동기화가 계속되는 한 HEALTHY 동기화 상태로 유지됩니다. 그러나 주 복제본만 동기-커밋 모드로 변경되는 경우에는 동기-커밋 보조 복제본이 PARTIALLY_HEALTHY 동기화 상태가 됩니다. 이 상태는 하나 이상의 데이터베이스가 SYNCHRONIZING 동기화 상태에 있지만 어떤 데이터베이스도 NOT SYNCHRONIZING 상태에 있지 않음을 나타냅니다.  
  
-   보조 복제본을 동기-커밋 가용성 모드로 변경합니다. 이렇게 하면 모든 해당 데이터베이스가 SYNCHRONIZED 동기화 상태가 될 때까지 보조 복제본이 PARTIALLY_HEALTHY 동기화 상태로 표시됩니다.  
  
> [!TIP]  
>  가용성 그룹, 가용성 복제본 또는 가용성 데이터베이스의 동기화 상태를 보려면 각각 **sys.dm_hadr_availability_group_states** , **sys.dm_hadr_availability_replica_states** 또는 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)의 [synchronization_health](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)또는 [synchronization_health_desc](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)열을 쿼리합니다.  
  
###  <a name="HowSyncWorks"></a> 보조 복제본에서 동기화가 작동하는 방법  
 동기-커밋 모드에서는 보조 복제본을 가용성 그룹에 조인하고 주 복제본과의 세션을 설정하고 나면 보조 복제본은 들어오는 로그 레코드를 디스크에 기록하고(*로그 확정*) 확인 메시지를 주 복제본으로 보냅니다. 보조 데이터베이스의 확정된 로그가 주 데이터베이스의 로그 끝을 따라잡으면 보조 데이터베이스의 상태가 SYNCHRONIZED로 설정됩니다. 동기화에 필요한 시간은 세션을 시작할 때 보조 데이터베이스와 주 데이터베이스 간의 격차(처음에 주 복제본으로부터 받은 로그 레코드 수로 측정), 주 데이터베이스의 작업 로드 및 보조 복제본을 호스팅하는 서버 인스턴스 컴퓨터의 속도에 따라 달라집니다.  
  
 동기화 작업은 다음 방식으로 유지 관리됩니다.  
  
1.  클라이언트로부터 트랜잭션을 받자마자 주 복제본은 트랜잭션에 대한 로그를 트랜잭션 로그에 쓰고 이와 동시에 로그 레코드를 보조 복제본으로 보냅니다.  
  
2.  주 데이터베이스의 트랜잭션 로그에 로그 레코드가 작성되면 현재 시점에서 해당 로그를 받지 못한 보조 데이터베이스로의 장애 조치가 있을 경우에만 트랜잭션을 실행 취소할 수 있습니다. 주 복제본은 동기-커밋 보조 복제본의 확인을 기다립니다.  
  
3.  보조 복제본은 로그를 확정하고 주 복제본으로 승인을 반환합니다.  
  
4.  보조 복제본의 확인을 받자마자 주 복제본은 커밋 처리를 마치고 확인 메시지를 클라이언트로 보냅니다.  
  
    > [!NOTE]  
    >  동기-커밋 보조 복제본이 로그를 확정했음을 확인하지 않은 상태에서 제한 시간이 만료되면 주 복제본이 해당 보조 복제본을 실패한 것으로 표시합니다. 보조 복제본의 연결 상태가 DISCONNECTED로 변경되고, 주 복제본이 보조 복제본의 확인을 더 이상 기다리지 않습니다. 이 동작은 실패한 동기-커밋 보조 복제본으로 인해 주 복제본에서 트랜잭션 로그가 확정되지 않는 것을 방지합니다.  
  
 동기-커밋 모드에서는 트랜잭션 대기 시간이 다소 늘어나더라도 두 위치의 데이터가 동기화되도록 하여 데이터를 보호합니다.  
  
### <a name="synchronous-commit-mode-with-only-manual-failover"></a>수동 장애 조치만 사용하는 동기-커밋 모드  
 이들 복제본이 연결되어 있으며 데이터베이스가 동기화된 경우 수동 장애 조치가 지원됩니다. 보조 복제본의 작동이 중단되어도 주 복제본은 영향을 받지 않습니다. SYNCHRONIZED 상태의 복제본이 없으면 주 복제본이 표시된 상태로, 즉 데이터를 보조 복제본에 보내지 않고 실행됩니다. 주 복제본이 손실되면 보조 복제본이 RESOLVING 상태가 되지만 데이터베이스 소유자가 보조 복제본으로의 강제 장애 조치를 수행할 수 있으며 이 경우 데이터가 손실될 수 있습니다. 자세한 내용은 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
###  <a name="SyncCommitWithAuto"></a> 자동 장애 조치를 사용하는 동기-커밋 모드  
 자동 장애 조치를 사용하면 주 복제본이 손실되어도 데이터베이스를 신속하게 다시 사용할 수 있으므로 고가용성이 보장됩니다. 자동 장애 조치에 대해 가용성 그룹을 구성하려면 현재 주 복제본과 하나의 보조 복제본을 모두 자동 장애 조치를 사용하는 동기-커밋 모드로 설정해야 합니다.  
  
 또한 특정 시점에 자동 장애 조치가 가능하려면 이 보조 복제본을 주 복제본과 동기화하고, 즉 보조 데이터베이스를 모두 동기화하고 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 쿼럼이 있어야 합니다. 위의 조건에서 주 복제본을 사용할 수 없게 되면 자동 장애 조치가 수행됩니다. 보조 복제본이 주 복제본의 역할로 전환하여 해당 데이터베이스를 주 데이터베이스로 제공합니다. 자세한 내용은의 "자동 장애 조치" 섹션을 참조 하십시오.는 [장애 조치 및 장애 조치 모드 &#40;AlwaysOn 가용성 그룹&#41; ](failover-and-failover-modes-always-on-availability-groups.md) 항목입니다.  
  
> [!NOTE]  
>  WSFC 쿼럼 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 모드와 장애 조치(failover) 모드를 변경하려면**  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
 **쿼럼 투표를 조정하려면**  
  
-   [클러스터 쿼럼 NodeWeight 설정 보기](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 구성](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
-   [쿼럼 없이 WSFC 클러스터 강제 시작](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
 **수동 장애 조치(failover)를 수행하려면**  
  
-   [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 장애 조치(Failover) 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
 **가용성 그룹, 가용성 복제본 및 데이터베이스 상태를 보려면**  
  
-   [sys.dm_hadr_availability_group_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](http://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치 및 장애 조치 모드 &#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
