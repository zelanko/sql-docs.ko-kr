---
title: sys.dm_exec_function_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c0064e35be2ab514e93b9119f7994849cf50cc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013198"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.dm_exec_function_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  캐시 된 함수에 대 한 성능 통계를 집계 하는 반환 합니다. 각 함수 캐시 된 계획에 대 한 하나의 행을 반환 하는 뷰 및 행의 유효 기간은 함수 동안 캐시 합니다. 함수는 캐시에서 제거 되 면 해당 행이 뷰에서 제거 됩니다. 이때 Performance Statistics SQL 추적 이벤트를 발생 비슷합니다 **sys.dm_exec_query_stats**합니다. 메모리에서 함수 및 CLR 스칼라 함수를 비롯 한 스칼라 함수에 대 한 정보를 반환 합니다. 테이블 반환 함수에 대 한 정보를 반환 하지 않습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보 공개를 방지 하려면 연결 된 테 넌 트에 속하지 않는 데이터가 포함 된 모든 행 필터링 됩니다.  
  
> [!NOTE]
> 초기 쿼리 **sys.dm_exec_function_stats** 중인 서버에서 현재 실행 중인 작업이 있을 경우 부정확 한 결과 생성할 수 있습니다. 쿼리를 다시 실행하면 보다 정확한 결과를 확인할 수 있습니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|함수가 상주 하는 데이터베이스 ID입니다.|  
|**object_id**|**int**|함수의 개체 id.|  
|**type**|**char(2)**|개체의 유형입니다.   FN = 스칼라 반환된 함수|  
|**type_desc**|**nvarchar(60)**|개체 유형에 대한 설명: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|이 쿼리는 상관 관계를 사용할 수 있습니다 **sys.dm_exec_query_stats** 이 함수 내에서 실행 된 합니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값을 사용 하 여 사용할 수는 **sys.dm_exec_cached_plans** 동적 관리 뷰.<br /><br /> 0x000 경우 고유 하 게 컴파일된 함수 쿼리 메모리 최적화 테이블은 항상입니다.|  
|**cached_time**|**datetime**|캐시에 추가 된 함수는 시간입니다.|  
|**last_execution_time**|**datetime**|함수는 실행 된 마지막 시간입니다.|  
|**execution_count**|**bigint**|마지막으로 컴파일된 함수 이후 실행 된 횟수입니다.|  
|**total_worker_time**|**bigint**|총 CPU 시간으로 컴파일된 이후 실행 될 때이 함수 사용 된 마이크로초입니다.<br /><br /> 고유 하 게 컴파일된 함수에 대 한 **total_worker_time** 보다 작거나 1 밀리초 소요 하는 경우 정확 하 게 되지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|CPU 시간을 마이크로초에서 함수가 실행 된 마지막으로 사용한입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|최소 CPU 시간, 단일 실행 중이 함수에 사용 된는 마이크로초입니다. <sup>1</sup>|  
|**max_worker_time**|**bigint**|최대 CPU 시간, 단일 실행 중이 함수에 사용 된는 마이크로초입니다. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|컴파일된 이후 실행 될 때이 함수 수행 된 물리적 읽기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|마지막으로 함수 실행을 수행 하는 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중이 함수에서 수행한 물리적 읽기의 최소 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|최대 단일 실행 중이 함수에서 수행한 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|컴파일된 이후 실행 될 때가이 함수에서 수행 된 논리적 쓰기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|계획이 마지막으로 실행될 때 변경된 버퍼 풀 페이지 수입니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중이 함수에서 수행한 논리적 쓰기의 최소 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중이 함수에서 수행한 논리적 쓰기의 최대 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|컴파일된 이후 실행 될 때가이 함수에서 수행 된 논리적 읽기의 총 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|마지막으로 함수 실행을 수행 하는 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중이 함수에서 수행한 논리적 읽기의 최소 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|최대 단일 실행 중이 함수에서 수행한 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_elapsed_time**|**bigint**|총 경과 시간, 완료 된 실행이 함수의 마이크로초에서입니다.|  
|**last_elapsed_time**|**bigint**|이 함수의 가장 최근에 완료 된 실행을 위해 마이크로초에서 경과 시간입니다.|  
|**min_elapsed_time**|**bigint**|최소 경과 시간 (마이크로초)에 대 한이 함수의 실행을 완료 합니다.|  
|**max_elapsed_time**|**bigint**|최대 경과 시간 (마이크로초)에 대 한이 함수의 실행을 완료 합니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="examples"></a>예  
 다음 예에서는 평균 경과 시간으로 식별 된 상위 10 개의 함수에 대 한 정보를 반환 합니다.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>관련 항목  
 [실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
