---
title: sys.dm_db_tuning_recommendations (Transact SQL) | Microsoft Docs
description: 잠재적인 성능 문제를 확인 하는 방법 자세히 알아보고 SQL Server 및 Azure SQL 데이터베이스에서 수정 권장
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
caps.latest.revision: 37
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d4f783c82d92aa0837ea9fbb90f9b3d2afc8c8d
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_튜닝\_권장 사항 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  튜닝 권장 구성에 대 한 자세한 정보를 반환 합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | 권장 구성의 고유 이름입니다. |
| **type** | **nvarchar(4000)** | 예를 들어 권장 생성 되는 자동 튜닝 옵션의 이름 `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 이 권장 사항을 제공 된 이유는 이유입니다. |
| **valid\_since** | **datetime2** | 처음으로이 권장 사항을 생성 되었습니다. |
| **last\_refresh** | **datetime2** | 이 권장 구성은 생성 된 마지막 시간입니다. |
| **상태** | **nvarchar(4000)** | 권장 구성의 상태를 설명 하는 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br />-   `currentValue` -권장 구성의 현재 상태입니다.<br />-   `reason` – 현재 상태에 권장 된 이유를 설명 하는 상수입니다.|
| **is\_executable\_action** | **bit** | 1 = 권장 사항을 통해 데이터베이스에 대해 실행할 수 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 스크립트입니다.<br />0 = 데이터베이스에 대해 권장 구성을 실행할 수 없습니다 (예: 정보 또는 되돌린에 권장 사항) |
| **is\_revertable\_action** | **bit** | 1 = 권장을 자동으로 모니터링 하 고 데이터베이스 엔진에 의해 설정 되었으며 수 있습니다.<br />0 = 권장을 자동으로 모니터링 하 고 되돌릴 수 없습니다. 대부분 &quot;실행&quot; 동작이 &quot;revertable&quot;합니다. |
| **execute\_action\_start\_time** | **datetime2** | 권장 구성 적용 되는 날짜입니다. |
| **execute\_action\_duration** | **time** | Execute 동작은의 기간입니다. |
| **execute\_action\_initiated\_by** | **nvarchar(4000)** | `User` = 수동으로 사용자 권장 구성에 대 한 계획을 강제합니다. <br /> `System` = 시스템 권장 구성 자동 적용 됩니다. |
| **execute\_action\_initiated\_time** | **datetime2** | 권장 구성 적용 된 날짜입니다. |
| **revert\_action\_start\_time** | **datetime2** | 권장 사항이 되돌려 날짜입니다. |
| **revert\_action\_duration** | **time** | 되돌리기 작업의 기간입니다. |
| **revert\_action\_initiated\_by** | **nvarchar(4000)** | `User` = 권장된 계획을 수동으로 unforced 사용자입니다. <br /> `System` = 시스템은 권장 구성을 자동으로 되돌려집니다. |
| **revert\_action\_initiated\_time** | **datetime2** | 권장 사항이 되돌려 날짜입니다. |
| **score** | **int** | 예상 값/영향에 대 한이 0-100을 위한이 권장 크기 조정 (클수록 좋습니다) |
| **details** | **nvarchar(max)** | 권장 구성에 대 한 자세한 정보가 포함 된 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br /><br />`planForceDetails`<br />-    `queryId` -쿼리\_이전 상태로 되돌아간된 쿼리의 id입니다.<br />-    `regressedPlanId` -이전 상태로 되돌아간된 계획의 plan_id 합니다.<br />-   `regressedPlanExecutionCount` -수가 회귀 분석 하기 전에 이전 상태로 되돌아간된 계획을 사용 하 여 쿼리 실행 될 때 검색 됩니다.<br />-    `regressedPlanAbortedCount` -이전 상태로 되돌아간된 계획의 실행 하는 동안 검색 된 오류의 수입니다.<br />-    `regressedPlanCpuTimeAverage` -회귀는 감지 하기 전에 이전 상태로 되돌아간 쿼리에서 사용 평균 CPU 시간입니다.<br />-    `regressedPlanCpuTimeStddev` -회귀 분석 하기 전에 이전 상태로 되돌아간된 쿼리에 사용 된 CPU 시간 표준 편차를 검색 했습니다.<br />-    `recommendedPlanId` -강제로 해야 하는 계획의 plan_id 합니다.<br />-   `recommendedPlanExecutionCount`-회귀는 감지 하기 전에 강제 해야 하는 계획에 쿼리 실행 오류 수입니다.<br />-    `recommendedPlanAbortedCount` -계획을 강제로 실행 하는 동안 검색 된 오류의 수입니다.<br />-    `recommendedPlanCpuTimeAverage` -평균 CPU 시간 (회귀는 감지 하기 전에 계산 됨)을 강제로 계획으로 실행 되는 쿼리에 사용 합니다.<br />-    `recommendedPlanCpuTimeStddev` 회귀 분석 하기 전에 이전 상태로 되돌아간된 쿼리에 사용 된 CPU 시간의 표준 편차를 검색 했습니다.<br /><br />`implementationDetails`<br />-  `method` -해결 회귀를 사용 해야 하는 메서드. 값은 항상 `TSql`합니다.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 권장 되는 계획을 강제로 실행 하는 스크립트입니다. |
  
## <a name="remarks"></a>주의  
 반환 된 정보 `sys.dm_db_tuning_recommendations` 데이터베이스 엔진 잠재적 쿼리 성능 저하를 식별 하 고 유지 되지 않습니다 때 업데이트 됩니다. 권장 사항 까지만 유지 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작 합니다. 서버 재활용 후 유지 하려는 경우 데이터베이스 관리자가 정기적으로 튜닝 권장 구성의 백업 복사본을 만들어야 합니다. 

 `currentValue` 필드에 `state` 열 다음 값을 가질 수 있습니다.
 | 상태 | Description |
 |--------|-------------|
 | `Active` | 활성 상태 이며 아직 적용 되지 않았습니다. 것이 좋습니다. 사용자는 권장 구성 스크립트를 사용 하 고 수동으로 실행할 수 있습니다. |
 | `Verifying` | 권장 구성 적용 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 내부 확인 프로세스를 이전 상태로 되돌아간 계획과 강제 계획의 성능을 비교 하 고 있습니다. |
 | `Success` | 권장 구성은 성공적으로 적용 됩니다. |
 | `Reverted` | 없는 성능이 크게 향상 있기 때문에 권장이 되돌려집니다. |
 | `Expired` | 권장 사항 만료 되어 더 이상 적용할 수 없습니다. |

JSON 문서에 `state` 열 현재 상태에 권장 된 이유를 설명 하는 이유를 포함 합니다. 이유 필드의 값이 같을 수 있습니다. 

| 원인 | Description |
|--------|-------------|
| `SchemaChanged` | 권장 구성에는 참조 테이블의 스키마가 변경 되었기 때문에 만료 되었습니다. |
| `StatisticsChanged`| 권장 사항 참조 테이블에서 통계 변경으로 인해 만료 되었습니다. |
| `ForcingFailed` | 쿼리에서 권장된 계획을 강제 적용할 수 없습니다. 찾을 `last_force_failure_reason` 에 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 오류의 이유를 찾으려면 보기. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` 확인 프로세스 중 사용자가 옵션이 비활성화 됩니다. 사용 하도록 설정 `FORCE_LAST_GOOD_PLAN` 옵션을 사용 하 여 [데이터베이스 설정 AUTOMATIC_TUNING ALTER &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 문이나 강제 계획에 스크립트를 사용 하 여 수동으로 `[details]` 열입니다. |
| `UnsupportedStatementType` | 쿼리 계획을 강제 적용할 수 없습니다. 지원 되지 않는 쿼리의 예는 커서가 및 `INSERT BULK` 문. |
| `LastGoodPlanForced` | 권장 구성은 성공적으로 적용 됩니다. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 잠재적인 성능 저하를 식별 하지만 `FORCE_LAST_GOOD_PLAN` 옵션은 – 볼 [데이터베이스 설정 AUTOMATIC_TUNING ALTER &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)합니다. 권장 사항을 수동으로 적용 또는 사용 `FORCE_LAST_GOOD_PLAN` 옵션입니다. |
| `VerificationAborted`| 확인 프로세스를 다시 시작 또는 쿼리 저장소가 정리로 인해 중단 됩니다. |
| `VerificationForcedQueryRecompile`| 상당한 성능 향상에 있기 때문에 쿼리가 다시 컴파일됩니다. |
| `PlanForcedByUser`| 사용자는 수동으로 사용 하 여 계획 강제 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) 프로시저입니다. |
| `PlanUnforcedByUser` | 사용자 수동으로 강제 적용 해제할 사용 하 여 계획 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) 프로시저입니다. |

 세부 정보 열에서 통계 런타임 계획 통계 (예를 들어 현재 CPU 시간)을 표시 하지 않습니다. 권장 사항 세부 정보 회귀 검색의 시간에 수행 되 고 이유를 설명 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 성능 저하를 식별 합니다. 사용 하 여 `regressedPlanId` 및 `recommendedPlanId` 쿼리에 [쿼리 저장소 카탈로그 뷰](../../relational-databases/performance/how-query-store-collects-data.md) 정확한 런타임 계획 통계를 찾습니다.

## <a name="using-tuning-recommendations-information"></a>튜닝 권장 구성 정보를 사용 하 여  
 이 문제를 해결 하는 T-SQL 스크립트를 가져오지 다음 쿼리를 사용할 수 있습니다.  
 
```
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 권장 구성 보기에서 쿼리 값을 사용할 수 있는 JSON 함수에 대 한 자세한 내용은 참조 [JSON 지원](../../relational-databases/json/index.md) 에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]합니다.
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:  
 [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 지원](../../relational-databases/json/index.md)
 
