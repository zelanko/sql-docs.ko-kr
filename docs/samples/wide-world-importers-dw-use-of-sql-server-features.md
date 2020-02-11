---
title: DW WideWorldImporters 데이터베이스의 주요 기능
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: dfce2ce4a6f13a25687d668268f532893c1404e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056295"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>SQL Server 기능 및 기능 WideWorldImportersDW 사용
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW는 데이터 웨어하우징 및 분석에 적합 한 SQL Server의 많은 주요 기능을 보여 주기 위해 설계 되었습니다. 다음은 SQL Server 기능 및 기능 목록과 WideWorldImportersDW에서 사용 하는 방법에 대 한 설명입니다.

## <a name="polybase"></a>PolyBase

[SQL Server에 적용 됨 (2016 이상)]

PolyBase는 WideWorldImportersDW의 판매 정보를 인구 통계에 대 한 공용 데이터 집합과 결합 하 여 판매의 추가 확장에 관심 있는 도시를 이해 하는 데 사용 됩니다.

예제 데이터베이스에서 PolyBase를 사용 하도록 설정 하려면 해당 데이터베이스가 설치 되어 있는지 확인 하 고 데이터베이스에서 다음 저장 프로시저를 실행 합니다.

    EXEC [Application].[Configuration_ApplyPolyBase]

Azure blob storage에 호스트 된 `dbo.CityPopulationStatistics` 미국의 도시에 대 한 인구 데이터를 포함 하는 공용 데이터 집합을 참조 하는 외부 테이블을 만듭니다. 구성 프로세스를 이해 하려면 저장 프로시저의 코드를 검토 하는 것이 좋습니다. Azure blob storage에서 사용자 고유의 데이터를 호스팅하고 일반 공용 액세스에서 안전 하 게 유지 하려면 추가 구성 단계를 수행 해야 합니다. 다음 쿼리는 해당 외부 데이터 집합의 데이터를 반환 합니다.

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

추가 확장에 관심을 가질 수 있는 도시를 이해 하기 위해 다음 쿼리는 도시의 증가율을 확인 하 고, 상당한 성장을 갖춘 상위 100 가장 큰 도시를 반환 하며, Wide Wide Wide Wide에는 판매가 없습니다. 이 쿼리에는 원격 테이블과 `dbo.CityPopulationStatistics` 로컬 테이블 간의 조인이 포함 되며 로컬 테이블과 `Fact.Sales`관련 된 필터가 포함 됩니다. `Dimension.City`

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

(전체 샘플 버전)

인덱스 CCI (클러스터형 Columnstore 인덱스)는 저장소 공간을 줄이고 쿼리 성능을 개선 하기 위해 모든 팩트 테이블에 사용 됩니다. CCI를 사용 하면 팩트 테이블의 기본 저장소에서 열 압축을 사용 합니다.

비클러스터형 인덱스는 기본 키 및 외래 키 제약 조건을 용이 하 게 하기 위해 클러스터형 columnstore 인덱스 위에서 사용 됩니다. 이러한 제약 조건은 매우 주의 해 서 추가 되었습니다. ETL 프로세스는 무결성을 적용 하는 제약 조건을 포함 하는 WideWorldImporters 데이터베이스의 데이터를 원본으로 합니다. Primary key 및 foreign key 제약 조건과 해당 지원 인덱스를 제거 하면 팩트 테이블의 저장소 공간이 줄어듭니다.

**데이터 크기**

예제 데이터베이스는 샘플을 쉽게 다운로드 하 고 설치할 수 있도록 제한 된 데이터 크기를 가집니다. 그러나 columnstore 인덱스의 실제 성능 이점을 확인 하려면 더 큰 데이터 집합을 사용 하는 것이 좋습니다.

다음 문을 실행 하 여 샘플 데이터의 다른 1200만 행을 `Fact.Sales` 삽입 하 여 테이블 크기를 늘릴 수 있습니다. 이러한 행은 모두 2012 년 동안 삽입 되며 ETL 프로세스에 대 한 간섭이 없습니다.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

이 문을 실행 하는 데 약 5 분이 걸립니다. 1200만 개를 초과 하는 행을 삽입 하려면이 저장 프로시저에 매개 변수로 삽입할 행의 수를 전달 합니다.

Columnstore를 사용 하거나 사용 하지 않고 쿼리 성능을 비교 하려면 클러스터형 columnstore 인덱스를 삭제 하거나 다시 만들 수 있습니다.

인덱스를 삭제 하려면:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

다시 만들려면:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>분할

(전체 샘플 버전)

데이터 웨어하우스의 데이터 크기는 매우 커질 수 있습니다. 그러므로 분할을 사용 하 여 데이터베이스에 있는 대량 테이블의 저장소를 관리 하는 것이 좋습니다.

모든 큰 팩트 테이블은 연도별로 분할 됩니다. 유일한 예외는 이며 `Fact.Stock Holdings`,이는 날짜 기반이 아니고 다른 팩트 테이블과 비교 하 여 데이터 크기가 제한 된 경우입니다.

분할 된 모든 테이블 `PF_Date`에 사용 되는 파티션 함수는 이며 사용 중인 파티션 구성표는 `PS_Date`입니다.

## <a name="in-memory-oltp"></a>메모리 내 OLTP

(전체 샘플 버전)

WideWorldImportersDW은 준비 테이블에 SCHEMA_ONLY 메모리 최적화 테이블을 사용 합니다. `Integration.` * 모든 `_Staging` 테이블은 메모리 최적화 테이블 SCHEMA_ONLY 됩니다.

SCHEMA_ONLY 테이블의 장점은 기록 되지 않으며 디스크 액세스가 필요 하지 않다는 것입니다. 이렇게 하면 ETL 프로세스의 성능이 향상 됩니다. 이러한 테이블은 기록 되지 않으므로 오류가 발생 하면 해당 내용이 손실 됩니다. 그러나 데이터 원본은 여전히 사용할 수 있으므로 오류가 발생 하면 ETL 프로세스를 다시 시작할 수 있습니다.
