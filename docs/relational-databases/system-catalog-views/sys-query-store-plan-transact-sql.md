---
title: sys.query_store_plan (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs: TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0950cf33d112d299de615a702d0fbac7cbfdc0e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreplan-transact-sql"></a>sys.query_store_plan (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  쿼리와 관련 된 각 실행 계획에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|기본 키입니다.|  
|**지정한 query_id**|**bigint**|외래 키입니다. 조인 [sys.query_store_query&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|계획 그룹의 ID입니다. 커서 쿼리에 일반적으로 여러 필요 (채우고 fetch) 계획 합니다. 함께 컴파일되는 인출 계획은 동일한 그룹을 채우고 있습니다.<br /><br /> 0 계획 그룹에 없는 것을 의미 합니다.|  
|**engine_version**|**nvarchar (32)**|계획을 컴파일하는 데 사용 하는 엔진의 버전 **'major.minor.build.revision'** 형식입니다.|  
|**compatibility_level**|**smallint**|쿼리에서 참조 되는 데이터베이스의 데이터베이스 호환성 수준입니다.|  
|**query_plan_hash**|**binary (8)**|각 계획의 MD5 해시입니다.|  
|**query_plan**|**nvarchar(max)**|쿼리 계획에 대 한 XML 실행 계획 합니다.|  
|**is_online_index_plan**|**bit**|온라인 인덱스 작성 하는 동안 계획을 사용 했습니다.|  
|**is_trivial_plan**|**bit**|계획은 trivial 계획 (쿼리 최적화 프로그램의 단계 0에서에서 출력).|  
|**is_parallel_plan**|**bit**|계획은 병렬입니다.|  
|**is_forced_plan**|**bit**|계획에는 사용자는 저장된 프로시저를 실행할 때 강제로 것으로 표시 되어 **sys.sp_query_store_force_plan**합니다. 강제 적용 메커니즘이 *작업이 반드시* 정확 하 게이 계획에서 참조 하는 쿼리에 대해 사용될지를 **query_id**합니다. 계획 강제 적용 하면 쿼리를 다시 컴파일해야 하 고 일반적으로 생성 정확히 동일 하거나 유사한 계획에서 참조 하는 계획에 **plan_id**합니다. 계획 강제 적용 성공 하지 않으면 **force_failure_count** 증가 하 고 **last_force_failure_reason** 실패 원인으로 채워집니다.|  
|**is_natively_compiled**|**bit**|계획에는 고유 하 게 컴파일된 메모리 액세스에 최적화 된 절차가 포함 됩니다. (0 = FALSE, 1 = TRUE).|  
|**force_failure_count**|**bigint**|이 계획을 강제 적용에 실패 한 번의 수입니다. 쿼리를 다시 컴파일할 경우에 증가 될 수 있습니다 (*모든 실행에 없는*). 그는 0으로 다시 설정 될 때마다 **is_plan_forced** 에서 변경 **FALSE** 를 **TRUE**합니다.|  
|**last_force_failure_reason**|**int**|계획 강제 적용에 실패 한 이유입니다.<br /><br /> 0: 없음 오류가 발생할 경우 실패를 강제로 발생 시킨 오류의 그렇지 않으면 오류 번호<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<다른 값 >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar (128)**|Last_force_failure_reason_desc의 텍스트 설명입니다.<br /><br /> ONLINE_INDEX_BUILD: 쿼리를 대상 테이블에 인덱스를 온라인으로 작성 하는 동안에 데이터를 수정 하기 위한<br /><br /> INVALID_STARJOIN: 계획에 잘못 된 StarJoin 지정<br /><br /> TIME_OUT: 초과 하는 최적화 프로그램 강제 계획에 따라 지정 된 계획을 검색 하는 동안 허용된 작업 수<br /><br /> NO_DB: 계획에 지정 된 데이터베이스가 존재 하지 않는<br /><br /> HINT_CONFLICT: 쿼리 컴파일할 수 없습니다 계획 쿼리 힌트와 충돌 하므로<br /><br /> DQ_NO_FORCING_SUPPORTED: 계획의 분산된 쿼리 또는 전체 텍스트 작업 사용과 충돌 하므로 쿼리를 실행할 수 없습니다.<br /><br /> NO_PLAN: 쿼리 프로세서 수 쿼리 계획을 생성할 쿼리에 대 한 유효한 것으로 강제 계획을 확인할 수 없습니다.<br /><br /> NO_INDEX: 더 이상 계획에 지정 된 인덱스가 없습니다.<br /><br /> VIEW_COMPILE_FAILED: 계획에서 참조 되는 인덱싱된 뷰에서 문제 때문에 쿼리 계획을 적용할 수 없습니다.<br /><br /> GENERAL_FAILURE: 일반 강제 오류 (위의 이유를 다루지 않음)|  
|**count_compiles**|**bigint**|컴파일 통계를 계획 합니다.|  
|**initial_compile_start_time**|**datetimeoffset**|컴파일 통계를 계획 합니다.|  
|**last_compile_start_time**|**datetimeoffset**|컴파일 통계를 계획 합니다.|  
|**last_execution_time**|**datetimeoffset**|마지막 실행 시간을 참조 마지막 쿼리/계획의 종료 시간입니다.|  
|**avg_compile_duration**|**float**|컴파일 통계를 계획 합니다.|  
|**last_compile_duration**|**bigint**|컴파일 통계를 계획 합니다.|  
  
## <a name="plan-forcing-limitations"></a>계획 제한 사항 적용
쿼리 저장소에는 쿼리 최적화 프로그램이 특정 실행 계획을 사용하도록 적용하는 메커니즘이 있습니다. 그러나 계획이 적용되지 않도록 하는 몇 가지 제한 사항이 있습니다. 

첫째, 계획에 다음과 같은 구성이 포함된 경우
* Insert bulk 문
* Insert bulk 문
* 외부 테이블에 대한 참조
* 분산 쿼리 또는 전체 텍스트 작업
* 전역 쿼리 사용 
* 커서
* 잘못된 스타 조인 사양 

둘째, 계획에 사용되는 개체를 더 이상 사용할 수 없는 경우
* 데이터베이스(계획이 발생한 데이터베이스가 더 이상 없는 경우)
* 인덱스(더 이상 없거나 사용할 수 없는 경우)

마지막으로, 계획 자체에 문제가 있는 경우
* 쿼리에 적합하지 않음
* 쿼리 최적화 프로그램이 허용되는 작업 수를 초과함
* 잘못 구성된 계획 XML

## <a name="permissions"></a>Permissions  
 필요는 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.database_query_store_options&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
