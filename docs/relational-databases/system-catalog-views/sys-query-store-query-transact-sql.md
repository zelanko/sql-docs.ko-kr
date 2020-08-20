---
description: sys. query_store_query (Transact-sql)
title: sys. query_store_query (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0908c3ad3995510eb7e5cf1509941b735235005e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460628"
---
# <a name="sysquery_store_query-transact-sql"></a>sys. query_store_query (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  쿼리와 관련 된 전체 집계 된 런타임 실행 통계에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|기본 키입니다.|  
|**query_text_id**|**bigint**|외래 키입니다. [Query_store_query_text &#40;transact-sql](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md) 에 조인&#41;|  
|**context_settings_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;query_context_settings ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)에 조인 합니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**object_id**|**bigint**|쿼리가 속한 데이터베이스 개체의 ID입니다 (저장 프로시저, 트리거, CLR UDF/UDAgg 등). 쿼리가 데이터베이스 개체 (임시 쿼리)의 일부로 실행 되지 않는 경우 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**batch_sql_handle**|**varbinary(64)**|쿼리가 속한 문 일괄 처리의 ID입니다. 쿼리가 임시 테이블 또는 테이블 변수를 참조 하는 경우에만 채워집니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 *NULL*을 반환 합니다.|  
|**query_hash**|**binary (8)**|논리적 쿼리 트리를 기반으로 하는 개별 쿼리의 MD5 해시입니다. 최적화 프로그램 힌트를 포함 합니다.|  
|**is_internal_query**|**bit**|쿼리가 내부적으로 생성 되었습니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**query_parameterization_type**|**tinyint**|매개 변수화의 종류:<br /><br /> 0 - 없음<br /><br /> 1-사용자<br /><br /> 2-단순<br /><br /> 3-강제<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**query_parameterization_type_desc**|**nvarchar(60)**|매개 변수화 형식에 대 한 텍스트 설명입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 *None*을 반환 합니다.|  
|**initial_compile_start_time**|**datetimeoffset**|컴파일 시작 시간입니다.|  
|**last_compile_start_time**|**datetimeoffset**|컴파일 시작 시간입니다.|  
|**last_execution_time**|**datetimeoffset**|마지막 실행 시간은 쿼리/계획의 마지막 종료 시간을 나타냅니다.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|쿼리가 마지막으로 사용 된 마지막 SQL 일괄 처리의 핸들입니다. 이 파일은 [dm_exec_sql_text &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 를 입력 하 여 일괄 처리의 전체 텍스트를 가져올 수 있습니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 *NULL*을 반환 합니다.|  
|**last_compile_batch_offset_start**|**bigint**|Last_compile_batch_sql_handle와 함께 dm_exec_sql_text에 제공할 수 있는 정보입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_compile_batch_offset_end**|**bigint**|Last_compile_batch_sql_handle와 함께 dm_exec_sql_text에 제공할 수 있는 정보입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**count_compiles**|**bigint**|컴파일 통계.<br/>**참고:** Azure SQL Data Warehouse은 항상 1을 반환 합니다.|  
|**avg_compile_duration**|**float**|컴파일 통계 (마이크로초)입니다.|  
|**last_compile_duration**|**bigint**|컴파일 통계 (마이크로초)입니다.|  
|**avg_bind_duration**|**float**|바인딩 통계 (마이크로초)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**last_bind_duration**|**bigint**|바인딩 통계.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**avg_bind_cpu_time**|**float**|바인딩 통계.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**last_bind_cpu_time**|**bigint**|바인딩 통계.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**avg_optimize_duration**|**float**|최적화 통계 (마이크로초)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_optimize_duration**|**bigint**|최적화 통계.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_optimize_cpu_time**|**float**|최적화 통계 (마이크로초)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_optimize_cpu_time**|**bigint**|최적화 통계.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_compile_memory_kb**|**float**|컴파일 메모리 통계입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_compile_memory_kb**|**bigint**|컴파일 메모리 통계입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_compile_memory_kb**|**bigint**|컴파일 메모리 통계입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**is_clouddb_internal_query**|**bit**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]온-프레미스의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
  
## <a name="permissions"></a>사용 권한  
 **VIEW DATABASE STATE** 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
