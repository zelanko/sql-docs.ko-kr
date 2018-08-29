---
title: sys.query_store_query (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2837f590d6dcfc0cf260012c18834768059ce9ae
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062016"
---
# <a name="sysquerystorequery-transact-sql"></a>sys.query_store_query (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  쿼리 및 해당 관련 된 전체 집계 된 런타임 실행 통계에 대 한 정보를 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|기본 키입니다.|  
|**query_text_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)합니다.|  
|**object_id**|**bigint**|쿼리가 포함 된 데이터베이스 개체의 ID입니다 (저장 프로시저, 트리거, CLR UDF/UDAgg, 등.). 쿼리는 데이터베이스 개체 (임시 쿼리)의 일부로 실행 되지 않으면 0입니다.|  
|**batch_sql_handle**|**varbinary(64)**|문 일괄 처리 쿼리 ID의 일부입니다. 임시 테이블 또는 테이블 변수 쿼리가 참조 하는 경우에 채워집니다.|  
|**query_hash**|**binary(8)**|논리 쿼리 트리를 기반으로 개별 쿼리의 MD5 해시입니다. 최적화 프로그램 힌트를 포함합니다.|  
|**is_internal_query**|**bit**|쿼리는 내부적으로 생성 되었습니다.|  
|**query_parameterization_type**|**tinyint**|매개 변수화의 종류:<br /><br /> 0 – 없음<br /><br /> 1-사용자<br /><br /> 2 – 단순<br /><br /> 3 – 강제|  
|**query_parameterization_type_desc**|**nvarchar(60)**|매개 변수화 형식에 대 한 텍스트 설명입니다.|  
|**initial_compile_start_time**|**datetimeoffset**|시작 시간을 컴파일하십시오.|  
|**last_compile_start_time**|**datetimeoffset**|시작 시간을 컴파일하십시오.|  
|**last_execution_time**|**datetimeoffset**|마지막 실행 시간을 참조 마지막 쿼리/계획의 종료 시간입니다.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|쿼리 된 마지막 시간을 사용 하는 데는 마지막 SQL 일괄 처리의 핸들입니다. 입력으로 제공할 수 있습니다 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 일괄 처리의 전체 텍스트를 가져옵니다.|  
|**last_compile_batch_offset_start**|**bigint**|Last_compile_batch_sql_handle 함께 sys.dm_exec_sql_text를 제공할 수 있는 정보입니다.|  
|**last_compile_batch_offset_end**|**bigint**|Last_compile_batch_sql_handle 함께 sys.dm_exec_sql_text를 제공할 수 있는 정보입니다.|  
|**count_compiles**|**bigint**|컴파일 통계입니다.|  
|**avg_compile_duration**|**float**|컴파일 통계 (마이크로초)에서입니다.|  
|**last_compile_duration**|**bigint**|컴파일 통계 (마이크로초)에서입니다.|  
|**avg_bind_duration**|**float**|바인딩 통계 (마이크로초)에서입니다.|  
|**last_bind_duration**|**bigint**|바인딩 통계입니다.|  
|**avg_bind_cpu_time**|**float**|바인딩 통계입니다.|  
|**last_bind_cpu_time**|**bigint**|바인딩 통계입니다.|  
|**avg_optimize_duration**|**float**|최적화 통계 (마이크로초)에서입니다.|  
|**last_optimize_duration**|**bigint**|최적화 된 통계입니다.|  
|**avg_optimize_cpu_time**|**float**|최적화 통계 (마이크로초)에서입니다.|  
|**last_optimize_cpu_time**|**bigint**|최적화 된 통계입니다.|  
|**avg_compile_memory_kb**|**float**|메모리 통계를 컴파일하십시오.|  
|**last_compile_memory_kb**|**bigint**|메모리 통계를 컴파일하십시오.|  
|**max_compile_memory_kb**|**bigint**|메모리 통계를 컴파일하십시오.|  
|**is_clouddb_internal_query**|**bit**|항상 0에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온-프레미스입니다.|  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
