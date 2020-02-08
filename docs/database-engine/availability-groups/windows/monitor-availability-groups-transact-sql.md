---
title: T-SQL(Transact-SQL)을 사용하여 가용성 그룹 모니터링
description: T-SQL(Transact-SQL)을 사용하여 Always On 가용성 그룹을 모니터링하는 방법의 설명입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
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
ms.openlocfilehash: 6a95082cd732b644105c14c4ba598f859f48456e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68014700"
---
# <a name="monitor-availability-groups-transact-sql"></a>가용성 그룹 모니터링(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하여 가용성 그룹, 복제본 및 연결된 데이터베이스를 모니터링할 수 있도록 여러 카탈로그 및 동적 관리 뷰와 서버 속성을 제공합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 문을 사용하여 뷰를 통해 가용성 그룹과 해당 복제본 및 데이터베이스를 모니터링할 수 있습니다. 지정된 가용성 그룹에 대해 반환되는 정보는 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 주 복제본을 호스팅 중인지 아니면 보조 복제본을 호스팅 중인지에 따라 다릅니다.  
  
> [!TIP]  
>  ID 열로 뷰를 조인하여 한 번의 쿼리로 여러 뷰에서 정보를 반환할 수 있습니다.  
  
  
##  <a name="Permissions"></a> 권한  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 카탈로그 뷰를 사용하려면 서버 인스턴스에 대한 모든 정의 보기 권한이 필요합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 동적 관리 뷰를 사용하려면 서버에 대한 서버 상태 보기 권한이 필요합니다.  
  
##  <a name="AoAgFeatureOnSI"></a> 서버 인스턴스의 Always On 가용성 그룹 모니터링 기능  
 서버 인스턴스의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능을 모니터링하려면 다음 기본 제공 함수를 사용합니다.  
  
 [SERVERPROPERTY](../../../t-sql/functions/serverproperty-transact-sql.md) 함수  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용할지 여부와 사용할 경우 서버 인스턴스에서 시작되었는지 여부에 대한 서버 속성 정보를 반환합니다.  
  
 **열 이름:** IsHadrEnabled, HadrManagerStatus  
  
##  <a name="WSFC"></a> WSFC 클러스터의 가용성 그룹 모니터링  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 사용되는 로컬 서버 인스턴스를 호스팅하는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하여 SQL Server 인스턴스를 호스트하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 WSFC 쿼럼이 있는 경우 **sys.dm_hadr_cluster** 는 쿼럼에 대한 클러스터 이름과 정보를 표시하는 행을 반환합니다. WSFC 노드에 쿼럼이 없으면 반환되는 행이 없습니다.  
  
 **열 이름:** cluster_name, quorum_type, quorum_type_desc, quorum_state, quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
 SQL Server의 로컬 Always On 사용 인스턴스를 호스트하는 WSFC 노드에 WSFC 쿼럼이 있는 경우 쿼럼을 구성하는 각 멤버에 대한 행과 각 멤버의 상태를 반환합니다.  
  
 **열 이름:** member_name, member_type, member_type_desc, member_state, member_state_desc, number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
 가용성 그룹의 서브넷 구성에 참여하는 모든 멤버에 대해 하나의 행을 반환합니다. 이 동적 관리 뷰를 사용하여 각 가용성 복제본에 대해 구성된 네트워크 가상 IP의 유효성을 검사할 수 있습니다.  
  
 **열 이름:** member_name, network_subnet_ip, network_subnet_ipv4_mask, network_subnet_prefix_length, is_public, is_ipv4  
  
 **기본 키:** member_name + network_subnet_IP + network_subnet_prefix_length  
  
 [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
 Always On 가용성 그룹에 조인된 가용성 복제본을 호스트하는 SQL Server의 모든 인스턴스에 대해 서버 인스턴스를 호스트하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드의 이름을 반환합니다. 이러한 동적 관리 뷰는 다음과 같이 사용됩니다.  
  
-   이 동적 관리 뷰는 동일한 WSFC 노드에서 호스팅되는 여러 가용성 복제본이 포함된 가용성 그룹을 검색하는 데 유용합니다. 이러한 구성은 가용성 그룹이 잘못 구성된 경우 FCI 장애 조치(failover) 이후 발생 가능한 지원되지 않는 구성입니다.  
  
-   여러 SQL Server 인스턴스가 동일한 WSFC 노드에 호스팅되는 경우 리소스 DLL이 이 동적 관리 뷰를 사용하여 연결할 SQL Server의 인스턴스를 확인합니다.  
  
 **열 이름:** ag_resource_id, instance_name, node_name  
  
 [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
 현재 SQL Server 인스턴스가 세 가지 고유한 ID인 가용성 그룹 ID, WSFC 리소스 ID 및 WSFC 그룹 ID에 조인된 Always On 가용성 그룹의 매핑을 보여 줍니다. 이 매핑의 목적은 WSFC 리소스/그룹의 이름이 바뀐 시나리오를 처리하기 위한 것입니다.  
  
 **열 이름:** ag_name, ag_id, ag_resource_id, ag_group_id  
  
> [!NOTE]  
>  또한 나중에 이 항목에 있는 [가용성 복제본 모니터링](#AvReplicas) 섹션에서 **sys.dm_hadr_availability_replica_cluster_nodes** 및 **sys.dm_hadr_availability_replica_cluster_states**를 참조하고 [가용성 데이터베이스 모니터링](#AvDbs) 섹션에서 **sys.availability_databases_cluster** 및 **sys.dm_hadr_database_replica_cluster_states**를 참조하세요.  
  
 WSFC 클러스터와 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 자세한 내용은 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md) 및 [장애 조치(failover) 클러스터링 및 Always On 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
##  <a name="AvGroups"></a> Monitoring Availability Groups  
 서버 인스턴스가 가용성 복제본을 호스팅하는 가용성 그룹을 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에서 가용성 복제본을 호스팅하는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 WSFC 클러스터의 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 가용성 그룹 메타데이터가 포함됩니다.  
  
 **열 이름:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 가용성 복제본이 있는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다.  
  
 **열 이름:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="AvReplicas"></a> sys.dm_hadr_availability_replica_cluster_states  
 가용성 복제본을 모니터링하려면 다음 뷰와 시스템 함수를 사용합니다.  
  
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
 현재 복제본이 기본 백업 복제본인지 여부를 결정합니다.  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터( **SQLServer:가용성 복제본**  성능 개체)에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
##  <a name="AvDbs"></a> sys.dm_hadr_database_replica_cluster_states  
 가용성 데이터베이스를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [가용성 데이터베이스 모니터링](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
 로컬 복사본 데이터베이스가 가용성 그룹에 조인되어 있는지 여부에 상관없이 클러스터의 모든 Always On 가용성 그룹의 일부인 SQL Server 인스턴스의 데이터베이스별로 하나의 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스가 가용성 그룹에 추가되면 주 데이터베이스가 그룹에 자동으로 조인됩니다. 보조 데이터베이스를 가용성 그룹에 조인하려면 각 보조 복제본에서 보조 데이터베이스를 준비해야 합니다.  
  
 **열 이름:** group_id, group_database_id, database_name  
  
 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 각 데이터베이스당 한 개의 행을 포함합니다. 데이터베이스가 가용성 복제본에 속하는 경우 해당 데이터베이스의 행에 복제본의 GUID와 가용성 그룹 내의 데이터베이스에 대한 고유 식별자가 표시됩니다.  
  
 **[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 열 이름:** replica_id, group_database_id  
  
 [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
 서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다. 이 뷰에는 지정된 주 데이터베이스 또는 보조 데이터베이스의 최신 자동 페이지 복구 시도에 대한 행이 포함됩니다(데이터베이스당 최대 100개 행). 데이터베이스가 최대값에 도달하는 즉시 다음 자동 페이지 복구 시도에 대한 행이 기존 항목 중 하나를 대체합니다.  
  
 **열 이름:** database_id, file_id, page_id, error_type, page_status, modification_time  
  
 [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스가 가용성 복제본을 호스팅 중인 모든 가용성 그룹에 참여하는 각 데이터베이스에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** database_id, group_id, replica_id, group_database_id, is_local, synchronization_state, synchronization_state_desc, is_commit_participant, synchronization_health, synchronization_health_desc, database_state, database_state_desc, is_suspended, suspend_reason, suspend_reason_desc, recovery_lsn, truncation_lsn, last_sent_lsn, last_sent_time, last_received_lsn, last_received_time, last_hardened_lsn, last_hardened_time, last_redone_lsn, last_redone_time, log_send_queue_size, log_send_rate, redo_queue_size, redo_rate, filestream_send_rate, end_of_log_lsn, last_commit_lsn, last_commit_time, low_water_mark_for_ghosts  
  
 [sys.availability_databases_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 각 가용성 그룹에 있는 가용성 데이터베이스의 상태를 파악하는 데 필요한 정보가 들어 있는 행을 반환합니다. 이 동적 관리 뷰는 장애 조치(failover)를 계획 또는 이에 응답하거나 지정된 주 데이터베이스의 로그 잘림을 보유 중인 가용성 그룹의 보조 복제본을 검색하는 데 유용합니다.  
  
 **열 이름:** replica_id, group_database_id, database_name, is_failover_ready, is_pending_secondary_suspend, is_database_joined, recovery_lsn, truncation_lsn  
  
> [!NOTE]  
>  주 복제본 위치는 가용성 그룹의 권한이 있는 원본입니다.  
  
> [!NOTE]  
>  가용성 데이터베이스의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 성능 카운터( **SQLServer:Database Replica** 성능 개체)에 대한 자세한 내용은 [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)을 참조하세요. 또한 가용성 데이터베이스에서 트랜잭션 로그 작업을 모니터링하려면 **SQLServer:Databases** 성능 개체: **Log Flush Write Time (ms)** , **Log Flushes/sec**, **Log Pool Cache Misses/sec**, **Log Pool Disk Reads/sec** 및 **Log Pool Requests/sec** 카운터를 사용합니다. 자세한 내용은 [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)을 참조하세요.  
  
##  <a name="AGlisteners"></a> 가용성 그룹 수신기 모니터링  
 WSFC 클러스터의 서브넷에서 가용성 그룹 수신기를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
 가용성 그룹 수신기에 대해 현재 온라인인 규칙에 부합하는 모든 가상 IP 주소에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
 지정된 가용성 그룹에 대해 0개의 행을 반환하여 가용성 그룹에 연결된 네트워크 이름이 없음을 나타내거나 WSFC 클러스터의 각 가용성 그룹 수신기 구성에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
 각 TCP 수신기에 대한 동적 상태 정보를 포함하는 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
 **기본 키:** listener_id  
  
 가용성 그룹 수신기에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **Always On 가용성 그룹 모니터링 태스크:**  
  
-   [개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
 **Always On 가용성 그룹 모니터링 참조(Transact-SQL):**  
  
-   [SERVERPROPERTY&#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)  
  
-   [sys.availability_group_listener_ip_addresses&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
  
-   [sys.availability_group_listeners&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
  
-   [sys.availability_databases_cluster&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
  
-   [sys.availability_groups&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
  
-   [sys.availability_read_only_routing_lists&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
  
-   [sys.availability_replicas&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_nodes&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
-   [sys.dm_hadr_auto_page_repair&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
  
-   [sys.dm_hadr_availability_group_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_cluster&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_members&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_networks&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_instance_node_map&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
  
-   [sys.dm_hadr_name_id_map&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
  
-   [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
-   [sys.dm_tcp_listener_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
  
-   [sys.fn_hadr_backup_is_preferred_replica&#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **Always On 성능 카운터:**  
  
-   [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server, Databases 개체](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **Always On 가용성 그룹에 대한 정책 기반 관리**  
  
-   [Always On 정책을 사용하여 가용성 그룹의 상태 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
