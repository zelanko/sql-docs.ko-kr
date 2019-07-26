---
title: T-sql을 사용 하 여 Python 모델 학습 및 저장
description: SQL Server에서 Transact-sql을 사용 하 여 모델을 학습 하 고 저장 하는 방법을 보여 주는 Python 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 41403018f6b3a2740328ad1576f8c357e7896b12
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470564"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>T-sql을 사용 하 여 Python 모델 학습 및 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)자습서의 일부입니다. 

이 단계에서는 Python 패키지 **scikit-배우기** 및 **revoscalepy**를 사용 하 여 기계 학습 모델을 학습 하는 방법을 알아봅니다. 이러한 Python 라이브러리는 SQL Server Machine Learning Services와 함께 이미 설치 되어 있습니다.

모듈을 로드 하 고 필요한 함수를 호출 하 SQL Server 저장 프로시저를 사용 하 여 모델을 만들고 학습 합니다. 모델에는 이전 단원에서 엔지니어링 한 데이터 기능이 필요 합니다. 마지막으로 학습 된 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장 합니다.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>샘플 데이터를 학습 집합과 테스트 집합으로 분할

1. **PyTrainTestSplit** 라는 저장 프로시저를 만들어 nyctaxi_sample 테이블의 데이터를 nyctaxi_sample_training와 nyctaxi_sample_testing의 두 부분으로 나눕니다. 

    이 저장 프로시저는 이미 생성 되어 있지만 다음 코드를 실행 하 여 만들 수 있습니다.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 사용자 지정 분할을 사용 하 여 데이터를 나누려면 저장 프로시저를 실행 하 고 학습 집합에 할당 된 데이터의 백분율을 나타내는 정수를 입력 합니다. 예를 들어 다음 문은 학습 집합에 60%의 데이터를 할당 합니다.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>로지스틱 회귀 모델 작성

데이터를 준비한 후 모델을 학습 하는 데 사용할 수 있습니다. 이렇게 하려면 일부 Python 코드를 실행 하는 저장 프로시저를 호출 하 여 학습 데이터 테이블을 입력 합니다. 이 자습서에서는 다음 두 가지 모델, 즉 이진 분류 모델을 만듭니다.

+ **PyTrainScikit** 저장 프로시저는 **scikit** 패키지를 사용 하 여 팁 예측 모델을 만듭니다.
+ **TrainTipPredictionModelRxPy** 저장 프로시저는 **revoscalepy** 패키지를 사용 하 여 팁 예측 모델을 만듭니다.

각 저장 프로시저는 사용자가 제공 하는 입력 데이터를 사용 하 여 로지스틱 회귀 모델을 만들고 학습 합니다. 모든 Python 코드는 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 래핑됩니다.

새 데이터에 모델을 더 쉽게 다시 학습 수 있도록 다른 저장 프로시저에서 sp_execute_exernal_script 호출을 래핑하고 새 학습 데이터를 매개 변수로 전달 합니다. 이 섹션에서는 해당 프로세스를 안내 합니다.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]새 **쿼리** 창을 열고 다음 문을 실행 하 여 **PyTrainScikit**저장 프로시저를 만듭니다.  저장 프로시저에 입력 데이터의 정의가 포함 되어 있으므로 입력 쿼리를 제공할 필요가 없습니다.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
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

2. 다음 SQL 문을 실행 하 여 학습 된 모델을 nyc\_taxi_models 테이블에 삽입 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    데이터 처리 및 모델 맞춤은 몇 분 정도 걸릴 수 있습니다. Python의 **stdout** 스트림으로 파이프 되는 메시지는의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **메시지** 창에 표시 됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

    *STDOUT message(s) from external script:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. *Nyc\_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

이 저장 프로시저는 새로운 Python 용 패키지인 새로운 **revoscalepy** 패키지를 사용 합니다. R 언어의 **RevoScaleR** 패키지에 제공 된 것과 유사한 개체, 변환 및 알고리즘을 포함 합니다. 

**Revoscalepy**를 사용 하 여 로지스틱 및 선형 회귀, 의사 결정 트리 등 널리 사용 되는 알고리즘을 사용 하 여 원격 계산 컨텍스트를 만들고, 계산 컨텍스트 간에 데이터를 이동 하 고, 데이터를 변환 하 고, 예측 모델을 학습할 수 있습니다. 자세한 내용은 SQL Server 및 [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) [의 revoscalepy 모듈](../python/ref-py-revoscalepy.md) 을 참조 하세요.

1. 에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]새 **쿼리** 창을 열고 다음 문을 실행 하 여 _TrainTipPredictionModelRxPy_저장 프로시저를 만듭니다.  저장 프로시저에 이미 입력된 데이터의 정의가 포함되므로 입력 쿼리를 제공할 필요가 없습니다.

    ```sql
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

    이 저장 프로시저는 모델 학습의 일부로 다음 단계를 수행 합니다.

    - SELECT 쿼리는 사용자 지정 스칼라 함수 _fnCalculateDistance_ 을 적용 하 여 선택 및 드롭다운 위치 간의 직접 거리를 계산 합니다. 쿼리 결과는 기본 Python 입력 변수인 `InputDataset`에 저장 됩니다.
    - _Passenger_count_, _trip_distance_, _trip_time_in_secs_및 _direct_distance_기능 열을 사용 하 여 모델은 *레이블* 또는 결과 열로 사용 되 고 모델은 적합 합니다.
    - 학습 된 모델은 serialize 되어 Python 변수에 `logitObj`저장 됩니다. T-sql 키워드 출력을 추가 하 여 저장 프로시저의 출력으로 변수를 추가할 수 있습니다. 다음 단계에서이 변수는 모델의 이진 코드를 데이터베이스 테이블 _nyc_taxi_models_삽입 하는 데 사용 됩니다. 이 메커니즘을 사용 하면 모델을 쉽게 저장 하 고 재사용할 수 있습니다.

2. 다음과 같이 저장 프로시저를 실행 하 여 학습 된 **revoscalepy** 모델을 *nyc_taxi_models*테이블에 삽입 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    데이터를 처리하고 모델에 맞추는 데 다소 시간이 걸릴 수 있습니다. Python의 **stdout** 스트림으로 파이프 되는 메시지는의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **메시지** 창에 표시 됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

    *STDOUT message(s) from external script:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. *nyc_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *revoscalepy_model* *0x8003637265766F7363616c....*

다음 단계에서는 학습 된 모델을 사용 하 여 예측을 만듭니다.

## <a name="next-step"></a>다음 단계

[저장 프로시저에 포함 된 Python을 사용 하 여 예측 실행](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>이전 단계

[T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)
