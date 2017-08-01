---
title: "Microsoft SQL 데이터베이스의 적응 쿼리 처리 | Microsoft Docs | Microsoft Docs"
description: "SQL Server 2017 이상 및 Azure SQL Database에서 쿼리 성능을 향상시키는 적응 쿼리 처리 기능입니다."
ms.custom: 
ms.date: 07/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: 
ms.assetid: 
author: joesackmsft
ms.author: josack;monicar
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: cf8509cab2424529ca0ed16c936fa63a139dfca4
ms.openlocfilehash: eff546e84d3f872406136f68a7fdbbd8147175ca
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---

# <a name="adaptive-query-processing-in-sql-databases"></a>SQL 데이터베이스의 적응 쿼리 처리

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

이 문서에서는 SQL Server 및 Azure SQL Database에서 쿼리 성능을 향상시키는 데 사용할 수 있는 다음과 같은 적응 쿼리 처리 기능을 소개합니다.
- 일괄 처리 모드 메모리 부여 피드백
- 일괄 처리 모드 적응 조인
- 인터리브 실행 

일반 수준에서 SQL Server는 다음과 같이 쿼리를 실행합니다.
1. 쿼리 최적화 프로세스는 특정 쿼리에 대한 가능한 실행 계획 집합을 생성합니다. 이 시간 동안 계획 옵션의 비용이 추정되고 예상 비용이 가장 낮은 계획이 사용됩니다.
1. 쿼리 실행 프로세스는 쿼리 최적화 프로그램에서 선택된 계획을 사용하고 실행에 이용합니다.
    
쿼리 최적화 프로그램에서 선택된 계획이 여러 가지 이유로 적합하지 않은 경우도 있습니다. 예를 들어 쿼리 계획을 통해 이동하는 예상 행 수가 잘못되었을 수 있습니다. 예상 비용은 실행에 이용하도록 선택되는 계획을 결정하는 데 도움이 됩니다. 카디널리티 예상치가 잘못된 경우 원래 추정이 부실해도 원래 계획이 사용됩니다.

![적응 쿼리 처리 기능](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>적응 쿼리 처리를 사용하도록 설정하는 방법
데이터베이스에 대해 호환성 수준 140을 사용하도록 설정하여 워크로드가 적응 쿼리 처리에 자동으로 적합하도록 만들 수 있습니다.  Transact-SQL을 사용하여 설정할 수 있습니다. 예를 들어
```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```
## <a name="batch-mode-memory-grant-feedback"></a>일괄 처리 모드 메모리 부여 피드백
SQL Server의 쿼리 실행 후 계획에는 실행에 필요한 최소 필수 메모리 및 모든 행을 메모리에 포함하기 위한 이상적인 메모리 부여 크기가 포함됩니다. 메모리 부여 크기가 잘못 지정된 경우 성능이 저하됩니다. 과도하게 부여하면 메모리가 낭비되고 동시성이 줄어듭니다. 메모리 부여가 부족하면 디스크로 분산되어 비용이 증가합니다. 반복 워크로드를 처리함으로써 일괄 처리 모드 메모리 부여 피드백은 쿼리에 필요한 실제 메모리를 다시 계산한 후 캐시된 계획에 대한 부여 값을 업데이트합니다.  동일한 쿼리 문을 실행할 경우 쿼리는 수정된 메모리 부여 크기를 사용하여 동시성에 영향을 주는 과도한 메모리 부여를 줄이고 디스크로 분산하여 비용을 늘리는 부족한 메모리 부여를 수정합니다.
다음 그래프에서는 일괄 처리 모드 적응 메모리 부여 피드백을 사용하는 한 가지 예를 보여 줍니다. 쿼리를 처음 실행하는 경우 높은 분산으로 인해 기간이 *88초*였습니다.
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

메모리 부여 피드백을 사용하여 두 번째로 실행하는 경우 기간이 *1초*(88초에서 감소)이고 분산이 완전히 제거되며 부여가 더 높습니다. 

![분산 없음](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>메모리 부여 피드백 크기 조정
*과도한 부여의 경우* 부여된 메모리가 실제로 사용된 메모리 크기의 두 배를 초과하면 메모리 부여 피드백이 메모리 부여를 다시 계산하고 캐시된 계획을 업데이트합니다.  메모리 부여가 1MB 미만인 계획은 초과분에 대해 다시 계산되지 않습니다.
*크기가 부족한 메모리 부여의 경우* 일괄 처리 모드 연산자에 대해 디스크로 분산이 발생하며 메모리 부여 피드백이 메모리 부여 다시 계산을 트리거합니다. 분산 이벤트는 메모리 부여 피드백에 보고되며, *spilling_report_to_memory_grant_feedback* XEvent 이벤트를 통해 표시될 수 있습니다. 이 이벤트는 계획의 노드 ID와 해당 노드의 분산 데이터 크기를 반환합니다.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>메모리 부여 피드백 및 매개 변수가 중요한 시나리오
최적 상태를 유지하려면 매개 변수 값마다 다른 쿼리 계획이 필요할 수도 있습니다. 이러한 유형의 쿼리를 "매개 변수가 중요한" 쿼리로 정의합니다. 매개 변수가 중요한 계획의 경우 메모리 요구 사항이 불안정하면 쿼리에서 메모리 부여 피드백이 자동으로 비활성화됩니다.  쿼리가 여러 번 반복 실행된 후 계획이 비활성화되며, *memory_grant_feedback_loop_disabled* XEvent를 모니터링하면 이를 관찰할 수 있습니다.

### <a name="memory-grant-feedback-caching"></a>메모리 부여 피드백 캐싱
단일 실행에 대해 캐시된 계획에 피드백을 저장할 수 있습니다. 그러나 메모리 부여 피드백 조정의 혜택을 받는 것은 해당 문의 연속 실행입니다. 이 기능은 문의 반복 실행에 적용됩니다. 메모리 부여 피드백은 캐시된 계획만 변경합니다. 변경 내용은 현재 쿼리 Ssore에 캡처되지 않습니다.
캐시에서 계획을 제거하면 피드백이 유지되지 않습니다. 장애 조치(failover)가 있는 경우에도 피드백이 손실됩니다. OPTION(RECOMPILE)을 사용하는 문은 새 계획을 만들지만 캐시하지 않습니다. 캐시되지 않으므로 메모리 부여 피드백이 생성되지 않으며 해당 컴파일 및 실행을 위해 저장되지 않습니다.  그러나 OPTION(RECOMPILE)을 사용하지 *않는* 동등한 문(즉, 동일한 쿼리 해시 포함)을 캐시한 후 다시 실행하는 경우 연속된 문은 메모리 부여 피드백에서 혜택을 받을 수 있습니다.

### <a name="tracking-memory-grant-feedback-activity"></a>메모리 부여 피드백 작업 추적
*memory_grant_updated_by_feedback* XEvent 이벤트를 사용하여 메모리 부여 피드백 이벤트를 추적할 수 있습니다.  이 이벤트는 현재 실행 횟수 기록, 메모리 부여 피드백이 계획을 업데이트한 횟수, 수정 전 적합한 추가 메모리 부여, 메모리 부여 피드백이 캐시된 계획을 수정한 후 적합한 추가 메모리 부여를 추적합니다.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>메모리 부여 피드백, 리소스 관리자 및 쿼리 힌트
부여되는 실제 메모리는 리소스 관리자 또는 쿼리 힌트에 따른 쿼리 메모리 제한을 준수합니다.

## <a name="batch-mode-adaptive-joins"></a>일괄 처리 모드 적응 조인
일괄 처리 모드 적응 조인 기능을 사용하면 해시 조인 또는 중첩된 루프 조인 메서드 선택을 첫 번째 입력이 검사된 *후*까지 지연할 수 있습니다.  적응 조인 연산자는 중첩된 루프 계획으로 전환할 시기를 결정하는 데 사용되는 임계값을 정의합니다. 따라서 계획이 실행 중에 더 나은 조인 전략으로 동적으로 전환할 수 있습니다.
작동 방식은 다음과 같습니다.
- 중첩된 루프 조인이 해시 조인보다 적합할 만큼 빌드 조인 입력의 행 수가 충분히 작으면 계획이 중첩된 루프 알고리즘으로 전환됩니다.
- 빌드 조인 입력이 특정 행 수 임계값을 초과하면 전환이 발생하지 않으며 계획이 해시 조인을 계속 사용합니다.

다음 쿼리는 적응 조인 예제를 설명하기 위해 사용됩니다.

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 360;
```

이 쿼리는 336개의 행을 반환합니다.  활성 쿼리 통계를 사용하도록 설정하면 다음 계획이 표시됩니다.

![쿼리 결과 336개 행](./media/4_AQPStats336Rows.png)

계획에 다음이 표시됩니다.
- 해시 조인 빌드 단계에 대한 행을 제공하는 데 사용되는 columnstore 인덱스 검색이 있습니다.
- 새 적응 조인 연산자가 있습니다. 이 연산자는 중첩된 루프 계획으로 전환할 시기를 결정하는 데 사용되는 임계값을 정의합니다.  이 예제에서 임계값은 78개 행입니다.  &gt;= 78개 행이면 모두 해시 조인을 사용합니다.  임계값보다 작으면 중첩된 루프 조인이 사용됩니다.
- 336개 행을 반환하기 때문에 임계값을 초과하므로 두 번째 분기가 표준 해시 조인 작업의 프로브 단계를 나타냅니다. 활성 쿼리 통계는 연산자를 통과하는 행(이 경우 "672/672")을 보여 줍니다.
- 마지막 분기는 임계값을 초과하지 않을 경우 중첩된 루프 조인에서 사용하기 위한 Clustered Index Seek입니다. "0/336"개 행이 표시됩니다(분기가 사용되지 않음).
 이제 계획과 동일한 쿼리를 비교해 보겠습니다. 하지만 이번에는 테이블에 하나의 행만 있는 Quantity 값에 대해 쿼리합니다.
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 361;
```
쿼리가 하나의 행을 반환합니다.  활성 쿼리 통계를 사용하도록 설정하면 다음 계획이 표시됩니다.

![쿼리 결과 하나의 행](./media/5_AQPStatsOneRow.png)

계획에 다음이 표시됩니다.
- 하나의 행이 반환되면 이제 Clustered Index Seek에 통과하는 행이 있음을 확인할 수 있습니다.
- 해시 조인 빌드 단계를 계속 진행하지 않았으므로 두 번째 분기를 통과하는 행이 0개로 표시됩니다.

### <a name="adaptive-join-benefits"></a>적응 조인 혜택
작은 조인 입력 검색과 큰 조인 입력 검색 간에 자주 변동하는 워크로드가 이 기능에서 가장 큰 혜택을 받게 됩니다.

### <a name="adaptive-join-overhead"></a>적응 조인 오버헤드
적응 조인은 동등한 인덱스 중첩된 루프 조인 계획보다 메모리 요구 사항이 더 높습니다. 중첩된 루프가 해시 조인인 것처럼 추가 메모리가 요청됩니다. 동등한 중첩된 루프 스트리밍 조인에 비해 스탑앤고(stop-and-go) 작업으로서 빌드 단계에 대한 오버헤드도 있습니다. 빌드 입력의 행 수가 변동될 수 있는 시나리오에서 해당 추가 비용과 함께 유연성이 제공됩니다.

### <a name="adaptive-join-caching-and-re-use"></a>적응 조인 캐싱 및 다시 사용
일괄 처리 모드 적응 조인은 문의 초기 실행에서 작동하며, 컴파일된 후에는 컴파일된 적응 조인 임계값과 외부 입력의 빌드 단계를 통과하는 런타임 행에 따라 연속 실행이 적응 상태로 유지됩니다.

### <a name="tracking-adaptive-join-activity"></a>적응 조인 작업 추적
적응 조인 연산자에는 다음과 같은 계획 연산자 특성이 있습니다.

| 계획 특성 | Description |
|--- |--- |
| AdaptiveThresholdRows | 해시 조인에서 중첩된 루프 조인으로 전환하는 데 사용되는 임계값을 보여 줍니다. |
| EstimatedJoinType | 가능한 조인 형식입니다. |
| ActualJoinType | 실제 계획에서 임계값에 따라 최종적으로 선택된 조인 알고리즘을 보여 줍니다. |

예상 계획은 정의된 적응 조인 임계값 및 예상 조인 형식과 함께 적응 조인 계획 모양을 보여 줍니다.

### <a name="adaptive-join-and-query-store-interoperability"></a>적응 조인 및 쿼리 저장소 상호 운용성
쿼리 저장소는 일괄 처리 모드 적응 조인 계획을 캡처하고 강제로 적용할 수 있습니다.

### <a name="adaptive-join-eligible-statements"></a>적응 조인 적합한 문
논리 조인을 일괄 처리 모드 적응 조인에 적합하게 만드는 몇 가지 조건은 다음과 같습니다.
- 데이터베이스 호환성 수준이 140입니다.
- 쿼리가 SELECT 문입니다(데이터 수정 문은 현재 적합하지 않음).
- 인덱싱된 중첩된 루프 조인 또는 해시 조인 실제 알고리즘 둘 다에서 조인을 실행할 수 있습니다.
- 해시 조인이 쿼리 전체의 Columnstore 인덱스 현재 상태를 통해 또는 조인에서 직접 참조되는 Columnstore 인덱싱된 테이블을 통해 일괄 처리 모드를 사용합니다.
- 중첩된 루프 조인 및 해시 조인의 생성된 대체 솔루션에 동일한 첫 번째 자식(외부 참조)이 있어야 합니다.

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>적응 조인 및 중첩된 루프 효율성
적응 조인이 중첩된 루프 작업으로 전환하는 경우 해시 조인 빌드에서 이미 읽은 행이 사용됩니다. 연산자는 외부 참조 행을 다시 읽지 *않습니다*.

### <a name="adaptive-threshold-rows"></a>적응 임계값 행
다음 차트에서는 해시 조인 비용과 중첩된 루프 조인 대안 비용 간의 교차 예를 보여 줍니다.  이 교차 지점에서 결정되는 임계값에 따라 다시 조인 작업에 사용되는 실제 알고리즘이 결정됩니다.

![조인 임계값](./media/6_AQPJoinThreshold.png)

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>다중 문 테이블 반환 함수에 대한 인터리브 실행
인터리브 실행을 사용하면 단일 쿼리 실행에 대한 최적화 및 실행 단계 사이의 단방향 경계가 변경되며 수정된 카디널리티 예상치에 따라 계획을 조정할 수 있습니다. 최적화 중에 현재 **MSTVF(다중 문 테이블 반환 함수)**인 인터리브 실행 후보를 발견할 경우 최적화를 일시 중지하고, 해당 하위 트리를 실행하고, 정확한 카디널리티 예상치를 캡처한 다음 다운스트림 작업에 대해 최적화를 다시 시작합니다.
SQL Server 2014 및 SQL Server 2016에서는 MSTVF에 대한 고정 카디널리티 추정이 "100"이고, 이전 버전에서는 "1"입니다. 인터리브 실행은 다중 문 테이블 반환 함수와 연결된 이러한 고정 카디널리티 예상치 때문에 발생하는 워크로드 성능 문제에 도움이 됩니다.

다음 이미지에서는 MSTVF의 고정 카디널리티 예상치 영향을 보여 주는 전체 실행 계획의 하위 집합인 활성 쿼리 통계 출력을 보여 줍니다. 실제 행 흐름 및 예상 행 수를 확인할 수 있습니다. 중요한 세 가지 계획 영역은 다음과 같습니다(오른쪽에서 왼쪽으로 흐름).
1. MSTVF 테이블 검색의 고정 예상치는 100개 행입니다. 그러나 이 예제에서는 실제/예상인 "527597/100"을 통해 활성 쿼리 통계에 표시되는 것처럼 *527,597*개 행이 이 MSTVF 테이블 검색을 통과하므로 고정 예상치와 큰 차이가 있습니다.
1. 중첩된 루프 작업의 경우 100개의 행만 조인의 외부 측면에서 반환된다고 가정합니다. 실제로 MSTVF에서 반환되는 많은 행 개수를 고려할 때 다른 조인 알고리즘을 사용하는 것이 나을 수도 있습니다.
1. 해시 일치 작업의 경우 작은 경고 기호가 표시되며, 이 경우 디스크로 분산을 나타냅니다.

![행 흐름 및 예상 행 수](./media/7_AQPFlowThreeAreas.png)

인터리브 실행을 사용하여 생성된 실제 계획과 이전 계획을 비교해 보세요.

![인터리브 계획](./media/8_AQPInterleavedEnabledPlan.png)

1. 이제 MSTVF 테이블 검색에 정확한 카디널리티 예상치가 반영됩니다. 또한 이 테이블 검색 및 기타 작업의 순서 변경을 확인합니다.
1. 조인 알고리즘의 경우 중첩된 루프 작업에서 다수의 행이 관련된 경우에 더 적합한 해시 일치 작업으로 전환했습니다.
1. 또한 MSTVF 테이블 검색에서 나오는 실제 행 수에 따라 더 많은 메모리를 다시 부여하기 때문에 분산 경고가 더 이상 표시되지 않습니다.

### <a name="interleaved-execution-eligible-statements"></a>인터리브 실행 적합한 문
인터리브 실행의 MSTVF 참조 문은 현재 읽기 전용이어야 하며 데이터 수정 작업에 포함되면 안 됩니다. 또한 MSTVF는 CROSS APPLY 내부에서 사용되는 경우 인터리브 실행에 적합하지 않습니다.

### <a name="interleaved-execution-benefits"></a>인터리브 실행 혜택
일반적으로 다운스트림 계획 작업 수와 더불어 실제 행 수와 예상치 간의 차이가 클수록 성능에 미치는 영향이 커집니다.
일반적으로 인터리브 실행은 다음과 같은 쿼리에 도움이 됩니다.
1. 중간 결과 집합(이 경우 MSTVF)에 대한 실제 행 수와 예상치 간에 큰 차이가 있습니다.
1. 전체 쿼리에서 중간 결과의 크기 변경이 중요합니다. 일반적으로 쿼리 계획의 하위 트리 위에 복잡한 트리가 있는 경우에 발생합니다.
단순한 MSTVF에서 "SELECT *"의 경우 인터리브 실행이 도움이 되지 않습니다.

### <a name="interleaved-execution-overhead"></a>인터리브 실행 오버헤드
오버헤드는 최소화되거나 없어야 합니다. MSTVF는 인터리브 실행이 도입되기 전에 이미 구체화되었지만, 이제 지연 최적화를 허용한 후 구체화된 행 집합의 카디널리티 예상치를 활용한다는 차이점이 있습니다.
계획에 영향을 주는 변경 내용과 마찬가지로, 일부 계획은 하위 트리의 카디널리티가 좋을수록 전체 쿼리에 대한 계획이 더 나빠지도록 변경될 수 있습니다. 완화에는 호환성 수준 되돌리기, 쿼리 저장소를 사용하여 비회귀 버전의 계획 강제 적용 등이 포함될 수 있습니다.

### <a name="interleaved-execution-and-consecutive-executions"></a>인터리브 실행 및 연속 실행
인터리브 실행 계획이 캐시되고 나면 첫 번째 실행에서 수정된 예상치가 있는 계획이 인터리브 실행을 다시 인스턴스화하지 않고 연속 실행에 사용됩니다.

### <a name="tracking-interleaved-execution-activity"></a>인터리브 실행 작업 추적
실제 쿼리 실행 계획에서 다음 사용 특성을 확인할 수 있습니다.

| 계획 특성 | Description |
| --- | --- |
| ContainsInterleavedExecutionCandidates | *QueryPlan* 노드에 적용할 때 "true"이면 계획에 인터리브 실행 후보가 포함됩니다. |
| IsInterleavedExecuted | 이 특성은 TVF 노드에 대한 RelOp 아래의 RuntimeInformation 요소 내부에 있습니다. "true"이면 작업이 인터리브 실행 작업의 일부로 구체화된 것입니다. |

다음과 같은 XEvent를 통해 인터리브 실행 발생을 추적할 수도 있습니다.

| XEvent | Description |
| ---- | --- |
| interleaved_exec_status | 이 이벤트는 인터리브 실행 시 발생합니다. |
| interleaved_exec_stats_update | 이 이벤트는 카디널리티 예상치가 인터리브 실행에 의해 업데이트되었음을 설명합니다. |
| Interleaved_exec_disabled_reason | 이 이벤트는 가능한 인터리브 실행 후보를 사용한 쿼리가 실제로 인터리브 실행되지 않는 경우에 발생합니다. |

인터리브 실행을 통해 MSTVF 카디널리티 예상치를 수정할 수 있으려면 쿼리를 실행해야 합니다. 그러나 예상 실행 계획은 ContainsInterleavedExecutionCandidates 특성을 통해 인터리브 실행 후보가 있는 경우를 보여 줍니다.

### <a name="interleaved-execution-caching"></a>인터리브 실행 캐싱
캐시에서 계획을 지우거나 제거한 경우 쿼리 실행 시 인터리브 실행을 사용하는 새 컴파일이 있습니다.
OPTION(RECOMPILE)을 사용하는 문은 인터리브 실행을 사용하는 새 계획을 만들고 캐시하지 않습니다.

### <a name="interleaved-execution-and-query-store-interoperability"></a>인터리브 실행 및 쿼리 저장소 상호 운용성
인터리브 실행을 사용하는 계획을 강제로 적용할 수 있습니다. 계획은 초기 실행에 따라 카디널리티 예상치를 수정한 버전입니다.

## <a name="see-also"></a>관련 항목:

[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](https://docs.microsoft.com/en-us/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database)   

[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)(적응 쿼리 처리 시연)      



