---
title: 가용성 그룹 모니터링(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- dynamic management views [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], databases
- catalog views [SQL Server], AlwaysOn Availability Groups
ms.assetid: 881a34de-8461-4811-8c62-322bf7226bed
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b97d62e7dede1cbbe4229f824407946f2fe43ba
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460980"
---
# <a name="monitor-availability-groups-transact-sql"></a>가용성 그룹 모니터링(Transact-SQL)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하여 가용성 그룹, 복제본 및 연결된 데이터베이스를 모니터링할 수 있도록 여러 카탈로그 및 동적 관리 뷰와 서버 속성을 제공합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 문을 사용하여 뷰를 통해 가용성 그룹과 해당 복제본 및 데이터베이스를 모니터링할 수 있습니다. 지정된 가용성 그룹에 대해 반환되는 정보는 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 주 복제본을 호스팅 중인지 아니면 보조 복제본을 호스팅 중인지에 따라 다릅니다.  
  
> [!TIP]  
>  ID 열로 뷰를 조인하여 한 번의 쿼리로 여러 뷰에서 정보를 반환할 수 있습니다.  
  
 
  
##  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 카탈로그 뷰를 사용하려면 서버 인스턴스에 대한 모든 정의 보기 권한이 필요합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 동적 관리 뷰를 사용하려면 서버에 대한 서버 상태 보기 권한이 필요합니다.  
  
##  <a name="AoAgFeatureOnSI"></a> 서버 인스턴스에서 AlwaysOn 가용성 그룹 기능을 모니터링합니다.  
 서버 인스턴스의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 모니터링하려면 다음 기본 제공 함수를 사용합니다.  
  
 [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) 함수  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용할지 여부와 사용할 경우 서버 인스턴스에서 시작되었는지 여부에 대한 서버 속성 정보를 반환합니다.  
  
 **열 이름:** IsHadrEnabled, HadrManagerStatus  
  
##  <a name="WSFC"></a> WSFC 클러스터의 가용성 그룹 모니터링  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 사용되는 로컬 서버 인스턴스를 호스팅하는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하여 SQL Server 인스턴스를 호스트하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 WSFC 쿼럼이 있는 경우 **sys.dm_hadr_cluster** 는 쿼럼에 대한 클러스터 이름과 정보를 표시하는 행을 반환합니다. WSFC 노드에 쿼럼이 없으면 반환되는 행이 없습니다.  
  
 **열 이름:** cluster_name, quorum_type, quorum_type_desc, quorum_state, quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
 SQL Server의 로컬 AlwaysOn 사용 인스턴스를 호스팅하는 WSFC 노드에 WSFC 쿼럼이 있는 경우 쿼럼을 구성하는 각 멤버에 대한 행과 각 멤버의 상태를 반환합니다.  
  
 **열 이름:** member_name, member_type, member_type_desc, member_state, member_state_desc, number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
 가용성 그룹의 서브넷 구성에 참여하는 모든 멤버에 대해 하나의 행을 반환합니다. 이 동적 관리 뷰를 사용하여 각 가용성 복제본에 대해 구성된 네트워크 가상 IP의 유효성을 검사할 수 있습니다.  
  
 **열 이름:** member_name, network_subnet_ip, network_subnet_ipv4_mask, network_subnet_prefix_length, is_public, is_ipv4  
  
 **기본 키:** member_name + network_subnet_IP + network_subnet_prefix_length  
  
 [sys.dm_hadr_instance_node_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
 AlwaysOn 가용성 그룹에 조인된 가용성 복제본을 호스팅하는 SQL Server의 모든 인스턴스에 대해 서버 인스턴스를 호스팅하는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드의 이름을 반환합니다. 이러한 동적 관리 뷰는 다음과 같이 사용됩니다.  
  
-   이 동적 관리 뷰는 동일한 WSFC 노드에서 호스팅되는 여러 가용성 복제본이 포함된 가용성 그룹을 검색하는 데 유용합니다. 이러한 구성은 가용성 그룹이 잘못 구성된 경우 FCI 장애 조치(failover) 이후 발생 가능한 지원되지 않는 구성입니다.  
  
-   여러 SQL Server 인스턴스가 동일한 WSFC 노드에 호스팅되는 경우 리소스 DLL이 이 동적 관리 뷰를 사용하여 연결할 SQL Server의 인스턴스를 확인합니다.  
  
 **열 이름:** ag_resource_id, instance_name, node_name  
  
 [sys.dm_hadr_name_id_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
 현재 SQL Server 인스턴스가 세 가지 고유한 ID인 가용성 그룹 ID, WSFC 리소스 ID 및 WSFC 그룹 ID에 조인된 AlwaysOn 가용성 그룹의 매핑을 보여 줍니다. 이 매핑의 목적은 WSFC 리소스/그룹의 이름이 바뀐 시나리오를 처리하기 위한 것입니다.  
  
 **열 이름:** ag_name, ag_id, ag_resource_id, ag_group_id  
  
> [!NOTE]  
>  또한 나중에 이 항목에 있는 [가용성 복제본 모니터링](#AvReplicas) 섹션에서 **sys.dm_hadr_availability_replica_cluster_nodes** 및 **sys.dm_hadr_availability_replica_cluster_states**를 참조하고 [가용성 데이터베이스 모니터링](#AvDbs) 섹션에서 **sys.availability_databases_cluster** 및 **sys.dm_hadr_database_replica_cluster_states**를 참조하세요.  
  
 WSFC에 대 한 정보를 클러스터에 대 한 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [Windows Server 장애 조치 클러스터링 &#40;WSFC&#41; SQL Server를 사용 하 여](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md) 하 고 [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL 서버&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)합니다.  
  
##  <a name="AvGroups"></a> Monitoring Availability Groups  
 서버 인스턴스가 가용성 복제본을 호스팅하는 가용성 그룹을 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에서 가용성 복제본을 호스팅하는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 WSFC 클러스터의 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 가용성 그룹 메타데이터가 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 가용성 복제본이 있는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다.  
  
 **열 이름:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="AvReplicas"></a> sys.dm_hadr_availability_replica_cluster_states  
 가용성 복제본을 모니터링하려면 다음 뷰와 시스템 함수를 사용합니다.  
  
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
 현재 복제본이 기본 백업 복제본인지 여부를 결정합니다.  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터( **SQLServer:가용성 복제본**  성능 개체)에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
##  <a name="AvDbs"></a> sys.dm_hadr_database_replica_cluster_states  
 가용성 데이터베이스를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [가용성 데이터베이스 모니터링](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
 로컬 복사본 데이터베이스가 가용성 그룹에 조인되어 있는지 여부에 상관없이 클러스터의 모든 AlwaysOn 가용성 그룹의 일부인 SQL Server 인스턴스의 데이터베이스별로 하나의 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스가 가용성 그룹에 추가되면 주 데이터베이스가 그룹에 자동으로 조인됩니다. 보조 데이터베이스를 가용성 그룹에 조인하려면 각 보조 복제본에서 보조 데이터베이스를 준비해야 합니다.  
  
 **열 이름:** group_id, group_database_id, database_name  
  
 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 각 데이터베이스당 한 개의 행을 포함합니다. 데이터베이스가 가용성 복제본에 속하는 경우 해당 데이터베이스의 행에 복제본의 GUID와 가용성 그룹 내의 데이터베이스에 대한 고유 식별자가 표시됩니다.  
  
 **[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 열 이름:** replica_id, group_database_id  
  
 [sys.dm_hadr_auto_page_repair](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
 서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다. 이 뷰에는 지정된 주 데이터베이스 또는 보조 데이터베이스의 최신 자동 페이지 복구 시도에 대한 행이 포함됩니다(데이터베이스당 최대 100개 행). 데이터베이스가 최대값에 도달하는 즉시 다음 자동 페이지 복구 시도에 대한 행이 기존 항목 중 하나를 대체합니다.  
  
 **열 이름:** database_id, file_id, page_id, error_type, page_status, modification_time  
  
 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스가 가용성 복제본을 호스팅 중인 모든 가용성 그룹에 참여하는 각 데이터베이스에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** database_id, group_id, replica_id, group_database_id, is_local, synchronization_state, synchronization_state_desc, is_commit_participant, synchronization_health, synchronization_health_desc, database_state, database_state_desc, is_suspended, suspend_reason, suspend_reason_desc, recovery_lsn, truncation_lsn, last_sent_lsn, last_sent_time, last_received_lsn, last_received_time, last_hardened_lsn, last_hardened_time, last_redone_lsn, last_redone_time, log_send_queue_size, log_send_rate, redo_queue_size, redo_rate, filestream_send_rate, end_of_log_lsn, last_commit_lsn, last_commit_time, low_water_mark_for_ghosts  
  
 [sys.availability_databases_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 각 가용성 그룹에 있는 가용성 데이터베이스의 상태를 파악하는 데 필요한 정보가 들어 있는 행을 반환합니다. 이 동적 관리 뷰는 장애 조치(failover)를 계획 또는 이에 응답하거나 지정된 주 데이터베이스의 로그 잘림을 보유 중인 가용성 그룹의 보조 복제본을 검색하는 데 유용합니다.  
  
 **열 이름:** replica_id, group_database_id, database_name, is_failover_ready, is_pending_secondary_suspend, is_database_joined, recovery_lsn, truncation_lsn  
  
> [!NOTE]  
>  주 복제본 위치는 가용성 그룹의 권한이 있는 원본입니다.  
  
> [!NOTE]  
>  가용성 데이터베이스의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 성능 카운터( **SQLServer:Database Replica** 성능 개체)에 대한 자세한 내용은 [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)을 참조하세요. 또한 가용성 데이터베이스에서 트랜잭션 로그 작업을 모니터링하려면 **SQLServer:Databases** 성능 개체의 **Log Flush Write Time (ms)**, **Log Flushes/sec**, **Log Pool Cache Misses/sec**, **Log Pool Disk Reads/sec**, **Log Pool Requests/sec**카운터를 사용합니다. 자세한 내용은 [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)을 참조하세요.  
  
##  <a name="AGlisteners"></a> 가용성 그룹 수신기 모니터링  
 WSFC 클러스터의 서브넷에서 가용성 그룹 수신기를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 가용성 그룹 수신기에 대해 현재 온라인인 규칙에 부합하는 모든 가상 IP 주소에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 지정된 가용성 그룹에 대해 0개의 행을 반환하여 가용성 그룹에 연결된 네트워크 이름이 없음을 나타내거나 WSFC 클러스터의 각 가용성 그룹 수신기 구성에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 각 TCP 수신기에 대한 동적 상태 정보를 포함하는 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
 **기본 키:** listener_id  
  
 가용성 그룹 수신기에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **AlwaysOn 가용성 그룹 모니터링 태스크:**  
  
-   [개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
 **AlwaysOn 가용성 그룹 모니터링 참조 (TRANSACT-SQL):**  
  
-   [SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
-   [sys.availability_group_listener_ip_addresses&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
  
-   [sys.availability_group_listeners&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
  
-   [sys.availability_databases_cluster&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
  
-   [sys.availability_groups&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
  
-   [sys.availability_read_only_routing_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_cluster_nodes&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_cluster_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
-   [sys.dm_hadr_auto_page_repair&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
  
-   [sys.dm_hadr_availability_group_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_cluster_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_cluster_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys.dm_hadr_cluster&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
  
-   [sys.dm_hadr_cluster_members&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
  
-   [sys.dm_hadr_cluster_networks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
  
-   [sys.dm_hadr_database_replica_cluster_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys.dm_hadr_instance_node_map&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
  
-   [sys.dm_hadr_name_id_map&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
  
-   [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
-   [sys.dm_tcp_listener_states&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
  
-   [sys.fn_hadr_backup_is_preferred_replica&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **AlwaysOn 성능 카운터:**  
  
-   [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server, Databases 개체](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **AlwaysOn 가용성 그룹에 대 한 정책 기반 관리**  
  
-   [AlwaysOn 정책을 사용 하 여 가용성 그룹의 상태를 보려면 &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 (SQL Server)](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
