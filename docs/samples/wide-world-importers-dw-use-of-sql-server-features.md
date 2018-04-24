---
title: WideWorldImporters OLAP 데이터베이스-SQL Server 사용 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 46272806944c87c7c0971229da9f56d10eea2c08
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>SQL Server 기능 및 특성의 WideWorldImportersDW 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
WideWorldImportersDW는 다양 한 데이터 웨어하우스 및 분석에 적합 한 SQL Server의 주요 기능을 보여 주기 위해 설계 되었습니다. 다음 목록은 SQL Server 기능 및 기능과 WideWorldImportersDW에서 사용 되는 방법을 설명 합니다.

## <a name="polybase"></a>PolyBase

[SQL Server (2016 이상)에 적용 됩니다]

PolyBase는 판매 정보를 WideWorldImportersDW sales의 추가 확장에 대 한 관심 있는 도시 이해 하려면 인구 통계에 대 한 공용 데이터 집합으로 결합 하는 데 사용 됩니다.

예제 데이터베이스에 PolyBase 사용을 활성화 하려면가 설치 되어 있는지 확인 하 고 데이터베이스에서 다음 저장된 프로시저를 실행 합니다.

    EXEC [Application].[Configuration_ApplyPolybase]

이렇게 하면 외부 테이블 만들어집니다 `dbo.CityPopulationStatistics` 미국의 Azure blob 저장소에서 호스팅되는 도시의 인구 데이터를 포함 하는 공용 데이터 집합을 참조 하는 합니다. 구성 프로세스를 이해 하는 저장된 프로시저의 코드를 검토 하 라는 메시지가 표시 됩니다. Azure blob 저장소에 직접 데이터를 호스팅하는 일반 공용 액세스에서 안전 하 게 유지 하려는 경우에 추가 구성 단계를 수행 해야 합니다. 다음 쿼리는 해당 외부 데이터 집합에서 데이터를 반환합니다.

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

어떤 도시 추가 확장을 위해 추가할 수 있습니다를 이해 하려면 다음 쿼리는 도시, 증가 속도 살펴보고을 크게 증가 하는 상위 100 개의 가장 큰 도시를 반환 Wide World Importers에 판매 있지 없는 합니다. 쿼리에 원격 테이블 간 조인을 포함 되어 `dbo.CityPopulationStatistics` 및 로컬 테이블 `Dimension.City`, 및 로컬 테이블과 관련 된 필터 `Fact.Sales`합니다.

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>클러스터형 columnstore 인덱스

(전체 버전의 샘플)

클러스터형된 Columnstore 인덱스 CCI ()를 저장소 공간을 줄이고 쿼리 성능을 향상 시킬 모든 팩트 테이블에 사용 됩니다. CCI 사용 하 여 팩트 테이블에 대 한 기본 저장소는 열 압축을 사용합니다.

비클러스터형 인덱스는 클러스터형된 columnstore 인덱스를 기반으로 기본 키 및 외래 키 제약 조건을 간편 하 게 사용 됩니다. 이러한 제약 조건은 다양 한 주의에서 추가 된-ETL 프로세스의 무결성을 적용 하는 제약 조건이 있는 WideWorldImporters 데이터베이스의 데이터 소스가 있습니다. 기본 및 외래 키 제약 조건 및 해당 지원 인덱스 제거 팩트 테이블의 저장소 사용 공간을 줄이는 것입니다.

**데이터 크기**

예제 데이터베이스를 쉽게 다운로드 하 고 샘플을 설치의 데이터 크기를 제한 했습니다. 그러나 columnstore 인덱스의 실제 성능 이점을 큰 데이터 집합을 사용 하려면 것입니다.

크기를 늘리려면 다음 문을 실행할 수 있습니다는 `Fact.Sales` 다른 12 백만 행의 샘플 데이터를 삽입 하 여 테이블입니다. 이러한 행이 모든 삽입, 2012 년에 대 한 간섭을 ETL 프로세스와 되도록 합니다.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

이 문을 실행 하려면 5 분 정도 걸립니다. 12 백만 개 이상의 행을 삽입 하려면 원하는 수의 행이 저장된 프로시저에 매개 변수로 전달 합니다.

쿼리 성능을 columnstore 없는 비교를 삭제 하거나 클러스터형된 columnstore 인덱스를 다시 만들 수 있습니다.

인덱스를 삭제 하려면

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

다시 만듭니다.

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>분할

(전체 버전의 샘플)

데이터 웨어하우스의 데이터 크기는 매우 커질 수 있습니다. 따라서 있기 분할을 사용 하는 데이터베이스의 대형 테이블의 저장소를 관리 하기 좋습니다.

더 큰 팩트 테이블의 모든 연도별로 분할 됩니다. 유일한 예외는 `Fact.Stock Holdings`되지 않는 날짜를 기준으로 하 고 다른 팩트 테이블은 제한 된 데이터 크기를 비교 합니다.

모든 분할 된 테이블에 사용 되는 파티션 함수는 `PF_Date`를 사용 하 고 파티션 구성표는 및 `PS_Date`합니다.

## <a name="in-memory-oltp"></a>메모리 내 OLTP

(전체 버전의 샘플)

WideWorldImportersDW는 SCHEMA_ONLY 메모리 액세스에 최적화 된 테이블을 사용 하 여 준비 테이블에 대 한 합니다. 모든 `Integration.` * `_Staging` 테이블은 SCHEMA_ONLY 메모리 액세스에 최적화 된 테이블입니다.

SCHEMA_ONLY 테이블의 장점은 기록 되지 않습니다 및 모든 디스크 액세스가 필요 없는 것입니다. 이렇게 하면 ETL 프로세스의 성능이 향상 됩니다. 이러한 테이블 로깅되지 않습니다 이후 오류가 발생 하는 경우 해당 내용이 손실 됩니다. 그러나 etl 간단히 다시 시작할 수 오류가 발생 하므로 데이터 원본은 계속 사용할 수입니다.
