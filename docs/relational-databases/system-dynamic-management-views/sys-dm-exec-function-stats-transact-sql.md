---
title: sys.dm_exec_function_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c85e25130214a6b12e630c186f275e75efd4b3d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.dm_exec_function_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  집계 캐시 된 함수에 대 한 성능 통계를 반환 합니다. 보기는 각 캐시 된 함수 계획에 대해 한 행을 반환 하 고 행의 유효 기간은 함수 동안 캐시 합니다. 함수는 캐시에서 제거 되 면 해당 행이이 보기에서 제거 됩니다. 이때 Performance Statistics SQL 추적 이벤트가 발생 비슷합니다 **sys.dm_exec_query_stats**합니다. 메모리에서 함수 및 CLR 스칼라 함수를 포함 하는 스칼라 함수에 대 한 정보를 반환 합니다. 테이블 반환 함수에 대 한 정보를 반환 하지 않습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다.  
  
> [!NOTE]
> 초기 쿼리 **sys.dm_exec_function_stats** 중인 서버에서 현재 실행 중인 작업이 있을 경우 부정확 한 결과가 나올 수 있습니다. 쿼리를 다시 실행하면 보다 정확한 결과를 확인할 수 있습니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|함수가 상주 하는 데이터베이스 ID입니다.|  
|**object_id**|**int**|함수의 개체 id.|  
|**type**|**char(2)**|개체의 유형: FN = 스칼라 반환된 함수|  
|**type_desc**|**nvarchar(60)**|개체 유형에 대 한 설명: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|이 쿼리는 상관 관계를 사용할 수 있습니다 **sys.dm_exec_query_stats** 이 함수 내에서 실행 된 합니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값을 함께 사용할 수 있습니다는 **sys.dm_exec_cached_plans** 동적 관리 뷰.<br /><br /> 0x000 때 고유 하 게 컴파일된 함수 쿼리는 메모리 액세스에 최적화 된 테이블은 항상입니다.|  
|**cached_time**|**datetime**|함수는 캐시에 추가 된 시간입니다.|  
|**last_execution_time**|**datetime**|마지막으로 함수 실행 된 시간입니다.|  
|**execution_count**|**bigint**|함수는 이후 실행 된 횟수 마지막으로 컴파일된입니다.|  
|**total_worker_time**|**bigint**|총 CPU 시간에 마이크로초 컴파일된 이후 실행 될 때이 함수 사용 된입니다.<br /><br /> 고유 하 게 컴파일된 함수에 대 한 **total_worker_time** 소요 1 미만이 면 결과가 되지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|CPU 시간, 마이크로초에서 사용 된 함수가 실행 된 마지막 시간입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|최소 CPU 시간, 마이크로초 단일 실행 중이 함수에 사용 된입니다. <sup>1</sup>|  
|**max_worker_time**|**bigint**|최대 CPU 시간, 마이크로초 단일 실행 중이 함수에 사용 된입니다. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|컴파일된 이후 실행 될 때가이 함수에서 수행 된 물리적 읽기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|마지막으로 함수 실행 되었을 때 수행 하는 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|최소 단일 실행 중이 함수에서 수행한 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|최대 단일 실행 중이 함수에서 수행한 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|컴파일된 이후 실행 될 때가이 함수에서 수행 된 논리적 쓰기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|계획이 마지막으로 실행될 때 변경된 버퍼 풀 페이지 수입니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중이 함수에서 수행한 논리적 쓰기의 최소 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중이 함수에서 수행한 논리적 쓰기의 최대 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|으로 컴파일된 이후 실행 될 때가이 함수에서 수행 된 논리적 읽기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|마지막으로 함수 실행 되었을 때 수행 하는 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|최소 단일 실행 중이 함수에서 수행한 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|최대 단일 실행 중이 함수에서 수행한 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_elapsed_time**|**bigint**|총 경과 시간 (밀리초)가 함수의 실행을 완료입니다.|  
|**last_elapsed_time**|**bigint**|경과 된 시간을 가장 최근에 마이크로초에서이 함수의 실행을 완료 합니다.|  
|**min_elapsed_time**|**bigint**|최소 경과 시간 (마이크로초)에 대 한이 함수의 실행을 완료 합니다.|  
|**max_elapsed_time**|**bigint**|최대 경과 시간 (마이크로초)에 대 한이 함수의 실행을 완료 합니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
  
## <a name="examples"></a>예  
 다음 예에서는 평균 경과 시간으로 식별 된 상위 10 가지 기능에 대 한 정보를 반환 합니다.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
