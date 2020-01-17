---
title: 가용성 그룹 시스템 개체 참조
description: Always On 가용성 그룹으로 작업하는 경우 사용할 수 있는 다양한 시스템 개체에 대한 참조입니다.
ms.custom: seo-lt-2019
ms.date: 04/03/2010
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2014||=sqlallproducts-allversions'
ms.openlocfilehash: 140953484006d33e7814c19b9eb5bd6abcd29009
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822459"
---
# <a name="always-on-availability-group-system-object-reference"></a>Always On 가용성 그룹 시스템 개체 참조

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
    
이 항목은 Always On 가용성 그룹으로 작업하는 경우 사용할 수 있는 모든 다양한 시스템 개체에 대한 참조 페이지 역할을 합니다. 

## <a name="system-catalog-views"></a>시스템 카탈로그 뷰

| 시스템 카탈로그 뷰 | Description|
| :------ | :----------------------------- |
| [가용성 데이터베이스 모니터링](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)   | 로컬 복사본 데이터베이스가 가용성 그룹에 조인되어 있는지 여부에 상관없이 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 모든 Always On 가용성 그룹에 대해 하나의 가용성 복제본을 호스팅하는 SQL Server 인스턴스에서 가용성 데이터베이스별로 하나의 행을 포함합니다. |
| [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  | WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 Always On 가용성 그룹 수신기에 연결되는 모든 IP 주소에 대해 하나의 행을 반환합니다. |
| [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)    | 각 Always On 가용성 그룹에 대해 0개의 행을 반환하여 가용성 그룹에 연결된 네트워크 이름이 없음을 나타내거나 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 각 가용성 그룹 수신기 구성에 대해 하나의 행을 반환합니다.  |
| [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   | SQL Server의 로컬 인스턴스에서 가용성 복제본을 호스트하는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다. |
| [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)    | WSFC(Windows Server 장애 조치(Failover) 클러스터링)의 각 Always On 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 WSFC 클러스터의 가용성 그룹 메타데이터가 포함됩니다. |
| [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)    | WSFC 장애 조치(Failover) 클러스터의 Always On 가용성 그룹에서 각각의 가용성 복제본의 읽기 전용 라우팅 목록에 대한 행을 반환합니다. |
| [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)    | WSFC 장애 조치(failover) 클러스터의 모든 Always On 가용성 그룹에 속해 있는 각 가용성 복제본에 대해 하나의 행을 반환합니다. |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>시스템 동적 관리 뷰


| 시스템 동적 관리 뷰 | Description|
| :------ | :----------------------------- |
| [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)   | 서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다.  |
| [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)    | SQL Server의 로컬 인스턴스에 가용성 복제본이 있는 각 Always On 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 지정된 가용성 그룹의 상태를 정의하는 상태가 표시됩니다. |
| [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)     | WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 Always On 가용성 그룹의 모든 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다. |
| [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)     | WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 모든 Always On 가용성 그룹(복제본 위치에 상관없음)의 각 Always On 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다. |
| [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)    | 각 로컬 복제본에 대해 하나의 행을 반환하고 로컬 복제본과 동일한 Always On 가용성 그룹의 각 원격 복제본에 대해 하나의 행을 반환합니다. 각 행에는 지정된 복제본의 상태에 대한 정보가 들어 있습니다. |
| [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)    | 클러스터 이름과 쿼럼에 대한 정보를 제공하는 하나의 행을 반환합니다. |
| [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)    | 쿼럼을 구성하는 각 구성원 및 각 구성원의 상태에 대해 하나의 행을 반환합니다. |
| [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)    | 가용성 그룹의 서브넷 구성에 참여하는 모든 WSFC 클러스터 구성원에 대해 하나의 행을 반환합니다.  |
| [sys.availability_databases_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)     | WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 각 Always On 가용성 그룹에 있는 Always On 가용성 그룹에서 가용성 데이터베이스의 상태를 파악하는 데 필요한 정보가 들어 있는 행을 반환합니다.  |
| [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)    | SQL Server의 로컬 인스턴스가 가용성 복제본을 호스팅하는 Always On 가용성 그룹에 참여 중인 각 데이터베이스에 대해 하나의 행을 반환합니다. |
| [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)    | Always On 가용성 그룹에 조인된 가용성 복제본을 호스트하는 SQL Server의 모든 인스턴스에 대해 서버 인스턴스를 호스트하는 WSFC(Windows Server 장애 조치(failover) 클러스터) 노드의 이름을 반환합니다. |
| [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)    | 현재 SQL Server 인스턴스가 세 가지 고유한 ID인 가용성 그룹 ID, WSFC 리소스 ID 및 WSFC 그룹 ID에 조인된 Always On 가용성 그룹의 매핑을 보여 줍니다. |
| [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)    | 각 TCP 수신기에 대한 동적 상태 정보를 포함하는 행을 반환합니다. |
| &nbsp; | &nbsp; |

## <a name="system-functions"></a>시스템 함수


| 시스템 함수 | Description|
| :------ | :----------------------------- |
| [sys.fn_hadr_is_primary_replica](../../../relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql.md)  | 현재 복제본이 주 복제본인지 확인하는 데 사용됩니다. |
| [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)    | 현재 복제본이 기본 백업 복제본인지 확인하는 데 사용됩니다. |
| [sys.fn_hadr_distributed_ag_replica](../../../relational-databases/system-functions/sys-fn-hadr-distributed-ag-replica-transact-sql.md)    | 분산된 가용성 그룹의 복제본을 로컬 가용성 그룹에 매핑하는 데 사용됩니다. |
| &nbsp; | &nbsp; |


  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   

  
