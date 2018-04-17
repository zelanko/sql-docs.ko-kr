---
title: sys.dm_hadr_database_replica_cluster_states (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de2182087dce5d924fba15b2000a860c25a1c47f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrdatabasereplicaclusterstates-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  각 Always On 가용성 그룹에 Windows Server 장애 조치 클러스터링 (WSFC) 클러스터에서 Always On 가용성 그룹의 가용성 데이터베이스의 상태에 대 한 정보를 제공 하는 필요한 정보가 들어 있는 행을 반환 합니다. 쿼리 **sys.dm_hadr_database_replica_states** 다음과 같은 질문에 답변할 수:  
  
-   가용성 그룹의 모든 데이터베이스에서 장애 조치(failover)를 수행할 준비가 되었습니까?  
  
-   강제 장애 조치(failover) 후 보조 데이터베이스를 로컬로 일시 중지하고 새 주 복제본에 대해 일시 중지된 상태를 승인했습니까?  
  
-   주 복제본을 현재 사용할 수 없는 경우 주 복제본으로 전환될 때 데이터 손실이 최소화되는 보조 복제본은 어느 것입니까?  
  
-   때의 값은 [sys.databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)**log_reuse_wait** 열이 지정된 된 주 데이터베이스의 로그 잘림을 보유 중인 가용성 그룹에 보조 복제본 "AVAILABILITY_REPLICA" ?  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|가용성 그룹 내 가용성 복제본의 식별자입니다.|  
|**group_database_id**|**uniqueidentifier**|가용성 그룹 내 데이터베이스의 식별자입니다. 이 식별자는 이 데이터베이스가 조인되는 모든 복제본에서 동일합니다.|  
|**database_name**|**sysname**|가용성 그룹에 속하는 데이터베이스의 이름입니다.|  
|**is_failover_ready**|**bit**|보조 데이터베이스가 해당 주 데이터베이스와 동기화되었는지 여부를 나타냅니다. 다음 중 하나입니다.<br /><br /> 0 = 데이터베이스가 클러스터에서 동기화된 상태로 표시되지 않습니다. 데이터베이스에서 장애 조치(failover)를 수행할 준비가 되지 않았습니다.<br /><br /> 1 = 데이터베이스가 클러스터에서 동기화된 상태로 표시됩니다. 데이터베이스에서 장애 조치(failover)를 수행할 준비가 되었습니다.|  
|**is_pending_secondary_suspend**|**bit**|강제 장애 조치 후 데이터베이스가 정지 중 보류 중인지 여부를 나타내며 다음 중 하나입니다.<br /><br /> 0 = HADR_SYNCHRONIZED_ SUSPENDED를 제외한 모든 상태.<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED. 강제 장애 조치가 완료되면 각 보조 데이터베이스는 HADR_SYNCHONIZED_SUSPENDED로 설정되고 새 주 복제본이 해당 보조 데이터베이스에서 SUSPEND 메시지에 대한 승인을 받을 때까지 이 상태를 유지합니다.<br /><br /> NULL = 알 수 없음(쿼럼 없음)|  
|**is_database_joined**|**bit**|이 가용성 복제본의 데이터베이스가 가용성 그룹에 조인되었는지 여부를 나타내며 다음 중 하나입니다.<br /><br /> 0 = 데이터베이스가 이 가용성 복제본의 가용성 그룹에 조인되지 않았습니다.<br /><br /> 1 = 데이터베이스가 이 가용성 복제본의 가용성 그룹에 조인되었습니다.<br /><br /> NULL = 알 수 없음(가용성 복제본에 쿼럼이 부족함)|  
|**recovery_lsn**|**numeric(25,0)**|주 복제본에서 복제본이 복구 또는 장애 조치(failover) 후 새 로그 레코드를 쓰기 전의 트랜잭션 로그 끝을 나타냅니다. 주 복제본에서 지정된 보조 데이터베이스에 대한 행에는 주 복제본에서 보조 복제본을 동기화(즉, 되돌려서 다시 초기화)하는 데 필요한 값이 있습니다.<br /><br /> 보조 복제본에서 이 값은 NULL입니다. 각 보조 복제본은 MAX을 갖거나 주 복제본이 보조 복제본에 다시 전달하도록 지시한 더 작은 값을 갖습니다.|  
|**truncation_lsn**|**numeric(25,0)**|[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 로그 잘림 값이며, 백업 작업 등에 의해 로컬 로그 잘림이 차단된 경우 로컬 잘림 LSN보다 클 수 있습니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [가용성 그룹 모니터링 & #40; Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [sys.dm_hadr_database_replica_states& #40; Transact SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
