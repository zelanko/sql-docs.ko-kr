---
title: sys.dm_exec_procedure_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e472d6f8b7b18bb7e73613a8c60a27461bb49b43
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418687"
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  캐시된 저장 프로시저에 대한 집계 성능 통계를 반환합니다. 이 뷰에는 캐시된 각 저장 프로시저 계획에 대해 하나의 행이 반환되며 행의 유효 기간은 저장 프로시저가 캐시에 남아 있는 기간과 같습니다. 캐시에서 저장 프로시저가 제거되면 이 뷰에서도 해당 행이 제거됩니다. 이때 Performance Statistics SQL 추적 이벤트를 발생 비슷합니다 **sys.dm_exec_query_stats**합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보 공개를 방지 하려면 연결 된 테 넌 트에 속하지 않는 데이터가 포함 된 모든 행 필터링 됩니다.  
  
> [!NOTE]
> 초기 쿼리 **sys.dm_exec_procedure_stats** 중인 서버에서 현재 실행 중인 작업이 있을 경우 부정확 한 결과 생성할 수 있습니다. 쿼리를 다시 실행하면 보다 정확한 결과를 확인할 수 있습니다.  
  
> [!NOTE]
> 이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_procedure_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|이 저장 프로시저가 있는 데이터베이스의 ID입니다.|  
|**object_id**|**int**|이 저장 프로시저의 개체 ID입니다.|  
|**type**|**char(2)**|개체의 유형입니다.<br /><br /> P = SQL 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> X = 확장 저장 프로시저|  
|**type_desc**|**nvarchar(60)**|개체 유형에 대한 설명:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|이 쿼리는 상관 관계를 사용할 수 있습니다 **sys.dm_exec_query_stats** 이 저장된 프로시저 내에서 실행 된 합니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값을 사용 하 여 사용할 수는 **sys.dm_exec_cached_plans** 동적 관리 뷰.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
|**cached_time**|**datetime**|이 저장 프로시저가 캐시에 추가된 시간입니다.|  
|**last_execution_time**|**datetime**|이 저장 프로시저가 마지막으로 실행된 시간입니다.|  
|**execution_count**|**bigint**|이후 저장된 프로시저가 실행 된 횟수 만큼 마지막 컴파일 되었습니다.|  
|**total_worker_time**|**bigint**|총 양 합니다 컴파일된 이후 실행이 저장된 프로시저에 의해 사용 된 CPU 시간입니다.<br /><br /> 고유하게 컴파일된 저장 프로시저의 경우 1초 미만이 소요되는 실행이 많으면 **total_worker_time** 이 정확하지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|이 저장 프로시저가 마지막으로 실행될 때 사용된 CPU 시간(마이크로초)입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|최소 CPU 시간 마이크로초 단위로이 저장 프로시저는 항상 사용 했습니다 단일 실행 하는 동안. <sup>1</sup>|  
|**max_worker_time**|**bigint**|최대 CPU 시간 마이크로초 단위로이 저장 프로시저는 항상 사용 했습니다 단일 실행 하는 동안. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|총 컴파일된 이후 실행이 저장된 프로시저에 의해 수행 된 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|저장된 프로시저가 실행 된 마지막으로 수행 하는 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중이 저장 프로시저는 물리적 읽기 최소 수행해 본.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|단일 실행 중이 저장 프로시저는 물리적 읽기 최대 수행해 본.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|총 컴파일된 이후 실행이 저장된 프로시저에 의해 수행 된 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|버퍼 풀 페이지 수 계획 실행 된 마지막 시간을 정리 합니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중이 저장 프로시저는 논리적 쓰기 최소 수행해 본.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중이 저장 프로시저는 논리적 쓰기 최대 수행해 본.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|총 컴파일된 이후 실행이 저장된 프로시저에 의해 수행 된 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|저장된 프로시저가 실행 된 마지막으로 수행 하는 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중이 저장 프로시저는 논리적 읽기 수가 최소 수행해 본.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|최대 단일 실행 중이 저장된 프로시저가 수행해 본는 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_elapsed_time**|**bigint**|총 경과 시간을 마이크로초가 저장 프로시저가 완료 된 실행.|  
|**last_elapsed_time**|**bigint**|경과 된 시간을 밀리초 가장 최근에 완료 된 실행에 대 한 저장 프로시저.|  
|**min_elapsed_time**|**bigint**|최소 경과 시간 (밀리초)가 완료 된 실행입니다 저장 프로시저.|  
|**max_elapsed_time**|**bigint**|최대 경과 시간 (밀리초)가 완료 된 실행입니다 저장 프로시저.|  
|**total_spills**|**bigint**|페이지 컴파일 되었습니다 때문에이 저장된 프로시저를 실행 하 여 소모전의 총 수입니다.<br /><br /> **적용 대상**: 부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|페이지 수가 소모전 저장된 프로시저가 실행 된 마지막 시간입니다.<br /><br /> **적용 대상**: 부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|이 저장된 프로시저는 단일 실행 하는 동안 엎지른 적이 페이지의 최소 수입니다.<br /><br /> **적용 대상**: 부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|단일 실행 중이 저장 프로시저는 최대 매수 할 엎지른.<br /><br /> **적용 대상**: 부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**pdw_node_id**|**int**|이 배포에 있는 노드에 대 한 식별자입니다.<br /><br />**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
 <sup>1</sup> 고유 하 게 컴파일된 저장된 프로시저에 대 한 통계 컬렉션을 사용 하면 작업자 시간이 밀리초 단위로 수집 됩니다. 쿼리가 밀리초 미만 단위로 실행되는 경우 값은 0이 됩니다.  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
   
## <a name="remarks"></a>Remarks  
 저장 프로시저의 실행이 완료되면 뷰에 있는 통계가 업데이트됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 평균 경과 시간으로 식별된 상위 10개의 저장 프로시저에 대한 정보를 반환합니다.  
  
```sql  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>관련 항목  
[실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)    
[sys.dm_exec_trigger_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)    
[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  
  


