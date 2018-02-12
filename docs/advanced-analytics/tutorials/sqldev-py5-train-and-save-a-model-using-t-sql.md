---
title: "5 단계: 학습 및 T-SQL을 사용 하 여 Python 모델을 저장할 | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: a2f0ffafb466030802b87dc96f905e9c875dd548
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>5 단계: 학습 및 T-SQL을 사용 하 여 Python 모델 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서의 일부는 [SQL 개발자를 위해 데이터베이스에서 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 Python 패키지를 사용 하 여 기계 학습 모델을 학습 하는 방법을 배웁니다 **scikit-자세한** 및 **revoscalepy**합니다. 이러한 Python 라이브러리는 이미 SQL Server 컴퓨터 학습 서비스와 함께 설치 됩니다.

모듈을 로드 하 고이 정보를 만들고 SQL Server 저장 프로시저를 사용 하 여 모델을 학습 하는 데 필요한 함수를 호출 합니다. 모델을 사용 하려면 이전 단원에서 엔지니어링 데이터 기능이 필요 합니다. 학습 된 모델을 저장 하는 마지막으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.

> [!IMPORTANT]
> 에 대 한 몇 가지 변경 사항이 **revoscalepy** 이 자습서에 대 한 코드에서 약간 변경 해야 하는 패키지입니다. 참조는 [못했기](sqldev-py6-operationalize-the-model.md#changes) 이 자습서의 끝에 있습니다. 
> 
> SLq Server 2017의 시험판 버전을 사용 하 여 Python 서비스를 설치한 경우에 최신 버전으로 업그레이드 하는 것이 좋습니다. 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>샘플 데이터를 학습 집합과 테스트 집합으로 분합니다

1. 저장된 프로시저를 사용할 수 **TrainTestSplit** 는 nyctaxi의 데이터를 나누는 데\_예제 테이블의 두 부분으로: nyctaxi\_샘플\_교육 및 nyctaxi\_샘플\_테스트 합니다. 

    이 저장된 프로시저를 위해 이미 만들 수 있지만 만들 다음 코드를 실행할 수 있습니다.

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 사용자 지정 분할을 사용 하 여 데이터를 나누는 데 저장된 프로시저를 실행 하 고 학습 집합에 할당 된 데이터의 비율을 나타내는 정수를 입력 합니다. 예를 들어 다음 문은 데이터를 학습 집합의 60% 할당 합니다.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>로지스틱 회귀 모델을 작성

데이터를 준비한 후에 모델 학습에 사용할 수 있습니다. 저장을 호출 하 여이 작업을 수행 기능적 일부 Python 코드를 실행 하는 프로시저는 학습 데이터 테이블을 입력 합니다. 이 자습서에서는 두 개의 모델, 두 이진 분류 모델을 만듭니다.

+ 저장된 프로시저 **TrainTipPredictionModelRxPy** 사용 하 여 팁 예측 모델을 만듭니다는 **revoscalepy** 패키지 합니다.
+ 저장된 프로시저 **TrainTipPredictionModelSciKitPy** 사용 하 여 팁 예측 모델을 만듭니다는 **scikit-자세한** 패키지 합니다.

각 저장된 프로시저는 입력된 데이터를 사용 하 여 로지스틱 회귀 모델 학습을 제공 합니다. 모든 Python 코드 시스템 저장 프로시저에 래핑됩니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

쉽게 새 데이터에 대 한 모델을 보존 하기 위해 다른 저장된 프로시저에서 sp_execute_exernal_script에 대 한 호출을 래핑하고 고 새 학습 데이터를 매개 변수로 전달 합니다. 이 섹션에서는 프로세스를 통해 안내 합니다.

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModelSciKitPy_합니다.  따라서 입력된 쿼리를 제공 하지 않아도 됩니다. 입력된 데이터의 정의 포함 하는 저장된 프로시저입니다.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
      EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
      import numpy
      import pickle
      from sklearn.linear_model import LogisticRegression
      
      ##Create SciKit-Learn logistic regression model
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      SKLalgo = LogisticRegression()
      logitObj = SKLalgo.fit(X, y)
      
      ##Serialize model
      trained_model = pickle.dumps(logitObj)
      ',
      @input_data_1 = N'
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_training
      ',
      @input_data_1_name = N'InputDataSet',
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT;
      ;
    END;
    GO
    ```

2. 다음 실행 하는 학습 된 모델에 삽입할 SQL 문을 테이블 nyc\_taxi_models 합니다.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    데이터를 처리 하 고 모델을 맞출 분 정도 걸릴 수 있습니다. Python의 파이프 될 메시지 **stdout** 스트림에 표시 되는 **메시지** 의 창 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 예를 들어

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 테이블을 열고 *nyc\_taxi_models*합니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *linear_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

이 저장된 프로시저를 사용 하 여 새 **revoscalepy** Python에 대 한 새 패키지입니다. 포함 된 개체, 변환 및 알고리즘 R 언어에 대해 제공 하는 것과 유사한 **RevoScaleR** 패키지 합니다. 

사용 하 여 **revoscalepy**, 원격 계산 컨텍스트를 만들 수 있습니다, 간에 이동 데이터 컨텍스트, 데이터 변환 및 의사 결정 트리, 선형 및 로지스틱 회귀와 같은 인기 있는 알고리즘을 사용 하 여 학습 예측 모델 계산 하 고 더 많은 합니다. 자세한 내용은 참조 [revoscalepy 란?](../python/what-is-revoscalepy.md)

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModelRxPy_합니다.  에 이미 저장된 프로시저는 입력된 데이터의 정의 포함 되므로 입력된 쿼리를 제공할 필요가 없습니다.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    이 저장된 프로시저 모델 학습의 일부로 다음 단계를 수행합니다.

    - 사용자 정의 스칼라 함수를 적용 하는 SELECT 쿼리 _fnCalculateDistance_ 를 직접 선택 및 자동 전송 위치 사이의 거리를 계산 합니다. 쿼리 결과 기본 Python 입력된 변수에 저장 됩니다 `InputDataset`합니다.
    - 이진 변수 _크리스마스_ 로 사용 되는 *레이블* 이러한 기능 열을 사용 하 여 결과 열을 모델은 적합 또는: _passenger_count_, _trip_ 거리_, _trip_time_in_secs_, 및 _direct_distance_합니다.
    - 학습 된 모델에서 serialize 되 고 Python 변수에 저장 된 `logitObj`합니다. T-SQL 키워드 출력을 추가 하 여 저장된 프로시저의 출력으로 변수를 추가할 수 있습니다. 다음 단계에서 해당 변수를 데이터베이스 테이블에는 모델의 이진 코드를 삽입 하는 데 사용 _nyc_taxi_models_합니다. 이 메커니즘을 사용 하면를 쉽게 저장할 수와 모델 다시 사용 합니다.

2. 그러면 학습 된 삽입 하려면 다음과 같이 저장된 프로시저 실행 **revoscalepy** 테이블 _nyc에 모델\_택시\_모델.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    데이터를 처리 하 고 모델을 맞출 시간이 걸릴 수 있습니다. Python의 파이프 될 메시지 **stdout** 스트림에 표시 되는 **메시지** 의 창 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 예를 들어

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. *nyc_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *rx_model* *0x8003637265766F7363616c....*

다음 단계에서는 학습된 된 모델을 사용 하 여 예측을 만듭니다.

## <a name="next-step"></a>다음 단계

[6 단계: SQL Server를 사용 하 여 Python 모델을 운용](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>이전 단계

[4단계: T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)
