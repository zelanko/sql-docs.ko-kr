---
title: 학습 및 T-SQL-SQL Server Machine Learning을 사용 하 여 Python 모델을 저장 합니다.
description: 학습 및 SQL Server에서 TRANSACT-SQL을 사용 하 여 모델을 저장 하는 방법을 보여 주는 Python 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e0505cf847a091a5650b392aab56f486cee16aa
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511250"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>학습 및 T-SQL을 사용 하 여 Python 모델을 저장 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서에 일부 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 Python 패키지를 사용 하 여 기계 학습 모델을 학습 하는 방법을 알아봅니다 **scikit-알아봅니다** 하 고 **revoscalepy**합니다. SQL Server Machine Learning Services를 사용 하 여 이러한 Python 라이브러리를 설치 되어 있습니다.

모듈을 로드 하 고 SQL Server 저장 프로시저를 사용 하 여 모델을 학습 하는 데 필요한 함수를 호출 합니다. 모델에는 이전 단원에서 엔지니어링 된 데이터 기능에 필요 합니다. 학습된 된 모델을 저장 하는 마지막으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>샘플 데이터를 학습 집합과 테스트 집합으로 분합니다

1. 호출할 저장된 프로시저를 만듭니다 **PyTrainTestSplit** nyctaxi_sample 테이블의에서 데이터를 두 부분으로 나누는: nyctaxi_sample_training 및 nyctaxi_sample_testing 합니다. 

    이 저장된 프로시저를 만든 해야 하지만을 만드는 다음 코드를 실행할 수 있습니다.

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

2. 사용자 지정 분할을 사용 하 여 데이터를 분할, 저장된 프로시저를 실행 하 고 학습 집합에 할당 된 데이터의 백분율을 나타내는 정수를 입력 합니다. 예를 들어 다음 문에서 학습 집합에 데이터를 60%를 할당 합니다.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>로지스틱 회귀 모델 작성

데이터를 준비한 후에 모델 학습에 사용할 수 있습니다. 이렇게 하려면 저장을 호출 하 여으로 수행 되는 몇 가지 Python 코드를 실행 하는 프로시저에는 학습 데이터 테이블을 입력 합니다. 이 자습서에서는 두 가지 모델, 이진 분류 모델을 모두 만듭니다.

+ 저장된 프로시저 **PyTrainScikit** 사용 하 여 팁 예측 모델을 만듭니다는 **scikit-알아봅니다** 패키지 있습니다.
+ 저장된 프로시저 **TrainTipPredictionModelRxPy** 사용 하 여 팁 예측 모델을 만듭니다는 **revoscalepy** 패키지 있습니다.

각 저장된 프로시저에 입력된 데이터를 사용 하 여 로지스틱 회귀 모델 학습을 제공 합니다. 모든 Python 코드는 시스템 저장 프로시저에 래핑됩니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

새 데이터에 대해 모델을 재 학습을 쉽게 다른 저장된 프로시저에 sp_execute_exernal_script 호출을 래핑할 고 매개 변수로 새 학습 데이터를 전달 합니다. 이 섹션에서는 해당 프로세스 안내 합니다.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 **PyTrainScikit**합니다.  저장된 프로시저 입력된 쿼리를 제공 하지 않아도 되므로 입력된 데이터의 정의 포함 합니다.

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

2. 다음 실행 하 여 학습 된 모델을 삽입 하는 SQL 문을 테이블 nyc\_taxi_models 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    데이터를 처리 하 고 모델을 맞추는 분 정도 걸릴 수 있습니다. Python의 파이프 되는 메시지 **stdout** 스트림은 표시 되는 **메시지** 기간 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 테이블을 엽니다 *nyc\_taxi_models*합니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

이 저장된 프로시저를 사용 하 여 새 **revoscalepy** Python에 대 한 새 패키지를 패키지 합니다. 개체, 변환 및 R 언어에 대해 제공 된 것과 비슷한 알고리즘 있기 **RevoScaleR** 패키지 있습니다. 

사용 하 여 **revoscalepy**, 원격 계산 컨텍스트를 만들 수 있습니다, 간에 데이터 이동 계산 컨텍스트, 데이터 변환 및 로지스틱 및 선형 회귀, 의사 결정 트리와 같은 인기 있는 알고리즘을 사용 하 여 예측 모델을 학습 하 고 자세한 합니다. 자세한 내용은 [SQL Server에서 revoscalepy 모듈](../python/ref-py-revoscalepy.md) 하 고 [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModelRxPy_합니다.  저장 프로시저에 이미 입력된 데이터의 정의가 포함되므로 입력 쿼리를 제공할 필요가 없습니다.

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

    이 저장된 프로시저 모델 학습의 일부로 다음 단계를 수행합니다.

    - 사용자 정의 스칼라 함수를 적용 하는 SELECT 쿼리에 _fnCalculateDistance_ 승차 및 하 차 위치 사이의 직접 거리를 계산 합니다. 쿼리 결과 기본 Python 입력 변수에 저장 됩니다 `InputDataset`합니다.
    - 이진 변수의 _tipped_ 으로 사용 되는 *레이블* 기능 열을 사용 하 여 결과 열을 모델을 맞춥니다 또는: _passenger_count_, _trip_ 거리_하십시오 _trip_time_in_secs_, 및 _direct_distance_합니다.
    - 학습 된 모델을 직렬화 하 고 Python 변수에 저장 된 `logitObj`합니다. T-SQL 키워드 출력에 추가 하 여 저장된 프로시저의 출력으로 변수를 추가할 수 있습니다. 다음 단계에서 해당 변수를 사용 하는 데이터베이스 테이블에 모델의 이진 코드를 삽입 _nyc_taxi_models_합니다. 이 메커니즘을 사용 하면 쉽게 저장 하 고 다시 사용 하 여 모델.

2. 그러면 학습 된 삽입을 다음과 같이 저장된 프로시저를 실행 **revoscalepy** 테이블로 모델 *nyc_taxi_models*합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    데이터를 처리하고 모델에 맞추는 데 다소 시간이 걸릴 수 있습니다. Python의 파이프 되는 메시지 **stdout** 스트림은 표시 되는 **메시지** 기간 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. *nyc_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *revoscalepy_model* *0x8003637265766F7363616c....*

다음 단계에서 사용 하 여 학습된 된 모델 예측을 만듭니다.

## <a name="next-step"></a>다음 단계

[저장된 프로시저에 포함 된 Python을 사용 하 여 예측을 실행 합니다.](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>이전 단계

[T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)
