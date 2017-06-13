---
title: "마이그레이션 후 유효성 검사 및 최적화 가이드 | Microsoft Docs"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: d81eabfa1bdb5736bbf6f53ed34c2e1ac157e782
ms.contentlocale: ko-kr
ms.lasthandoff: 05/25/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>마이그레이션 후 유효성 검사 및 최적화 가이드
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]사후 마이그레이션 단계는 모든 데이터의 정확성과 완결성을 조정 하는 데 매우 중요으로 통해 작업의 성능 문제.

# <a name="common-performance-scenarios"></a>일반적인 성능 시나리오 
다음은 몇 가지 일반적인 성능 시나리오로 마이그레이션한 후 발생 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 플랫폼 및이 문제를 해결 하는 방법입니다. 한 시나리오를 specifdic를 여기에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 외래 플랫폼 (예: Oracle, DB2, MySQL 및 Sybase) 뿐만 아니라 마이그레이션 (최신 버전으로 이전 버전) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

## <a name="Parameter Sniffing"></a>매개 변수 스니핑에 대 한 민감도

**적용 대상:** 외래 플랫폼 (예: Oracle, DB2, MySQL 및 Sybase)을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

> [!NOTE]
> 에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 문제는 원본에 존재 하는 경우 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최신 버전으로 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로-을이 시나리오를 다루지 합니다. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]해당 입력 내용을 데이터 분포에 대 한 액세스에 최적화 된 매개 변수가 있는 및 다시 사용할 수 있는 계획을 생성 하는 첫 번째 컴파일에 입력된 매개 변수 스니핑를 사용 하 여 저장된 프로시저에 쿼리 계획을 컴파일합니다. 하지 저장 프로시저, 경우에 사소한 계획을 생성 하는 대부분 문 매개 변수화 됩니다. 먼저 계획을 캐시 한 후 나중에 실행 되는 이전에 캐시 된 계획에 매핑됩니다.
잠재적인 문제에는 해당 첫 번째 컴파일 되지 사용 했을 수는 가장 일반적인 매개 변수 집합이 일반적인 작업에 대 한 경우 발생 합니다. 다른 매개 변수에 대 한 동일한 실행 계획 비효율적인 됩니다.

### <a name="steps-to-resolve"></a>해결 단계

1.    사용 하 여 `RECOMPILE` 힌트입니다. 계획에는 각 매개 변수 값에 적용할 때마다 계산 됩니다.
2.    옵션을 사용 하려면 저장된 프로시저를 다시 작성 `(OPTIMIZE FOR(<input parameter> = <value>))`합니다. 대부분의 관련 작업이 생성 및를 효율적으로 매개 변수가 있는 값에 대 한 계획을 유지 관리 도구를 사용 하는 값에 적합 한 결정 합니다.
3.    프로시저 내의 지역 변수를 사용 하 여 저장된 프로시저를 다시 작성 합니다. 이제는 최적화 프로그램이 사용는 밀도 벡터 양이나에 대 한 결과 매개 변수 값에 관계 없이 동일한 계획 합니다.
4.    옵션을 사용 하려면 저장된 프로시저를 다시 작성 `(OPTIMIZE FOR UNKNOWN)`합니다. 로컬 변수 기술을 사용 하는 것과 같습니다.
5.    힌트를 사용 하도록 쿼리를 다시 작성 `DISABLE_PARAMETER_SNIFFING`합니다. 하지 않는 한 매개 변수 스니핑 완전히 사용 하지 않도록 설정 하 여 로컬 변수 기술을 사용 하 여 효과가 같음 `OPTION(RECOMPILE)`, `WITH RECOMPILE` 또는 `OPTIMIZE FOR <value>` 사용 됩니다.

> [!TIP] 
> 활용 하는 방법의 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 계획 분석 기능 신속 하 게 식별할 경우 이런 동기화 문제가 발생 합니다. 추가 정보가 제공 [여기](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/)합니다.

## <a name="Missing indexes"></a>누락 된 인덱스

**적용 대상:** 외래 플랫폼 (예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

잘못 되었거나 누락 된 인덱스 추가 메모리를 별도 I/O 불필요 하 게 되 고 CPU 사용 하면 됩니다. 이 이전 사용 하는 등 작업 부하 프로필 변경 되었기 때문에 기존 무효화 하는 다른 조건자 인덱스 디자인 합니다. 작업 부하 프로필의 변경 내용 또는 저하 인덱싱 전략의 증명 정보는 다음과 같습니다.
-   중복을 중복 거의 사용 되지 않는 완전히 사용 되지 않는 인덱스를 찾습니다.
-   업데이트를 사용 하지 않는 인덱스를 특별 한 주의 합니다.

### <a name="steps-to-resolve"></a>해결 단계

1.    모든 누락 된 인덱스 참조에 대 한 그래픽 실행 계획을 활용 합니다.
2.    에 의해 생성 된 제안 하는 인덱스가 [데이터베이스 엔진 튜닝 관리자](../tools/dta/tutorial-database-engine-tuning-advisor.md)합니다.
3.    활용 하는 방법의 [누락 된 인덱스 DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) 또는 [SQL Server 성능 대시보드](https://www.microsoft.com/en-us/download/details.aspx?id=29063)합니다.
4.    기존 Dmv를 사용 하 여 모든 인덱스 참조가 암시/에 하드 코딩 기존 프로시저 및 함수 데이터베이스의 경우 뿐만 아니라 모든 누락, 중복, 중복, 거의 사용 되지 않는 및 완전히 사용 하지 않은 인덱스에 대 한 정보를 제공 하는 기존 스크립트를 활용 합니다. 

> [!TIP] 
> 이러한 기존 스크립트의 예로 [인덱스 생성](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) 및 [인덱스 정보](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information)합니다. 

## <a name="Inability to use predicates"></a>데이터를 필터링 하는 조건자를 사용할 수

**적용 대상:** 외래 플랫폼 (예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

> [!NOTE]
> 에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 문제는 원본에 존재 하는 경우 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최신 버전으로 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로-을이 시나리오를 다루지 합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]쿼리 최적화 프로그램 컴파일 타임에 알려 지는 정보에 대 한 설명만 수 있습니다. 작업 실행 시간에만 알고 있어야 하는 조건자를 사용 하는 경우에 저하 계획 선택에 대 한 가능성이 증가 합니다. 더 나은 품질 계획에 대 한 조건자 해야 **SARGable**, 또는 **S**earch **Arg**문서**수**합니다.

비 SARGable 조건자의 예:
-   VARCHAR, NVARCHAR로 또는 VARCHAR로는 INT와 같은 암시적 데이터 변환 실제 실행 계획에서 런타임 CONVERT_IMPLICIT 경고를 찾아보십시오. 한 형식에서 다른 형식으로 변환 하는 경우에 정밀도 손실이 발생할 수 있습니다.
-   와 같은 복잡 한 임의의 식을 `WHERE UnitPrice + 1 < 3.975`, 아닌 `WHERE UnitPrice < 320 * 200 * 32`합니다.
-   와 같은 함수를 사용 하 여 식을 `WHERE ABS(ProductID) = 771` 또는`WHERE UPPER(LastName) = 'Smith'`
-   와 같은 선행 와일드 카드 문자를 문자열 `WHERE LastName LIKE '%Smith'`, 아닌 `WHERE LastName LIKE 'Smith%'`합니다.

### <a name="steps-to-resolve"></a>해결 단계

1. 항상 의도 한 대상으로 변수/매개 변수를 선언 [데이터 형식을](../t-sql/data-types/data-types-transact-sql.md)합니다. 
  -   기본 테이블에 사용 되는 데이터 형식에 대 한 정보를 보유 하는 시스템 테이블 (예: 저장된 프로시저, 사용자 정의 함수 또는 뷰) 데이터베이스에 저장 되어 있는 모든 사용자 정의 코드 구문을 비교 눌러야 할 수 있습니다 (예: [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)).
2. 를 이전 시점에 모든 코드를 통과할 수 없는 경우 다음 같은 목적을 위해 데이터 형식을 변경 테이블에 있는 변수/매개 변수 선언은 일치 하도록 합니다.
3. 다음과 같은 구문이의 유용성 아웃 이유:
  -   조건자로 사용 되는 함수
  -   와일드 카드 검색 합니다.
  -   – 칼럼 형식 데이터를 기반으로 하는 복잡 한 식 대신; 인덱싱할 수 있는 지속형된 계산된 열을 만들 필요가 평가

> [!NOTE] 
> 위의 모든 가능 programmaticaly 합니다.

## <a name="Table Valued Functions"></a>테이블 반환 함수 (다중 문 vs 인라인)의 사용

**적용 대상:** 외래 플랫폼 (예: Oracle, DB2, MySQL 및 Sybase) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 마이그레이션.

> [!NOTE]
> 에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 문제는 원본에 존재 하는 경우 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최신 버전으로 마이그레이션 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로-을이 시나리오를 다루지 합니다.

테이블 반환 함수는 보기에는 대신 일 수 있는 테이블 데이터 형식을 반환 합니다. 뷰에서 단일 `SELECT` 문, 사용자 정의 함수 보기에서 가능한 것 보다 더 많은 논리를 허용 하는 추가 문을 포함할 수 있습니다.

> [!IMPORTANT] 
> 컴파일 타임에는 MSTVF (다중 문 테이블 반환 함수)의 출력 테이블을 만들지는 이후는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램 추론 및 행은 예측이 잘못 확인 하려면 하지 실제 통계 의존 합니다. 기본 테이블에 인덱스를 추가 하는 경우에이 잘못 된 수 있도록 합니다. MSTVFs에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 MSTVF에서 반환할 예상 행 수가 1의 고정된 예측을 사용 하 여 (부터는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 추정을 고정 하는 100 개 행).

### <a name="steps-to-resolve"></a>해결 단계
1.    다중 문 TVF 하나의 문으로 이면 인라인 TVF를 변환 합니다.

    ```tsql
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

    ```tsql
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

2.    더 복잡 한 경우에 메모리 액세스에 최적화 된 테이블이 나 임시 테이블에 저장 된 중간 결과 사용 하는 것이 좋습니다.

##  <a name="Additional_Reading"></a> 더 보기  
 [쿼리 저장소에 대한 모범 사례](../relational-databases/performance/best-practice-with-the-query-store.md)  
[메모리 액세스에 최적화된 테이블](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[사용자 정의 함수](../relational-databases/user-defined-functions/user-defined-functions.md)  
[테이블 변수 및 행은 예측이 잘못-1 부](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[테이블 변수 및 행은 예측이 잘못-2 부](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[실행 계획 캐싱 및 재사용](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

