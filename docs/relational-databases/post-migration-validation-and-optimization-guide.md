---
title: 마이그레이션 후 유효성 검사 및 최적화 가이드 | Microsoft Docs
ms.custom: ''
ms.date: 5/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: ''
ms.openlocfilehash: 72d3f28c6cc0e2998004b8b4883fdb846e2a92e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="post-migration-validation-and-optimization-guide"></a>마이그레이션 후 유효성 검사 및 최적화 가이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션 후 단계는 데이터 정확도와 완전성을 조정하고 작업의 성능 문제를 파악하는 데 매우 중요합니다.

# <a name="common-performance-scenarios"></a>일반적인 성능 시나리오 
다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 플랫폼으로 마이그레션한 후 발생하는 몇 가지 일반적인 성능 시나리오와 해결 방법입니다. 여기에는 이전 버전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 새 버전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션 및 Oracle, DB2, MySQL, Sybase 등의 외래 플랫폼에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션에 특정한 시나리오가 포함됩니다.

## <a name="CEUpgrade"></a>CE 버전 변경으로 인한 쿼리 성능 저하

**적용 대상:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 이상 버전으로 마이그레이션할 때, 그리고 [데이터베이스 호환성 수준](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)을 최신으로 업그레이드할 때는 작업이 성능 저하 위험에 노출될 수 있습니다.

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]부터는 쿼리 최적화 프로그램의 모든 변경 내용이 최신 [데이터베이스 호환성 수준](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)에 연결되므로 계획이 업그레이드 시점에 즉시 변경되지 않고 사용자가 `COMPATIBILITY_LEVEL` 데이터베이스 옵션을 최신 상태로 변경하는 경우에 변경됩니다. 이 기능은 쿼리 저장소와 함께 업그레이드 프로세스에서 쿼리 성능에 대한 뛰어난 제어 수준을 제공합니다. 

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에 도입된 쿼리 최적화 프로그램 변경 사항에 대한 자세한 내용은 [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](http://msdn.microsoft.com/library/dn673537.aspx)(SQL Server 2014 카디널리티 평가기로 쿼리 계획 최적화)를 참조하세요.

### <a name="steps-to-resolve"></a>해결 단계

[데이터베이스 호환성 수준](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)을 소스 버전으로 변경하고 다음 그림에 나온 권장 업그레이드 워크플로를 따릅니다.

![query-store-usage-5](../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  

이 항목에 대한 자세한 내용은 [Keep performance stability during the upgrade to newer SQL Server](../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)(최신 SQL Server로 업그레이드하는 동안 성능 안정성 유지)를 참조하세요.

## <a name="ParameterSniffing"></a> 매개 변수 검색의 민감도

**적용 대상:** 외래 플랫폼(예: Oracle, DB2, MySQL 및 Sybase)에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션은 이 문제가 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있는 경우 최신 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 그대로 마이그레이션해도 이 시나리오가 해결되지 않습니다. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 첫 컴파일 시 입력 매개 변수를 검색하고 해당 입력 데이터 분포에 최적화된 매개 변수가 있고 재사용 가능한 계획을 생성하여 저장 프로시저의 쿼리 계획을 컴파일합니다. 저장 프로시저가 아닌 경우에도 간단한 계획을 생성하는 문은 대부분 매개 변수가 가집니다. 계획이 처음 캐시된 후 이후 실행은 모두 기존에 캐시된 계획에 매핑됩니다.
첫 번째 컴파일 시 일반 작업에 대해 가장 일반적인 매개 변수 집합을 사용하지 않았을 경우 문제가 발생할 수 있습니다. 매개 변수가 다르면 같은 실행 계획의 효율이 떨어집니다. 이 항목에 대한 자세한 내용은 [매개 변수 스니핑](../relational-databases/query-processing-architecture-guide.md#ParamSniffing)을 참조하세요.

### <a name="steps-to-resolve"></a>해결 단계

1.  `RECOMPILE` 힌트를 사용합니다. 각 매개 변수 값이 조정될 때마다 계획이 계산됩니다.
2.  `(OPTIMIZE FOR(<input parameter> = <value>))` 옵션을 사용하도록 저장 프로시저를 다시 작성합니다. 관련 작업 대부분에 적합한 값을 사용할 값으로 결정하여 매개 변수가 있는 값에 효율적인 하나의 계획을 만들고 유지합니다.
3.  프로시저 내의 지역 변수를 사용하여 저장 프로시저를 다시 작성합니다. 최적화 프로그램은 예상치에 밀도 벡터를 사용하므로 매개 변수 값과 관계없이 계획이 동일합니다.
4.  `(OPTIMIZE FOR UNKNOWN)` 옵션을 사용하도록 저장 프로시저를 다시 작성합니다. 지역 변수 기술을 사용하는 것과 결과가 같습니다.
5.  `DISABLE_PARAMETER_SNIFFING` 힌트를 사용하도록 쿼리를 다시 작성합니다. `OPTION(RECOMPILE)`, `WITH RECOMPILE` 또는 `OPTIMIZE FOR <value>`를 사용하는 경우 외에는 매개 변수 검색을 완전히 사용하지 않도록 설정하므로 지역 변수 기술을 사용하는 것과 결과가 같습니다.

> [!TIP] 
> [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 계획 분석 기능을 활용하면 이로 인해 문제가 발생하는지 빠르게 식별할 수 있습니다. 자세한 내용은 [여기](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/)를 참조하세요.

## <a name="MissingIndexes"></a> 누락된 인덱스

**적용 대상:** 외래 플랫폼(예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션

인덱스가 잘못되거나 누락되면 추가 I/O가 발생하여 메모리와 CPU가 불필요하게 사용됩니다. 다른 조건자 사용, 기존 인덱스 디자인 무효화 등과 같이 작업 프로필이 변경되기 때문일 수 있습니다. 잘못된 인덱싱 전략이나 작업 프로필의 변경을 알 수 있는 방법은 다음과 같습니다.
-   중복되는 인덱스, 거의 사용되지 않거나 완전히 사용되지 않는 인덱스를 찾습니다.
-   업데이트가 있는 사용되지 않는 인덱스에 특히 주의합니다.

### <a name="steps-to-resolve"></a>해결 단계

1.  모든 누락된 인덱스 참조에 대해 그래픽 실행 계획을 활용합니다.
2.  [데이터베이스 엔진 튜닝 관리자](../tools/dta/tutorial-database-engine-tuning-advisor.md)에서 생성한 인덱싱 제안 사항을 검토합니다.
3.  [SQL Server 성능 대시보드](https://www.microsoft.com/en-us/download/details.aspx?id=29063)를 통해 [누락된 인덱스 DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)를 활용합니다.
4.  기존 DMV를 사용하여 누락되거나 중복되거나 거의 사용되지 않거나 전혀 사용되지 않는 인덱스에 대한 정보를 제공할 수 있는 기존 스크립트를 활용하고 인덱스 참조가 힌트로 제공되거나 데이터베이스의 기존 프로시저 및 함수에 하드 코딩되었는지 확인합니다. 

> [!TIP] 
> 이러한 기존 스크립트의 예로 [Index Creation](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) 및 [Index Information](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information)을 들 수 있습니다. 

## <a name="InabilityPredicates"></a> 조건자를 사용하여 데이터를 필터링할 수 없음

**적용 대상:** 외래 플랫폼(예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션은 이 문제가 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있는 경우 최신 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 그대로 마이그레이션해도 이 시나리오가 해결되지 않습니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 컴파일 시간에 알려진 정보만 설명할 수 있습니다. 작업에서 실행 시간에만 알 수 있는 조건자를 사용하는 경우 잘못된 계획을 선택할 가능성이 증가합니다. 계획의 품질을 개선하려면 조건자가 **SARGable** 또는 **S**earch **Arg**ument**able**이어야 합니다.

SARGable이 아닌 조건자의 몇 가지 예:
-   VARCHAR에서 NVARCHAR로, INT에서 VARCHAR로 등의 암시적 데이터 변환. 실제 실행 계획에서 런타임 CONVERT_IMPLICIT 경고를 찾습니다. 형식을 다른 형식으로 변환하면 정밀도도 떨어질 수 있습니다.
-   `WHERE UnitPrice + 1 < 3.975` 같은 결정되지 않은 복잡한 식이지만 `WHERE UnitPrice < 320 * 200 * 32`는 아님.
-   `WHERE ABS(ProductID) = 771` 또는`WHERE UPPER(LastName) = 'Smith'` 등과 같은 함수를 사용하는 식
-   `WHERE LastName LIKE '%Smith'`이지만 `WHERE LastName LIKE 'Smith%'`는 아님과 같이 선행 와일드카드 문자를 사용하는 문자열

### <a name="steps-to-resolve"></a>해결 단계

1. 항상 변수/매개 변수를 원하는 대상 [데이터 형식](../t-sql/data-types/data-types-transact-sql.md)으로 선언합니다. 
  -   이를 위해서는 데이터베이스(예: 저장 프로시저, 사용자 정의 함수 또는 뷰)에 저장된 사용자 정의 코드 구문을 기본 테이블(예: [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md))에서 사용되는 데이터 형식에 대한 정보를 저장하는 시스템 테이블과 비교해야 할 수 있습니다.
2. 모든 코드를 이전 시점으로 트래버스할 수 없는 경우에는 같은 목적으로 테이블의 데이터 형식을 변수/매개 변수 선언과 일치하도록 변경합니다.
3. 다음 구문을 유용성을 생각해 보세요.
  -   조건자로 사용되는 함수
  -   와일드카드 검색
  -   칼럼 형식 데이터를 기반으로 하는 복잡한 식 - 인덱싱할 수 있는 지속형 계산 열 대신 만들 필요가 있는지 평가

> [!NOTE] 
> 위의 모든 작업을 프로그래밍 방식으로 수행할 수 있습니다.

## <a name="TableValuedFunctions"></a> 테이블 반환 함수(다중 문 및 인라인) 사용

**적용 대상:** 외래 플랫폼(예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로의 마이그레이션은 이 문제가 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있는 경우 최신 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 그대로 마이그레이션해도 이 시나리오가 해결되지 않습니다.

테이블 반환 함수는 뷰 대신 사용할 수 있는 테이블 데이터 형식을 반환합니다. 뷰에서는 `SELECT` 문을 하나만 사용할 수 있지만 사용자 정의 함수에서는 여러 문을 사용할 수 있으므로 뷰에서보다 논리를 더 추가할 수 있습니다.

> [!IMPORTANT] 
> MSTVF(다중 문 테이블 반환 함수)의 출력 테이블은 컴파일 시간에 생성되지 않으므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 실제 통계가 아닌 추론을 사용하여 행 예상치를 결정합니다. 이 경우 인덱스를 기본 테이블에 추가하더라도 도움이 되지 않습니다. MSTVF의 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 MSTVF에서 반환할 것으로 예상되는 행 수에 고정 예상치 1([!INCLUDE[ssSQL14](../includes/sssql14-md.md)]부터 고정 예상치는 100개 행)을 사용합니다.

### <a name="steps-to-resolve"></a>해결 단계
1.  다중 문 TVF에 문이 하나뿐인 경우 인라인 TVF로 변환합니다.

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```
    수행할 작업 

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.  더 복잡한 경우 메모리 액세스에 최적화된 테이블 또는 임시 테이블에 저장된 중간 결과를 사용합니다.

##  <a name="Additional_Reading"></a> 더 보기  
 [쿼리 저장소에 대한 모범 사례](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[사용자 정의 함수](../relational-databases/user-defined-functions/user-defined-functions.md)  
[Table Variables and Row Estimations - Part 1](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)(테이블 변수 및 행 예상치 - 1부)  
[Table Variables and Row Estimations - Part 2](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)(테이블 변수 및 행 예상치 - 2부)  
[실행 계획 캐싱 및 다시 사용](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)
