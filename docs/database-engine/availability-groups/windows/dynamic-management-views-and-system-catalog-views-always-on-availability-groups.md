---
title: 동적 관리 뷰 및 시스템 카탈로그 뷰(Always On 가용성 그룹-SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4320a4a4-6183-462b-8bda-e7424e7cb706
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 819a7acb18b47227411d7ccf1683deb2fc63a3d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-management-views-and-system-catalog-views-always-on-availability-groups"></a>동적 관리 뷰 및 시스템 카탈로그 뷰(Always On 가용성 그룹)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 토픽에서는 가용성 그룹을 모니터링 및 문제 해결하는 데 사용할 수 있는 Always On DMV(동적 관리 뷰)에 대한 몇 가지 일반 쿼리를 보여 줍니다.  
  
> [!TIP]  
>  Always On 대시보드에서 해당 테이블 헤더를 마우스 오른쪽 단추로 클릭하고 표시하거나 숨기려는 DMV를 선택하여 가용성 복제본 및 가용성 데이터베이스에 대해 많은 DMV를 표시하도록 GUI를 쉽게 구성할 수 있습니다.  
  
 가용성 그룹 DMV에 대한 자세한 내용은 [Always On 가용성 그룹 동적 관리 뷰 및 기능&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)을 참조하세요. 가용성 그룹 카탈로그 뷰에 대한 자세한 내용은 [Always On 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)를 참조하세요.  
  
## <a name="check-the-wsfc-cluster-node-configuration"></a>WSFC 클러스터 노드 구성 확인  
 다음 T-SQL(Transact-SQL) 쿼리는 현재 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터에서 모든 노드의 상태를 검색합니다.  
  
```sql  
use master  
go  
select * from sys.dm_hadr_cluster_members  
go  
```  
  
 이 결과 집합은 현재 WSFC 클러스터의 각 멤버 노드의 상태를 보고합니다. 쿼럼이 **노드 및 파일 공유 과반수**로 정의된 경우 파일 공유도 보고됩니다. 각 노드의 투표 가중치([number_of_quorum_votes](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md) 값)를 포함한 각 노드의 상태를 볼 수 있습니다.  
  
## <a name="explore-the-cluster-network"></a>클러스터 네트워크 탐색  
 다음 쿼리는 현재 WSFC 클러스터의 네트워크 구성을 검색합니다.  
  
```sql  
select * from sys.dm_hadr_cluster_networks  
```  
  
 결과 집합은 WSFC 클러스터의 각 네트워크 어댑터에 대해 행 한 개를 포함합니다. 예를 들어 각 노드에 두 네트워크 어댑터를 포함하는 2-노드 클러스터에서 이 쿼리는 행 4개를 반환합니다.  
  
## <a name="explore-the-availability-groups"></a>가용성 그룹 탐색  
 다음 쿼리는 가용성 그룹에 관한 정보를 검색합니다.  
  
```sql  
select primary_replica, primary_recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_group_states  
go  
select * from sys.availability_groups  
go  
select * from sys.availability_groups_cluster  
go  
```  
  
 DMVs [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md), [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 및 [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)는 모두 현재 WSFC 클러스터의 가용성 그룹에 관한 정보를 반환합니다. 사실 [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 및 [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)는 같은 정보를 반환하는 것처럼 보입니다.  
  
 그러나 [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)는 WSFC 클러스터에 저장된 가용성 그룹 메타데이터를 보고하는 반면, [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)은 SQL Server 프로세스 공간에 캐시된 가용성 그룹 메타데이터를 보고합니다. 또한 이 두 DMV는 구성 정보를 보고하는 반면에 [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)은 가용성 그룹의 현재 상태를 보고합니다.  
  
> [!IMPORTANT]  
>  이 명칭은 가용성 복제본 및 가용성 데이터베이스를 문서화하는 DMV를 전달합니다.  
  
## <a name="explore-the-availability-replicas"></a>가용성 복제본 탐색  
 다음 쿼리는 가용성 그룹에 정의된 가용성 복제본에 관한 정보를 검색합니다.  
  
```sql  
select replica_id, role_desc, connected_state_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
select replica_server_name, replica_id, availability_mode_desc, endpoint_url from sys.availability_replicas  
go  
select replica_server_name, join_state_desc from sys.dm_hadr_availability_replica_cluster_states  
go  
```  
  
 가용성 그룹 DMV와 유사하게 가용성 복제본에 관하여 보고하는 DMV 3개를 찾을 수 있습니다. [sys.dm_hadr_availability_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)는 SQL Server에 로컬로 캐시된 가용성 복제본에 관한 상태 정보를 보고하며, [sys.dm_hadr_availability_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)는 WSFC 클러스터의 가용성 복제본에 관한 상태 정보를 보고합니다. 끝으로 [sys.availability_replicas](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)는 SQL Server에 로컬로 캐시된 가용성 복제본에 관한 구성 데이터를 보고합니다.  
  
## <a name="explore-availability-replica-health"></a>가용성 복제본 상태 탐색  
 다음 쿼리는 가용성 복제본에 관한 현재 상태 정보를 검색합니다.  
  
```sql  
select replica_id, role_desc, recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
```  
  
 주 복제본 및 보조 복제본에 관한 쿼리 결과를 비교해 보면 보조 복제본에 관한 상태 정보가 가용성 그룹의 다른 복제본에 대해서가 아닌 해당 복제본에 대해서만 보고된다는 것을 알 수 있습니다.  
  
## <a name="explore-the-availability-databases"></a>가용성 데이터베이스 탐색  
 다음 쿼리는 가용성 그룹에 정의된 가용성 복제본에 관한 정보를 검색합니다. 가용성 데이터베이스에 대한 데이터 이동을 일시 중단하기 전 및 후의 쿼리 결과 변화를 관찰할 수 있습니다.  
  
```sql
select * from sys.availability_databases_cluster  
go  
select group_database_id, database_name, is_failover_ready  from sys.dm_hadr_database_replica_cluster_states  
go  
select database_id, synchronization_state_desc, synchronization_health_desc, last_hardened_lsn, redo_queue_size, log_send_queue_size from sys.dm_hadr_database_replica_states  
go  
```  
  
 여기서 다시 Always On DMV 3가지가 가용성 데이터베이스에 관하여 보고합니다. [sys.availability_databases_cluster](~/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)는 WSFC 클러스터의 가용성 데이터베이스에 관한 구성 정보를 보고합니다. [sys.dm_hadr_database_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)는 SQL Server에 로컬로 캐시된 데이터베이스 복제본에 관한 상태 정보를 보고합니다. 즉, 가용성 복제본의 장애 조치(failover) 준비 상태 같은 몇 가지 중요한 상태 정보를 포함합니다. 끝으로 [sys.dm_hadr_database_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)는 주 및 보조 데이터베이스 복제본의 로그에 대한 LSN 진행 정보 등 각각의 가용성 데이터베이스에 관한 ID 및 상태 정보를 보고하는 아주 자세한 결과입니다.  
  
## <a name="explore-availability-database-health"></a>가용성 데이터베이스 상태 탐색  
 다음 쿼리는 복제본에 있는 각 가용성 데이터베이스의 상태에 관한 정보를 검색합니다. 가용성 데이터베이스에 대한 데이터 이동을 일시 중단하기 전 및 후의 쿼리 결과 변화를 관찰할 수 있습니다.  
  
```sql  
select dc.database_name, dr.database_id, dr.synchronization_state_desc,   
dr.suspend_reason_desc, dr.synchronization_health_desc  
from sys.dm_hadr_database_replica_states dr  join sys.availability_databases_cluster dc  
on dr.group_database_id=dc.group_database_id   
where is_local=1  
go  
```  
  
  