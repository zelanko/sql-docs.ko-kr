---
title: sys. query_store_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc78decc0c911376b61cc429ba538be11cbaded6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831440"
---
# <a name="sysquery_store_plan-transact-sql"></a>sys.query_store_plan(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  쿼리와 관련 된 각 실행 계획에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|기본 키입니다.|  
|**query_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;query_store_query ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)에 조인 합니다.|  
|**plan_group_id**|**bigint**|계획 그룹의 ID입니다. 커서 쿼리에는 일반적으로 여러 (채우기 및 페치) 계획이 필요 합니다. 함께 컴파일되는 채우기 및 인출 계획은 동일한 그룹에 있습니다.<br /><br /> 0은 계획이 그룹에 없음을 의미 합니다.|  
|**engine_version**|**nvarchar(32)**|**' 주. 부. 빌드. 수정 버전 '** 형식의 계획을 컴파일하는 데 사용 되는 엔진의 버전입니다.|  
|**compatibility_level**|**smallint**|쿼리에서 참조 되는 데이터베이스의 데이터베이스 호환성 수준입니다.|  
|**query_plan_hash**|**binary (8)**|개별 계획의 MD5 해시입니다.|  
|**query_plan**|**nvarchar(max)**|쿼리 계획에 대 한 실행 계획 XML입니다.|  
|**is_online_index_plan**|**bit**|온라인 인덱스 작성 중에 요금제를 사용 했습니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**is_trivial_plan**|**bit**|요금제는 쿼리 최적화 프로그램의 0 단계에서 출력 되는 간단한 계획입니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**is_parallel_plan**|**bit**|계획이 병렬 계획입니다. <br/>**참고:** Azure SQL Data Warehouse은 항상 1을 반환 합니다.|  
|**is_forced_plan**|**bit**|사용자가 저장 프로시저 **sys. sp_query_store_force_plan**를 실행 하면 계획이 강제로 표시 됩니다. 메커니즘을 강제 적용 하면 **query_id**에서 참조 하는 쿼리에 정확히이 계획이 사용 되는 것을 *보장할 수 없습니다* . 계획 강제 적용을 수행 하면 쿼리가 다시 컴파일되고 일반적으로 **plan_id**에서 참조 하는 계획에 대해 정확 하 게 동일 하거나 유사한 계획을 생성 합니다. 계획 강제 적용에 성공 하지 않으면 **force_failure_count** 증가 하 고 **last_force_failure_reason** 실패 원인으로 채워집니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**is_natively_compiled**|**bit**|계획에는 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저가 포함 됩니다. (0 = FALSE, 1 = TRUE). <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**force_failure_count**|**bigint**|이 계획을 강제로 적용 하지 못한 횟수입니다. 쿼리가 다시 컴파일되는 경우에만 증가 시킬 수 있습니다 (*모든 실행에는 아님*). **Is_plan_forced** 이 **FALSE** 에서 **TRUE**로 변경 될 때마다 0으로 다시 설정 됩니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**last_force_failure_reason**|**int**|계획 강제 적용에 실패 한 이유입니다.<br /><br /> 0: 오류가 발생 하지 않습니다. 그렇지 않으면 강제 실패를 일으킨 오류의 오류 번호<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<기타 값>: GENERAL_FAILURE <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Last_force_failure_reason_desc에 대 한 텍스트 설명입니다.<br /><br /> ONLINE_INDEX_BUILD: 쿼리에서 대상 테이블에 온라인으로 작성 되는 인덱스를 포함 하는 동안 데이터를 수정 하려고 합니다.<br /><br /> INVALID_STARJOIN: 계획에 잘못 된 StarJoin 사양이 있습니다.<br /><br /> TIME_OUT: 최적화 프로그램이 강제 계획으로 지정 된 계획을 검색 하는 동안 허용 되는 작업 수를 초과 했습니다.<br /><br /> NO_DB: 계획에 지정 된 데이터베이스가 없습니다.<br /><br /> HINT_CONFLICT: 계획이 쿼리 힌트와 충돌 하므로 쿼리를 컴파일할 수 없습니다.<br /><br /> DQ_NO_FORCING_SUPPORTED: 계획은 분산 쿼리 또는 전체 텍스트 작업 사용과 충돌 하므로 쿼리를 실행할 수 없습니다.<br /><br /> NO_PLAN: 강제 계획이 쿼리에 대해 유효한 지 확인할 수 없으므로 쿼리 프로세서에서 쿼리 계획을 생성할 수 없습니다.<br /><br /> NO_INDEX: 계획에 지정 된 인덱스가 더 이상 존재 하지 않습니다.<br /><br /> VIEW_COMPILE_FAILED: 계획에서 참조 되는 인덱싱된 뷰의 문제로 인해 쿼리 계획을 강제 실행할 수 없습니다.<br /><br /> GENERAL_FAILURE: 일반 강제 오류 (위의 이유로 다루지 않음) <br/>**참고:** Azure SQL Data Warehouse는 항상 *NONE*을 반환 합니다.|  
|**count_compiles**|**bigint**|컴파일 통계를 계획 합니다.|  
|**initial_compile_start_time**|**datetimeoffset**|컴파일 통계를 계획 합니다.|  
|**last_compile_start_time**|**datetimeoffset**|컴파일 통계를 계획 합니다.|  
|**last_execution_time**|**datetimeoffset**|마지막 실행 시간은 쿼리/계획의 마지막 종료 시간을 나타냅니다.|  
|**avg_compile_duration**|**float**|컴파일 통계를 계획 합니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**last_compile_duration**|**bigint**|컴파일 통계를 계획 합니다. <br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**plan_forcing_type**|**int**|계획 강제 적용 유형입니다.<br /><br />0: 없음<br /><br />1: 수동<br /><br />2: 자동|  
|**plan_forcing_type_desc**|**nvarchar(60)**|Plan_forcing_type에 대 한 텍스트 설명입니다.<br /><br />없음: 계획을 강제 적용 하지 않습니다.<br /><br />수동: 사용자가 강제 계획<br /><br />AUTO: 자동 조정으로 강제 계획|  

## <a name="plan-forcing-limitations"></a>계획 강제 적용 제한 사항
쿼리 저장소에는 쿼리 최적화 프로그램이 특정 실행 계획을 사용하도록 적용하는 메커니즘이 있습니다. 그러나 계획이 적용되지 않도록 하는 몇 가지 제한 사항이 있습니다. 

첫째, 계획에 다음과 같은 구성이 포함된 경우
* Insert bulk 문
* 외부 테이블에 대한 참조
* 분산 쿼리 또는 전체 텍스트 작업
* 전역 쿼리 사용 
* 동적 또는 키 집합 커서 
* 잘못된 스타 조인 사양 

> [!NOTE]
> Azure SQL Database 및 SQL Server 2019 지원 계획은 정적 및 빠른 전방 커서에 적용 됩니다.

둘째, 계획에 사용되는 개체를 더 이상 사용할 수 없는 경우
* 데이터베이스(계획이 발생한 데이터베이스가 더 이상 없는 경우)
* 인덱스(더 이상 없거나 사용할 수 없는 경우)

마지막으로, 계획 자체에 문제가 있는 경우
* 쿼리에 적합하지 않음
* 쿼리 최적화 프로그램이 허용되는 작업 수를 초과함
* 잘못 구성된 계획 XML

## <a name="permissions"></a>사용 권한  
 **VIEW DATABASE STATE** 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
