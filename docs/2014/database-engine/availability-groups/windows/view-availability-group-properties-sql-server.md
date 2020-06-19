---
title: 가용성 그룹 속성 보기(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b7d1f57a9bd29b6c65160ec9a163bc77dfca48b4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936224"
---
# <a name="view-availability-group-properties-sql-server"></a>가용성 그룹 속성 보기(SQL Server)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 사용하여 AlwaysOn 가용성 그룹에 대한 가용성 그룹 속성을 보는 방법에 대해 설명합니다.  
  

  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹의 속성을 보고 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  속성을 보려는 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **속성** 명령을 선택합니다.  
  
4.  **가용성 그룹 속성** 대화 상자에서 **일반** 및 **백업 기본 설정** 페이지를 사용하여 선택한 가용성 그룹의 속성을 보고 필요한 경우 변경합니다. 자세한 내용은 [가용성 그룹 속성 및 새 가용성 그룹&#40;일반 페이지&#41;](availability-group-properties-new-availability-group-general-page.md) 및 [가용성 그룹 속성: 새 가용성 그룹&#40;백업 기본 설정 페이지&#41;](availability-group-properties-new-availability-group-backup-preferences-page.md)을 참조하세요.  
  
     **사용 권한** 페이지를 사용하여 가용성 그룹과 연결된 현재 로그인, 역할 및 명시적 권한을 확인할 수 있습니다. 자세한 내용은 [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md)을 참조하세요.  
  

  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹의 속성 및 상태를 보려면**  
  
 서버 인스턴스가 가용성 복제본을 호스팅하는 가용성 그룹의 속성 및 상태를 쿼리하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에서 가용성 복제본을 호스팅하는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 WSFC 클러스터의 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 가용성 그룹 메타데이터가 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 가용성 복제본이 있는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다.  
  
 **열 이름:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  

  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
 **가용성 그룹에 대한 자세한 내용을 보려면**  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server의 운영 문제에 대 한 AlwaysOn 정책&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [가용성 그룹 모니터링&#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
 **기존 가용성 그룹을 구성하려면**  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹 수신기 제거&#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 제거&#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
  
 **가용성 그룹을 수동으로 장애 조치하려면**  
  
-   [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>참고 항목  
 &#40;&#41;AlwaysOn 가용성 그룹의 [운영 문제에 대 한 transact-sql &#40;AlwaysOn 정책](always-on-policies-for-operational-issues-always-on-availability.md) [SQL Server 가용성 그룹을 모니터링](monitor-availability-groups-transact-sql.md) 하 [는 AlwaysOn 가용성 그룹 &#40;&#41;SQL Server의 개요](overview-of-always-on-availability-groups-sql-server.md)&#41; 
  
  
