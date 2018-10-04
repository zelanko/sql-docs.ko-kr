---
title: 가용성 복제본 속성 보기(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- ', policies'
ms.assetid: 14fed3c4-8ecc-4e1c-931d-a7ec1e9f9e90
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a1ca87fc977ee97900be9e821cab4918064c7a44
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097273"
---
# <a name="view-availability-replica-properties-sql-server"></a>가용성 복제본 속성 보기(SQL Server)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 사용하여 AlwaysOn 가용성 그룹에 대한 가용성 복제본 속성을 보는 방법에 대해 설명합니다.  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 복제본의 속성을 보고 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 복제본이 속하는 가용성 그룹을 확장하고 **가용성 복제본** 노드를 확장합니다.  
  
4.  속성을 보려는 가용성 복제본을 마우스 오른쪽 단추로 클릭하고 **속성** 명령을 선택합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 **일반** 페이지를 사용하여 이 복제본의 속성을 봅니다. 주 복제본에 연결된 경우 가용성 모드, 장애 조치(failover) 모드, 주 역할에 대한 연결 액세스, 보조 역할에 대한 읽기 액세스(읽기 가능 보조), 세션 제한 시간 값 등의 속성을 변경할 수 있습니다. 자세한 내용은 [가용성 복제본 속성 &#40;일반 페이지&#41;](availability-replica-properties-general-page.md)합니다.  
  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본의 속성 및 상태를 보려면**  
  
 가용성 복제본의 속성 및 상태를 보려면 다음 뷰와 시스템 함수를 사용합니다.  
  
 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에서 가용성 복제본을 호스팅하는 각 가용성 그룹의 모든 가용성 복제본에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** replica_id, group_id, replica_metadata_id, replica_server_name, owner_sid, endpoint_url, availability_mode, availability_mode_desc, failover_mode, failover_mode_desc, session_timeout, primary_role_allow_connections, primary_role_allow_connections_desc, secondary_role_allow_connections, secondary_role_allow_connections_desc, create_date, modify_date, backup_priority, read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
 WSFC 장애 조치(Failover) 클러스터의 AlwaysOn 가용성 그룹에서 각각의 가용성 복제본의 읽기 전용 라우팅 목록에 대한 행을 반환합니다.  
  
 **열 이름:** replica_id, routing_priority, read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 AlwaysOn 가용성 그룹의 모든 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** group_name, replica_server_name, node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 모든 AlwaysOn 가용성 그룹(복제본 위치에 상관없음)의 각 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** replica_id, replica_server_name, group_id, join_state, join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
 각 로컬 가용성 복제본의 상태를 보여 주는 행과 동일한 가용성 그룹의 각 원격 가용성 복제본에 대한 행을 반환합니다.  
  
 **열 이름:** replica_id, group_id, is_local, role, role_desc, operational_state, operational_state_desc, connected_state, connected_state_desc, recovery_health, recovery_health_desc, synchronization_health, synchronization_health_desc, last_connect_error_number, last_connect_error_description, last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
 현재 복제본이 기본 백업 복제본인지 여부를 결정합니다. 현재 서버 인스턴스의 데이터베이스가 기본 복제본이면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터( **SQLServer:가용성 복제본**  성능 개체)에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 그룹에 대한 자세한 내용을 보려면**  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
-   [AlwaysOn 가용성 그룹의 운영 문제에 대 한 AlwaysOn 정책 &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [가용성 그룹 모니터링&#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
 **가용성 복제본을 관리하려면**  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
 **가용성 데이터베이스를 관리하려면**  
  
-   [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 데이터베이스 일시 중지&#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [가용성 데이터베이스 재개&#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
-   [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 가용성 그룹의 운영 문제에 대 한 AlwaysOn 정책 &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [가용성 그룹 관리&#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)  
  
  
