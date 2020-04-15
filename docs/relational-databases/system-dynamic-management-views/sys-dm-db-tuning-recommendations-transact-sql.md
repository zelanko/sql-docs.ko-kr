---
title: sys.dm_db_tuning_recommendations (거래-SQL) | 마이크로 소프트 문서
description: SQL Server 및 Azure SQL Database에서 잠재적인 성능 문제 및 권장 수정 사항을 찾는 방법을 알아봅니다.
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285523"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_db 튜닝\_권장 사항(거래-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  권장 사항 조정에 대한 자세한 정보를 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보가 노출되지 않도록 연결된 테넌트에 속하지 않는 데이터가 포함된 모든 행이 필터링됩니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| **(이름)** | **nvarchar(4000)** | 권장 사항의 고유한 이름입니다. |
| **종류** | **nvarchar(4000)** | 예를 들어 권장 사항을 생성한 자동 튜닝 옵션의 이름입니다.`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 이 권장 사항이 제공된 이유. |
| **이후\_유효합니다.** | **datetime2** | 이 권장 사항이 처음 생성되었습니다. |
| **마지막\_새로 고침** | **datetime2** | 이 권장 사항이 마지막으로 생성된 시간입니다. |
| **상태** | **nvarchar(4000)** | 권장 사항의 상태를 설명하는 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br />-   `currentValue`- 권장 사항의 현재 상태.<br />-   `reason`- 권장 사항이 현재 상태에 있는 이유를 설명하는 상수입니다.|
| **\_실행 가능한\_작업입니다.** | **bit** | 1 = 권장 사항은 스크립트를 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 통해 데이터베이스에 대해 실행할 수 있습니다.<br />0 = 데이터베이스에 대해 권장 사항을 실행할 수 없습니다(예: 정보만 또는 되돌릴 수 있는 권장 사항) |
| **반향\_가능한\_조치입니다.** | **bit** | 1 = 권장 사항을 데이터베이스 엔진에서 자동으로 모니터링하고 되돌릴 수 있습니다.<br />0 = 권장 사항을 자동으로 모니터링하고 되돌릴 수 없습니다. 대부분의 &quot;실행 가능한&quot; 작업은 &quot;반향이&quot;될 것입니다. |
| **실행\_\_작업\_시작 시간** | **datetime2** | 권장 사항이 적용되는 날짜입니다. |
| **작업\_\_지속 시간 실행** | **time** | 실행 작업의 기간입니다. |
| **에서\_\_시작된\_작업을 실행합니다.** | **nvarchar(4000)** | `User`= 사용자가 권장 사항에 수동으로 강제 계획을 강제합니다. <br /> `System`= 시스템이 자동으로 권장 사항을 적용했습니다. |
| **실행\_\_작업\_시작 시간** | **datetime2** | 권장 사항이 적용된 날짜입니다. |
| **작업\_\_시작\_시간 되돌리기** | **datetime2** | 권장 사항이 되돌린 날짜입니다. |
| **작업\_\_지속 시간 되돌리기** | **time** | 되돌리기 작업의 기간입니다. |
| **에서\_시작된\_\_작업 되돌리기** | **nvarchar(4000)** | `User`= 사용자가 수동으로 강제되지 않은 권장 계획입니다. <br /> `System`= 시스템이 자동으로 권장 사항을 되돌렸습니다. |
| **작업\_\_시작\_시간 되돌리기** | **datetime2** | 권장 사항이 되돌린 날짜입니다. |
| **평점** | **Int** | 0-100 척도에서 이 권장 사항에 대한 예상 값/영향(클수록 좋습니다). |
| **세부 정보** | **nvarchar (최대)** | 권장 사항에 대한 자세한 내용을 포함하는 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br /><br />`planForceDetails`<br />-    `queryId`-\_회귀 된 쿼리의 쿼리 ID입니다.<br />-    `regressedPlanId`- 회귀 계획의 plan_id.<br />-   `regressedPlanExecutionCount`- 회귀 계획이 감지되기 전에 회귀 계획이 있는 쿼리의 실행 수입니다.<br />-    `regressedPlanAbortedCount`- 회귀 계획의 실행 중에 감지된 오류 수입니다.<br />-    `regressedPlanCpuTimeAverage`- 회귀 쿼리가 회귀 쿼리에서 소비한 평균 CPU 시간(마이크로 초)입니다.<br />-    `regressedPlanCpuTimeStddev`- 회귀가 감지되기 전에 회귀 쿼리에 의해 소비되는 CPU 시간의 표준 편차입니다.<br />-    `recommendedPlanId`- 강제해야 계획의 plan_id.<br />-   `recommendedPlanExecutionCount`- 회귀가 감지되기 전에 강제로 수행해야 하는 계획이 있는 쿼리 실행 수입니다.<br />-    `recommendedPlanAbortedCount`- 강제해야 할 계획을 실행하는 동안 감지 된 오류의 수입니다.<br />-    `recommendedPlanCpuTimeAverage`- 강제해야 하는 계획으로 실행된 쿼리에서 소비되는 평균 CPU 시간(마이크로 초)입니다(회귀가 감지되기 전에 계산됨).<br />-    `recommendedPlanCpuTimeStddev`회귀가 검색되기 전에 회귀 쿼리에서 사용한 CPU 시간의 표준 편차입니다.<br /><br />`implementationDetails`<br />-  `method`- 회귀를 수정하는 데 사용해야 하는 방법. 값은 `TSql`항상 .<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]권장 계획을 강제로 실행해야 하는 스크립트입니다. |
  
## <a name="remarks"></a>설명  
 반환되는 `sys.dm_db_tuning_recommendations` 정보는 데이터베이스 엔진이 잠재적인 쿼리 성능 회귀를 식별하고 유지되지 않을 때 업데이트됩니다. 권장 사항은 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작될 때까지만 유지됩니다. 데이터베이스 관리자는 서버 를 재활용한 후에도 유지하려는 경우 조정 권장 사항의 백업 복사본을 주기적으로 만들어야 합니다. 

 `currentValue`열의 `state` 필드에는 다음 값이 있을 수 있습니다.
 
 | 상태 | Description |
 |--------|-------------|
 | `Active` | 권장 사항이 활성 상태이며 아직 적용되지 않습니다. 사용자는 권장 스크립트를 받아 수동으로 실행할 수 있습니다. |
 | `Verifying` | 권장 사항이 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 적용되고 내부 확인 프로세스는 강제 계획의 성능을 회귀 계획과 비교합니다. |
 | `Success` | 권장 사항이 성공적으로 적용됩니다. |
 | `Reverted` | 성능이 크게 향상되지 않으므로 권장 사항이 되돌아갑니다. |
 | `Expired` | 권장 사항이 만료되어 더 이상 적용할 수 없습니다. |

열에 있는 `state` JSON 문서에는 현재 상태의 권장 사항이 권장 되는 이유를 설명하는 이유가 포함되어 있습니다. 이유 필드의 값은 다음과 같은 것일 수 있습니다. 

| 이유 | 설명 |
|--------|-------------|
| `SchemaChanged` | 참조된 테이블의 스키마가 변경되어 권장 사항이 만료되었습니다. 새 스키마에서 새 쿼리 계획 회귀가 검색되면 새 권장 사항이 만들어집니다. |
| `StatisticsChanged`| 참조된 테이블의 통계 변경으로 인해 권장 사항이 만료되었습니다. 새 통계에 따라 새 쿼리 계획 회귀가 검색되면 새 권장 사항이 만들어집니다. |
| `ForcingFailed` | 권장 계획은 쿼리에 강제할 수 없습니다. `last_force_failure_reason` [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 보기에서 실패의 원인을 찾습니다. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`옵션은 확인 프로세스 중에 사용자가 비활성화합니다. [Transact-SQL&#41;문과 &#40;데이터베이스 set AUTOMATIC_TUNING ALTER 데이터베이스 set을](../../t-sql/statements/alter-database-transact-sql-set-options.md) 사용하여 옵션을 사용하거나 `[details]` `FORCE_LAST_GOOD_PLAN` 열의 스크립트를 사용하여 계획을 수동으로 강제합니다. |
| `UnsupportedStatementType` | 계획은 쿼리에 강제할 수 없습니다. 지원되지 않는 쿼리의 예로는 커서 `INSERT BULK` 및 명령문이 있습니다. |
| `LastGoodPlanForced` | 권장 사항이 성공적으로 적용됩니다. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]잠재적인 성능 회귀를 식별했지만 `FORCE_LAST_GOOD_PLAN` 옵션이 활성화되지 않음 - [Transact-SQL&#41;&#40;데이터베이스 set AUTOMATIC_TUNING ALTER ](../../t-sql/statements/alter-database-transact-sql-set-options.md)를 참조하십시오. 권장 사항을 수동으로 `FORCE_LAST_GOOD_PLAN` 적용하거나 옵션을 사용하도록 설정합니다. |
| `VerificationAborted`| 다시 시작하거나 쿼리 저장소 정리로 인해 확인 프로세스가 중단됩니다. |
| `VerificationForcedQueryRecompile`| 성능이 크게 향상되지 않아 쿼리가 다시 컴파일됩니다. |
| `PlanForcedByUser`| 사용자는 수동으로 [sp_query_store_force_plan &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) 절차를 사용하여 계획을 강제로. 사용자가 명시적으로 일부 계획을 강제로 적용하기로 결정한 경우 데이터베이스 엔진은 권장 사항을 적용하지 않습니다. |
| `PlanUnforcedByUser` | 사용자는 [&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) 절차를 sp_query_store_unforce_plan 사용하여 계획을 수동으로 강제 해제했습니다. 사용자가 권장 계획을 명시적으로 되돌렸기 때문에 데이터베이스 엔진은 현재 계획을 계속 사용하고 나중에 일부 계획 회귀가 발생하는 경우 새 권장 사항을 생성합니다. |

 세부 정보 열의 통계에는 런타임 계획 통계(예: 현재 CPU 시간)가 표시되지 않습니다. 권장 사항 세부 정보는 회귀 검색 시 수행되며 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 확인된 성능 회귀 이유를 설명합니다. 쿼리 `regressedPlanId` `recommendedPlanId` 저장소 [카탈로그 보기를](../../relational-databases/performance/how-query-store-collects-data.md) 쿼리하여 정확한 런타임 계획 통계를 찾습니다.

## <a name="examples-of-using-tuning-recommendations-information"></a>조정 권장 사항 정보 사용의 예  

### <a name="example-1"></a>예 1
다음은 지정된 쿼리에 대한 좋은 계획을 강제하는 생성된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 가져옵니다.  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>예제 2
다음은 주어진 쿼리에 대한 좋은 계획과 예상 이득에 대한 추가 정보를 강제하는 생성된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 가져옵니다.

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

### <a name="example-3"></a>예제 3
다음은 지정된 쿼리에 대한 좋은 계획과 쿼리 저장소에 저장된 쿼리 계획 및 쿼리 계획을 포함하는 추가 정보를 강제하는 생성된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 가져옵니다.

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

권장 사항 보기에서 값을 쿼리하는 데 사용할 수 있는 [JSON](../../relational-databases/json/index.md) 함수에 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]대한 자세한 내용은 에서 JSON 지원을 참조하십시오.
  
## <a name="permissions"></a>사용 권한  

에서 `VIEW SERVER STATE` 사용 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]권한이 필요합니다.   
에서 `VIEW DATABASE STATE` 데이터베이스에 대한 권한이 필요합니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]   

## <a name="see-also"></a>참고 항목  
 [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;거래 SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;거래 -SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 지원](../../relational-databases/json/index.md)
 
