---
title: 가용성 복제본 속성 보기(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ', policies'
ms.assetid: 14fed3c4-8ecc-4e1c-931d-a7ec1e9f9e90
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 585c2df207fb3709e3c8fa59e34e65280fdb055e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="view-availability-replica-properties-sql-server"></a>가용성 복제본 속성 보기(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 사용하여 Always On 가용성 그룹에 대한 가용성 복제본 속성을 보는 방법에 대해 설명합니다.  
  
-   **다음을 사용하여 가용성 복제본 속성을 보려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 복제본의 속성을 보고 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 복제본이 속하는 가용성 그룹을 확장하고 **가용성 복제본** 노드를 확장합니다.  
  
4.  속성을 보려는 가용성 복제본을 마우스 오른쪽 단추로 클릭하고 **속성** 명령을 선택합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 **일반** 페이지를 사용하여 이 복제본의 속성을 봅니다. 주 복제본에 연결된 경우 가용성 모드, 장애 조치(failover) 모드, 주 역할에 대한 연결 액세스, 보조 역할에 대한 읽기 액세스(읽기 가능 보조), 세션 제한 시간 값 등의 속성을 변경할 수 있습니다. 자세한 내용은 [가용성 복제본 속성&#40;일반 페이지&#41;](../../../database-engine/availability-groups/windows/availability-replica-properties-general-page.md)를 참조하세요.  

   [!NOTE]
   >클러스터 유형이 none이면 장애 조치 모드를 변경할 수 없습니다.
  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본의 속성 및 상태를 보려면**  
  
 가용성 복제본의 속성 및 상태를 보려면 다음 뷰와 시스템 함수를 사용합니다.  
  
 [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에서 가용성 복제본을 호스팅하는 각 가용성 그룹의 모든 가용성 복제본에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** replica_id, group_id, replica_metadata_id, replica_server_name, owner_sid, endpoint_url, availability_mode, availability_mode_desc, failover_mode, failover_mode_desc, session_timeout, primary_role_allow_connections, primary_role_allow_connections_desc, secondary_role_allow_connections, secondary_role_allow_connections_desc, create_date, modify_date, backup_priority, read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
 WSFC 장애 조치(Failover) 클러스터의 Always On 가용성 그룹에서 각각의 가용성 복제본의 읽기 전용 라우팅 목록에 대한 행을 반환합니다.  
  
 **열 이름:** replica_id, routing_priority, read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 Always On 가용성 그룹의 모든 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** group_name, replica_server_name, node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 모든 Always On 가용성 그룹(복제본 위치에 상관없음)의 각 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** replica_id, replica_server_name, group_id, join_state, join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
 각 로컬 가용성 복제본의 상태를 보여 주는 행과 동일한 가용성 그룹의 각 원격 가용성 복제본에 대한 행을 반환합니다.  
  
 **열 이름:** replica_id, group_id, is_local, role, role_desc, operational_state, operational_state_desc, connected_state, connected_state_desc, recovery_health, recovery_health_desc, synchronization_health, synchronization_health_desc, last_connect_error_number, last_connect_error_description, last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
 현재 복제본이 기본 백업 복제본인지 여부를 결정합니다. 현재 서버 인스턴스의 데이터베이스가 기본 복제본이면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터( **SQLServer:가용성 복제본**  성능 개체)에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 그룹에 대한 자세한 내용을 보려면**  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Always On 가용성 그룹의 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
-   [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
 **가용성 복제본을 관리하려면**  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
 **가용성 데이터베이스를 관리하려면**  
  
-   [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 데이터베이스 일시 중지&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
-   [가용성 데이터베이스 재개&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
-   [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹을 통한 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)   
 [가용성 그룹 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)  
  
  
