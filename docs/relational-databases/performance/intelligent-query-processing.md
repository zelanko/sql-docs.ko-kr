---
title: Microsoft SQL 데이터베이스의 지능형 쿼리 처리 | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 쿼리 성능을 향상시키는 지능형 쿼리 처리 기능입니다.
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b92bc15079fcc85212ea3d1b51be64a3348a4b1
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305371"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 데이터베이스의 지능형 쿼리 처리

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

지능형 QP(쿼리 처리) 기능 제품군에는 광범위한 영향을 가진 기능이 포함됩니다. 이 기능은 최소한의 구현 노력으로 기존 워크로드의 성능을 개선합니다. 자동으로 이 기능 제품군의 혜택을 얻으려면 해당하는 데이터베이스 호환성 수준으로 이동합니다.

| **IQP 기능** | **Azure SQL Database에서 지원** | **SQL Server에서 지원** |
| --- | --- | --- |
| [적응 조인(일괄 처리 모드)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 SQL Server 2017부터|
| [대략적인 Count Distinct](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | 예. 공개 미리 보기| 예. SQL Server 2019 CTP 2.0부터, 공개 미리 보기|
| [Rowstore의 일괄 처리 모드](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | 예. 호환성 수준 150 미만, 공개 미리 보기| 예. 호환성 수준 150 미만 SQL Server 2019 CTP 2.0부터, 공개 미리 보기|
| [인터리브 실행](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 SQL Server 2017부터|
| [메모리 부여 피드백(일괄 처리 모드)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | 예. 호환성 수준 140 미만| 예. 호환성 수준 140 미만 SQL Server 2017부터|
| [메모리 부여 피드백(행 모드)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | 예. 호환성 수준 150 미만, 공개 미리 보기| 예. 호환성 수준 150 미만 SQL Server 2019 CTP 2.0부터, 공개 미리 보기|
| [스칼라 UDF 인라인 처리](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | 아니요. 하지만 향후 업데이트에 대해 계획됨 | 예. 호환성 수준 150 미만 SQL Server 2019 CTP 2.1부터, 공개 미리 보기|
| [테이블 변수 지연 컴파일](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | 예. 호환성 수준 150 미만, 공개 미리 보기| 예. 호환성 수준 150 미만 SQL Server 2019 CTP 2.0부터, 공개 미리 보기|



## <a name="adaptive-query-processing"></a>적응 쿼리 처리

적응 쿼리 처리 기능 제품군에는 다음 쿼리 처리 개선 사항이 포함됩니다. 이 개선 사항은 애플리케이션 워크로드의 런타임 조건에 대한 최적화 전략에 맞게 조정됩니다. 
- 일괄 처리 모드 적응 조인
- 메모리 부여 피드백
- MSTVF(다중 문 테이블 반환 함수)에 대한 인터리브 실행

### <a name="batch-mode-adaptive-joins"></a>일괄 처리 모드 적응 조인

이 기능을 사용하면 계획인 단일 캐시된 계획을 사용하여 실행 중에 더 나은 조인 전략으로 동적으로 전환될 수 있습니다.

일괄 처리 모드 적응 조인에 대한 자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](../../relational-databases/performance/adaptive-query-processing.md)를 참조하세요.

### <a name="row-and-batch-mode-memory-grant-feedback"></a>행 및 일괄 처리 모드 메모리 부여 피드백

> [!NOTE]
> 행 모드 메모리 부여 피드백은 공용 미리 보기 기능입니다.  

이 기능은 쿼리에 필요한 실제 메모리를 다시 계산합니다. 그런 다음, 캐시된 계획의 부여 값을 업데이트합니다. 동시성에 영향을 주는 과도한 메모리 부여를 줄입니다. 이 기능은 디스크로 분산되어 비용을 늘리는 과소 예측된 메모리 부여도 수정합니다.

메모리 부여 피드백에 대한 자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](../../relational-databases/performance/adaptive-query-processing.md)를 참조하세요.

### <a name="interleaved-execution-for-mstvfs"></a>MSTVF에 대한 인터리브 실행

인터리브 실행에서 함수의 실제 행 개수는 다운스트림 쿼리 계획을 보다 잘 결정하는 데 사용됩니다. MSTVF(다중 명령문 테이블 반환 함수)에 대한 자세한 내용은 [테이블 반환 함수](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)를 참조하세요.

인터리브된 실행에 대한 자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](../../relational-databases/performance/adaptive-query-processing.md)를 참조하세요.

## <a name="table-variable-deferred-compilation"></a>테이블 변수 지연 컴파일

> [!NOTE]
> 테이블 변수 지연 컴파일은 공개 미리 보기 기능입니다.  

테이블 변수 지연 컴파일은 테이블 변수를 참조하는 쿼리의 계획 품질 및 전체 성능을 개선합니다. 최적화 및 초기 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다. 이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화합니다.

테이블 변수 지연 컴파일은 문이 실제로 처음 실행될 때까지 테이블 변수를 참조하는 문 컴파일을 지연합니다. 이 지연 컴파일 동작은 임시 테이블의 동작과 동일합니다. 이 변경으로 인해 원래 1행 추측 대신에 실제 카디널리티가 사용됩니다. 

Azure SQL Database에서 테이블 변수 지연 컴파일의 공개 미리 보기를 사용하도록 설정할 수 있습니다. 이 작업을 수행하려면 쿼리를 실행할 때 연결된 데이터베이스의 데이터베이스 호환성 수준 150을 사용하도록 설정합니다.

자세한 내용은 [테이블 변수 지연 컴파일](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation)을 참조하세요.

## <a name="scalar-udf-inlining"></a>스칼라 UDF 인라인 처리

> [!NOTE]
> 스칼라 UDF(사용자 정의 함수) 인라인 처리는 공개 미리 보기 기능입니다.  

스칼라 UDF 인라인 처리는 [스칼라 UDF](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)를 관계형 식으로 자동으로 변환합니다. 그런 다음, 해당 식을 호출 SQL 쿼리에 포함합니다. 이 변환은 스칼라 UDF를 활용하는 워크로드의 성능을 개선합니다. 스칼라 UDF 인라인 처리는 UDF 내부에서 작업의 비용 기반 최적화를 이용합니다. 비효율적이고 반복적인 직렬 실행 계획 대신에, 효율적인 세트 지향 병렬 실행 계획이 생성됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

자세한 내용은 [스칼라 UDF 인라인 처리](../user-defined-functions/scalar-udf-inlining.md)를 참조하세요.

## <a name="approximate-query-processing"></a>대략적인 쿼리 처리

> [!NOTE]
> **APPROX_COUNT_DISTINCT**는 공개 미리 보기 기능입니다.  

대략적인 쿼리 처리는 새로운 기능 제품군입니다. 이 기능은 절대적인 정밀도보다 응답성이 더 중요한 큰 데이터 세트를 기반으로 집계합니다. 예를 들어 대시보드에 표시하기 위해 100억 개 행을 기반으로 **COUNT(DISTINCT())** 를 계산합니다. 이 경우 절대적인 정밀도가 아니라 응답성이 중요합니다. 새 **APPROX_COUNT_DISTINCT** 집계 함수는 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다.

자세한 내용은 [APPROX_COUNT_DISTINCT(Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)를 참조하세요.

## <a name="batch-mode-on-rowstore"></a>rowstore의 일괄 처리 모드 

> [!NOTE]
> rowstore의 일괄 처리 모드는 공개 미리 보기 기능입니다.  

rowstore의 일괄 처리 모드는 columnstore 인덱스를 요구하지 않고도 분석 워크로드에 대한 일괄 처리 모드를 실행할 수 있습니다.  이 기능은 디스크 힙 및 B-트리 인덱스에 대한 일괄 처리 모드 실행 및 비트맵 필터를 지원합니다. rowstore의 일괄 처리 모드는 기존의 모든 일괄 처리 모드 지원 연산자를 지원할 수 있습니다.

### <a name="background"></a>배경

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 분석 워크로드를 가속화하기 위한 새로운 기능인 columnstore 인덱스를 도입했습니다. 각 후속 릴리스에서 사용 사례를 확장하고 columnstore 인덱스의 성능을 개선했습니다. 지금까지 이러한 모든 기능을 단일 기능으로 표시하고 문서화했습니다. 테이블의 columnstore 인덱스를 만듭니다. 또한 분석 워크로드가 더 빠르게 이동합니다. 그러나 관련이 있으나 고유한 두 가지 기술 세트가 사용됩니다.
- **columnstore** 인덱스를 사용하면 분석 쿼리는 필요한 열의 데이터에만 액세스합니다. 또한 columnstore 형식의 페이지 압축은 기존 **rowstore** 인덱스의 압축보다 더 효과적입니다. 
- **일괄 처리 모드** 처리를 사용하면 쿼리 연산자가 데이터를 더 효율적으로 처리합니다. 이 연산자는 한 번에 하나의 행이 아니라 행 일괄 처리에서 작동합니다. 향상된 여러 다른 확장성이 일괄 처리 모드와 관련이 있습니다. 일괄 처리 모드에 대한 자세한 내용은 [실행 모드](../../relational-databases/query-processing-architecture-guide.md#execution-modes)를 참조하세요.

다음 두 가지 기능이 함께 작동해서 I/O(입출력) 및 CPU 사용을 개선합니다.
- columnstore 인덱스를 사용하면 더 많은 데이터가 메모리에 저장됩니다. I/O에 대한 필요성이 줄어듭니다.
- 일괄 처리 모드는 CPU를 보다 효율적으로 사용합니다.

두 기술은 가능한 경우 서로를 활용합니다. 예를 들어, 일괄 처리 모드 집계를 columnstore 인덱스 검색의 일부로 평가할 수 있습니다. 일괄 처리 모드 조인 및 일괄 처리 모드 집계를 사용하면 실행 길이 인코딩을 사용하여 압축한 columnstore 데이터를 훨씬 더 효율적으로 처리할 수 있습니다. 
 
두 가지 기능은 개별적으로 사용할 수 있습니다.
* Columnstore 인덱스를 사용하는 행 모드 계획을 가져옵니다.
* rowstore 인덱스만 사용하는 일괄 처리 모드 계획을 가져옵니다. 

일반적으로 두 기능을 함께 사용할 때 최상의 결과를 얻을 수 있습니다. 따라서 현재까지 SQL Server 쿼리 최적화 프로그램은 columnstore 인덱스에 하나 이상의 테이블을 연결하는 쿼리에 대해서만 일괄 처리 모드를 고려했습니다.

Columnstore 인덱스는 일부 애플리케이션에 적합하지 않습니다. 애플리케이션이 columnstore 인덱스에서 지원되지 않는 일부 다른 기능을 사용할 수 있습니다. 예를 들어 바로 수정 기능은 columnstore 압축과 호환되지 않습니다. 따라서 클러스터형 columnstore 인덱스가 있는 테이블에서는 트리거가 지원되지 않습니다. 무엇보다도 columnstore 인덱스는 **DELETE** 및 **UPDATE** 문에 대한 오버헤드를 추가합니다. 

일부 하이브리드 트랜잭션 분석 워크로드에서는 columnstore 인덱스의 이점보다 워크로드의 트랜잭션 측면에서 발생하는 오버헤드가 더 큽니다. 해당 시나리오는 일괄 처리 모드 처리에서만 CPU 사용을 개선할 수 있습니다. 그 이유는 rowstore 기능의 일괄 처리 모드는 모든 쿼리에서 일괄 처리 모드를 고려하기 때문입니다. 사용된 인덱스가 무엇인지는 중요하지 않습니다.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>rowstore에서 일괄 처리 모드를 활용할 수 있는 워크로드

다음 워크로드는 rowstore에서 일괄 처리 모드를 활용할 수 있습니다.
* 워크로드의 상당한 부분이 분석 쿼리로 구성됩니다. 일반적으로 해당 쿼리에는 수십만 개 이상의 행을 처리하는 조인 또는 집계 같은 연산자가 포함됩니다.
* 워크로드는 CPU에 따라 제한됩니다. I/O에서 병목 상태가 나타나면 가능한 경우 columnstore 인덱스를 고려하는 것이 좋습니다.
* Columnstore 인덱스를 만들면 워크로드의 트랜잭션 부분에 너무 많은 오버헤드가 추가됩니다. 그렇지 않더라도 애플리케이션이 columnstore 인덱스에서 아직 지원되지 않는 기능을 사용하기 때문에 columnstore 인덱스는 적합하지 않습니다.

> [!NOTE]
> rowstore의 일괄 처리 모드는 CPU 사용량을 줄여야 도움이 됩니다. 병목 상태가 I/O와 관련되고 데이터가 아직 캐시(“콜드” 캐시)되지 않은 경우 rowstore의 일괄 처리 모드는 경과된 시간을 개선하지 않습니다. 마찬가지로 컴퓨터에 모든 데이터를 캐시할 메모리가 충분하지 않은 경우 성능이 저하될 가능성이 높습니다.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>rowstore의 일괄 처리 모드 변경 내용은?

호환성 수준 150으로 전환하는 것 외에, 후보 워크로드의 rowstore에서 일괄 처리 모드를 사용하도록 설정하기 위해 사용자가 수행해야 하는 변경 작업은 없습니다.

쿼리가 columnstore 인덱스에 어떤 테이블도 연결하지 않지만, 쿼리 프로세서는 이제 추론을 사용하여 일괄 처리 모드를 고려할지 여부를 결정합니다. 추론은 다음 검사로 구성됩니다.
1. 입력 쿼리에서 테이블 크기, 사용되는 연산자, 예상 카디널리티의 초기 검사
2. 추가 검사점(최적화 프로그램이 쿼리에 대해 좀 더 저렴한 새 계획을 검색하기 때문에 필요) 이 대체 계획이 일괄 처리 모드를 충분히 사용하지 않을 경우 최적화 프로그램은 일괄 처리 모드의 대안을 더 이상 검색하지 않습니다.

rowstore에서 일괄 처리 모드가 사용되는 경우에는 쿼리 계획에서 실제 실행 모드가 **일괄 처리 모드**로 표시됩니다. scan 연산자는 디스크의 힙 및 B-트리 인덱스에 일괄 처리 모드를 사용합니다. 이 일괄 처리 모드 검사는 일괄 처리 모드 비트맵 필터를 평가할 수 있습니다. 또한 계획에 다른 일괄 처리 모드 연산자가 표시될 수 있습니다. 예를 들어 해시 조인, 해시 기반 집계, 정렬, 창 집계, 필터, 연결 및 계산 스칼라 연산자가 있습니다.

### <a name="remarks"></a>Remarks

* 쿼리 계획이 항상 일괄 처리 모드를 사용하는 것은 아닙니다. 쿼리 최적화 프로그램은 해당 일괄 처리 모드가 쿼리에 도움이 되는지 결정할 수 있습니다. 
* 쿼리 최적화 프로그램의 검색 공간이 변경되고 있습니다. 행 모드 계획을 가져오는 경우 더 낮은 호환성 수준에서 가져오는 계획과 같을 수 있습니다. 일괄 처리 모드 계획을 가져오는 경우 columnstore 인덱스와 함께 가져오는 계획과 같지 않을 수 있습니다. 
* 새 일괄 처리 모드 rowstore 검사 때문에 columnstore 및 rowstore 인덱스를 혼합하는 쿼리의 경우 계획이 변경될 수도 있습니다.
* rowstore 검사의 새 일괄 처리 모드에 대한 현재 제한 사항은 다음과 같습니다. 
    * 메모리 내 OLTP 테이블 또는 디스크에 있는 힙 및 B-트리 이외의 인덱스에는 이러한 제한이 적용되지 않습니다. 
    * 대형 개체(LOB) 열을 가져오거나 필터링하는 경우에도 제한이 적용되지 않습니다. 이 제한 사항에는 스파스 열 집합 및 XML 열이 포함됩니다.
* 일괄 처리 모드가 columnstore 인덱스와 함께 사용되지 않는 쿼리가 있습니다. 예를 들어 커서가 포함된 쿼리입니다. rowstore의 일괄 처리 모드에도 이 제외가 동일하게 적용됩니다.

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

## <a name="see-also"></a>관련 항목:

[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)    
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[조인](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)(적응 쿼리 처리 시연)       
[Demonstrating Intelligent QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)(지능형 QP 시연)   
