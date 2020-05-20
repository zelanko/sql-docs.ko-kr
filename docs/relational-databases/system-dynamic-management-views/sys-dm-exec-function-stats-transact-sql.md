---
title: sys. dm_exec_function_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 02cff18af9c0824d7f28e5685f5fc63a0bf45128
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821248"
---
# <a name="sysdm_exec_function_stats-transact-sql"></a>sys. dm_exec_function_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  캐시 된 함수에 대 한 집계 성능 통계를 반환 합니다. 이 뷰는 캐시 된 각 함수 계획에 대해 하나의 행을 반환 하 고, 해당 함수는 캐시 된 상태로 유지 되는 동안에는 행의 수명이 지속 됩니다. 캐시에서 함수를 제거 하면 해당 행이이 뷰에서 제거 됩니다. 이때 Performance Statistics SQL 추적 이벤트가 **sys.dm_exec_query_stats**와 유사하게 발생합니다. 메모리 내 함수 및 CLR 스칼라 함수를 비롯 한 스칼라 함수에 대 한 정보를 반환 합니다. 는 테이블 반환 함수에 대 한 정보를 반환 하지 않습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.  
  
> [!NOTE]
> 데이터는 완료 된 쿼리만 반영 하 고 아직 진행 중인 쿼리는 반영 하지 않으므로, **dm_exec_function_stats** 의 결과는 각 실행에 따라 달라질 수 있습니다. 

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|함수가 있는 데이터베이스 ID입니다.|  
|**object_id**|**int**|함수의 개체 id입니다.|  
|**type**|**char(2)**|개체의 유형: FN = 스칼라 반환 함수|  
|**type_desc**|**nvarchar(60)**|개체 유형에 대 한 설명: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|이 함수 내에서 실행 된 **dm_exec_query_stats** 의 쿼리와 상호 연결 하는 데 사용할 수 있습니다.|  
|**plan_handle**|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값은 **dm_exec_cached_plans** 동적 관리 뷰와 함께 사용할 수 있습니다.<br /><br /> 고유 하 게 컴파일된 함수가 메모리 최적화 테이블을 쿼리하면 항상 0x000입니다.|  
|**cached_time**|**datetime**|함수가 캐시에 추가 된 시간입니다.|  
|**last_execution_time**|**datetime**|함수가 마지막으로 실행 된 시간입니다.|  
|**execution_count**|**bigint**|함수가 마지막으로 컴파일된 이후 실행 된 횟수입니다.|  
|**total_worker_time**|**bigint**|이 함수가 컴파일된 이후 실행 되는 동안 사용 된 총 CPU 시간 (마이크로초)입니다.<br /><br /> 고유 하 게 컴파일된 함수에 대해 많은 실행이 1 밀리초 미만으로 소요 되는 경우 **total_worker_time** 정확 하지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|함수가 마지막으로 실행 되었을 때 사용 된 CPU 시간 (마이크로초)입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|단일 실행 중에이 함수가 사용한 최소 CPU 시간 (마이크로초)입니다. <sup>1</sup>|  
|**max_worker_time**|**bigint**|단일 실행 중이 함수가 사용한 최대 CPU 시간 (마이크로초)입니다. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|이 함수가 컴파일된 이후 실행 될 때 수행 된 총 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|함수가 마지막으로 실행 되었을 때 수행 된 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중이 함수가 수행한 최소 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|단일 실행 중이 함수가 수행한 최대 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|이 함수가 컴파일된 이후 실행 될 때 수행 된 총 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|계획이 마지막으로 실행될 때 변경된 버퍼 풀 페이지 수입니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중이 함수가 수행한 최소 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중이 함수가 수행한 최대 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|이 함수가 컴파일된 이후 실행 될 때 수행 된 총 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|함수가 마지막으로 실행 되었을 때 수행 된 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중이 함수가 수행한 최소 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|단일 실행 중이 함수가 수행한 최대 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_elapsed_time**|**bigint**|이 함수의 실행을 완료 하는 데 소요 된 총 경과 시간 (마이크로초)입니다.|  
|**last_elapsed_time**|**bigint**|가장 최근에이 함수의 실행을 완료 하는 데 소요 된 경과 시간 (마이크로초)입니다.|  
|**min_elapsed_time**|**bigint**|이 함수의 실행을 완료 하는 데 소요 된 최소 경과 시간 (마이크로초)입니다.|  
|**max_elapsed_time**|**bigint**|이 함수의 실행을 완료 하는 데 소요 된 최대 경과 시간 (마이크로초)입니다.|  
|**total_page_server_reads**|**bigint**|이 함수가 컴파일된 이후 실행 될 때 수행 된 총 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL Database Hyperscale.|  
|**last_page_server_reads**|**bigint**|함수가 마지막으로 실행 되었을 때 수행 된 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL Database Hyperscale.|  
|**min_page_server_reads**|**bigint**|단일 실행 중이 함수가 수행한 최소 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL Database Hyperscale.|  
|**max_page_server_reads**|**bigint**|단일 실행 중이 함수가 수행한 최대 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL Database Hyperscale.|
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
