---
title: 인텔리전트 쿼리 처리
description: SQL Server 및 Azure SQL Database에서 쿼리 성능을 향상시키는 지능형 쿼리 처리 기능입니다.
ms.custom: seo-dt-2019
ms.date: 11/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f555713a25db2068a4f6a923504db765d3f3a09e
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287537"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 데이터베이스의 지능형 쿼리 처리

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

IQP(인텔리전트 쿼리 처리) 기능 제품군에는 최소한의 구현 노력으로 기존 워크로드의 성능을 개선하는 광범위한 영향을 가진 기능이 포함됩니다. 

![지능형 쿼리 처리](./media/iqp-feature-family.png)

인텔리전트 쿼리 처리에 대한 개요는 6분 분량의 다음 동영상을 시청하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Intelligent-Query-processing-in-SQL-Server-2019/player?WT.mc_id=dataexposed-c9-niner]


데이터베이스에 대해 적용 가능한 호환성 수준을 활성화하여 워크로드를 자동으로 지능형 쿼리 처리에 적합하게 만들 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 설정할 수 있습니다. 다음은 그 예입니다.  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

다음 표에는 데이터베이스 호환성 수준에 대한 요구 사항과 함께 모든 지능형 쿼리 처리 기능이 자세히 설명되어 있습니다.

| **IQP 기능** | **Azure SQL Database에서 지원** | **SQL Server에서 지원** |**설명** |
| --- | --- | --- |--- |
| [적응 조인(일괄 처리 모드)](#batch-mode-adaptive-joins) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터|적응형 조인은 실제 입력된 행에 따라 런타임 동안 조인 유형을 동적으로 선택합니다.|
| [대략적인 Count Distinct](#approximate-query-processing) | 예| 예. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터|고성능 및 낮은 메모리 사용 공간을 통해 빅 데이터 시나리오에 대한 대략적인 COUNT DISTINCT를 제공합니다. |
| [Rowstore의 일괄 처리 모드](#batch-mode-on-rowstore) | 예. 호환성 수준 150 미만| 예. 호환성 수준 150 미만 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터|columnstore 인덱스를 요구하지 않고 CPU 바인딩된 관계형 DW 워크로드에 대한 일괄 처리 모드를 제공합니다.  | 
| [인터리브 실행](#interleaved-execution-for-mstvfs) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터|고정 추측 대신 첫 번째 컴파일에서 발생한 다중 명령문 테이블 값 함수의 실제 카디널리티를 사용합니다.|
| [메모리 부여 피드백(일괄 처리 모드)](#batch-mode-memory-grant-feedback) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터|일괄 처리 모드 쿼리에 디스크로 분산되는 작업이 있는 경우 연속 실행을 위한 메모리를 더 추가합니다. 쿼리가 50%가 넘는 할당된 메모리를 낭비하는 경우 연속 실행을 위한 메모리 부여 측면을 줄입니다.|
| [메모리 부여 피드백(행 모드)](#row-mode-memory-grant-feedback) | 예. 호환성 수준 150 미만| 예. 호환성 수준 150 미만 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터|행 모드 쿼리에 디스크로 분산되는 작업이 있는 경우 연속 실행을 위한 메모리를 더 추가합니다. 쿼리가 50%가 넘는 할당된 메모리를 낭비하는 경우 연속 실행을 위한 메모리 부여 측면을 줄입니다.|
| [스칼라 UDF 인라인 처리](#scalar-udf-inlining) | 예 | 예. 호환성 수준 150 미만 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터|스칼라 UDF는 호출 쿼리로 “인라인”되는 해당 관계형 식으로 변환되어 성능이 크게 향상됩니다.|
| [테이블 변수 지연 컴파일](#table-variable-deferred-compilation) | 예. 호환성 수준 150 미만| 예. 호환성 수준 150 미만 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터|고정 추측 대신 첫 번째 컴파일에서 발생한 테이블의 변수의 실제 카디널리티를 사용합니다.|

## <a name="batch-mode-adaptive-joins"></a>일괄 처리 모드 적응 조인
일괄 처리 모드 적응 조인 기능을 사용하면 [해시 조인 또는 중첩된 루프 조인](../../relational-databases/performance/joins.md) 메서드 선택을 단일 캐시 계획을 통해 첫 번째 입력이 검사된 **후**까지 지연할 수 있습니다. 적응 조인 연산자는 중첩된 루프 계획으로 전환할 시기를 결정하는 데 사용되는 임계값을 정의합니다. 따라서 계획이 실행 중에 더 나은 조인 전략으로 동적으로 전환할 수 있습니다.

호환성 수준을 변경하지 않고 적응형 조인을 사용하지 않도록 설정하는 방법을 포함하여 자세한 내용은 [적응형 조인 이해](../../relational-databases/performance/joins.md#adaptive)를 참조하세요.

## <a name="batch-mode-memory-grant-feedback"></a>일괄 처리 모드 메모리 부여 피드백
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 쿼리 실행 후 계획에는 실행에 필요한 최소 필수 메모리 및 모든 행을 메모리에 포함하기 위한 이상적인 메모리 부여 크기가 포함됩니다. 메모리 부여 크기가 잘못 지정된 경우 성능이 저하됩니다. 과도하게 부여하면 메모리가 낭비되고 동시성이 줄어듭니다. 메모리 부여가 부족하면 디스크로 분산되어 비용이 증가합니다. 반복 워크로드를 처리함으로써 일괄 처리 모드 메모리 부여 피드백은 쿼리에 필요한 실제 메모리를 다시 계산한 후 캐시된 계획에 대한 부여 값을 업데이트합니다. 동일한 쿼리 문을 실행할 경우 쿼리는 수정된 메모리 부여 크기를 사용하여 동시성에 영향을 주는 과도한 메모리 부여를 줄이고 디스크로 분산하여 비용을 늘리는 부족한 메모리 부여를 수정합니다.
다음 그래프에서는 일괄 처리 모드 적응 메모리 부여 피드백을 사용하는 한 가지 예를 보여 줍니다. 쿼리를 처음 실행하는 경우 높은 분산으로 인해 기간이 **88초**였습니다.   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![높은 분산](./media/2_AQPGraphHighSpills.png)

메모리 부여 피드백을 사용하여 두 번째로 실행하는 경우 기간이 **1초**(88초에서 감소)이고 분산이 완전히 제거되며 부여가 더 높습니다. 

![분산 없음](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>메모리 부여 피드백 크기 조정
과도한 메모리 부여 조건의 경우 부여된 메모리가 실제로 사용된 메모리 크기의 두 배를 초과하면 메모리 부여 피드백이 메모리 부여를 다시 계산하고 캐시된 계획을 업데이트합니다. 메모리 부여가 1MB 미만인 계획은 초과분에 대해 다시 계산되지 않습니다.
크기가 부족한 메모리 부여 조건의 경우 일괄 처리 모드 연산자에 대해 디스크로 분산이 발생하며 메모리 부여 피드백이 메모리 부여 다시 계산을 트리거합니다. 분산 이벤트는 메모리 부여 피드백에 보고되며, *spilling_report_to_memory_grant_feedback* xEvent 이벤트를 통해 표시될 수 있습니다. 이 이벤트는 계획의 노드 ID와 해당 노드의 분산 데이터 크기를 반환합니다.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>메모리 부여 피드백 및 매개 변수가 중요한 시나리오
최적 상태를 유지하려면 매개 변수 값마다 다른 쿼리 계획이 필요할 수도 있습니다. 이러한 유형의 쿼리를 "매개 변수가 중요한" 쿼리로 정의합니다. 매개 변수가 중요한 계획의 경우 메모리 요구 사항이 불안정하면 쿼리에서 메모리 부여 피드백이 자동으로 비활성화됩니다. 쿼리가 여러 번 반복 실행된 후 계획이 비활성화되며, *memory_grant_feedback_loop_disabled* xEvent를 모니터링하면 이를 관찰할 수 있습니다. 매개 변수 스니핑 및 매개 변수 민감도에 대한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)를 참조하세요.

### <a name="memory-grant-feedback-caching"></a>메모리 부여 피드백 캐싱
단일 실행에 대해 캐시된 계획에 피드백을 저장할 수 있습니다. 그러나 메모리 부여 피드백 조정의 혜택을 받는 것은 해당 문의 연속 실행입니다. 이 기능은 문의 반복 실행에 적용됩니다. 메모리 부여 피드백은 캐시된 계획만 변경합니다. 변경 내용은 현재 쿼리 저장소에 캡처되지 않습니다.
캐시에서 계획을 제거하면 피드백이 유지되지 않습니다. 장애 조치(failover)가 있는 경우에도 피드백이 손실됩니다. `OPTION (RECOMPILE)`을 사용하는 문은 새 계획을 만들지만 캐시하지 않습니다. 캐시되지 않으므로 메모리 부여 피드백이 생성되지 않으며 해당 컴파일 및 실행을 위해 저장되지 않습니다. 그러나 `OPTION (RECOMPILE)`을 사용하지 **않는** 동등한 문(즉, 동일한 쿼리 해시 포함)을 캐시한 후 다시 실행하는 경우 연속된 문은 메모리 부여 피드백에서 혜택을 받을 수 있습니다.

### <a name="tracking-memory-grant-feedback-activity"></a>메모리 부여 피드백 작업 추적
*memory_grant_updated_by_feedback* xEvent 이벤트를 사용하여 메모리 부여 피드백 이벤트를 추적할 수 있습니다. 이 이벤트는 현재 실행 횟수 기록, 메모리 부여 피드백이 계획을 업데이트한 횟수, 수정 전 적합한 추가 메모리 부여, 메모리 부여 피드백이 캐시된 계획을 수정한 후 적합한 추가 메모리 부여를 추적합니다.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>메모리 부여 피드백, 리소스 관리자 및 쿼리 힌트
부여되는 실제 메모리는 리소스 관리자 또는 쿼리 힌트에 따른 쿼리 메모리 제한을 준수합니다.

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 일괄 처리 모드 메모리 부여 피드백 비활성화
데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 메모리 부여 피드백을 비활성화할 수 있습니다. 데이터베이스에서 발생하는 모든 쿼리 실행에 대한 일괄 처리 모드 메모리 부여 피드백을 비활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

활성화될 경우 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)에서 이 설정이 enabled로 표시됩니다.

데이터베이스에서 발생하는 모든 쿼리 실행에 대한 일괄 처리 모드 메모리 부여 피드백을 재활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

또한 `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK`을 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)로 지정하여 특정 쿼리에 대한 일괄 처리 모드 메모리 부여 피드백을 비활성화할 수 있습니다. 다음은 그 예입니다.

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT 쿼리 힌트는 데이터베이스 범위 구성 또는 추적 플래그 설정보다 우선합니다.

## <a name="row-mode-memory-grant-feedback"></a>행 모드 메모리 부여 피드백

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

행 모드 메모리 부여 피드백은 일괄 처리 및 행 모드 연산자의 메모리 부여 크기를 둘 다 조정하여 일괄 처리 모드 메모리 부여 피드백 기능을 확장합니다.  

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 행 모드 메모리 부여 피드백을 사용하도록 설정하려면 쿼리를 실행할 때 연결된 데이터베이스의 데이터베이스 호환성 수준 150을 사용하도록 설정합니다.

행 모드 메모리 부여 피드백 작업은 **memory_grant_updated_by_feedback** XEvent를 통해 표시됩니다. 

행 모드 메모리 부여 피드백부터 실제 실행 후 계획에 대한 두 가지 새로운 쿼리 계획 특성이 표시됩니다. ***IsMemoryGrantFeedbackAdjusted*** 및 ***LastRequestedMemory***는 *MemoryGrantInfo* 쿼리 계획 XML 요소에 추가됩니다. 

*LastRequestedMemory*는 이전 쿼리 실행에서 부여된 메모리를 KB(킬로바이트) 단위로 표시합니다. *IsMemoryGrantFeedbackAdjusted* 특성을 사용하면 실제 쿼리 실행 계획 내의 명령문에 대한 메모리 부여 피드백의 상태를 확인할 수 있습니다. 이 특성에 표시된 값은 다음과 같습니다.

| IsMemoryGrantFeedbackAdjusted 값 | Description |
|---|---|
| 아니요: 첫 번째 실행 | 메모리 부여 피드백은 첫 번째 컴파일 및 연결된 실행에 대한 메모리를 조정하지 않습니다.  |
| 아니요: Accurate Grant | 디스크에 분산이 없고 문이 부여된 메모리의 50% 이상을 사용하면 메모리 부여 피드백이 트리거되지 않습니다. |
| 아니요: Feedback 사용 안 함 | 메모리 부여 피드백이 지속적으로 트리거되고 메모리 증가 작업과 메모리 감소 작업 간에 변동되면 문에 대한 메모리 부여 피드백을 사용할 수 없습니다. |
| 예: 조정 | 메모리 부여 피드백이 적용되었고 다음 실행에 맞게 추가 조정될 수 있습니다. |
| 예: Stable | 메모리 부여 피드백이 적용되었고 이제 부여된 메모리가 안정적입니다. 이는 이전 실행에 마지막으로 부여된 메모리가 현재 실행에 부여된 메모리와 같음을 의미합니다. |

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 행 모드 메모리 부여 피드백 비활성화
데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 행 모드 메모리 부여 피드백을 비활성화할 수 있습니다. 데이터베이스에서 발생하는 모든 쿼리 실행에 대한 행 모드 메모리 부여 피드백을 비활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

데이터베이스에서 발생하는 모든 쿼리 실행에 대한 행 모드 메모리 부여 피드백을 재활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

또한 `DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK`을 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)로 지정하여 특정 쿼리에 대한 행 모드 메모리 부여 피드백을 비활성화할 수 있습니다. 다음은 그 예입니다.

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT 쿼리 힌트는 데이터베이스 범위 구성 또는 추적 플래그 설정보다 우선합니다.

## <a name="interleaved-execution-for-mstvfs"></a>MSTVF에 대한 인터리브 실행
인터리브 실행에서 함수의 실제 행 개수는 다운스트림 쿼리 계획을 보다 잘 결정하는 데 사용됩니다. MSTVF(다중 명령문 테이블 반환 함수)에 대한 자세한 내용은 [테이블 반환 함수](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)를 참조하세요.

인터리브 실행을 사용하면 단일 쿼리 실행에 대한 최적화 및 실행 단계 사이의 단방향 경계가 변경되며 수정된 카디널리티 예상치에 따라 계획을 조정할 수 있습니다. 최적화 중에 현재 **MSTVF(다중 명령문 테이블 반환 함수)** 인 인터리브 실행 후보를 발견할 경우 최적화를 일시 중지하고, 해당 하위 트리를 실행하고, 정확한 카디널리티 예상치를 캡처한 다음, 다운스트림 작업에 대해 최적화를 다시 시작합니다.   

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 MSTVF에 대한 고정 카디널리티 추정이 100이고, 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 1입니다. 인터리브 실행은 MSTVF와 연결된 이러한 고정 카디널리티 예상치 때문에 발생하는 워크로드 성능 문제에 도움이 됩니다. MSTVF에 대한 자세한 내용은 [사용자 정의 함수 만들기(데이터베이스 엔진)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)를 참조하세요.

다음 이미지에서는 MSTVF의 고정 카디널리티 예상치 영향을 보여주는 전체 실행 계획의 하위 집합인 [활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md) 출력을 보여줍니다. 실제 행 흐름 및 예상 행 수를 확인할 수 있습니다. 중요한 세 가지 계획 영역은 다음과 같습니다(오른쪽에서 왼쪽으로 흐름).
1. MSTVF 테이블 검색의 고정 예상치는 100개 행입니다. 그러나 이 예제에서는 실제/예상인 *527597/100*을 통해 활성 쿼리 통계에 표시되는 것처럼 527,597개 행이 이 MSTVF 테이블 검색을 통과하므로 고정 예상치와 큰 차이가 있습니다.
1. 중첩된 루프 작업의 경우 100개의 행만 조인의 외부 측면에서 반환된다고 가정합니다. 실제로 MSTVF에서 반환되는 많은 행 개수를 고려할 때 다른 조인 알고리즘을 사용하는 것이 나을 수도 있습니다.
1. 해시 일치 작업의 경우 작은 경고 기호가 표시되며, 이 경우 디스크로 분산을 나타냅니다.

![행 흐름 및 예상 행 수](./media/7_AQPFlowThreeAreas.png)

인터리브 실행을 사용하여 생성된 실제 계획과 이전 계획을 비교해 보세요.

![인터리브 계획](./media/8_AQPInterleavedEnabledPlan.png)

1. 이제 MSTVF 테이블 검색에 정확한 카디널리티 예상치가 반영됩니다. 또한 이 테이블 검색 및 기타 작업의 순서 변경을 확인합니다.
1. 조인 알고리즘의 경우 중첩된 루프 작업에서 다수의 행이 관련된 경우에 더 적합한 해시 일치 작업으로 전환했습니다.
1. 또한 MSTVF 테이블 검색에서 나오는 실제 행 수에 따라 더 많은 메모리를 다시 부여하기 때문에 분산 경고가 더 이상 표시되지 않습니다.

### <a name="interleaved-execution-eligible-statements"></a>인터리브 실행 적합한 문
인터리브 실행의 MSTVF 참조 문은 현재 읽기 전용이어야 하며 데이터 수정 작업에 포함되면 안 됩니다. 또한 런타임 상수를 사용하지 않는 경우 MSTVF는 인터리브 방식으로 실행할 수 없습니다.

### <a name="interleaved-execution-benefits"></a>인터리브 실행 혜택
일반적으로 다운스트림 계획 작업 수와 더불어 실제 행 수와 예상치 간의 차이가 클수록 성능에 미치는 영향이 커집니다.
일반적으로 인터리브 실행은 다음과 같은 쿼리에 도움이 됩니다.
1. 중간 결과 집합(이 경우 MSTVF)에 대한 실제 행 수와 예상치 간에 큰 차이가 있습니다.
1. 전체 쿼리에서 중간 결과의 크기 변경이 중요합니다. 일반적으로 쿼리 계획의 하위 트리 위에 복잡한 트리가 있는 경우에 발생합니다.
단순한 MSTVF에서 `SELECT *`의 경우 인터리브 실행이 도움이 되지 않습니다.

### <a name="interleaved-execution-overhead"></a>인터리브 실행 오버헤드
오버헤드는 최소화되거나 없어야 합니다. MSTVF는 인터리브 실행이 도입되기 전에 이미 구체화되었지만, 이제 지연 최적화를 허용한 후 구체화된 행 집합의 카디널리티 예상치를 활용한다는 차이점이 있습니다.
계획에 영향을 주는 변경 내용과 마찬가지로, 일부 계획은 하위 트리의 카디널리티가 좋을수록 전체 쿼리에 대한 계획이 더 나빠지도록 변경될 수 있습니다. 완화에는 호환성 수준 되돌리기, 쿼리 저장소를 사용하여 비회귀 버전의 계획 강제 적용 등이 포함될 수 있습니다.

### <a name="interleaved-execution-and-consecutive-executions"></a>인터리브 실행 및 연속 실행
인터리브 실행 계획이 캐시되고 나면 첫 번째 실행에서 수정된 예상치가 있는 계획이 인터리브 실행을 다시 인스턴스화하지 않고 연속 실행에 사용됩니다.

### <a name="tracking-interleaved-execution-activity"></a>인터리브 실행 작업 추적
실제 쿼리 실행 계획에서 다음 사용 특성을 확인할 수 있습니다.

| 실행 계획 특성 | Description |
| --- | --- |
| ContainsInterleavedExecutionCandidates | *QueryPlan* 노드에 적용됩니다. *true*이면 계획에 인터리브 실행 후보가 포함됩니다. |
| IsInterleavedExecuted | TVF 노드에 대한 RelOp 아래의 *RuntimeInformation* 요소의 특성입니다. *true*이면 작업이 인터리브 실행 작업의 일부로 구체화된 것입니다. |

다음과 같은 xEvent를 통해 인터리브 실행 발생을 추적할 수도 있습니다.

| xEvent | Description |
| ---- | --- |
| interleaved_exec_status | 이 이벤트는 인터리브 실행 시 발생합니다. |
| interleaved_exec_stats_update | 이 이벤트는 카디널리티 예상치가 인터리브 실행에 의해 업데이트되었음을 설명합니다. |
| Interleaved_exec_disabled_reason | 이 이벤트는 가능한 인터리브 실행 후보를 사용한 쿼리가 실제로 인터리브 실행되지 않는 경우에 발생합니다. |

인터리브 실행을 통해 MSTVF 카디널리티 예상치를 수정할 수 있으려면 쿼리를 실행해야 합니다. 그러나 예상 실행 계획은 `ContainsInterleavedExecutionCandidates` 실행 계획 특성을 통해 인터리브 실행 후보가 있는 경우를 보여줍니다.    

### <a name="interleaved-execution-caching"></a>인터리브 실행 캐싱
캐시에서 계획을 지우거나 제거한 경우 쿼리 실행 시 인터리브 실행을 사용하는 새 컴파일이 있습니다.
`OPTION (RECOMPILE)`을 사용하는 명령문은 인터리브 실행을 사용하는 새 계획을 만들고 캐시하지 않습니다.     

### <a name="interleaved-execution-and-query-store-interoperability"></a>인터리브 실행 및 쿼리 저장소 상호 운용성
인터리브 실행을 사용하는 계획을 강제로 적용할 수 있습니다. 계획은 초기 실행에 따라 카디널리티 예상치를 수정한 버전입니다.    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 인터리브된 실행 비활성화
데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 인터리브된 실행을 비활성화할 수 있습니다.  데이터베이스에서 발생하는 모든 쿼리 실행에 대한 인터리브된 실행을 비활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = OFF;
```

활성화될 경우 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)에서 이 설정이 enabled로 표시됩니다.
데이터베이스에서 발생하는 모든 쿼리 실행에 대한 인터리브된 실행을 재활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = ON;
```

또한 `DISABLE_INTERLEAVED_EXECUTION_TVF`를 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)로 지정하여 특정 쿼리에 대한 인터리브 실행을 비활성화할 수 있습니다. 다음은 그 예입니다.

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

USE HINT 쿼리 힌트는 데이터베이스 범위 구성 또는 추적 플래그 설정보다 우선합니다.

## <a name="table-variable-deferred-compilation"></a>테이블 변수 지연 컴파일

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

**테이블 변수 지연 컴파일**은 테이블 변수를 참조하는 쿼리의 플랜 품질 및 전체 성능을 개선합니다. 최적화 및 초기 플랜 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다. 이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화하는 데 사용됩니다.

테이블 변수 지연 컴파일을 사용하면 테이블 변수를 참조하는 문 컴파일은 문이 실제로 처음 실행될 때까지 지연됩니다. 이 지연 컴파일 동작은 임시 테이블의 동작과 동일합니다. 이 변경으로 인해 원래 1행 추측 대신에 실제 카디널리티가 사용됩니다. 

테이블 변수 지연 컴파일을 사용하도록 설정하려면 쿼리가 실행될 때 연결된 데이터베이스의 데이터베이스 호환성 수준 150을 사용하도록 설정합니다.

테이블 변수 지연 컴파일은 테이블 변수의 다른 특성을 변경하지 **않습니다**. 예를 들어 이 기능은 테이블 변수에 열 통계를 추가하지 않습니다.

테이블 변수 지연 컴파일은 **다시 컴파일 빈도를 늘리지 않습니다**. 대신 초기 컴파일이 발생하는 위치를 이동합니다. 그 결과로 캐시된 계획은 초기 지연 컴파일 테이블 변수 행 개수를 기반으로 생성됩니다. 캐시된 계획은 연속 쿼리에서 다시 사용됩니다. 해당 계획은 계획이 제거되거나 다시 컴파일될 때까지 다시 사용됩니다. 

초기 계획 컴파일에 사용되는 테이블 변수 행 개수는 일반적인 값이 고정된 행 개수 추측과 다를 수 있음을 나타냅니다. 이러한 행 개수가 다른 경우 다운스트림 작업에 도움이 됩니다. 테이블 변수 행 개수가 실행 간에 크게 달라지는 경우, 이 기능으로 성능이 향상되지 않을 수 있습니다.

### <a name="disabling-table-variable-deferred-compilation-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 테이블 변수 지연 컴파일 비활성화
데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 또는 문 범위에서 테이블 변수 지연 컴파일을 사용하지 않도록 설정합니다. 데이터베이스에서 발생하는 모든 쿼리 실행에 대한 테이블 변수 지연 컴파일을 사용하지 않도록 설정하려면 해당 데이터베이스의 컨텍스트 내에서 다음 예제를 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = OFF;
```

데이터베이스에서 발생하는 모든 쿼리 실행에 대한 테이블 변수 지연 컴파일을 다시 사용하도록 설정하려면 해당 데이터베이스의 컨텍스트 내에서 다음 예제를 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = ON;
```

DISABLE_DEFERRED_COMPILATION_TV를 USE HINT 쿼리 힌트로 할당하여 특정 쿼리에 대한 테이블 변수 지연 컴파일을 사용하지 않도록 설정할 수도 있습니다.  다음은 그 예입니다.

```sql
DECLARE @LINEITEMS TABLE 
    (L_OrderKey INT NOT NULL,
     L_Quantity INT NOT NULL
    );

INSERT @LINEITEMS
SELECT L_OrderKey, L_Quantity
FROM dbo.lineitem
WHERE L_Quantity = 5;

SELECT  O_OrderKey,
    O_CustKey,
    O_OrderStatus,
    L_QUANTITY
FROM    
    ORDERS,
    @LINEITEMS
WHERE   O_ORDERKEY  =   L_ORDERKEY
    AND O_OrderStatus = 'O'
OPTION (USE HINT('DISABLE_DEFERRED_COMPILATION_TV'));
```

## <a name="scalar-udf-inlining"></a>스칼라 UDF 인라인 처리

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

스칼라 UDF 인라인 처리는 [스칼라 UDF](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)를 관계형 식으로 자동으로 변환합니다. 그런 다음, 해당 식을 호출 SQL 쿼리에 포함합니다. 이 변환은 스칼라 UDF를 활용하는 워크로드의 성능을 개선합니다. 스칼라 UDF 인라인 처리는 UDF 내부에서 작업의 비용 기반 최적화를 이용합니다. 비효율적이고 반복적인 직렬 실행 계획 대신에, 효율적인 세트 지향 병렬 실행 계획이 생성됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

자세한 내용은 [스칼라 UDF 인라인 처리](../user-defined-functions/scalar-udf-inlining.md)를 참조하세요.

## <a name="approximate-query-processing"></a>대략적인 쿼리 처리

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

대략적인 쿼리 처리는 새로운 기능 제품군입니다. 이 기능은 절대적인 정밀도보다 응답성이 더 중요한 큰 데이터 세트를 기반으로 집계합니다. 예를 들어 대시보드에 표시하기 위해 100억 개 행을 기반으로 **COUNT(DISTINCT())** 를 계산합니다. 이 경우 절대적인 정밀도가 아니라 응답성이 중요합니다. 새 **APPROX_COUNT_DISTINCT** 집계 함수는 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다.

자세한 내용은 [APPROX_COUNT_DISTINCT(Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)를 참조하세요.

## <a name="batch-mode-on-rowstore"></a>rowstore의 일괄 처리 모드 

**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

rowstore의 일괄 처리 모드는 columnstore 인덱스를 요구하지 않고도 분석 워크로드에 대한 일괄 처리 모드를 실행할 수 있습니다.  이 기능은 디스크 힙 및 B-트리 인덱스에 대한 일괄 처리 모드 실행 및 비트맵 필터를 지원합니다. rowstore의 일괄 처리 모드는 기존의 모든 일괄 처리 모드 지원 연산자를 지원할 수 있습니다.

### <a name="background"></a>배경
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 분석 워크로드를 가속화하기 위한 새로운 기능인 columnstore 인덱스를 도입했습니다. 각 후속 릴리스에서 사용 사례를 확장하고 columnstore 인덱스의 성능을 개선했습니다. 지금까지 이러한 모든 기능을 단일 기능으로 표시하고 문서화했습니다. 테이블의 columnstore 인덱스를 만듭니다. 또한 분석 워크로드가 더 빠르게 이동합니다. 그러나 관련이 있으나 고유한 두 가지 기술 세트가 사용됩니다.
- **columnstore** 인덱스를 사용하면 분석 쿼리는 필요한 열의 데이터에만 액세스합니다. 또한 columnstore 형식의 페이지 압축은 기존 **rowstore** 인덱스의 압축보다 더 효과적입니다. 
- **일괄 처리 모드** 처리를 사용하면 쿼리 연산자가 데이터를 더 효율적으로 처리합니다. 이 연산자는 한 번에 하나의 행이 아니라 행 일괄 처리에서 작동합니다. 향상된 여러 다른 확장성이 일괄 처리 모드와 관련이 있습니다. 일괄 처리 모드에 대한 자세한 내용은 [실행 모드](../../relational-databases/query-processing-architecture-guide.md#execution-modes)를 참조하세요.

다음 두 가지 기능이 함께 작동해서 I/O(입출력) 및 CPU 사용률을 개선합니다.
- columnstore 인덱스를 사용하면 더 많은 데이터가 메모리에 저장됩니다. 이로 인해 I/O 워크로드가 줄어듭니다.
- 일괄 처리 모드는 CPU를 보다 효율적으로 사용합니다.

두 기술은 가능한 경우 서로를 활용합니다. 예를 들어, 일괄 처리 모드 집계를 columnstore 인덱스 검색의 일부로 평가할 수 있습니다. 또한 일괄 처리 모드 조인 및 일괄 처리 모드 집계를 사용하면 실행 길이 인코딩을 사용하여 압축한 columnstore 데이터가 훨씬 더 효율적으로 처리됩니다. 
 
그러나 두 기능이 독립적이라는 것을 이해해야 합니다.
* columnstore 인덱스를 사용하는 행 모드 계획을 가져올 수 있습니다.
* rowstore 인덱스만 사용하는 일괄 처리 모드 계획을 가져올 수 있습니다. 

일반적으로 두 기능을 함께 사용할 때 최상의 결과를 얻을 수 있습니다. 따라서 현재까지 SQL Server 쿼리 최적화 프로그램은 columnstore 인덱스에 하나 이상의 테이블을 연결하는 쿼리에 대해서만 일괄 처리 모드를 고려했습니다.

columnstore 인덱스는 일부 애플리케이션에 적합하지 않을 수 있습니다. 애플리케이션이 columnstore 인덱스에서 지원되지 않는 일부 다른 기능을 사용할 수 있습니다. 예를 들어 바로 수정 기능은 columnstore 압축과 호환되지 않습니다. 따라서 클러스터형 columnstore 인덱스가 있는 테이블에서는 트리거가 지원되지 않습니다. 무엇보다도 columnstore 인덱스는 **DELETE** 및 **UPDATE** 문에 대한 오버헤드를 추가합니다. 

일부 하이브리드 트랜잭션 분석 워크로드에서는 columnstore 인덱스 사용에서 얻는 이점보다 트랜잭션 워크로드의 오버헤드가 더 큽니다. 해당 시나리오는 일괄 처리 모드 처리만 채택하여 개선된 CPU 사용량을 활용할 수 있습니다. 그 이유는 rowstore 기능의 일괄 처리 모드는 관련된 인덱스 형식과 관계없이 모든 쿼리에서 일괄 처리 모드를 고려하기 때문입니다.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>rowstore에서 일괄 처리 모드를 활용할 수 있는 워크로드
다음 워크로드는 rowstore에서 일괄 처리 모드를 활용할 수 있습니다.
* 워크로드의 상당한 부분이 분석 쿼리로 구성됩니다. 일반적으로 해당 쿼리에는 수십만 개 이상의 행을 처리하는 조인 또는 집계 같은 연산자가 사용됩니다.
* 워크로드는 CPU에 따라 제한됩니다. I/O에서 병목 상태가 나타나면 가능한 경우 columnstore 인덱스를 고려하는 것이 좋습니다.
* Columnstore 인덱스를 만들면 워크로드의 트랜잭션 부분에 너무 많은 오버헤드가 추가됩니다. 그렇지 않더라도 애플리케이션이 columnstore 인덱스에서 아직 지원되지 않는 기능을 사용하기 때문에 columnstore 인덱스는 적합하지 않습니다.


> [!NOTE]
> rowstore의 일괄 처리 모드는 CPU 사용량을 줄여야 도움이 됩니다. 병목 상태가 I/O와 관련되고 데이터가 아직 캐시(“콜드” 캐시)되지 않은 경우 rowstore의 일괄 처리 모드는 쿼리 경과 시간을 개선하지 않습니다. 마찬가지로 머신에 모든 데이터를 캐시할 메모리가 충분하지 않은 경우 성능이 저하될 가능성이 높습니다.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>rowstore의 일괄 처리 모드 변경 내용은?

데이터베이스를 호환성 수준 150으로 설정합니다. 다른 변경은 필요하지 않습니다.

쿼리가 columnstore 인덱스에 어떤 테이블에도 액세스하지 않지만, 쿼리 프로세서는 추론을 사용하여 일괄 처리 모드를 고려할지 여부를 결정합니다. 추론은 다음 검사로 구성됩니다.
1. 입력 쿼리에서 테이블 크기, 사용되는 연산자, 예상 카디널리티의 초기 검사
2. 추가 검사점(최적화 프로그램이 쿼리에 대해 좀 더 저렴한 새 계획을 검색하기 때문에 필요) 이 대체 계획이 일괄 처리 모드를 충분히 사용하지 않을 경우 최적화 프로그램은 일괄 처리 모드의 대안을 더 이상 검색하지 않습니다.


rowstore에서 일괄 처리 모드가 사용되는 경우에는 쿼리 계획에서 실제 실행 모드가 **일괄 처리 모드**로 표시됩니다. scan 연산자는 디스크의 힙 및 B-트리 인덱스에 일괄 처리 모드를 사용합니다. 이 일괄 처리 모드 검사는 일괄 처리 모드 비트맵 필터를 평가할 수 있습니다. 또한 계획에 다른 일괄 처리 모드 연산자가 표시될 수 있습니다. 예를 들어 해시 조인, 해시 기반 집계, 정렬, 창 집계, 필터, 연결 및 컴퓨팅 스칼라 연산자가 있습니다.

### <a name="remarks"></a>설명

쿼리 계획이 항상 일괄 처리 모드를 사용하는 것은 아닙니다. 쿼리 최적화 프로그램에서 일괄 처리 모드가 쿼리에 도움이 되는지 결정할 수 있습니다. 

쿼리 최적화 프로그램의 검색 공간이 변경되고 있습니다. 행 모드 계획을 가져오는 경우 더 낮은 호환성 수준에서 가져오는 계획과 같을 수 있습니다. 일괄 처리 모드 계획을 가져오는 경우 columnstore 인덱스와 함께 가져오는 계획과 같지 않을 수 있습니다. 

새 일괄 처리 모드 rowstore 검사 때문에 columnstore 및 rowstore 인덱스를 혼합하는 쿼리의 경우 계획이 변경될 수도 있습니다.

rowstore 검사의 새 일괄 처리 모드에 대한 현재 제한 사항은 다음과 같습니다. 
- 메모리 내 OLTP 테이블 또는 디스크에 있는 힙 및 B-트리 이외의 인덱스에는 이러한 제한이 적용되지 않습니다. 
- 대형 개체(LOB) 열을 가져오거나 필터링하는 경우에도 제한이 적용되지 않습니다. 이 제한 사항에는 스파스 열 집합 및 XML 열이 포함됩니다.

일괄 처리 모드가 columnstore 인덱스와 함께 사용되지 않는 쿼리가 있습니다. 예를 들어 커서가 포함된 쿼리입니다. rowstore의 일괄 처리 모드에도 이 제외가 동일하게 적용됩니다.

### <a name="configure-batch-mode-on-rowstore"></a>rowstore에서 일괄 처리 모드 구성
**BATCH_MODE_ON_ROWSTORE** 데이터베이스 범위 구성은 기본적으로 켜집니다. 이 구성은 데이터베이스 호환성 수준을 변경하지 않고도 rowstore의 일괄 처리 모드를 사용하지 않도록 설정합니다.

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

데이터베이스 범위 구성을 통해 rowstore에서 일괄 처리 모드를 사용하지 않도록 설정할 수 있습니다. 하지만 **ALLOW_BATCH_MODE** 쿼리 힌트를 사용하여 쿼리 수준에서 설정을 재정의할 수 있습니다. 다음 예제에서는 데이터베이스 범위 구성을 통해 일괄 처리 기능이 사용되지 않도록 설정되었어도 rowstore에서 일괄 처리 모드를 사용하도록 설정합니다.

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

또한 **DISALLOW_BATCH_MODE** 쿼리 힌트를 사용하여 특정 쿼리의 rowstore에서 일괄 처리 모드를 사용하지 않도록 설정할 수 있습니다. 다음 예제를 참조하십시오.

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>참고 항목
[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)    
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[조인](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)(적응 쿼리 처리 시연)       
[지능형 쿼리 처리 시연](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)   
