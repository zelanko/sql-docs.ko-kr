---
title: 자동 튜닝 | Microsoft Docs
description: SQL Server 및 Azure SQL 데이터베이스의 자동 튜닝 하는 방법에 대 한 자세한 내용은
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 0e77a1d7e24fa2635b3e699672338e588c1f5c1c
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707771"
---
# <a name="automatic-tuning"></a>자동 튜닝
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  자동 튜닝은 잠재적 쿼리 성능 문제에 대한 정보를 제공하고, 솔루션을 권장하며, 식별된 문제를 자동으로 해결하는 데이터베이스 기능입니다.

자동 조정 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 잠재적 성능 문제를 발견 하 고 수정 동작을 적용할 수 있습니다 될 때마다 알림을 표시 하거나 있습니다는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동으로 성능 문제를 수정 합니다.
자동 조정 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 식별 하 고에 따른 성능 문제를 수정 하면 **SQL 계획 선택 재발**합니다. 자동 조정 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 필요한 인덱스를 생성 하 고 사용 되지 않는 인덱스를 삭제 합니다.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 데이터베이스에서 실행 되 고 자동으로 작업의 성능을 향상 하는 쿼리를 모니터링 합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에 자동으로 조정 하 고 데이터베이스 작업에 맞게 동적으로 적용 하 여 쿼리의 성능을 향상 시킬 수 있는 기본 제공 intelligence 메커니즘이 있습니다. 사용할 수 있는 두 가지 자동 튜닝 기능이 있습니다.

 -  **자동 계획 수정** (에서 사용할 수 있는 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) 문제가 있는 쿼리 실행 계획을 식별 하 고 수정 SQL 성능 문제를 계획 합니다.
 -  **자동 인덱스 관리** (에서만 사용할 수 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) 식별 하는 데이터베이스에 추가 해야 하는 인덱스 및 인덱스를 제거 해야 합니다.

## <a name="why-automatic-tuning"></a>이유 자동 튜닝?

클래식 데이터베이스 관리에서 하는 주요 작업 중 하나는 중요 한 식별 하는 작업을 모니터링 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 성능 향상을 위해 추가 해야 하며 거의 인덱스를 사용 하는 인덱스를 쿼리 합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 쿼리 및 모니터링 해야 하는 인덱스에 대 한 자세한 정보를 제공 합니다. 그러나 지속적으로 모니터링 되는 데이터베이스 데이터베이스가 많은 처리할 때 하드 및 지루한 작업입니다. 상당 수의 데이터베이스 관리를 효율적으로 수행할 수 수 있습니다. 모니터링 수동으로 데이터베이스를 튜닝 하는 대신 해야 할 일부 모니터링 위임 하 고 작업을 튜닝 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동 튜닝 기능을 사용 합니다.

### <a name="how-does-automatic-tuning-works"></a>자동 튜닝 작동은 어떻게 하나요?

자동 튜닝은 연속 모니터링 및 워크 로드의 특징에 대 한 알아냅니다 지속적으로 분석 프로세스 하 고 잠재적인 문제 및 향상 된 기능을 식별 합니다.

![자동 튜닝 프로세스](./media/tuning-process.png)

이 프로세스는 인덱스 및 계획에 작업의 성능을 향상 시킬 수 및 인덱스 작업에 영향을 검색 하 여 작업에 맞게 동적으로 조정 하는 데이터베이스를 사용 합니다. 이러한 결과에 따라, 자동 튜닝 워크 로드의 성능을 향상 시키는 튜닝 작업은 적용 됩니다. 또한 데이터베이스의 변경 내용은 자동 튜닝 하 여 워크 로드의 성능을 향상 시키는 있는지 확인 한 후 성능 지속적으로 모니터링 합니다. 성능을 개선 하지 않은 모든 작업은으로 자동으로. 이 확인 프로세스는 변경 내용은 자동 튜닝 작업 성능이 저하 되지 않도록 보장 하는 주요 기능입니다.

## <a name="automatic-plan-correction"></a>자동 계획 수정

자동 계획 수정이 식별 하는 자동 튜닝 기능 **SQL 계획 선택 재발** 하 고 자동으로 마지막 알려진된 좋은 계획을 강제 적용 하 여 문제를 해결 합니다.

### <a name="what-is-sql-plan-choice-regression"></a>SQL 계획 선택 재발 이란?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 서로 다른 SQL 계획 실행에 사용할 수는 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 쿼리 합니다. 쿼리 계획 통계, 인덱스 및 기타 요인에 따라 다릅니다. 일부 실행에 사용 해야 하는 최적의 계획 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 쿼리 시간이 지남에 따라 변경 될 수 있습니다. 경우에 따라 새 계획 이전 보다 더 나은 수 있으며 새 계획 성능 저하를 발생할 수 있습니다.

 ![SQL 계획 선택 재발](media/plan-choice-regression.png "SQL 계획 선택 재발") 

계획 선택 재발을 알게 될 때마다 있습니다 이전 몇 가지 유용한 계획 하 고는 현재 하나 사용 하는 대신 강제로 `sp_query_store_force_plan` 프로시저입니다.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 계획 저하 되 고 권장 되는 수정 작업에 대 한 정보를 제공 합니다.
또한 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 하면를 완벽 하 게이 프로세스를 자동화할 수 있도록 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계획 변경 내용과 관련 된 모든 문제를 찾을 수를 수정 합니다.

### <a name="automatic-plan-choice-correction"></a>자동 계획 선택 수정

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동으로 전환할 수는 마지막 알려진된 좋은 계획 계획 선택 재발이 감지 될 때마다.

![SQL 계획 선택 수정](media/force-last-good-plan.png "SQL 계획 선택 수정") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 잘못 된 계획을 대신 사용 해야 하는 계획을 포함 한 모든 잠재적 계획 선택 재발을 자동으로 검색 합니다.
경우는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 마지막 적용 알려진 좋은 계획을 자동으로 모니터링 하 여 강제 계획의 성능입니다. 새 계획을 강제 됩니다 강제 계획을 이전 상태로 되돌아간된 계획 보다 더 나은 없으면 및 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 새로운 계획이 컴파일됩니다. 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 확인 강제 계획은 이전 상태로 되돌아간된 것 보다 더 나은, 강제 계획 이전 상태로 되돌아간된 계획 보다 더 나은 경우 (예를 들어 다음 통계 또는 스키마 변경)에 다시 컴파일 될 때까지 유지 됩니다.

참고: 강제 계획 자동 모든 SQL Server 인스턴스를 다시 시작에 persit 하지 않습니다.

### <a name="enabling-automatic-plan-choice-correction"></a>자동 계획 선택 보정을 사용 하도록 설정

데이터베이스마다 자동 튜닝을 활성화하고 일부 계획 변경 재발이 검색될 때마다 마지막 좋은 계획이 강제로 적용되어야 함을 지정할 수 있습니다. 다음 명령을 사용하여 자동 튜닝이 활성화됩니다.

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
작동 되도록 하면이 옵션을 면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 자동으로 위치 예상된 CPU 이득이 작을 10 초 보다 큰 값 또는 새 계획에 있는 오류의 수 오류 개수 보다 높은 권장된 계획의 모든 권장 사항을 적용 하 고 있는지 확인은 강제 계획은 현재 보다 더 나은 합니다.

### <a name="alternative---manual-plan-choice-correction"></a>대신-수동 계획 선택 수정

자동 튜닝 없이 사용자는 시스템을 주기적으로 모니터링하고 재발된 쿼리를 찾아야 합니다. 모든 계획 재발 하는 경우 사용자를 찾아야 이전 몇 가지 유용한 계획은 현재 하나 사용 하는 대신 강제로 `sp_query_store_force_plan` 프로시저입니다. 모범 사례 이전 계획 통계 또는 인덱스 변경 내용으로 인해 잘못 될 수 있으므로 마지막 알려진된 좋은 계획을 강제 적용할 수 있습니다. 마지막 알려진된 좋은 계획을 강제로 사용자는 강제 계획을 사용 하 여 실행 되는 쿼리의 성능을 모니터링 하 고 예상 대로 작동 하는 강제 계획을 확인 해야 합니다. 모니터링 및 분석의 결과 따라 계획을 강제로 해야 하거나 사용자 쿼리를 최적화 하는 다른 방법이 찾아야 합니다.
수동으로 강제 계획은 강제로 종료 되지 영원히 때문에 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 최적의 계획을 적용할 수 있어야 합니다. 사용자 또는 DBA를 사용 하 여 계획 강제 결국 `sp_query_store_unforce_plan` let 프로시저와 저장 프로시저는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에 최적의 계획을 찾습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 필요한 보기와 성능을 모니터링 하 고 쿼리 저장소의 문제를 해결 하는 데 필요한 절차를 제공 합니다.

[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], 쿼리 저장소가 시스템 뷰를 사용 하는 계획 선택 재발을 찾을 수 있습니다. [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 검색 하 고 잠재적인 계획 선택 재발 및 적용 해야 하는 권장 되는 작업 표시는 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 보기. 보기의 중요 문제를 성과 식별 된 쿼리를 이전 상태로 되돌아간된 계획의 ID를 기준으로 비교를 위해 사용 된 계획의 ID와 같은 세부 정보, 문제에 대 한 정보를 표시 및 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 문제를 해결 하려면 실행 될 수 있는 문에 문제가 발생 했습니다.

| 유형 | description | DATETIME | score | 자세히 | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 4 ms에서 14 ms로 변경 하는 CPU 시간 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 37 ms에서 84 ms로 변경 하는 CPU 시간 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

이 보기에서 일부 열은 다음 목록에 설명 되어 있습니다.
 - 권장된 조치-유형의 `FORCE_LAST_GOOD_PLAN`합니다.
 - 이유 정보를 포함 하는 설명 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계획 이렇게 한 잠재적 성능 저하를 생각 합니다.
 - 잠재적인 회귀 검색 되 면 Datetime입니다.
 - 이 권장 구성의 점수입니다. 
 - 검색 된 계획을 강제로 문제를 해결 하는 계획의 ID 이전 상태로 되돌아간된 계획의 ID의 ID와 같은 문제에 대 한 세부 정보 [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 적용할 수 있는지 등 문제를 해결 하는 스크립트입니다. 세부 정보에 저장 된 [JSON 형식](../../relational-databases/json/index.md)합니다.

다음 쿼리를 가져올 예상에 대 한 추가 정보와 문제를 해결 하는 스크립트를 사용 하 여 얻을 수 있습니다.

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

| reason | score | 스크립트(script) | 쿼리\_id | 현재 계획\_id | 계획 권장\_id | 예상\_얻을 | 오류\_발생 하기 쉬운
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 3 ms에서 46 ms로 변경 하는 CPU 시간 | 36 | EXEC sp\_쿼리\_저장\_강제로\_계획 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 현재 계획 하는 대신 실행 되는 권장된 계획 저장 하는 시간 (초)의 예상된 수를 나타냅니다. 이득이 작을 10 초 보다 큰 경우 현재 계획 하는 대신 권장된 계획을 강제로 해야 합니다. 에 있는 경우 더 많은 오류가 (예를 들어 시간 제한 또는 중단 된 실행) 보다 현재 계획에서 권장 되는 계획을 열 `error_prone` 값으로 설정 됩니다 `YES`합니다. 오류가 발생 하기 쉬운 계획은 현재 항목 대신 권장된 계획을 강제로 하는 이유는 또 다른 이유입니다.

하지만 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 식별 계획 선택 재발; 지속적인 모니터링 및 성능 문제를 수정 하는 데 필요한 모든 정보 지루한 과정 수도 제공 합니다. 자동 튜닝 하면 훨씬 쉽게이 프로세스입니다.

참고:이 DMV에는 데이터가 SQL Server 인스턴스를 다시 시작한 후 유지 되지 않습니다.

## <a name="automatic-index-management"></a>자동 인덱스 관리

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], 인덱스 관리를 쉽게 때문에 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 작업에 대해 학습 하 고 데이터는 항상 최적의 인덱스 지 되도록 합니다. 적절 한 인덱스 디자인은 워크 로드의 최적의 성능을 위해 중요 하 고 자동 인덱스 management 인덱스를 최적화 하는 데 도움이 될 수 있습니다. 자동 인덱스 관리 수 중 하나 인덱싱된 올바르지 않게 데이터베이스의 성능 문제를 해결 하거나 유지 관리 하 고 기존 데이터베이스 스키마에 대 한 인덱스를 향상 시키십시오. 자동 조정 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 다음 작업을 수행 합니다.

 - 테이블에서 데이터를 읽는 T-SQL 쿼리의 성능을 향상 시킬 수 있는 인덱스를 식별 합니다.
 - 중복 인덱스 또는 더 긴 시간 내에 제거할 수는 사용 되지 않은 인덱스를 식별 합니다. 불필요 한 인덱스를 제거 하면 테이블 데이터를에서 업데이트 하는 쿼리의 성능을 향상 됩니다.

### <a name="why-do-you-need-index-management"></a>인덱스 관리 왜 필요 합니까?

인덱스는 일부 쿼리는 테이블에서 데이터를 읽는 속도 그러나 데이터를 업데이트 하는 쿼리 느려질 수 있습니다. 열 및 인덱스를 만들 시기를 신중 하 게 분석 하면 인덱스에 포함 해야 합니다. 일정 시간이 지난 후 일부 인덱스를 필요할 수 있습니다. 따라서 정기적으로 식별 하 고 모든 혜택을 가져오지 않는 인덱스를 삭제 해야 합니다. 사용 되지 않는 인덱스를 무시 하면에서 데이터를 읽는 쿼리 아무런 장점 없이 데이터를 업데이트 하는 쿼리의 성능이 저하 될 것입니다. 사용 되지 않는 인덱스도 추가 업데이트에 불필요 한 로깅 필요 하기 때문에 시스템의 전반적인 성능에 영향을 합니다.

테이블에서 데이터를 읽고 업데이트에 미치는 영향이 최소화 하는 쿼리의 성능을 개선 하는 인덱스의 최적 집합을 찾는 연속 및 복잡 한 분석이 필요할 수 있습니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 사용 하 여 기본 제공 인텔리전스 및 사용자 쿼리를 분석 하는 고급 규칙 될 현재 작업 프로그램에 대 한 최적의 인덱스를 식별 하 고 인덱스를 제거 될 수 있습니다. Azure SQL 데이터베이스는 필요한 최소한의 다른 쿼리에 미치는 영향 최소화 된 데이터를 읽는 쿼리를 최적화 하는 인덱스 있는지를 확인 합니다.

### <a name="automatic-index-management"></a>자동 인덱스 관리

검색 기능 외에도 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 자동 식별 된 권장 사항을 적용할 수 있습니다. 기본 제공 규칙은 데이터베이스의 성능을 향상 하를 찾을 경우 하도록 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 인덱스를 자동으로 관리 합니다.

Azure SQL 데이터베이스에서 자동으로 튜닝을 사용 하도록 설정 하 고 자동 튜닝 기능을 완벽 하 게 작업을 관리할 수 있도록 참조 [Azure 포털을 사용 하 여 Azure SQL 데이터베이스에서 자동으로 조정 기능 사용](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable)합니다.

경우는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] CREATE INDEX 문이나 DROP INDEX 권장 구성이 적용 됩니다. 자동으로 인덱스에 의해 영향을 받는 쿼리 성능을 모니터링 합니다. 새 인덱스의 영향을 받는 쿼리 성능이 향상 되는 경우에 유지 됩니다. 인덱스의 없기 때문에 느리게 실행 하는 일부 쿼리에 있는 경우 삭제 된 인덱스가 자동으로 다시 생성 됩니다.

### <a name="automatic-index-management-considerations"></a>자동 인덱스 관리 고려 사항

작업에 필요한 인덱스를 만드는 데 필요한 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 리소스를 소비 하며 시간적 워크 로드 성능에 영향을 줄 수 있습니다. 인덱스 생성 작업 성능에 영향을 최소화 하려면 Azure SQL 데이터베이스 인덱스의 관리 작업에 대해 적절 한 기간을 찾습니다. 데이터베이스가 리소스 워크 로드를 실행 하는 경우 지연 되 고 데이터베이스에 충분 한 경우 시작 작업을 튜닝 유지 관리 태스크에 사용할 수 있는 사용 되지 않는 리소스입니다. 자동 인덱스 관리에서 중요 한 기능 중 하나는 작업의 확인 합니다. Azure SQL 데이터베이스를 만들거나 인덱스를 삭제 때 모니터링 프로세스는 작업 성능을 향상 되었는지 확인 하려면 작업의 성능을 분석 합니다. 훨씬 향상 된 기능 –를 가져올 하지 않은 경우 작업이 즉시 되돌려집니다. 이러한 방식으로 Azure SQL 데이터베이스는 자동 작업 부정적인 영향을 주지 않습니다 작업 성능이 보장 합니다. 자동 튜닝 하 여 만든 인덱스는 기본 스키마에 대 한 유지 관리 작업에 대 한 투명 합니다. 열 이름 바꾸기 또는 삭제와 같은 스키마 변경 내용은 자동으로 만든된 인덱스의로 차단 되지 않습니다. Azure SQL 데이터베이스에서 자동으로 생성 된 인덱스의 삭제 즉시 됩니다 관련 테이블이 나 열 삭제 됩니다.

### <a name="alternative---manual-index-management"></a>대신-수동 인덱스 관리

자동 인덱스 관리 하지 않고 사용자를 수동으로 쿼리하려면 해야 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) 성능 향상, 세부 정보를 사용 하 여 인덱스를 만들 수 있는 인덱스를 찾을 수 보기 이 뷰와 수동으로 쿼리 성능 모니터링에 제공 합니다. 사용자는 삭제 해야 하는 인덱스를 찾기 위해 찾기 거의 사용 되지 않는 인덱스에 있는 인덱스의 통계 운영 사용 현황을 모니터링 해야 합니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 이 프로세스를 간소화합니다. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 해당 작업을 분석, 새 인덱스를 사용 하면 더 빠르게 실행 될 수 있는 쿼리를 식별 하 고 사용 되지 않거나 중복 된 인덱스를 식별 합니다. 변경 해야 하는 인덱스의 id에 대 한 자세한 정보를 찾을 [인덱스 권장 사항을 Azure 포털에서 찾을](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)합니다.

## <a name="see-also"></a>관련 항목  
 [ALTER 데이터베이스 집합 AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 함수](../../relational-databases/json/index.md)
