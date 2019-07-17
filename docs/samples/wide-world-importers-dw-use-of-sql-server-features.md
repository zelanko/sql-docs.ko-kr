---
title: WideWorldImporters OLAP 데이터베이스-SQL Server 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 313f85c5d5ec3590e231bdac4a746318c927a33a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104221"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>SQL Server 기능과 WideWorldImportersDW 사용
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW는 다양 한 데이터 웨어하우징 및 분석에 적합 한 SQL Server의 주요 기능을 보여 주도록 설계 되었습니다. 다음은 SQL Server 기능 및 기능을 WideWorldImportersDW의 사용 방법에 대 한 설명을의 목록입니다.

## <a name="polybase"></a>PolyBase

[SQL Server 2016 이상에 적용 됩니다]

PolyBase는 도시의 판매 추가 확장을 위해 유용할 수 있습니다를 이해 하려면 인구 통계에 대 한 공용 데이터 집합을 사용 하 여 WideWorldImportersDW에서 판매 정보를 결합 하는 데 사용 됩니다.

샘플 데이터베이스의 PolyBase 사용을 사용 하려면가 설치 되어 있는지 확인 하 고 데이터베이스에 다음 저장된 프로시저를 실행 합니다.

    EXEC [Application].[Configuration_ApplyPolyBase]

외부 테이블 만들기는이 `dbo.CityPopulationStatistics` 참조 하는 Azure blob storage에서 호스트 되는 미국에서는 도시 인구 데이터를 포함 하는 공용 데이터 집합입니다. 당신은 구성 프로세스를 이해 하려면 저장된 프로시저에서 코드를 검토 하는 것이 좋습니다. 사용자 고유의 데이터를 Azure blob 저장소를 호스트 하 고 일반 공용 액세스를 안전 하 게 유지 하려는 경우에 추가 구성 단계를 수행 해야 합니다. 다음 쿼리는 외부 데이터 집합에서 데이터를 반환합니다.

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

도시 추가 확장을 위해 유용할 수 있습니다를 이해 하려면 다음 쿼리 도시, 증가 속도 살펴보고 및 상당히 증가 사용 하 여 가장 큰 상위 100 개 도시를 반환 합니다. 판매 프로그램이 Wide World Importers 없는 합니다. 쿼리는 원격 테이블 간 조인을 `dbo.CityPopulationStatistics` 테이블과 로컬 `Dimension.City`, 및 로컬 테이블과 관련 된 필터 `Fact.Sales`합니다.

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

(샘플의 전체 버전)

저장소 공간을 줄이고 쿼리 성능을 향상 시킬 모든 팩트 테이블을 클러스터형된 Columnstore 인덱스 (CCI) 사용 됩니다. CCI 사용 하 여 팩트 테이블에 대 한 기본 저장소는 열 압축을 사용합니다.

비클러스터형 인덱스는 클러스터형된 columnstore 인덱스를 기반으로 primary key 및 foreign key 제약 조건을 용이 하 게 사용 됩니다. 이러한 제약 조건을 주의 풍부 하 게에서 추가 된-ETL 프로세스에 무결성을 적용 하는 제약 조건이 있는 WideWorldImporters 데이터베이스에서 데이터 원본입니다. 기본 및 외래 키 제약 조건 및 지원 해당 인덱스를 제거는 팩트 테이블의 저장소 공간을 줄일 수 있습니다.

**데이터 크기**

샘플 데이터베이스 다운로드 및 샘플 설치 작업을 좀 더 쉽게 데이터 크기를 제한 했습니다. 그러나 columnstore 인덱스의 실제 성능 혜택을 보려면 하려는 큰 데이터 집합을 사용 합니다.

크기를 늘리려면 다음 문을 실행할 수 있습니다는 `Fact.Sales` 샘플 데이터의 또 다른 12 백만 행을 삽입 하 여 테이블입니다. 이러한 행은 모든 삽입 2012 년 ETL 프로세스를 사용 하 여 간섭이 되도록.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

이 문을 실행 하려면 약 5 분 정도 걸립니다. 12 백만 개 이상의 행을 삽입 하려면 원하는 수의 행이 저장된 프로시저에 매개 변수로 전달 합니다.

Columnstore 하지 않고 사용 하 여 쿼리 성능을 비교를 삭제 하거나 클러스터형된 columnstore 인덱스를 다시 만들 수 있습니다.

인덱스를 삭제 합니다.

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

다시 만듭니다.

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>분할

(샘플의 전체 버전)

데이터 웨어하우스에서 데이터 크기는 매우 커질 수 있습니다. 따라서 분할을 사용 하 여 데이터베이스의 대형 테이블의 저장소를 관리 하기 좋습니다 것입니다.

큰 팩트 테이블의 모든 연도별로 분할 됩니다. 유일한 예외는 `Fact.Stock Holdings`없는 날짜를 기준으로 하 고 다른 팩트 테이블을 사용 하 여 제한 된 데이터 크기를 비교 합니다.

모든 분할 된 테이블에 사용 되는 파티션 함수는 `PF_Date`를 사용 하 고 파티션 구성표 이며 `PS_Date`합니다.

## <a name="in-memory-oltp"></a>메모리 내 OLTP

(샘플의 전체 버전)

WideWorldImportersDW는 SCHEMA_ONLY 메모리 최적화 테이블을 사용 하 여 준비 테이블에 대 한 합니다. 모든 `Integration.` * `_Staging` 테이블은 SCHEMA_ONLY 메모리 최적화 테이블입니다.

SCHEMA_ONLY 테이블의 장점은 로깅되지 않습니다 하며 모든 디스크 액세스할 필요가 없습니다. 이 ETL 프로세스의 성능이 향상 됩니다. 이러한 테이블은 기록 되지 하므로 오류가 발생 하는 경우 해당 내용이 손실 됩니다. 그러나 데이터 원본 이므로 계속 사용할 수 있는 ETL 프로세스는 단순히 다시 시작할 수 있습니다 오류가 발생 하는 경우.
