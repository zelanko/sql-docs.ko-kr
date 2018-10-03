---
title: 자동 튜닝 | Microsoft Docs
description: SQL Server 및 Azure SQL Database 자동 튜닝에 대해 알아봅니다
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 639b2f5fd09ad017f94881358f8b2731cbd39c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849331"
---
# <a name="automatic-tuning"></a>자동 튜닝
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  자동 튜닝은 잠재적 쿼리 성능 문제에 대한 정보를 제공하고, 솔루션을 권장하며, 식별된 문제를 자동으로 해결하는 데이터베이스 기능입니다.

자동 튜닝 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 잠재적인 성능 문제가 검색 되 고 정정 작업을 적용 하면 때마다 알림을 표시 하거나 있습니다를 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동으로 성능 문제를 해결 합니다.
자동 튜닝 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 식별 하 고으로 인 한 성능 문제를 해결할 수 있습니다 **SQL 계획 선택 재발**합니다. 자동 조정을 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 필요한 인덱스를 생성 하 고 사용 되지 않는 인덱스를 삭제 합니다.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 데이터베이스에서 실행 되 고 자동으로 워크 로드의 성능을 향상 하는 쿼리를 모니터링 합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에 자동으로 조정 하 고 데이터베이스 워크 로드를 동적으로 적용 하 여 쿼리의 성능을 향상 시킬 수 있는 기본 제공 인텔리전스 메커니즘이 있습니다. 사용할 수 있는 두 가지 자동 튜닝 기능을 가지 있습니다.

 -  **자동 계획 수정** (사용할 수 있습니다 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 고 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) 문제가 있는 쿼리 실행 계획을 식별 하 고 수정 SQL 계획 성능 문제.
 -  **자동 인덱스 관리** (에서만 사용할 수 있습니다 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) 데이터베이스에 추가 해야 하는 인덱스 및 제거 되어야 하는 인덱스를 식별 하는 합니다.

## <a name="why-automatic-tuning"></a>왜 자동 튜닝?

식별 중요 한 워크 로드를 모니터링 하는 클래식 데이터베이스 관리의 기본 작업의 세 가지 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 해야 하는 성능 향상을 위해 추가 되 고 식별 거의 사용 되지 않고 인덱스를 쿼리 합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 쿼리 및 모니터링 해야 하는 인덱스에 대 한 자세한 정보를 제공 합니다. 그러나 데이터베이스를 지속적으로 모니터링 많은 데이터베이스를 사용 하 여 처리할 때 힘들고 지루한 작업입니다. 상당히 많은 데이터베이스 관리 작업을 효율적으로 수행할 수 수 있습니다. 대신 모니터링과 데이터베이스를 수동으로 조정 해야 할 모니터링의 일부를 위임 하 고 작업을 튜닝 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동 튜닝 기능을 사용 합니다.

### <a name="how-does-automatic-tuning-work"></a>자동 튜닝 작업을 어떻게 하나요?

자동 튜닝은 워크 로드의 특성에 대 한 지속적으로 학습 하는 분석 프로세스 및 연속 모니터링 하 고 잠재적인 문제 및 향상 된 기능을 식별 합니다.

![자동 튜닝 프로세스](./media/tuning-process.png)

이 프로세스에는 데이터베이스를 워크 로드는 인덱스 및 계획에 워크 로드의 성능을 향상 시킬 수 및 인덱스 워크 로드에 영향을 검색 하 여 동적으로 적용할 수 있습니다. 이러한 결과 따라 자동 조정 작업의 성능을 향상 시키는 조정 작업은 적용 됩니다. 또한 데이터베이스 워크 로드의 성능을 향상 시키는 되도록 자동 조정 하 여 변경 후 성능을 지속적으로 모니터링 합니다. 성능을 향상 하지 않은 하는 모든 작업은 자동으로 되돌려집니다. 이 확인 프로세스는 자동 조정에서 변경 작업의 성능을 저하 되지 않게 보장 하는 주요 기능입니다.

## <a name="automatic-plan-correction"></a>자동 계획 수정

자동 계획 수정은 식별 하는 자동 튜닝 기능 **SQL 계획 선택 재발** 자동으로 알려진된 마지막 좋은 계획을 강제 적용 하 여 문제를 해결 합니다.

### <a name="what-is-sql-plan-choice-regression"></a>SQL 계획 선택 회귀 란?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 다른 SQL 계획 실행에 사용할 수는 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리 합니다. 쿼리 계획 통계, 인덱스 및 기타 요인에 따라 달라 집니다. 일부 실행에 사용 해야 하는 최적의 계획 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리 시간이 지남에 따라 변경 될 수 있습니다. 경우에 따라 새 계획을 이전 보다 더 나은 되지 않을 수 있으며 새 계획이 성능 저하를 발생할 수 있습니다.

 ![SQL 계획 선택 재발](media/plan-choice-regression.png "SQL 계획 선택 재발") 

이전 몇 가지 유용한 계획 하 고는 현재 사용 하 여 대신 강제로 찾아야 계획 선택 재발을 표시 하는 때마다 `sp_query_store_force_plan` 프로시저입니다.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 계획 회귀 및 권장 되는 수정 작업에 대 한 정보를 제공 합니다.
또한 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 를 완벽 하 게이 프로세스를 자동화할 수 있도록 하면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계획 변경과 관련 된 발견 된 모든 문제를 해결 합니다.

### <a name="automatic-plan-choice-correction"></a>자동 계획 선택 수정

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계획 선택 재발이 검색 될 때마다 알려진된 마지막 좋은 계획으로 전환할 자동으로 수 있습니다.

![SQL 계획 선택 수정](media/force-last-good-plan.png "SQL 계획 선택 수정") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 잘못 된 계획 대신 사용 해야 하는 계획을 포함 한 모든 잠재적 계획 선택 재발을 자동으로 검색 합니다.
경우는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 마지막 적용 알려진 좋은 계획을 자동으로 모니터링 강제 계획의 성능입니다. 새 계획을 강제 됩니다 강제로 적용된 된 계획이 재발된 된 계획 보다 더 나은 경우 및 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 새 계획을 컴파일되지 것입니다. 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 강제 계획은 이전 상태로 되돌아간된 것 보다 더 나은 확인이 강제 된 계획 재발된 된 계획 보다 더 나은 경우 (예를 들어, 다음 통계 또는 스키마 변경)에서 recompile 될 때까지 유지 됩니다.

참고: 강제 계획 자동 모든 SQL Server 인스턴스를 다시 시작 하지 persit를 수행 합니다.

### <a name="enabling-automatic-plan-choice-correction"></a>자동 계획 선택 수정 사용

데이터베이스마다 자동 튜닝을 활성화하고 일부 계획 변경 재발이 검색될 때마다 마지막 좋은 계획이 강제로 적용되어야 함을 지정할 수 있습니다. 다음 명령을 사용하여 자동 튜닝이 활성화됩니다.

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
이 옵션을 켜면, 면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동으로 예상된 된 CPU 이득이 10 초 보다 높습니다. 하거나 새 계획에는 오류 개수 보다 크면 오류 수가 권장 되는 계획에 있는 권장 사항을 적용 하 고 있는지 확인 합니다 강제 계획은 현재 버전 보다 더 나은입니다.

### <a name="alternative---manual-plan-choice-correction"></a>대안-수동 계획 선택 수정

자동 튜닝 없이 사용자는 시스템을 주기적으로 모니터링하고 재발된 쿼리를 찾아야 합니다. 이전 몇 가지 유용한 계획 하 고는 현재 사용 하 여 대신 강제로 사용자를 찾아야 계획이 재발 된 경우 `sp_query_store_force_plan` 프로시저입니다. 가장 좋은 방법은 이전 계획 통계 또는 인덱스 변경 내용으로 인해 잘못 될 수 있으므로 알려진된 마지막 좋은 계획을 적용할 것입니다. 알려진된 마지막 좋은 계획을 강제로 사용자는 강제 계획을 사용 하 여 실행 되는 쿼리의 성능을 모니터링 하 고 해당 강제 계획 예상 대로 작동 하는지 확인 해야 합니다. 모니터링 및 분석의 결과 따라 계획을 강제로 해야 하거나 사용자 쿼리를 최적화 하는 다른 방법이 찾아야 합니다.
수동으로 강제 계획 해서는 안 됩니다 영원히 때문에 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 최적의 계획을 적용할 수 있어야 합니다. 사용자 또는 DBA는 최종적으로 강제 적용 해제 하 여 계획 `sp_query_store_unforce_plan` 프로시저와 수를 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 최적의 계획을 찾으실 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 필요한 뷰 및 성능을 모니터링 하 고 쿼리 저장소의 문제를 해결 하는 데 필요한 절차를 제공 합니다.

[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], 쿼리 저장소 시스템 뷰를 사용 하 여 계획 선택 회귀를 찾을 수 있습니다. [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]의 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 검색 하 고 잠재적 계획 선택 회귀 및에 적용 해야 하는 권장된 작업을 표시 합니다 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 보기. 문제, 재발 된 계획의 ID를 기준으로 비교에 사용 된 계획의 ID 식별된 된 쿼리 등의 세부 정보와 문제를의 중요성에 대 한 정보를 표시 하는 뷰 및 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 문제를 해결 하려면 실행 될 수 있는 문에 문제가 발생 했습니다.

| 유형 | description | DATETIME | score | 자세히 | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 14 ms 4ms에서 변경 하는 CPU 시간 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 84 ms 37 ms에서 변경 하는 CPU 시간 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

이 보기에서 일부 열은 다음 목록에 설명 되어 있습니다.
 - 권장 되는 작업-유형의 `FORCE_LAST_GOOD_PLAN`합니다.
 - 이유 정보를 포함 하는 설명 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 이 계획 변경 잠재적인 성능 저하를 인지 하는 것으로 생각 합니다.
 - 잠재적인 회귀 검색 되 면 Datetime입니다.
 - 이러한 권장 사항의 점수입니다. 
 - 검색 된 계획 회귀 된 계획을 강제로 문제를 해결 하는 계획의 ID의 ID의 ID와 같은 문제에 대 한 세부 정보 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 등 문제를 해결 하려면 적용할 수 있는 스크립트입니다. 세부 정보에 저장 됩니다 [JSON 형식을](../../relational-databases/json/index.md)합니다.

예상에 대 한 추가 정보와 문제를 수정 하는 스크립트를 가져오려면 다음 쿼리를 사용 하 여 얻을 수 있습니다.

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | 스크립트(script) | 쿼리\_id | 현재 계획\_id | 계획 권장\_id | 예상\_얻기 | 오류\_발생 하기 쉬운
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 3 밀리초에서 46 밀리초로 변경 하는 CPU 시간 | 36 | EXEC sp\_쿼리\_저장할\_강제로\_계획 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 현재 계획 대신 권장 되는 계획을 실행 하는 경우 절약 되는 시간 (초)의 예상된 수를 나타냅니다. 10 초 보다 큰 경우 현재 계획 대신 권장 되는 계획을 강제 해야 합니다. 에 있는 경우 더 많은 오류 (예: 시간 제한 또는 중단 된 실행) 보다 현재 계획에 권장 되는 계획을 열 `error_prone` 값으로 설정할 수는 `YES`합니다. 오류가 발생 하기 쉬운 계획은 대신 현재 권장 되는 계획을 강제로 하는 이유는 또 다른 이유입니다.

하지만 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 제공 계획 선택 재발; 연속 모니터링 및 성능 문제 해결을 식별 하는 데 필요한 모든 정보 걸릴 수 있습니다. 자동 튜닝이 프로세스가 훨씬 쉬워집니다.

참고:이 DMV에는 데이터는 SQL Server 인스턴스를 다시 시작한 후 유지 되지 않습니다.

## <a name="automatic-index-management"></a>자동 인덱스 관리

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], 인덱스 관리가 쉬운 있으므로 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 작업에 대해 학습 하 고 하면 데이터는 항상 최적으로 인덱싱됩니다. 적절 한 인덱스 디자인은 작업의 최적의 성능을 위해 중요 하 고 자동 인덱스 관리 인덱스를 최적화 하는 데 도움이 됩니다. 자동 인덱스 관리 하거나 올바르지 않게 인덱싱된 데이터베이스의 성능 문제를 해결 또는 유지 관리를 기존 데이터베이스 스키마에 대 한 인덱스를 향상 시키십시오. 자동 조정을 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 다음 작업을 수행 합니다.

 - 테이블에서 데이터를 읽는 T-SQL 쿼리의 성능을 향상 시킬 수 있는 인덱스를 식별 합니다.
 - 중복 인덱스 또는 제거할 수 있는 시간이 더 긴 기간에 사용 되지 않은 인덱스를 식별 합니다. 불필요 한 인덱스를 제거 합니다. 테이블의 데이터를 업데이트 하는 쿼리의 성능을 향상 시킵니다.

### <a name="why-do-you-need-index-management"></a>인덱스 관리는 왜 필요 한가요?

인덱스는 테이블에서 데이터를 읽는 쿼리의 일부 속도 그러나 데이터를 업데이트 하는 쿼리의 느려질 수 있습니다. 인덱스를 만들어야 하는 경우 및 어떤 열을 신중 하 게 분석 해야 할 인덱스에 포함 해야 합니다. 일정 시간이 지난 후 일부 인덱스를 필요할 수 있습니다. 따라서 정기적으로 식별 하 고 모든 혜택을 가져오지 않는 인덱스를 삭제 해야 합니다. 사용 되지 않는 인덱스를 무시 하면 데이터를 읽는 쿼리에 대 한 아무런 이점 없이 데이터를 업데이트 하는 쿼리 성능이 저하 될 것입니다. 사용 되지 않는 인덱스도 추가 업데이트에 불필요 한 로깅이 필요 하기 때문에 시스템의 전반적인 성능이 영향을 줍니다.

테이블에서 데이터 읽기 및 업데이트에 최소한의 영향을 주지는 쿼리의 성능을 개선 하는 인덱스의 최적 집합을 찾는 연속 고 복잡 한 분석이 필요할 수 있습니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 사용 하 여 기본 제공 인텔리전스, 쿼리를 분석 하는 고급 규칙 식별 하 고 현재 작업에 최적인 인덱스 및 인덱스 제거 될 수 있습니다. Azure SQL Database는 인덱스는 다른 쿼리에 미치는 영향을 최소화 하 고 데이터를 읽는 쿼리를 최적화 하는 데 필요한 최소한 있는지를 확인 합니다.

### <a name="automatic-index-management"></a>자동 인덱스 관리

검색 하는 것 외에도 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 자동 식별 된 권장 사항을 적용할 수 있습니다. 기본 제공 규칙은 데이터베이스의 성능을 향상 시킬는 찾을 수 있습니다 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 인덱스를 자동으로 관리 합니다.

Azure SQL Database에서 자동 조정을 사용 하도록 설정 하 고 자동 조정 기능을 완벽 하 게 워크 로드를 관리할 수 있도록, 참조 [Azure portal을 사용 하 여 Azure SQL Database에서 자동 조정을 활성화](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable)합니다.

경우는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] CREATE INDEX 문이나 DROP INDEX 권장 구성 적용 인덱스의 영향을 받는 쿼리의 성능을 자동으로 모니터링 합니다. 새 인덱스는 영향을 받는 쿼리의 성능을 향상 하는 경우에 유지 됩니다. 인덱스의 부재로 인해 더 느리게 실행 되는 일부 쿼리의 경우 삭제 된 인덱스가 자동으로 다시 생성 됩니다.

### <a name="automatic-index-management-considerations"></a>자동 인덱스 관리 고려 사항

필요한 인덱스를 만드는 데 필요한 작업 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 리소스가 소비 되 고 일시적으로 워크 로드 성능에 영향을 줄 수 있습니다. 인덱스 생성이 워크 로드 성능에 미치는 영향을 최소화 하려면 Azure SQL Database는 인덱스 관리 작업에 대 한 적절 한 기간을 찾습니다. 데이터베이스 워크 로드를 실행 하는 리소스가 필요한 경우 연기 되며 데이터베이스 공간이 충분 한 경우 시작 작업을 튜닝 사용 되지 않는 리소스를 유지 관리 작업에 사용할 수 있습니다. 자동 인덱스 관리에서 중요 한 기능 중 하나는 작업의 확인 됩니다. Azure SQL Database를 만듭니다 또는 인덱스를 삭제 하는 경우 모니터링 프로세스는 작업 성능을 향상 되었는지 확인 하려면 작업의 성능을 분석 합니다. 향상 – 가져오지 않은 경우에 작업은 즉시 되돌려집니다. 이러한 방식으로 Azure SQL Database는 자동 작업 부정적인 영향을 주지 워크 로드의 성능을 확인 합니다. 자동 조정으로 만든 인덱스는 기본 스키마에 대 한 유지 관리 작업에 대해 투명 합니다. 열 이름 바꾸기 또는 삭제와 같은 스키마 변경 내용은 자동으로 만든된 인덱스의 현재 상태에서 차단 되지 않습니다. Azure SQL Database에서 자동으로 생성 되는 인덱스는 즉시 삭제 될 때 관련 테이블 또는 열 삭제 됩니다.

### <a name="alternative---manual-index-management"></a>대안-수동 인덱스 관리

자동 인덱스 관리 없이 사용자를 수동으로 쿼리하려면 해야 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) 성능 향상, 세부 정보를 사용 하 여 인덱스를 만들 수는 인덱스를 찾을 수 보기 이 뷰와 수동으로 쿼리 성능 모니터링에 제공 합니다. 삭제 해야 하는 인덱스를 찾기 위해 사용자는 거의 사용 찾기 인덱스에 인덱스의 통계 운영 사용 현황을 모니터링 해야 합니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 이 프로세스를 간소화 합니다. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 워크 로드를 분석 하 여, 새 인덱스를 사용 하 여 더 빠르게 실행 될 수 있는 쿼리를 식별 하 고 사용 되지 않거나 중복 된 인덱스를 식별 합니다. 변경 해야 하는 인덱스의 id에 대 한 자세한 정보를 찾으려면 [Azure portal에서 인덱스 권장 사항을 찾거나](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)합니다.

## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 함수](../../relational-databases/json/index.md)
