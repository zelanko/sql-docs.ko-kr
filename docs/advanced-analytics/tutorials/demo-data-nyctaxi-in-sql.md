---
title: 임베디드 R 및 Python 용 NYC Taxi demo 데이터 및 스크립트 다운로드
description: 뉴욕 도시 taxi 샘플 데이터를 다운로드 하 고 데이터베이스를 만드는 방법에 대 한 지침입니다. 데이터는 SQL Server 저장 프로시저 및 T-sql 함수에 스크립트를 포함 하는 방법을 보여 주는 SQL Server Python 및 R 언어 자습서에서 사용 됩니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d5d74090713666a2da6058d9eccee1e33e4d7cb
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469749"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 및 R 자습서에 대 한 NYC Taxi demo 데이터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [뉴욕 도시 Taxi 및 리무진 위원회](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)의 공용 데이터로 구성 된 샘플 데이터베이스를 설정 하는 방법을 설명 합니다. 이 데이터는 SQL Server의 데이터베이스 내 분석을 위한 여러 R 및 Python 자습서에서 사용 됩니다. 샘플 코드를 더 빨리 실행하기 위해 데이터의 대표적인 1 % 샘플링을 만들었습니다. 시스템에서 데이터베이스 백업 파일은 90 MB 보다 약간 더 기본 데이터 테이블에 170만 행을 제공 합니다.

이 연습을 완료 하려면 데이터베이스 백업 파일을 복원 하 고 T-sql 쿼리를 실행할 수 있는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 다른 도구가 있어야 합니다.

이 데이터 집합을 사용 하는 자습서 및 빠른 시작에는 다음이 포함 됩니다.

+ [SQL Server에서 R을 사용 하 여 데이터베이스 내 분석 학습](sqldev-in-database-r-for-sql-developers.md)
+ [SQL Server에서 Python을 사용 하 여 데이터베이스 내 분석 학습](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>파일 다운로드

예제 데이터베이스는 Microsoft에서 호스팅하는 SQL Server 2016 .BAK 파일입니다. SQL Server 2016 이상에서 복원할 수 있습니다. 링크를 클릭 하면 파일 다운로드가 즉시 시작 됩니다. 

파일 크기는 약 90 MB입니다.

1. [NYCTaxi_Sample](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) 을 클릭 하 여 데이터베이스 백업 파일을 다운로드 합니다.

2. C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup 폴더에 파일을 복사 합니다.

3. Management Studio에서 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **파일 및 파일 그룹 복원**을 선택 합니다.

4. 데이터베이스 이름으로 *NYCTaxi_Sample* 을 입력 합니다.

5. **장치에서** 를 클릭 한 다음 파일 선택 페이지를 열어 백업 파일을 선택 합니다. **추가** 를 클릭 하 여 NYCTaxi_Sample를 선택 합니다.

6. **복원** 확인란을 선택 하 고 **확인** 을 클릭 하 여 데이터베이스를 복원 합니다.

## <a name="review-database-objects"></a>데이터베이스 개체 검토
   
을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]인스턴스에 데이터베이스 개체가 존재 하는지 확인 합니다. 데이터베이스, 테이블, 함수 및 저장 프로시저를 확인 해야 합니다.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 데이터베이스의 개체

다음 표에서는 NYC Taxi demo 데이터베이스에서 만든 개체를 요약 합니다.

|**개체 이름**|**개체 유형**|**설명**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | 데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />nyctaxi_sample 테이블: 주 NYC Taxi 데이터 집합을 포함 합니다. 스토리지 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플은이 테이블에 삽입 됩니다.<br /><br />nyc _taxi_models 테이블: 학습 된 고급 분석 모델을 유지 하는 데 사용 됩니다.|
|**fnCalculateDistance** |스칼라 반환 함수(scalar-valued function) | 픽업 및 차 위치 간의 직접 거리를 계산 합니다. 이 함수는 [데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md), [모델 학습 및 저장](sqldev-train-and-save-a-model-using-t-sql.md) 및 [R 모델 운영](sqldev-operationalize-the-model.md)에 사용 됩니다.|
|**fnEngineerFeatures** |테이블 반환 함수(table-valued function) | 모델 학습을 위한 새 데이터 기능을 만듭니다. 이 함수는 [데이터 생성 기능](sqldev-create-data-features-using-t-sql.md) 및 [R 모델 운영](sqldev-operationalize-the-model.md)에 사용 됩니다.|


저장 프로시저는 다양 한 자습서에서 제공 하는 R 및 Python 스크립트를 사용 하 여 생성 됩니다. 다음 표에서는 다양 한 단원에서 스크립트를 실행할 때 선택적으로 NYC Taxi demo 데이터베이스에 추가할 수 있는 저장 프로시저를 요약 하 여 보여 줍니다.

|**저장 프로시저**|**언어**|**설명**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | RevoScaleR rxHistogram 함수를 호출 하 여 변수의 히스토그램을 플롯 한 다음 플롯을 이진 개체로 반환 합니다. 이 저장 프로시저는 데이터를 [탐색 하 고 시각화 하](sqldev-explore-and-visualize-the-data.md)는 데 사용 됩니다.|
|**RPlotRHist** |R| 위해 함수를 사용 하 여 그래픽을 만들고 로컬 PDF 파일로 출력을 저장 합니다. 이 저장 프로시저는 데이터를 [탐색 하 고 시각화 하](sqldev-explore-and-visualize-the-data.md)는 데 사용 됩니다.|
|**RxTrainLogitModel**  |R| R 패키지를 호출 하 여 로지스틱 회귀 모델을 학습 합니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다. 이 저장 프로시저는 [모델 학습 및 저장](sqldev-train-and-save-a-model-using-t-sql.md)에 사용 됩니다.|
|**RxPredictBatchOutput**  |R | 학습 된 모델을 호출 하 여 모델을 사용 하 여 예측을 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다. 이 저장 프로시저는 [잠재적 결과를 예측](sqldev-operationalize-the-model.md)하는 데 사용 됩니다.|
|**RxPredictSingleRow**  |R| 학습 된 모델을 호출 하 여 모델을 사용 하 여 예측을 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다. 이 저장 프로시저는 [잠재적 결과를 예측](sqldev-operationalize-the-model.md)하는 데 사용 됩니다.|

## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행 하 여 데이터가 업로드 되었는지 확인 합니다.

1. 개체 탐색기의 데이터베이스에서 **NYCTaxi_Sample** 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
데이터베이스에는 170만 행이 포함 되어 있습니다.

3. 데이터베이스 내의는 데이터 집합을 포함 하는 **nyctaxi_sample** 테이블입니다. 테이블은 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md)를 추가 하 여 집합 기반 계산에 최적화 되었습니다. 아래 문을 실행해서 테이블에 대한 빠른 요약을 생성합니다.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
결과는 다음 스크린샷에 표시 된 것과 유사 합니다.

  ![테이블 요약 정보](media/nyctaxidatatablesummary.png "쿼리 결과")

## <a name="next-steps"></a>다음 단계

NYC Taxi 샘플 데이터는 이제 실습 학습에 사용할 수 있습니다.

+ [SQL Server에서 R을 사용 하 여 데이터베이스 내 분석 학습](sqldev-in-database-r-for-sql-developers.md)
+ [SQL Server에서 Python을 사용 하 여 데이터베이스 내 분석 학습](sqldev-in-database-python-for-sql-developers.md)