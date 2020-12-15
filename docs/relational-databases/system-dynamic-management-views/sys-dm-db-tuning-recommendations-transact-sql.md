---
title: sys.dm_db_tuning_recommendations (Transact-sql) | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 잠재적 성능 문제 및 권장 픽스를 찾는 방법에 대해 알아봅니다.
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
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cad75b88b14fd9bc64acbbd8b167619d3dbcc2e3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472884"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm \_ db \_ 튜닝 \_ 권장 구성 (transact-sql)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  튜닝 권장 구성에 대 한 자세한 정보를 반환 합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | 권장 사항의 고유한 이름입니다. |
| **type** | **nvarchar(4000)** | 권장 구성을 생성 한 자동 조정 옵션의 이름 (예:) `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 이 권장 사항이 제공 된 이유입니다. |
| **다음 \_ 이후 유효** | **datetime2** | 이 권장 구성이 처음으로 생성 된 시간입니다. |
| **마지막 \_ 새로 고침** | **datetime2** | 이 권장 구성이 마지막으로 생성 된 시간입니다. |
| **state** | **nvarchar(4000)** | 권장 사항의 상태를 설명 하는 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br />-   `currentValue` -권장 사항의 현재 상태입니다.<br />-   `reason` -권장 구성이 현재 상태에 있는 이유를 설명 하는 상수입니다.|
| **\_실행 가능 \_ 동작** | **bit** | 1 = 스크립트를 통해 데이터베이스에 대해 권장 사항을 실행할 수 있습니다 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] .<br />0 = 데이터베이스에 대해 권장 사항을 실행할 수 없습니다 (예: 정보 전용 또는 되돌린 권장 사항). |
| **\_revertable \_ 동작** | **bit** | 1 = 데이터베이스 엔진에서 권장 사항을 자동으로 모니터링 하 고 되돌릴 수 있습니다.<br />0 = 권장 사항을 자동으로 모니터링 하 고 되돌릴 수 없습니다. 대부분의 &quot; 실행 가능한 &quot; 작업은 &quot; revertable &quot; 입니다. |
| **\_작업 \_ 시작 \_ 시간 실행** | **datetime2** | 권장 사항이 적용 되는 날짜입니다. |
| **\_작업 실행 \_ 기간** | **time** | 실행 작업의 기간입니다. |
| **다음 \_ \_ 에서 시작한 \_ 작업 실행** | **nvarchar(4000)** | `User` = 권장 사항에서 사용자가 수동으로 강제 계획 합니다. <br /> `System` = 시스템 자동 적용 권장 사항 |
| **\_작업 \_ 시작 \_ 시간 실행** | **datetime2** | 권장 사항이 적용 된 날짜입니다. |
| **\_작업 \_ 시작 \_ 시간 되돌리기** | **datetime2** | 권장 사항이 되돌려 진 날짜입니다. |
| **\_작업 \_ 기간 되돌리기** | **time** | 되돌리기 작업의 기간입니다. |
| **\_시작한 작업 \_ 되돌리기 \_** | **nvarchar(4000)** | `User` = 사용자가 수동 권장 계획을 사용 하지 않습니다. <br /> `System` = 시스템이 권장 사항을 자동으로 되돌렸습니다. |
| **\_작업 \_ 시작 \_ 시간 되돌리기** | **datetime2** | 권장 사항이 되돌려 진 날짜입니다. |
| **점수** | **int** | 0-100 배율에 대 한이 권장 사항에 대 한 예상 값/영향 (보다 큼) |
| **대해** | **nvarchar(max)** | 권장 사항에 대 한 자세한 정보를 포함 하는 JSON 문서입니다. 다음 필드를 사용할 수 있습니다.<br /><br />`planForceDetails`<br />-    `queryId` - \_ 회귀 된 쿼리의 쿼리 id입니다.<br />-    `regressedPlanId` -회귀 된 계획의 plan_id입니다.<br />-   `regressedPlanExecutionCount` -회귀를 검색 하기 전에 재발 된 계획이 있는 쿼리 실행의 수입니다.<br />-    `regressedPlanAbortedCount` -회귀 된 계획을 실행 하는 동안 검색 된 오류 수입니다.<br />-    `regressedPlanCpuTimeAverage` -재발이 검색 되기 전에 재발 된 쿼리에서 사용한 평균 CPU 시간 (마이크로초)입니다.<br />-    `regressedPlanCpuTimeStddev` -재발이 검색 되기 전에 재발 된 쿼리에 사용 되는 CPU 시간의 표준 편차입니다.<br />-    `recommendedPlanId` -강제 적용 해야 하는 계획의 plan_id입니다.<br />-   `recommendedPlanExecutionCount`-회귀를 검색 하기 전에 강제 적용 해야 하는 계획을 포함 하는 쿼리 실행의 수입니다.<br />-    `recommendedPlanAbortedCount` -강제 적용 해야 하는 계획을 실행 하는 동안 검색 된 오류 수입니다.<br />-    `recommendedPlanCpuTimeAverage` -강제 적용 되어야 하는 계획을 사용 하 여 실행 되는 쿼리에서 사용 되는 평균 CPU 시간 (마이크로초)입니다 (회귀 검색 전에 계산).<br />-    `recommendedPlanCpuTimeStddev` 재발을 감지 하기 전에 재발 된 쿼리에 사용 되는 CPU 시간의 표준 편차입니다.<br /><br />`implementationDetails`<br />-  `method` -회귀를 수정 하는 데 사용 해야 하는 메서드입니다. 값은 항상 `TSql` 입니다.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 권장 계획을 적용 하기 위해 실행 해야 하는 스크립트입니다. |
  
## <a name="remarks"></a>설명  
 에서 반환 하 `sys.dm_db_tuning_recommendations` 는 정보는 데이터베이스 엔진이 잠재적인 쿼리 성능 회귀를 식별할 때 업데이트 되며 지속 되지 않습니다. 권장 사항은가 다시 시작 될 때 까지만 유지 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 데이터베이스 관리자는 서버 재활용 후에도 튜닝 권장 구성의 백업 복사본을 정기적으로 만들어야 합니다. 

 `currentValue``state`열의 필드 값은 다음과 같습니다.
 
 | 상태 | 설명 |
 |--------|-------------|
 | `Active` | 권장 사항이 활성 상태 이며 아직 적용 되지 않았습니다. 사용자는 권장 스크립트를 사용 하 여 수동으로 실행할 수 있습니다. |
 | `Verifying` | 권장 사항은에 의해 적용 되 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 고 내부 확인 프로세스는 강제 계획의 성능과 회귀 된 계획을 비교 합니다. |
 | `Success` | 권장 사항이 적용 되었습니다. |
 | `Reverted` | 성능이 크게 향상 되지 않으므로 권장 사항이 되돌려집니다. |
 | `Expired` | 권장 사항이 만료 되었으며 더 이상 적용할 수 없습니다. |

열의 JSON 문서에는 `state` 현재 상태의 권장 구성이 무엇 인지 설명 하는 이유가 포함 되어 있습니다. 이유 필드의 값은 다음과 같을 수 있습니다. 

| 이유 | 설명 |
|--------|-------------|
| `SchemaChanged` | 참조 된 테이블의 스키마가 변경 되어 권장 구성이 만료 되었습니다. 새 스키마에서 새 쿼리 계획 회귀를 검색 하면 새로운 권장 사항이 생성 됩니다. |
| `StatisticsChanged`| 참조 된 테이블의 통계 변경으로 인해 권장 구성이 만료 되었습니다. 새 통계를 기반으로 새 쿼리 계획 회귀를 검색 하면 새로운 권장 사항이 생성 됩니다. |
| `ForcingFailed` | 권장 계획은 쿼리에 강제 적용할 수 없습니다. `last_force_failure_reason`실패 이유를 확인 하려면 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 뷰에서를 찾습니다. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` 확인 프로세스 중에 사용자가 옵션을 사용할 수 없습니다. `FORCE_LAST_GOOD_PLAN` [ALTER database SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 문을 사용 하 여 옵션을 설정 하거나 열에서 스크립트를 사용 하 여 계획을 수동으로 적용 합니다 `[details]` . |
| `UnsupportedStatementType` | 쿼리에 대해 계획을 강제 적용할 수 없습니다. 지원 되지 않는 쿼리의 예로는 cursor와 `INSERT BULK` statement가 있습니다. |
| `LastGoodPlanForced` | 권장 사항이 적용 되었습니다. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 잠재적인 성능 회귀를 확인 했지만 `FORCE_LAST_GOOD_PLAN` 옵션을 사용할 수 없습니다. [ALTER database SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조 하십시오. 권장 사항을 수동으로 적용 하거나 `FORCE_LAST_GOOD_PLAN` 옵션을 사용 하도록 설정 합니다. |
| `VerificationAborted`| 다시 시작 또는 쿼리 저장소 정리로 인해 확인 프로세스가 중단 되었습니다. |
| `VerificationForcedQueryRecompile`| 성능이 크게 향상 되지 않으므로 쿼리가 다시 컴파일됩니다. |
| `PlanForcedByUser`| 사용자가 [sp_query_store_force_plan &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) 프로시저를 사용 하 여 수동으로 계획을 적용 했습니다. 사용자가 명시적으로 계획을 적용 하도록 결정 한 경우에는 데이터베이스 엔진에서 권장 사항을 적용 하지 않습니다. |
| `PlanUnforcedByUser` | 사용자가 [sp_query_store_unforce_plan &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) 프로시저를 사용 하 여 수동으로 계획을 강제 적용 하지 않았습니다. 사용자가 권장 계획을 명시적으로 되돌린 이후 데이터베이스 엔진은 현재 계획을 계속 사용 하 고 나중에 일부 계획 회귀를 수행 하는 경우 새 권장 구성을 생성 합니다. |

 세부 정보 열의 통계가 런타임 계획 통계 (예: 현재 CPU 시간)를 표시 하지 않습니다. 권장 사항 세부 정보는 회귀 검색 시에 수행 되며, 확인 된 성능 회귀의 원인을 설명 합니다 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] . `regressedPlanId`및 `recommendedPlanId` 를 사용 하 여 정확한 런타임 계획 통계를 찾으려면 [쿼리 저장소 카탈로그 뷰](../../relational-databases/performance/how-query-store-collects-data.md) 를 쿼리 합니다.

## <a name="examples-of-using-tuning-recommendations-information"></a>튜닝 권장 구성 정보를 사용 하는 예  

### <a name="example-1"></a>예 1
다음은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정 된 쿼리에 대해 좋은 계획을 적용 하는 생성 된 스크립트를 가져옵니다.  
 
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
다음은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정 된 쿼리에 대 한 적절 한 계획을 강제 적용 하는 생성 된 스크립트와 예상 된 이득에 대 한 추가 정보를 가져옵니다.

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
다음은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정 된 쿼리에 대해 좋은 계획을 적용 하는 생성 된 스크립트와 쿼리 저장소에 저장 된 쿼리 텍스트 및 쿼리 계획을 포함 하는 추가 정보를 가져옵니다.

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

권장 사항 뷰에서 값을 쿼리 하는 데 사용할 수 있는 JSON 함수에 대 한 자세한 내용은의 [Json 지원](../json/json-data-sql-server.md) 을 참조 하세요 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] .
  
## <a name="permissions"></a>사용 권한  

`VIEW SERVER STATE`에서 권한이 필요 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 합니다.   
`VIEW DATABASE STATE`에서 데이터베이스에 대 한 권한이 필요 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 합니다.   

## <a name="see-also"></a>참고 항목  
 [자동 조정](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [Transact-sql&#41;sys.database_automatic_tuning_options &#40;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [Transact-sql&#41;sys.database_query_store_options &#40;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 지원](../json/json-data-sql-server.md)
