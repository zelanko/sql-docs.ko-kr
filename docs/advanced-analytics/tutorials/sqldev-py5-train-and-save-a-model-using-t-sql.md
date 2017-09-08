---
title: "5단계: T-SQL을 사용하여 모델 학습 및 저장 | Microsoft 문서"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>5 단계: 학습 및 T-SQL을 사용 하 여 모델 저장

이 단계에서는 Python 패키지를 사용 하 여 기계 학습 모델을 학습 하는 방법을 배웁니다 **scikit-자세한** 및 **revoscalepy**합니다. 이러한 Python 라이브러리 모듈을 로드 하 고 저장된 프로시저 내에서 필요한 함수를 호출할 수 있도록 SQL Server 컴퓨터 학습 services에 설치 되어 있습니다. 방금 만든 데이터 기능을 사용하여 모델을 학습한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 학습된 모델을 저장합니다.

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>샘플 데이터를 학습 집합과 테스트 집합으로 분합니다

1. 데이터는 nyctaxi에서 하는 저장된 프로시저를 생성 하려면 다음 T-SQL 명령을 실행\_예제 테이블의 두 부분으로: nyctaxi\_샘플\_교육 및 nyctaxi\_샘플\_테스트 합니다.

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

2. 저장된 프로시저를 실행 하 고 학습 집합에 할당 된 데이터의 비율을 나타내는 정수를 입력 합니다. 예를 들어 다음 문은 데이터를 학습 집합의 60% 할당 합니다. 학습 및 테스트 데이터는 두 개의 별도 테이블에 저장 됩니다.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>Scikit를 사용 하 여 로지스틱 회귀 모델을 작성-자세한 내용은

이 섹션에서는 지금까지 준비한 학습 데이터를 사용 하 여 모델 학습에 사용할 수 있는 저장된 프로시저를 만듭니다. 이 저장된 프로시저는 입력된 데이터를 정의 하 고 사용 하 여 한 **scikit-자세한** 로지스틱 회귀 모델을 학습 하는 함수입니다. 시스템 저장 프로시저를 사용 하 여 SQL Server와 함께 설치 되는 Python 런타임의 호출 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

모델을 다시 학습 좀 더 쉽게 다른 저장된 프로시저에 sp_execute_exernal_script에 대 한 호출을 래핑할 수 있으며 매개 변수로 새 학습 데이터를 전달 키를 누릅니다. 이 섹션에서는 프로세스를 통해 안내 합니다.

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModelSciKitPy_합니다.  따라서 입력된 쿼리를 제공 하지 않아도 됩니다. 저장된 프로시저 입력된 데이터의 정의 포함 하는 참고 합니다.

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
      import pandas
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

    *외부 스크립트의 STDOUT 메시지:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 테이블을 열고 *nyc\_taxi_models*합니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *linear_model* *0x800363736B6C6561726E2E6C696E6561...*

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>사용 하 여 로지스틱 모델 빌드는 _revoscalepy_ 패키지

이제 새를 사용 하 여 다른 저장된 프로시저를 만들 **revoscalepy** 로지스틱 회귀 모델을 학습 하는 패키지입니다. **revoscalepy** 개체, 변환 및 R 언어에 대해 제공 하는 것과 유사한 알고리즘을 포함 하는 Python에 대 한 패키지 **RevoScaleR** 패키지 합니다. 이 라이브러리와 계산 컨텍스트, 데이터를 변환 및 물류 및 선형 회귀, 의사 결정 트리 등과 같은 인기 있는 알고리즘을 사용 하 여 예측 모델을 학습 간에 데이터를 이동, 한 계산 컨텍스트를 만듭니다 수 있습니다. 자세한 내용은 참조 [revoscalepy 란?](../python/what-is-revoscalepy.md)

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModelRxPy_합니다.  이 모델도 지금까지 준비한 학습 데이터를 사용 합니다. 에 이미 저장된 프로시저는 입력된 데이터의 정의 포함 되므로 입력된 쿼리를 제공할 필요가 없습니다.

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
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - Nyctaxi에서 revoscalepy 패키지를 사용 하 여 로지스틱 회귀 모델을 학습\_샘플\_학습 데이터입니다.
    - SELECT 쿼리는 사용자 지정 스칼라 함수 _fnCalculateDistance_ 를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과 기본 Python 입력된 변수에 저장 됩니다 `InputDataset`합니다.
    - 에 포함 되어 있는 revoscalepy의 LogisticRegression 함수를 호출 하는 Python 스크립트 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 로지스틱 회귀 모델을 만듭니다.
    - 이진 변수 _tipped_ 는 *label* 또는 결과 열로 사용되며  _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_등의 기능 열을 사용하여 모델을 맞춥니다.
    - Python 변수에 포함 하는 학습 된 모델 `logitObj`, serialize 되 고 출력 매개 변수를 삽입 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 출력 데이터베이스 테이블에 삽입 됩니다 _nyc_taxi_models_, 새 행으로 해당 이름과 함께 검색 하 고 이후의 예측에 사용할 수 있도록 합니다.

2. 그러면 학습 된 삽입 하려면 다음과 같이 저장된 프로시저 실행 **revoscalepy** 테이블 _nyc에 모델\_택시\_모델.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    데이터를 처리 하 고 모델을 맞출 시간이 걸릴 수 있습니다. Python의 파이프 될 메시지 **stdout** 스트림에 표시 되는 **메시지** 의 창 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 예를 들어

    *외부 스크립트의 STDOUT 메시지:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. *nyc_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    *rx_model* *0x8003637265766F7363616c...*

다음 단계에서는 학습된 된 모델을 사용 하 여 예측을 만듭니다.

## <a name="next-step"></a>다음 단계

[6 단계: 모델을 운용](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>이전 단계

[4 단계: T-SQL을 사용 하 여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

