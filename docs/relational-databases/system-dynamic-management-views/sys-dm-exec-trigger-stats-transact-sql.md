---
title: sys.dm_exec_trigger_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  캐시된 트리거에 대한 집계 성능 통계를 반환합니다. 이 뷰에는 트리거당 하나의 행이 포함되며 행의 유효 기간은 트리거가 캐시에 남아 있는 기간과 같습니다. 캐시에서 트리거가 제거되면 이 뷰에서도 해당 행이 제거됩니다. 이때 Performance Statistics SQL 추적 이벤트가 발생 비슷합니다 **sys.dm_exec_query_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|이 트리거가 있는 데이터베이스 ID입니다.|  
|**object_id**|**int**|이 트리거의 개체 ID입니다.|  
|**유형**|**char(2)**|개체의 유형입니다.<br /><br /> TA = 어셈블리(CLR) 트리거<br /><br /> TR = SQL 트리거|  
|**Type_desc**|**nvarchar (60)**|개체 유형에 대한 설명:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|이 쿼리는 상관 관계를 사용할 수 있습니다 **sys.dm_exec_query_stats** 이 트리거 내에서 실행 된 합니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값을 함께 사용할 수 있습니다는 **sys.dm_exec_cached_plans** 동적 관리 뷰.|  
|**cached_time**|**datetime**|이 트리거가 캐시에 추가된 시간입니다.|  
|**last_execution_time**|**datetime**|이 트리거가 마지막으로 실행된 시간입니다.|  
|**execution_count**|**bigint**|이 트리거가 마지막으로 컴파일된 이후 실행된 횟수입니다.|  
|**total_worker_time**|**bigint**|이 트리거가 컴파일된 이후 실행되는 데 사용된 총 CPU 시간(마이크로초)입니다.|  
|**last_worker_time**|**bigint**|이 트리거가 마지막으로 실행될 때 사용된 CPU 시간(마이크로초)입니다.|  
|**min_worker_time**|**bigint**|단일 실행 중 이 트리거에 사용된 최대 CPU 시간(마이크로초)입니다.|  
|**max_worker_time**|**bigint**|단일 실행 중 이 트리거에 사용된 최대 CPU 시간(마이크로초)입니다.|  
|**total_physical_reads**|**bigint**|이 트리거가 컴파일된 이후 실행될 때 수행된 총 물리적 읽기 수입니다.|  
|**last_physical_reads**|**bigint**|이 트리거가 마지막으로 실행될 때 수행된 물리적 읽기 수입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중 이 트리거가 수행한 최소 물리적 읽기 수입니다.|  
|**max_physical_reads**|**bigint**|단일 실행 중 이 트리거가 수행한 최대 물리적 읽기 수입니다.|  
|**total_logical_writes**|**bigint**|이 트리거가 컴파일된 이후 실행될 때 수행된 총 논리적 쓰기 수입니다.|  
|**last_logical_writes**|**bigint**|**total_physical_reads**트리거가 실행 된 마지막 시간을 수행 하는 논리적 쓰기 수입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중 이 트리거가 수행한 최소 논리적 쓰기 수입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중 이 트리거가 수행한 최대 논리적 쓰기 수입니다.|  
|**total_logical_reads**|**bigint**|이 트리거가 컴파일된 이후 실행될 때 수행된 총 논리적 읽기 수입니다.|  
|**last_logical_reads**|**bigint**|이 트리거가 마지막으로 실행될 때 수행된 논리적 읽기 수입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중 이 트리거가 수행한 최소 논리적 읽기 수입니다.|  
|**max_logical_reads**|**bigint**|단일 실행 중 이 트리거가 수행한 최대 논리적 읽기 수입니다.|  
|**total_elapsed_time**|**bigint**|이 트리거의 실행을 완료하는 데 소요된 총 경과 시간(마이크로초)입니다.|  
|**last_elapsed_time**|**bigint**|가장 최근에 이 트리거의 실행을 완료하는 데 소요된 경과 시간(마이크로초)입니다.|  
|**min_elapsed_time**|**bigint**|이 트리거의 실행을 완료하는 데 소요된 최소 경과 시간(마이크로초)입니다.|  
|**max_elapsed_time**|**bigint**|이 트리거의 실행을 완료하는 데 소요된 최대 경과 시간(마이크로초)입니다.|  
  
## <a name="remarks"></a>주의  
 Microsoft Azure SQL Database에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보를 노출할 수 없거나 사용자가 액세스할 수 있는 다른 데이터베이스에 대한 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다.  

쿼리가 완료되면 뷰의 통계가 업데이트됩니다.  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정.
  
  
## <a name="examples"></a>예  
 다음 예에서는 평균 경과 시간으로 식별된 상위 5개의 트리거에 대한 정보를 반환합니다.  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [실행 관련 동적 관리 뷰 및 함수 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [sys.dm_exec_procedure_stats&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [sys.dm_exec_cached_plans&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
