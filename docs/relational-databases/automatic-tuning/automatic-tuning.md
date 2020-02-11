---
title: 자동 조정 | Microsoft Docs
description: SQL Server 및 Azure SQL Database의 자동 조정에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ad185085c19d8286fa6a09e46742860a948849a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67934553"
---
# <a name="automatic-tuning"></a>자동 조정
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

자동 튜닝은 잠재적 쿼리 성능 문제에 대한 정보를 제공하고, 솔루션을 권장하며, 식별된 문제를 자동으로 해결하는 데이터베이스 기능입니다.

에서 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 자동 조정은 잠재적 성능 문제가 감지 될 때마다 사용자에 게 알리고 정정 작업을 적용 하거나에서 성능 문제를 자동 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 으로 해결할 수 있도록 합니다.
의 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 자동 조정 기능을 사용 하면 **쿼리 실행 계획 선택 재발**으로 인 한 성능 문제를 식별 하 고 해결할 수 있습니다. 또한의 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 자동 조정은 필요한 인덱스를 만들고 사용 하지 않는 인덱스를 삭제 합니다. 쿼리 실행 계획에 대 한 자세한 내용은 [실행 계획](../../relational-databases/performance/execution-plans.md)을 참조 하세요.

는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스에서 실행 되는 쿼리를 모니터링 하 고 자동으로 작업의 성능을 향상 시킵니다. 에 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 는 데이터베이스를 작업에 동적으로 적용 하 여 쿼리 성능을 자동으로 조정 하 고 향상 시킬 수 있는 기본 제공 인텔리전스 메커니즘이 있습니다. 다음과 같은 두 가지 자동 조정 기능을 사용할 수 있습니다.

 -  **자동 계획 수정** 은 문제가 있는 쿼리 실행 계획을 식별 하 고 쿼리 실행 계획 성능 문제를 해결 합니다. **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **자동 인덱스 관리** 는 데이터베이스에 추가 되어야 하는 인덱스 및 제거 되어야 하는 인덱스를 식별 합니다. **적용**대상:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>자동 조정을 사용하는 이유는 무엇입니까?

클래식 데이터베이스 관리의 세 가지 주요 태스크는 워크 로드를 모니터링 하 고, [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 중요 한 쿼리를 식별 하 고, 성능을 향상 시키기 위해 추가 해야 하는 인덱스를 식별 하 고, 거의 사용 되지 않는 것입니다 는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 모니터링 해야 하는 쿼리 및 인덱스에 대 한 자세한 정보를 제공 합니다. 그러나 데이터베이스를 지속적으로 모니터링 하는 작업은 특히 많은 데이터베이스를 처리할 때 어렵고 지루한 작업입니다. 매우 많은 수의 데이터베이스를 관리 하는 것은 효율적이 지 않을 수 있습니다. 수동으로 데이터베이스를 모니터링 하 고 튜닝 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 하는 대신 자동 조정 기능을 사용 하 여 일부 모니터링 및 튜닝 작업을 위임 하는 것을 고려할 수 있습니다.

### <a name="how-does-automatic-tuning-work"></a>자동 조정의 작동 방식은 무엇입니까?

자동 조정은 워크 로드의 특성을 지속적으로 학습 하 고 잠재적인 문제 및 향상 된 기능을 식별 하는 연속 모니터링 및 분석 프로세스입니다.

![자동 조정 프로세스](./media/tuning-process.png)

이 프로세스를 통해 데이터베이스는 워크 로드의 성능을 향상 시킬 수 있는 인덱스 및 계획과 워크 로드에 영향을 주는 인덱스를 검색 하 여 워크 로드에 동적으로 적용할 수 있습니다. 이러한 결과에 따라 자동 조정은 작업의 성능을 향상시키는 조정 작업을 적용합니다. 또한 데이터베이스는 자동 조정에 의해 변경 된 후 성능을 지속적으로 모니터링 하 여 워크 로드의 성능을 향상 시킵니다. 성능을 향상 시 키 지 않는 작업은 자동으로 되돌려집니다. 이 확인 프로세스는 자동 조정에서 만든 변경 사항이 작업의 성능을 저하시키지 않도록 보장하는 주요 기능입니다.

## <a name="automatic-plan-correction"></a>자동 계획 수정

자동 계획 수정은 **실행 계획 선택 회귀** 를 식별 하 고 마지막으로 성공한 계획을 적용 하 여 문제를 자동으로 해결 하는 자동 조정 기능입니다. 쿼리 실행 계획 및 쿼리 최적화 프로그램에 대 한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)를 참조 하세요.

### <a name="what-is-execution-plan-choice-regression"></a>실행 계획 선택 회귀 란 무엇 인가요?

는 [!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 다른 실행 계획을 사용 하 여 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리를 실행할 수 있습니다. 쿼리 계획은 통계, 인덱스 및 기타 요인에 따라 달라 집니다. 일부 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리를 실행 하는 데 사용 해야 하는 최적의 계획은 시간이 지남에 따라 변경 될 수 있습니다. 경우에 따라 새 계획이 이전 계획 보다 더 좋을 수도 있고 새 계획으로 인해 성능 재발이 발생할 수도 있습니다.

 ![쿼리 실행 계획 선택 회귀](media/plan-choice-regression.png "쿼리 실행 계획 선택 회귀") 

계획 선택 회귀를 확인할 때마다 몇 가지 이전 좋은 계획을 찾아 현재 프로시저를 사용 하 `sp_query_store_force_plan` 는 것이 아닌 다른 계획을 적용 해야 합니다.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 재발 계획 및 권장 되는 정정 작업에 대 한 정보를 제공 합니다.
또한를 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 사용 하 여이 프로세스를 완전히 자동화 하 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 고 계획 변경과 관련 된 문제를 수정할 수 있습니다.

### <a name="automatic-plan-choice-correction"></a>자동 계획 선택 수정

[!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 계획 선택 회귀를 검색할 때마다 마지막으로 성공한 계획으로 자동으로 전환할 수 있습니다.

![쿼리 실행 계획 선택 수정](media/force-last-good-plan.png "쿼리 실행 계획 선택 수정") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 잘못 된 계획 대신 사용 해야 하는 계획을 포함 하 여 잠재적 계획 선택 회귀를 자동으로 검색 합니다.
가 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 마지막으로 성공한 계획을 적용 하는 경우 강제 계획의 성능을 자동으로 모니터링 합니다. 강제 계획이 재발 된 계획 보다 더 적합 하지 않은 경우 새 계획이 강제로 적용 되지 않으며에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 새 계획을 컴파일합니다. 에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 강제 계획이 재발 된 계획 보다 더 좋은지 확인 하는 경우 다시 컴파일을 수행할 때까지 (예: 다음 통계 업데이트 또는 스키마 변경 시) 강제 계획이 재발 된 계획 보다 더 나은 경우 유지 됩니다.

> [!NOTE]
> 자동 강제 적용 되는 모든 실행 계획은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작할 때마다 지속 되지 않습니다.

### <a name="enabling-automatic-plan-choice-correction"></a>자동 계획 선택 수정 사용

데이터베이스마다 자동 튜닝을 활성화하고 일부 계획 변경 재발이 검색될 때마다 마지막 좋은 계획이 강제로 적용되어야 함을 지정할 수 있습니다. 다음 명령을 사용하여 자동 튜닝이 활성화됩니다.

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

이 옵션을 사용 하도록 설정 하면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에서 예상 CPU 이득을 10 초 이상으로 설정 하거나 새 계획의 오류 개수가 권장 계획의 오류 수보다 많은 권장 사항을 자동으로 적용 하 여 강제 계획이 현재 계획 보다 더 좋은지 확인 합니다.

### <a name="alternative---manual-plan-choice-correction"></a>대안 - 수동 계획 선택 수정

자동 튜닝 없이 사용자는 시스템을 주기적으로 모니터링하고 재발된 쿼리를 찾아야 합니다. 계획을 재발 하는 경우 사용자는 이전의 좋은 계획을 찾아 현재 프로시저를 사용 하 `sp_query_store_force_plan` 는 것 보다는이를 적용 해야 합니다. 통계 또는 인덱스 변경으로 인해 이전 계획이 유효 하지 않을 수 있기 때문에 마지막으로 알려진 좋은 계획을 적용 하는 것이 가장 좋습니다. 마지막으로 성공한 계획을 강제 적용 하는 사용자는 강제 계획을 사용 하 여 실행 되는 쿼리의 성능을 모니터링 하 고 강제 계획이 예상 대로 작동 하는지 확인 합니다. 모니터링 및 분석의 결과에 따라 계획을 강제 적용 하거나 사용자가 쿼리를 최적화 하는 다른 방법을 찾아야 합니다.
에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 최적의 계획을 적용할 수 있기 때문에 수동으로 강제 계획을 강제 적용할 수 없습니다. 사용자 또는 DBA는 프로시저를 사용 하 `sp_query_store_unforce_plan` 여 계획을 강제로 해제 하 고 최적의 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계획을 찾도록 합니다. 

> [!TIP]
> Alternativelly 계획 쿼리 저장소 뷰에서 **쿼리** 를 사용 하 여 계획을 찾고 해제 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]쿼리 저장소에서 성능을 모니터링 하 고 문제를 해결 하는 데 필요한 모든 보기 및 절차를 제공 합니다.

에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]쿼리 저장소 시스템 뷰를 사용 하 여 계획 선택 회귀를 찾을 수 있습니다. 에서 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 잠재적 계획 선택 재발 및 [dm_db_tuning_recommendations &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 뷰에 적용 해야 하는 권장 작업을 검색 하 고 표시 합니다. 이 보기에는 문제에 대 한 정보, 문제의 중요성, 식별 된 쿼리, 재발 된 계획의 ID, 비교 시 기준선으로 사용 된 계획의 ID 및 문제를 해결 하기 위해 실행할 수 있는 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 문이 표시 됩니다.

| type | description | Datetime | score에 대한 임계값 수준 보기 | 세부 정보 | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | CPU 시간이 4 밀리초에서 14 밀리초로 변경 되었습니다. | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | CPU 시간이 37 밀리초에서 84 밀리초로 변경 되었습니다. | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

이 보기의 일부 열은 다음 목록에 설명 되어 있습니다.
 - 권장 작업의 유형-`FORCE_LAST_GOOD_PLAN`
 - 이 계획이 변경 될 수 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 있는 성능 재발을 나타내는 정보가 포함 된 설명입니다.
 - 잠재적 재발이 검색 된 날짜/시간
 - 이 권장 사항의 점수
 - 검색 된 계획의 ID, 재발 된 계획의 ID, 문제를 해결 하기 위해 강제로 적용 해야 하는 계획의 ID, 문제를 해결 하기 위해 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 적용 될 수 있는 스크립트 등의 문제에 대 한 세부 정보입니다. 세부 정보는 [JSON 형식](../../relational-databases/json/index.md) 으로 저장 됩니다.

다음 쿼리를 사용 하 여 문제를 해결 하는 스크립트와 예상 된 이득에 대 한 추가 정보를 얻을 수 있습니다.

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
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

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score에 대한 임계값 수준 보기 | script | 쿼리\_id | 현재 계획\_id | 권장 계획\_id | 예상\_이득 | 오류가\_발생 하기 쉽습니다.
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CPU 시간이 3 밀리초에서 46 밀리초로 변경 되었습니다. | 36 | EXEC sp\_쿼리\_저장소\_강제\_요금제 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain`현재 계획 대신 권장 계획을 실행 하는 경우 저장 되는 예상 시간 (초)을 나타냅니다. 이득을 10 초 보다 큰 경우에는 현재 계획 대신 권장 계획을 강제로 적용 해야 합니다. 현재 계획에 권장 계획 보다 더 많은 오류 (예: 시간 초과 또는 중단 된 실행)가 있는 경우이 열 `error_prone` 은 값 `YES`으로 설정 됩니다. 오류가 발생할 수 있는 계획은 현재 권장 계획 대신 강제 적용 해야 하는 또 다른 이유입니다.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 는 계획 선택 재발을 식별 하는 데 필요한 모든 정보를 제공 합니다. 지속적으로 모니터링 하 고 성능 문제를 해결 하는 것은 지루한 프로세스가 될 수 있습니다. 자동 조정 기능을 사용 하면이 프로세스를 훨씬 더 쉽게 수행할 수 있습니다.

> [!NOTE]
> Dm_db_tuning_recommendations DMV의 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작할 때마다 지속 되지 않습니다.

## <a name="automatic-index-management"></a>자동 인덱스 관리

에서 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]인덱스 관리는 워크 로드에 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 대해 학습 하 고 데이터가 항상 최적으로 인덱스 되도록 하기 때문에 간단 합니다. 적절한 인덱스 디자인은 작업의 최적의 성능을 위해 중요하고 자동 인덱스 관리는 인덱스를 최적화하는 데 도움이 될 수 있습니다. 자동 인덱스 관리는 올바르지 않게 인덱싱된 데이터베이스의 성능 문제를 해결하거나 기존 데이터베이스 스키마에 대한 인덱스를 유지 관리하고 향상시킬 수 있습니다. 에서 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 자동 조정 작업은 다음 작업을 수행 합니다.

 - 테이블에서 데이터를 읽는 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 쿼리의 성능을 향상 시킬 수 있는 인덱스를 식별 합니다.
 - 제거할 수 있는 더 긴 기간 동안 사용 되지 않은 중복 인덱스 또는 인덱스를 식별 합니다. 불필요 한 인덱스를 제거 하면 테이블의 데이터를 업데이트 하는 쿼리의 성능이 향상 됩니다.

### <a name="why-do-you-need-index-management"></a>인덱스 관리가 필요한 이유는 무엇입니까?

인덱스는 테이블에서 데이터를 읽는 일부 쿼리의 속도를 높이지만 데이터를 업데이트하는 쿼리의 속도가 저하될 수 있습니다. 인덱스를 만들 시기와 인덱스에 포함해야 하는 열을 신중하게 분석해야 합니다. 일부 인덱스는 일정 시간이 지난 후 필요하지 않을 수 있습니다. 따라서 이점을 가져오지 않는 인덱스를 정기적으로 식별하고 삭제해야 합니다. 사용되지 않는 인덱스를 무시하는 경우 데이터를 읽는 쿼리에 대한 아무런 이점 없이 데이터를 업데이트하는 쿼리의 성능이 저하될 것입니다. 추가 업데이트에는 불필요한 로깅이 필요하기 때문에 사용되지 않는 인덱스도 시스템의 전반적인 성능에 영향을 줍니다.

테이블에서 데이터를 읽는 쿼리의 성능을 개선하고 업데이트에 최소의 영향을 주는 인덱스의 최적 집합을 찾는 데 지속적이고 복잡한 분석이 필요할 수 있습니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]에서는 쿼리를 분석 하 고, 현재 작업에 가장 적합 한 인덱스를 식별 하 고, 인덱스를 제거할 수 있는 기본 제공 인텔리전스 및 고급 규칙을 사용 합니다. Azure SQL Database는 다른 쿼리에 미치는 영향을 최소화하여 데이터를 읽는 쿼리를 최적화하는 최소한으로 필요한 인덱스 세트를 갖도록 합니다.

### <a name="automatic-index-management"></a>자동 인덱스 관리

검색 외에도에서 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 식별 된 권장 사항을 자동으로 적용할 수 있습니다. 기본 제공 규칙을 사용 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 하 여 데이터베이스의 성능을 향상 시킬 수 있는 경우 인덱스를 자동으로 관리할 수 있습니다.

에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 자동 조정을 사용 하도록 설정 하 고 자동 조정 기능을 사용 하 여 작업을 완벽 하 게 관리 하려면 [Azure Portal를 사용 하 여 Azure SQL Database에서 자동 조정 사용](/azure/sql-database/sql-database-automatic-tuning-enable)을 참조 하세요.

에서 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] CREATE index 또는 DROP INDEX 권장 사항을 적용 하는 경우 인덱스의 영향을 받는 쿼리의 성능을 자동으로 모니터링 합니다. 영향을 받는 쿼리의 성능이 향상 되는 경우에만 새 인덱스가 유지 됩니다. 삭제 된 인덱스는 인덱스가 없기 때문에 느리게 실행 되는 일부 쿼리가 자동으로 다시 생성 됩니다.

### <a name="automatic-index-management-considerations"></a>자동 인덱스 관리 고려 사항

에서 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 필요한 인덱스를 만드는 데 필요한 동작은 리소스를 소비 하 고 일시적으로는 워크 로드 성능에 영향을 줄 수 있습니다. 인덱스 생성이 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 워크 로드 성능에 미치는 영향을 최소화 하기 위해는 인덱스 관리 작업을 위한 적절 한 시간 창을 찾습니다. 데이터베이스가 작업을 실행하기 위해 리소스가 필요한 경우 조정 작업은 지연되고 데이터베이스에 유지 관리 작업에 사용될 수 있는 사용되지 않는 충분한 리소스가 있는 경우 시작됩니다. 자동 인덱스 관리에서 중요한 기능 중 하나는 작업의 확인입니다. 에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 인덱스를 만들거나 삭제 하는 경우 모니터링 프로세스는 작업의 성능을 분석 하 여 작업의 성능이 향상 되었는지 확인 합니다. 크게 향상 되지 않은 경우에는 작업이 즉시 되돌려집니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 이렇게 하면 자동 작업이 작업 성능에 부정적인 영향을 주지 않습니다. 자동 조정으로 만든 인덱스는 기본 스키마에서 유지 관리 작업에 대해 투명합니다. 열 삭제 또는 이름 바꾸기와 같은 스키마 변경 내용은 자동으로 만들어진 인덱스에 의해 차단되지 않습니다. 에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 자동으로 만드는 인덱스는 관련 테이블이 나 열을 삭제할 때 즉시 삭제 됩니다.

### <a name="alternative---manual-index-management"></a>대체-수동 인덱스 관리

자동 인덱스 관리를 사용 하지 않을 경우 사용자는 [dm_db_missing_index_details &#40;&#41;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) 을 수동으로 쿼리해야 하거나에서 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 성능 대시보드 보고서를 사용 하 여 성능을 향상 시킬 수 있는 인덱스를 찾고이 뷰에 제공 된 세부 정보를 사용 하 여 인덱스를 만들고 쿼리 성능을 수동으로 모니터링 해야 합니다. 삭제할 인덱스를 찾기 위해 사용자는 인덱스에 대 한 운영 사용 통계를 모니터링 하 여 자주 사용 하지 않는 인덱스를 찾아야 합니다.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]이 프로세스를 간소화 합니다. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]작업을 분석 하 고, 새 인덱스를 사용 하 여 더 빠르게 실행 될 수 있는 쿼리를 식별 하 고, 사용 하지 않거나 중복 된 인덱스를 식별 합니다. 
  [Azure Portal에서 인덱스 찾기 권장 사항](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)에서 변경되어야 하는 인덱스의 ID에 대한 자세한 정보를 찾아보세요.

## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [database_automatic_tuning_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [dm_db_tuning_recommendations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [dm_db_missing_index_details &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_force_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [Transact-sql&#41;sp_query_store_unforce_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 함수](../../relational-databases/json/index.md)    
 [실행 계획](../../relational-databases/performance/execution-plans.md)    
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [쿼리 튜닝 길잡이](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
