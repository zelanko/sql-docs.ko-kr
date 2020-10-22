---
title: 자습서용 뉴욕시 택시 데모 데이터
description: 뉴욕시 택시 샘플 데이터를 포함하는 데이터베이스를 만듭니다. 이 데이터 세트는 SQL Server Machine Learning Services용 R 및 Python 자습서에서 사용됩니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1e5e4a4856b91cd717e9498fb96567ecd6c70ca6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192646"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 및 R 자습서용 뉴욕시 택시 데모 데이터
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 문서에서는 [뉴욕시 택시 및 리무진 위원회](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)의 공용 데이터로 구성된 샘플 데이터베이스를 설정하는 방법을 설명합니다. 이 데이터는 SQL Server의 데이터베이스 내 분석에 대한 여러 R 및 Python 자습서에서 사용됩니다. 샘플 코드가 더 빨리 실행되도록 데이터의 대표 1% 샘플링을 만들었습니다. 시스템에서 데이터베이스 백업 파일은 90MB를 약간 초과하고 기본 데이터 테이블에 170만 개 행을 제공합니다.

이 연습을 완료하려면 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md?view=sql-server-2017) 또는 데이터베이스 백업 파일을 복원하고 T-SQL 쿼리를 실행할 수 있는 다른 도구가 있어야 합니다.

이 데이터 세트를 사용하는 자습서 및 빠른 시작에는 다음이 포함됩니다.

+ [SQL Server에서 R을 사용한 데이터베이스 내 분석 알아보기](r-taxi-classification-introduction.md)
+ [SQL Server에서 Python을 사용한 데이터베이스 내 분석 알아보기](python-taxi-classification-introduction.md)

## <a name="download-files"></a>파일 다운로드

샘플 데이터베이스는 Microsoft에서 호스팅하는 SQL Server 2016 BAK 파일입니다. SQL Server 2016 이상에서 복원할 수 있습니다. 링크를 클릭하면 파일 다운로드가 즉시 시작됩니다. 

파일 크기는 약 90MB입니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
>[!NOTE]
>[SQL Server 빅 데이터 클러스터](../../big-data-cluster/big-data-cluster-overview.md)에서 샘플 데이터베이스를 복원하려면 [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)를 다운로드하고 [SQL Server 빅 데이터 클러스터 마스터 인스턴스로 데이터베이스 복원](../../big-data-cluster/data-ingestion-restore-database.md)의 지침을 따릅니다.
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
>[!NOTE]
>[Azure SQL Managed Instance의 Machine Learning Services(미리 보기)](/azure/azure-sql/managed-instance/machine-learning-services-overview)에서 샘플 데이터베이스를 복원하려면 [빠른 시작: 데이터베이스를 Azure SQL Managed Instance로 복원](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)(뉴욕시 택시 데모 데이터베이스 .bak 파일: [https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) 사용)의 지침을 따릅니다.
::: moniker-end

1. [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)를 클릭하여 데이터베이스 백업 파일을 다운로드합니다.

2. C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup 폴더에 파일을 복사합니다.

3. Management Studio에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **파일 및 파일 그룹 복원**을 선택합니다.

4. 데이터베이스 이름으로 *NYCTaxi_Sample*을 입력합니다.

5. **디바이스에서**를 클릭한 다음, 파일 선택 페이지를 열어 백업 파일을 선택합니다. **추가**를 클릭하여 NYCTaxi_Sample.bak를 선택합니다.

6. **복원** 확인란을 선택하고 **확인**을 클릭하여 데이터베이스를 복원합니다.

## <a name="review-database-objects"></a>데이터베이스 개체 검토
   
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스 개체가 있는지 확인합니다. 데이터베이스, 테이블, 함수 및 저장 프로시저가 보여야 합니다.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxi_sample-database"></a>NYCTaxi_Sample 데이터베이스의 개체

다음 표에는 뉴욕시 택시 데모 데이터베이스에서 만든 개체가 요약되어 있습니다.

|**개체 이름**|**개체 유형**|**설명**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | 데이터베이스 | 데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />dbo. nyctaxi_sample 테이블: 주 뉴욕시 택시 데이터 세트를 포함합니다. 스토리지 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. 뉴욕시 택시 데이터 세트의 1% 샘플이 이 테이블에 삽입됩니다.<br /><br />dbo.nyc_taxi_models 테이블: 학습된 고급 분석 모델을 저장하는 데 사용됩니다.|
|**fnCalculateDistance** |스칼라 반환 함수(scalar-valued function) | 승하차 위치 사이의 직접 거리를 계산합니다. 이 함수는 [데이터 요소 만들기](r-taxi-classification-create-features.md), [모델 학습 및 저장](r-taxi-classification-train-model.md)과 [R 모델 운영화](r-taxi-classification-deploy-model.md)에서 사용됩니다.|
|**fnEngineerFeatures** |테이블 반환 함수(table-valued function) | 모델 학습을 위한 새 데이터 요소를 만듭니다. 이 함수는 [데이터 요소 만들기](r-taxi-classification-create-features.md) 및 [R 모델 운영화](r-taxi-classification-deploy-model.md)에서 사용됩니다.|


저장 프로시저는 다양한 자습서에서 제공하는 R 및 Python 스크립트를 사용하여 생성됩니다. 다음 표에는 다양한 단원에서 스크립트를 실행할 때 선택적으로 뉴욕시 택시 데모 데이터베이스에 추가할 수 있는 저장 프로시저가 요약되어 있습니다.

|**저장 프로시저**|**언어**|**설명**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | RevoScaleR rxHistogram 함수를 호출하여 변수 히스토그램을 그린 다음, 플롯을 이진 개체로 반환합니다. 이 저장 프로시저는 [데이터 탐색 및 시각화](r-taxi-classification-explore-data.md)에서 사용됩니다.|
|**RPlotRHist** |R| Hist 함수를 사용하여 그래픽을 만들고 출력을 로컬 PDF 파일로 저장합니다. 이 저장 프로시저는 [데이터 탐색 및 시각화](r-taxi-classification-explore-data.md)에서 사용됩니다.|
|**RxTrainLogitModel**  |R| R 패키지를 호출하여 로지스틱 회귀 모델을 학습시킵니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다. 이 저장 프로시저는 [모델 학습 및 저장](r-taxi-classification-train-model.md)에 사용됩니다.|
|**RxPredictBatchOutput**  |R | 학습된 모델을 호출하여 모델을 사용해서 예측을 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다. 이 저장 프로시저는 [잠재적 결과 예측](r-taxi-classification-deploy-model.md)에 사용됩니다.|
|**RxPredictSingleRow**  |R| 학습된 모델을 호출하여 모델을 사용해서 예측을 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다. 이 저장 프로시저는 [잠재적 결과 예측](r-taxi-classification-deploy-model.md)에 사용됩니다.|

## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행하여 데이터가 업로드되었는지 확인합니다.

1. 개체 탐색기의 데이터베이스에서 **NYCTaxi_Sample** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 새 쿼리를 시작합니다.

2. 몇 가지 간단한 쿼리를 실행합니다.

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
데이터베이스에는 170만 개 행이 포함되어 있습니다.

3. 데이터베이스 내에는 데이터 세트를 포함하는 **nyctaxi_sample** 테이블이 있습니다. 이 테이블은 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md)를 추가하는 방식으로 집합 기반 계산에 최적화되었습니다. 이 문을 실행하여 테이블에 대한 빠른 요약을 생성합니다.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
결과는 다음 스크린샷에 표시된 것과 유사합니다.

  ![테이블 요약 정보](media/nyctaxidatatablesummary.png "쿼리 결과")

## <a name="next-steps"></a>다음 단계

뉴욕시 택시 샘플 데이터를 이제 실습 학습에 사용할 수 있습니다.

+ [SQL Server에서 R을 사용한 데이터베이스 내 분석 알아보기](r-taxi-classification-introduction.md)
+ [SQL Server에서 Python을 사용한 데이터베이스 내 분석 알아보기](python-taxi-classification-introduction.md)