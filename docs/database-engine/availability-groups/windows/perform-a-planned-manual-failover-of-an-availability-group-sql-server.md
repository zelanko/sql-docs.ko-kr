---
title: 가용성 그룹의 계획된 수동 장애 조치(failover) 수행
description: 이 항목에서는 Always On 가용성 그룹의 계획된 수동 장애 조치(failover)를 수행하는 방법을 설명합니다.
ms.custom: seodec18
ms.date: 10/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2346c770c5fec742d7c5805f028bd87bebaf71b1
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287207"
---
# <a name="perform-a-planned-manual-failover-of-an-always-on-availability-group-sql-server"></a>Always On 가용성 그룹의 계획된 수동 장애 조치(failover) 수행(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에서 데이터 손실 없이 수동 장애 조치(failover)를 수행하는 방법(*계획된 수동 장애 조치(failover)* )에 대해 설명합니다. 가용성 그룹은 가용성 복제본의 수준에서 장애 조치(Failover)됩니다. AlwaysOn 가용성 그룹 장애 조치(Failover)처럼 계획된 수동 장애 조치는 보조 복제본을 기본 역할로 전환합니다. 동시에 장애 조치(Failover)는 이전 주 복제본을 보조 역할로 전환합니다.  
  
계획된 수동 장애 조치(Failover)는 주 복제본과 대상 보조 복제본이 동기 커밋 모드에서 실행 중이고 현재 동기화된 경우에만 지원됩니다. 계획된 수동 장애 조치(Failover)는 대상 보조 복제본의 가용성 그룹에 조인된 보조 데이터베이스의 모든 데이터를 유지합니다. 이전 주 복제본이 보조 역할로 전환되면 해당 데이터베이스는 보조 데이터베이스가 됩니다. 그런 다음 새 기본 데이터베이스와 동기화되기 시작합니다. 데이터베이스가 모두 SYNCHRONIZED 상태로 전환된 후 새로운 보조 복제본은 향후 계획 수동 장애 조치(failover)의 대상 역할을 수행할 수 있습니다.  
  
> [!NOTE]  
>  보조 복제본과 주 복제본이 모두 자동 장애 조치(Failover) 모드에 대해 구성된 경우 보조 복제본이 동기화되면 자동 장애 조치(Failover)의 대상 역할도 수행할 수 있습니다. 자세한 내용은 [가용성 모드&#40;AlwaysOn 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)를 참조하세요.  
   
##  <a name="BeforeYouBegin"></a> 시작하기 전에 

>[!IMPORTANT]
>클러스터 관리자가 없는 읽기 확장 가용성 그룹을 장애 조치하는 특정 절차가 있습니다. 가용성 그룹에 CLUSTER_TYPE = NONE이 있는 경우 [읽기 확장 가용성 그룹에서 주 복제본 장애 조치](#fail-over-the-primary-replica-on-a-read-scale-availability-group) 아래의 절차를 따르세요.

###  <a name="Restrictions"></a> 제한 사항 
  
- 장애 조치 명령은 대상 복제본에서 명령을 수락하는 즉시 반환하지만 데이터베이스 복구는 가용성 그룹의 장애 조치가 끝난 후 비동기로 수행됩니다. 
- 장애 조치(failover) 시 가용성 그룹 내에서 데이터베이스 간 일관성은 유지되지 않을 수 있습니다. 
  
    > [!NOTE] 
    >  데이터베이스 간 트랜잭션 및 분산 트랜잭션 지원은 SQL Server 및 운영 체제 버전에 따라 달라집니다. 자세한 내용은 [AlwaysOn 가용성 그룹에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션과 데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)을 참조하세요. 
  
###  <a name="Prerequisites"></a> 필수 조건 및 제한 사항 
  
-   대상 보조 복제본과 주 복제본이 모두 동기-커밋 가용성 모드에서 실행 중이어야 합니다. 
-   현재 대상 보조 복제본이 주 복제본과 동기화되어 있어야 합니다. 이 보조 복제본의 모든 보조 데이터베이스는 이미 가용성 그룹에 조인되어 있어야 합니다. 또한 해당 주 데이터베이스와 동기화되어야 합니다(즉, 로컬 보조 데이터베이스가 동기화되어야 함). 
  
    > [!TIP] 
    >  보조 복제본의 장애 조치(Failover) 준비를 확인하려면 [sys.dm_hadr_database_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) 동적 관리 뷰에서 **is_failover_ready** 열을 쿼리합니다. 또는 [AlwaysOn 그룹 대시 보드](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)의 **장애 조치(Failover) 준비** 열을 볼 수 있습니다. 
-   이 태스크는 대상 보조 복제본에서만 지원됩니다. 대상 보조 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다. 
  
###  <a name="Security"></a> 보안 
  
####  <a name="Permissions"></a> 권한 
 가용성 그룹에서는 ALTER AVAILABILITY GROUP 권한이 필요합니다. CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한도 필요합니다. 
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용 
 가용성 그룹을 수동으로 장애 조치하려면 
  
1. 개체 탐색기에서 장애 조치해야 할 가용성 그룹의 보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 서버 트리를 확장합니다. 
  
2. **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다. 
  
3. 장애 조치할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **장애 조치(Failover)** 를 선택합니다. 
  
4. 가용성 그룹 장애 조치 마법사가 시작됩니다. 자세한 내용은 [가용성 그룹 장애 조치(Failover) 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)을 참조하세요. 
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용 
 가용성 그룹을 수동으로 장애 조치하려면 
  
1. 대상 보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 
  
2. 다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다. 
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER 
  
     명령문에서 *group_name*은 가용성 그룹의 이름입니다. 
  
     다음 예에서는 *MyAg* 가용성 그룹을 연결된 보조 복제본으로 수동으로 장애 조치합니다. 
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용 
 가용성 그룹을 수동으로 장애 조치하려면 
  
1. 대상 보조 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다. 
  
2. **Switch-SqlAvailabilityGroup** cmdlet을 사용합니다. 
  
    > [!NOTE] 
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] cmdlet을 사용합니다. 자세한 내용은 [SQL Server PowerShell에 대한 도움말 보기](../../../relational-databases/scripting/get-help-sql-server-powershell.md)를 참조하세요. 
  
     다음 예에서는 지정한 경로를 사용하여 *MyAg* 가용성 그룹을 보조 복제본으로 수동으로 장애 조치합니다. 
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
    SQL Server PowerShell 공급자를 설정하고 사용하려면 
  
    -   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md) 
    -   [SQL Server PowerShell에 대한 도움말 보기](../../../relational-databases/scripting/get-help-sql-server-powershell.md) 

##  <a name="FollowUp"></a> 후속 작업: 가용성 그룹을 수동으로 장애 조치(failover)한 후 
 가용성 그룹의 [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] 외부로 장애 조치한 경우 새로운 가용성 그룹 구성을 반영하도록 Windows Server 장애 조치(Failover) 클러스터링 노드의 쿼럼 투표를 조정합니다. 자세한 내용은 [SQL Server의 WSFC&#40;Windows Server 장애 조치(Failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)을 참조하세요. 

<a name = "ReadScaleOutOnly"><a/>

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>읽기 확장 가용성 그룹에서 주 복제본 장애 조치

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="see-also"></a>참고 항목 

 * [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 
 * [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;AlwaysOn 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 
 * [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) 
  
  
