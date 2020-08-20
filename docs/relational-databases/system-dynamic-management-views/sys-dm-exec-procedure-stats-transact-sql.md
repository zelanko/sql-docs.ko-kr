---
description: sys.dm_exec_procedure_stats(Transact-SQL)
title: sys. dm_exec_procedure_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 116196bf58c37c63fe64ce9566dd21d3191c022b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493792"
---
# <a name="sysdm_exec_procedure_stats-transact-sql"></a>sys.dm_exec_procedure_stats(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  캐시된 저장 프로시저에 대한 집계 성능 통계를 반환합니다. 이 뷰에는 캐시된 각 저장 프로시저 계획에 대해 하나의 행이 반환되며 행의 유효 기간은 저장 프로시저가 캐시에 남아 있는 기간과 같습니다. 캐시에서 저장 프로시저가 제거되면 이 뷰에서도 해당 행이 제거됩니다. 이때 Performance Statistics SQL 추적 이벤트가 **sys.dm_exec_query_stats**와 유사하게 발생합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.  
  
> [!NOTE]
> 데이터는 완료 된 쿼리만 반영 하 고 아직 진행 중인 쿼리는 반영 하지 않으므로, **dm_exec_procedure_stats**  의 결과는 각 실행에 따라 달라질 수 있습니다.
> 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_exec_procedure_stats**을 사용 합니다. 

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------| 
|**database_id**|**int**|이 저장 프로시저가 있는 데이터베이스의 ID입니다.|  
|**object_id**|**int**|이 저장 프로시저의 개체 ID입니다.|  
|**type**|**char(2)**|개체의 유형입니다.<br /><br /> P = SQL 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> X = 확장 저장 프로시저|  
|**type_desc**|**nvarchar(60)**|개체 유형에 대한 설명:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|이 저장 프로시저 내에서 실행 된 **dm_exec_query_stats** 의 쿼리와 상호 연결 하는 데 사용할 수 있습니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값은 **dm_exec_cached_plans** 동적 관리 뷰와 함께 사용할 수 있습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
|**cached_time**|**datetime**|이 저장 프로시저가 캐시에 추가된 시간입니다.|  
|**last_execution_time**|**datetime**|이 저장 프로시저가 마지막으로 실행된 시간입니다.|  
|**execution_count**|**bigint**|저장 프로시저가 마지막으로 컴파일된 이후 실행 된 횟수입니다.|  
|**total_worker_time**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 되는 동안 사용 된 총 CPU 시간 (마이크로초)입니다.<br /><br /> 고유하게 컴파일된 저장 프로시저의 경우 1초 미만이 소요되는 실행이 많으면 **total_worker_time** 이 정확하지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|이 저장 프로시저가 마지막으로 실행될 때 사용된 CPU 시간(마이크로초)입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|단일 실행 중이 저장 프로시저가 사용한 최소 CPU 시간 (마이크로초)입니다. <sup>1</sup>|  
|**max_worker_time**|**bigint**|단일 실행 중이 저장 프로시저가 사용한 최대 CPU 시간 (마이크로초)입니다. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 될 때 수행 된 총 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|저장 프로시저가 마지막으로 실행 되었을 때 수행 된 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최소 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최대 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 될 때 수행 된 총 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|계획이 마지막으로 실행 되었을 때 변경 된 버퍼 풀 페이지 수입니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최소 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최대 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 될 때 수행 된 총 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|저장 프로시저가 마지막으로 실행 되었을 때 수행 된 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최소 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최대 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_elapsed_time**|**bigint**|이 저장 프로시저의 실행을 완료 하는 데 소요 된 총 경과 시간 (마이크로초)입니다.|  
|**last_elapsed_time**|**bigint**|가장 최근에이 저장 프로시저의 실행을 완료 하는 데 경과 된 시간 (마이크로초)입니다.|  
|**min_elapsed_time**|**bigint**|이 저장 프로시저의 실행을 완료 하는 데 소요 된 최소 경과 시간 (마이크로초)입니다.|  
|**max_elapsed_time**|**bigint**|이 저장 프로시저의 실행을 완료 하는 데 소요 된 최대 경과 시간 (마이크로초)입니다.|  
|**total_spills**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 될 때 발생 한 총 페이지 수입니다.<br /><br /> **적용 대상**: CU3부터 시작 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**last_spills**|**bigint**|저장 프로시저가 마지막으로 실행 되었을 때에 분산 된 페이지의 수입니다.<br /><br /> **적용 대상**: CU3부터 시작 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**min_spills**|**bigint**|단일 실행 중이 저장 프로시저가 연결한 최소 페이지 수입니다.<br /><br /> **적용 대상**: CU3부터 시작 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**max_spills**|**bigint**|단일 실행 중이 저장 프로시저가 연결한 최대 페이지 수입니다.<br /><br /> **적용 대상**: CU3부터 시작 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**pdw_node_id**|**int**|이 배포가 설정 된 노드의 식별자입니다.<br /><br />**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
|**total_page_server_reads**|**bigint**|이 저장 프로시저가 컴파일된 이후 실행 될 때 수행 된 페이지 서버 읽기의 총 수입니다.<br /><br /> **적용 대상**: Azure SQL Database hyperscale|  
|**last_page_server_reads**|**bigint**|저장 프로시저가 마지막으로 실행 되었을 때 수행 된 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상**: Azure SQL Database hyperscale|  
|**min_page_server_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최소 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상**: Azure SQL Database hyperscale|  
|**max_page_server_reads**|**bigint**|단일 실행 중이 저장 프로시저가 수행한 최대 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상**: Azure SQL Database hyperscale|  
  
 <sup>1</sup> 통계 수집을 사용 하는 경우 고유 하 게 컴파일된 저장 프로시저의 경우 작업자 시간이 밀리초 단위로 수집 됩니다. 쿼리가 밀리초 미만 단위로 실행되는 경우 값은 0이 됩니다.  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
   
## <a name="remarks"></a>설명  
 저장 프로시저의 실행이 완료되면 뷰에 있는 통계가 업데이트됩니다.  
  
## <a name="examples"></a>예제  
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
[Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행 ](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)    
[dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)    
[sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  
  


