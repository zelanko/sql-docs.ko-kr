---
title: 가용성 그룹의 계획된 수동 장애 조치(Failover) 수행(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
caps.latest.revision: 34
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 2573df633ca63b480869831b2f5edc0993ad4a56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082540"
---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>가용성 그룹의 계획된 수동 장애 조치(Failover) 수행(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에서 데이터 손실 없이 수동 장애 조치(failover)를 수행하는 방법(*계획된 수동 장애 조치(failover)*)에 대해 설명합니다. 가용성 그룹은 가용성 복제본의 수준에서 장애 조치(Failover)됩니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 장애 조치(failover)와 같은 계획 수동 장애 조치(failover)를 수행하면 보조 복제본이 주 역할로 전환되며 동시에 이전 주 복제본은 보조 역할로 전환됩니다.  
  
 주 복제본과 대상 보조 복제본이 동기-커밋 모드에서 실행 중이고 현재 동기화된 경우에만 지원되는 계획 수동 장애 조치(failover)는 대상 보조 복제본의 가용성 그룹에 조인되는 보조 데이터베이스에서 모든 데이터를 보존합니다. 이전 주 복제본이 보조 역할로 전환되면 해당 데이터베이스는 보조 데이터베이스가 되고 새로운 주 데이터베이스와 동기화됩니다. 데이터베이스가 모두 SYNCHRONIZED 상태로 전환된 후 새로운 보조 복제본은 향후 계획 수동 장애 조치(failover)의 대상 역할을 수행할 수 있습니다.  
  
> [!NOTE]  
>  보조 복제본과 주 복제본이 모두 자동 장애 조치(failover) 모드에 대해 구성된 경우 보조 복제본이 동기화되면 자동 장애 조치(failover)의 대상 역할도 수행할 수 있습니다. 자세한 내용은 [가용성 모드&#40;AlwaysOn 가용성 그룹&#41;](availability-modes-always-on-availability-groups.md)를 참조하세요.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   장애 조치 명령은 대상 복제본에서 명령을 수락하는 즉시 반환하지만 데이터베이스 복구는 가용성 그룹의 장애 조치가 끝난 후 비동기로 수행됩니다.  
  
-   장애 조치 시 가용성 그룹 내에서 데이터베이스 간 일관성은 유지되지 않습니다.  
  
    > [!NOTE]  
    >  데이터베이스 간 트랜잭션 또는 분산 트랜잭션은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 지원되지 않습니다. 자세한 내용은 [데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션&#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md)을 참조하세요.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항 및 제한 사항  
  
-   대상 보조 복제본과 주 복제본이 모두 동기-커밋 가용성 모드에서 실행 중이어야 합니다.  
  
-   대상 보조 복제본이 주 복제본과 현재 동기화되어 있어야 합니다. 이렇게 하려면 보조 복제본에 있는 모든 보조 데이터베이스가 가용성 그룹에 조인되어 있어야 하며 해당 주 데이터베이스와 동기화되어 있어야 합니다. 즉, 로컬 보조 데이터베이스가 SYNCHRONIZED 상태여야 합니다.  
  
    > [!TIP]  
    >  보조 복제본의 장애 조치(failover) 준비를 확인하려면 [sys.dm_hadr_database_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql) 동적 관리 뷰에서 **is_failover_ready** 열을 쿼리하거나 [AlwaysOn 그룹 대시보드](use-the-always-on-dashboard-sql-server-management-studio.md)에서 **장애 조치(Failover) 준비** 열을 확인합니다.  
  
-   이 태스크는 대상 보조 복제본에서만 지원됩니다. 대상 보조 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹을 수동으로 장애 조치하려면**  
  
1.  개체 탐색기에서 장애 조치해야 할 가용성 그룹의 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  장애 조치할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **장애 조치(Failover)** 명령을 선택합니다.  
  
4.  그러면 가용성 그룹 장애 조치(failover) 마법사가 시작됩니다. 자세한 내용은 [가용성 그룹 장애 조치(failover) 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹을 수동으로 장애 조치하려면**  
  
1.  대상 보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     여기서 *group_name* 은 가용성 그룹의 이름입니다.  
  
     다음 예에서는 *MyAg* 가용성 그룹을 연결된 보조 복제본으로 수동으로 장애 조치합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹을 수동으로 장애 조치하려면**  
  
1.  디렉터리를 변경 (`cd`) 대상 보조 복제본을 호스팅하는 서버 인스턴스에 있습니다.  
  
2.  사용 하 여 `Switch-SqlAvailabilityGroup` cmdlet.  
  
    > [!NOTE]  
    >  Cmdlet의 구문을 보려면에서 사용 하 여는 `Get-Help` cmdlet에는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
     다음 예에서는 지정한 경로를 사용하여 *MyAg* 가용성 그룹을 보조 복제본으로 수동으로 장애 조치합니다.  
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 그룹을 수동으로 장애 조치(failover)한 후  
 가용성 그룹의 [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] 외부로 장애 조치한 경우 새로운 가용성 그룹 구성을 반영하도록 WSFC 노드의 쿼럼 투표를 조정합니다. 자세한 내용은 [SQL Server의 WSFC&#40;Windows Server 장애 조치(Failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치 및 장애 조치 모드 &#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
  
