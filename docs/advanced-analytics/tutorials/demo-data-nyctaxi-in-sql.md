---
title: 포함 된 R 및 Python (SQL Server Machine Learning)에 대 한 NYC Taxi 데이터 및 스크립트 다운로드 | Microsoft Docs
description: 뉴욕 시 택시 샘플 데이터를 다운로드 하 고 데이터베이스를 만들기 위한 지침입니다. 데이터는 SQL Server 저장 프로시저 및 T-SQL 함수에서 스크립트를 포함 하는 방법에 대 한 SQL Server Python 및 R 언어 자습서에 사용 됩니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ea4651c76d0c8fbc14d22a51c7789d65a20b8484
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701351"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 및 R 자습서에 대 한 NYC Taxi 데이터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 공용 데이터로 구성 된 샘플 데이터베이스를 설정 하는 방법에 설명 합니다 [뉴욕 시 택시 및 리무진 수수료](https://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)합니다. 이 데이터는 SQL Server에서 데이터베이스 내 분석에 대 한 몇 가지 R 및 Python 자습서에 사용 됩니다. 샘플 코드를 더 빨리 실행하기 위해 데이터의 대표적인 1 % 샘플링을 만들었습니다. 시스템 데이터베이스 백업 파일에는 약간 넘는 90MB, 기본 데이터 테이블의 1.7 백만 행을 제공 합니다.

이 연습을 완료 하려면 있어야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 데이터베이스 백업 파일을 복원 하 고 T-SQL 쿼리를 실행할 수 있는 다른 도구입니다.

이 데이터 집합을 사용 하 여 퀵 스타트 및 자습서에는 다음과 같습니다.

+ [SQL Server에서 R을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](sqldev-in-database-r-for-sql-developers.md)
+ [SQL Server에서 Python을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>파일 다운로드

예제 데이터베이스는 Microsoft에서 호스팅하는 SQL Server 2016 BAK 파일입니다. SQL Server 2016 이상 복원할 수 있습니다. 파일 다운로드 링크를 클릭할 때 즉시 시작 합니다. 

파일 크기는 약 90입니다.

1. 클릭 [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) 데이터베이스 백업 파일을 다운로드 합니다.

2. C:\Program files\Microsoft SQL server\mssql.-인스턴스-name\MSSQL\Backup 폴더로 파일을 복사 합니다.

3. Management studio에서 마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **복원 파일 및 파일 그룹**합니다.

4. 입력 *NYCTaxi_Sample* 데이터베이스 이름으로 합니다.

5. 클릭 **장치의** 백업 파일을 선택 하려면 파일 선택 페이지를 엽니다. 클릭 **추가** NYCTaxi_Sample.bak를 선택 합니다.

6. 선택 합니다 **복원** 확인란을 클릭 하 고 **확인** 데이터베이스를 복원 합니다.

## <a name="review-database-objects"></a>데이터베이스 개체를 검토 합니다.
   
데이터베이스 개체의 존재를 확인 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]입니다. 데이터베이스, 테이블, 함수 및 저장된 프로시저 표시 됩니다.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 데이터베이스의 개체

다음 표에서 NYC Taxi 데모 데이터베이스에서 생성 되는 개체를 보여 줍니다.

|**개체 이름**|**개체 유형**|**설명**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | 데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />dbo.nyctaxi_sample 테이블: 주 NYC Taxi 데이터 집합을 포함 합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플이이 테이블에 삽입 됩니다.<br /><br />dbo.nyc_taxi_models 테이블: 고급 분석 학습 된 모델을 유지 하는 데 사용 합니다.|
|**fnCalculateDistance** |스칼라 반환 함수(scalar-valued function) | 승차 및 하 차 위치 사이의 직접 거리를 계산합니다. 이 함수는 [데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md), [학습 모델을 저장 하 고](sqldev-train-and-save-a-model-using-t-sql.md) 하 고 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|
|**fnEngineerFeatures** |테이블 반환 함수(table-valued function) | 모델 학습을 위한 새로운 데이터 기능을 만듭니다. 이 함수는 [데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md) 하 고 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|


저장된 프로시저에 다양 한 자습서는 R 및 Python 스크립트를 사용 하 여 생성 됩니다. 다음 표에서 다양 한 단원에서 스크립트를 실행 하는 경우 필요에 따라 NYC Taxi 데모 데이터베이스에 추가할 수 있는 저장된 프로시저를 보여 줍니다.

|**저장된 프로시저**|**언어**|**설명**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 변수 히스토그램을 그린 RevoScaleR rxHistogram 함수를 호출 하 고 그림을 이진 개체로 반환 합니다. 이 저장된 프로시저는 [데이터 탐색 및 시각화](sqldev-explore-and-visualize-the-data.md)합니다.|
|**RPlotRHist** |R| Hist 함수를 사용 하 여 그래픽을 만들고 로컬 PDF 파일로 출력을 저장 합니다. 이 저장된 프로시저는 [데이터 탐색 및 시각화](sqldev-explore-and-visualize-the-data.md)합니다.|
|**RxTrainLogitModel**  |R| R 패키지를 호출 하 여 로지스틱 회귀 모델을 학습 합니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다. 이 저장된 프로시저는 [학습 모델을 저장 하 고](sqldev-train-and-save-a-model-using-t-sql.md)입니다.|
|**RxPredictBatchOutput**  |R | 모델을 사용 하 여 예측을 만들려면 학습된 된 모델을 호출 합니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다. 이 저장된 프로시저는 [잠재적인 결과 예측](sqldev-operationalize-the-model.md)합니다.|
|**RxPredictSingleRow**  |R| 모델을 사용 하 여 예측을 만들려면 학습된 된 모델을 호출 합니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다. 이 저장된 프로시저는 [잠재적인 결과 예측](sqldev-operationalize-the-model.md)합니다.|

## <a name="query-the-data"></a>데이터를 쿼리 합니다.

유효성 검사 단계로, 데이터가 업로드 되었는지 확인 하는 쿼리를 실행 합니다.

1. 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 합니다 **NYCTaxi_Sample** 데이터베이스 및 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
데이터베이스는 1.7 백만 행을 포함합니다.

3. 데이터베이스 내에서 한 **nyctaxi_sample** 데이터 집합을 포함 하는 테이블입니다. 추가 집합 기반 계산에 최적화 된 테이블을 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md)합니다. 아래 문을 실행해서 테이블에 대한 빠른 요약을 생성합니다.

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
결과 다음 스크린샷에 표시 된 비슷해야 합니다.

  ![요약 정보를 테이블](media/nyctaxidatatablesummary.png "쿼리 결과")

## <a name="next-steps"></a>다음 단계

NYC Taxi 샘플 데이터 실습에 대 한 출시 되었습니다.

+ [SQL Server에서 R을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](sqldev-in-database-r-for-sql-developers.md)
+ [SQL Server에서 Python을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](sqldev-in-database-python-for-sql-developers.md)