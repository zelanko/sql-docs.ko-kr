---
title: 'Python 자습서: 모델 학습 및 저장'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈의 4부에서는 SQL Machine Learning을 통해 SQL Server의 Transact-SQL을 사용하여 Python에서 모델을 학습시키고 저장합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 18cd0c279493dcb41d043d3f76d6debe71eb402c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194481"
---
# <a name="python-tutorial-train-and-save-a-python-model-using-t-sql"></a>Python 자습서: T-SQL을 사용하여 Python 모델 학습 및 저장
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 5부 자습서 시리즈의 4부에서는 Python 패키지 **scikit-learn** 및 **revoscalepy**를 사용하여 기계 학습 모델을 학습시키는 방법을 알아봅니다. 이러한 Python 라이브러리는 SQL Server Machine Learning에 이미 설치되어 있습니다.

SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시킵니다. 모델에는 이 자습서 시리즈의 이전 부분에서 엔지니어링한 데이터 기능이 필요합니다. 마지막으로, 학습된 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + SQL 저장 프로시저를 사용하여 모델 만들기 및 학습
> + 학습된 모델을 SQL 테이블에 저장

[1부](python-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](python-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성했습니다.

[3부](python-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 배웠습니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만들었습니다.

[5부](python-taxi-classification-deploy-model.md)에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>샘플 데이터를 학습 집합 및 테스트 집합으로 분할

1. **PyTrainTestSplit**라는 저장 프로시저를 만들어 nyctaxi_sample 테이블의 데이터를 nyctaxi_sample_training 및 nyctaxi_sample_testing이라는 두 부분으로 나눕니다. 

   이 저장 프로시저는 이미 자동으로 생성되어 있지만 다음 코드를 실행하여 만들 수 있습니다.

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

2. 사용자 지정 분할을 사용하여 데이터를 나누려면 저장 프로시저를 실행하고 학습 집합에 할당된 데이터의 비율을 나타내는 정수를 입력합니다. 예를 들어 다음 명령문은 학습 집합에 60%의 데이터를 할당합니다.

   ```sql
   EXEC PyTrainTestSplit 60
   GO
   ```

## <a name="build-a-logistic-regression-model"></a>로지스틱 회귀 모델 빌드

데이터가 준비되면 데이터를 사용하여 모델을 학습시킬 수 있습니다. 이렇게 하려면 일부 Python 코드를 실행하는 저장 프로시저를 호출하고 학습 데이터 테이블을 입력합니다. 이 자습서에서는 두 가지 모델을 만들며, 둘 다 이진 분류 모델입니다.

+ 저장 프로시저 **PyTrainScikit**는 **scikit-learn** 패키지를 사용하여 팁 예측 모델을 만듭니다.
+ 저장 프로시저 **TrainTipPredictionModelRxPy**는 **revoscalepy** 패키지를 사용하여 팁 예측 모델을 만듭니다.

각 프로시저는 사용자가 제공한 입력 데이터를 사용하여 로지스틱 회귀 모델을 만들고 학습시킵니다. 모든 Python 코드는 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 래핑됩니다.

모델에 새 데이터를 더 쉽게 재학습시키려면 sp_execute_external_script에 대한 호출을 다른 저장 프로시저에 래핑하고 새 학습 데이터를 매개 변수로 전달합니다. 이 섹션에서는 이러한 프로세스를 안내합니다.

### <a name="pytrainscikit"></a>PyTrainScikit

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 **쿼리** 창을 열고 다음 명령문을 실행하여 저장 프로시저 **PyTrainScikit**를 만듭니다.  이 저장 프로시저에는 입력 데이터 정의가 포함되어 있으므로 입력 쿼리를 제공하지 않아도 됩니다.

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

2. 다음 SQL 문을 실행하여 학습된 모델을 nyc\_taxi_models 테이블에 삽입합니다.

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC PyTrainScikit @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
   ```

   데이터를 처리하고 모델을 맞추는 데 몇 분 정도 걸릴 수 있습니다. Python의 **stdout** 스트림에 파이프되는 메시지는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **메시지** 창에 표시됩니다. 예를 들어:

   ```text
   STDOUT message(s) from external script:
   C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy
   ```

3. *nyc\_taxi_models* 테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

   ```text
   SciKit_model
   0x800363736B6C6561726E2E6C696E6561....
   ```

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

이 저장 프로시저는 새로운 Python용 패키지인 새로운 **revoscalepy** 패키지를 사용합니다. 여기에는 R 언어의 **RevoScaleR** 패키지에 제공되는 것과 유사한 개체, 변환 및 알고리즘이 포함되어 있습니다. 

**revoscalepy**를 사용하여 로지스틱 및 선형 회귀, 의사 결정 트리 등과 같이 널리 사용되는 알고리즘을 통해 원격 컴퓨팅 컨텍스트를 만들고, 컴퓨팅 컨텍스트 간에 데이터를 이동하고, 데이터를 변환하고, 예측 모델을 학습시킬 수 있습니다. 자세한 내용은 [SQL Server의 revoscalepy 모듈](../python/ref-py-revoscalepy.md) 및 [revoscalepy 함수 참조](/r-server/python-reference/revoscalepy/revoscalepy-package)를 참조하세요.

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 **쿼리** 창을 열고 다음 명령문을 실행하여 저장 프로시저 _TrainTipPredictionModelRxPy_를 만듭니다.  저장 프로시저에는 입력 데이터 정의가 이미 포함되어 있으므로 입력 쿼리를 제공하지 않아도 됩니다.

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

   이 저장 프로시저는 모델 학습의 일부로 다음 단계를 수행합니다.

   + SELECT 쿼리는 사용자 지정 스칼라 함수 _fnCalculateDistance_를 적용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과는 기본 Python 입력 변수인 `InputDataset`에 저장됩니다.
   + 이진 변수 _tipped_는 *label* 또는 결과 열로 사용되며, 모델은 _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_ 등의 기능 열을 사용하여 맞춰집니다.
   + 학습된 모델은 직렬화되어 Python 변수 `logitObj`에 저장됩니다. T-SQL 키워드 OUTPUT을 추가하여 이 변수를 저장 프로시저의 출력으로 추가할 수 있습니다. 다음 단계에서는 이 변수를 사용하여 모델의 이진 코드를 데이터베이스 테이블 _nyc_taxi_models_에 삽입합니다. 이 메커니즘을 사용하면 모델을 쉽게 저장하고 재사용할 수 있습니다.

2. 다음과 같이 저장 프로시저를 실행하여 학습된 **revoscalepy** 모델을 *nyc_taxi_models* 테이블에 삽입합니다.

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC TrainTipPredictionModelRxPy @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
   ```

   데이터를 처리하고 모델을 맞추는 데 시간이 걸릴 수도 있습니다. Python의 **stdout** 스트림에 파이프되는 메시지는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **메시지** 창에 표시됩니다. 예를 들어:

   ```text
   STDOUT message(s) from external script:
   C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy
   ```

3. *nyc_taxi_models*테이블을 엽니다. _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

   ```text
   revoscalepy_model
   0x8003637265766F7363616c....
   ```

이 자습서의 다음 부분에서는 학습된 모델을 사용하여 예측을 생성합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + SQL 저장 프로시저를 사용하여 모델 만들기 및 학습
> + 학습된 모델을 SQL 테이블에 저장

> [!div class="nextstepaction"]
> [Python 자습서: 저장 프로시저에 포함된 Python을 사용하여 예측 실행](python-taxi-classification-deploy-model.md)