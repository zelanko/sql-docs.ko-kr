---
title: 'Python 자습서: SQL 저장 프로시저에서 예측 실행'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈의 5부에서는 SQL Machine Learning을 통해 T-SQL을 사용하여 SQL 저장 프로시저에 포함된 Python 스크립트를 운영합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: 4e101a017197d83217a574ca6521dd60328f536a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470334"
---
# <a name="python-tutorial-run-predictions-using-python-embedded-in-a-stored-procedure"></a>Python 자습서: 저장 프로시저에 포함된 Python을 사용하여 예측 실행
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 5부 자습서 시리즈의 5부에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

이 시나리오에서 말하는 운영은 채점에 사용할 수 있도록 프로덕션 환경에 모델을 배포하는 것을 의미합니다. SQL Server와 통합하면 Python 코드를 저장 프로시저에 포함할 수 있으므로 이 작업을 매우 쉽게 수행할 수 있습니다. 새 입력을 기반으로 모델에서 예측을 얻으려면 간단하게 애플리케이션에서 저장 프로시저를 호출하고 새 데이터를 전달하면 됩니다.

이 자습서 부분에서는 Python 모델을 기반으로 예측을 만드는 두 가지 방법인 일괄 처리 채점과 행 단위 채점을 보여줍니다.

+ **일괄 처리 채점:** 여러 입력 데이터 행을 제공하려면 SELECT 쿼리를 저장 프로시저에 인수로 전달합니다. 그 결과는 입력 사례에 해당하는 관찰 테이블입니다.
+ **개별 채점:** 개별 매개 변수 값 세트를 입력으로 전달합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

채점에 필요한 모든 Python 코드는 저장 프로시저의 일부로 제공됩니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + 일괄 처리 채점을 위한 저장 프로시저 만들기 및 사용
> + 단일 행 채점을 위한 저장 프로시저 만들기 및 사용

[1부](python-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](python-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성했습니다.

[3부](python-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 배웠습니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만들었습니다.

[4부](python-taxi-classification-train-model.md)에서는 SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시켰습니다.

## <a name="batch-scoring"></a>일괄 처리 점수 매기기

처음 두 저장 프로시저는 Python 예측 호출을 저장 프로시저에 래핑하는 기본 구문을 보여줍니다. 두 저장 프로시저 모두 입력으로 데이터 테이블이 필요합니다.

+ 사용할 정확한 모델 이름은 저장 프로시저에 대한 입력 매개 변수로 제공됩니다. 저장 프로시저는 저장 프로시저의 SELECT 문을 사용하여 데이터베이스 테이블 `nyc_taxi_models`.table에서 직렬화된 모델을 로드합니다.
+ 직렬화된 모델은 Python을 사용하여 추가 처리할 수 있도록 Python 변수 `mod`에 저장됩니다.
+ 채점이 필요한 새로운 사례는 `@input_data_1`에 지정된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 가져옵니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다.
+ 두 저장 프로시저는 `sklearn`의 함수를 사용하여 정확도 메트릭 AUC(곡선 아래의 영역)를 계산합니다. AUC 같은 정확도 메트릭은 대상 레이블(_팁받음_ 열)까지 입력하는 경우에만 생성할 수 있습니다. 예측에는 대상 레이블(`y` 변수)이 필요 없지만, 정확도 메트릭 계산에는 필요합니다.

  따라서 데이터를 채점할 대상 레이블이 없는 경우 저장 프로시저를 수정하여 AUC 계산을 제거하고, 기능의 팁 확률(저장 프로시저의 `X` 변수)만 반환할 수 있습니다.

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

다음 T-SQL 문을 실행하여 저장 프로시저를 만듭니다. 이 저장 프로시저는 scikit-learn 패키지와 관련된 함수를 사용하므로 이 패키지를 기반으로 하는 모델이 필요합니다.

입력을 포함하고 있는 데이터 프레임은 로지스틱 회귀 모델 `mod`의 `predict_proba` 함수에 전달됩니다. `predict_proba` 함수(`probArray = mod.predict_proba(X)`)는 금액에 관계없이 팁을 받을 확률을 나타내는 **float** 입니다.

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = mod.predict_proba(X)
probList = []
for i in range(len(probArray)):
  probList.append((probArray[i])[1])

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',  
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

이 저장 프로시저는 동일한 입력을 사용하여 이전 저장 프로시저와 동일한 종류의 점수를 만들지만, SQL Server 기계 학습과 함께 제공되는 **revoscalepy** 패키지의 함수를 사용합니다.

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics
from revoscalepy.functions.RxPredict import rx_predict;

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = rx_predict(mod, X)
probList = probArray["tipped_Pred"].values 

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>SELECT 쿼리를 사용하여 일괄 처리 채점 실행

**PredictTipSciKitPy** 및 **PredictTipRxPy** 저장 프로시저에는 두 개의 입력 매개 변수가 필요합니다.

+ 채점할 데이터를 검색하는 쿼리
+ 학습된 모델의 이름

이러한 인수를 저장 프로시저에 전달하여 특정 모델을 선택하거나 채점에 사용할 데이터를 변경할 수 있습니다.

1. **scikit-learn** 모델을 채점에 사용하려면 **PredictTipSciKitPy** 저장 프로시저를 호출하고, 모델 이름과 쿼리 문자열을 입력으로 전달합니다.

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
   ```

   저장 프로시저는 입력 쿼리의 일부로 전달된 각 운행의 예상 확률을 반환합니다. 

   SSMS(SQL Server Management Studio)를 사용하여 쿼리를 실행하는 경우 확률은 **결과** 창에 표로 표시됩니다. **메시지** 창은 값이 약 0.56인 정확도 메트릭(AUC 또는 곡선 아래의 영역)을 출력합니다.

2. **revoscalepy** 모델을 채점에 사용하려면 **PredictTipRxPy** 저장 프로시저를 호출하고, 모델 이름과 쿼리 문자열을 입력으로 전달합니다.

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
   ```

## <a name="single-row-scoring"></a>단일 행 채점

일괄 처리 채점 대신, 단일 사례를 전달하고, 애플리케이션에서 값을 가져오고, 해당 값을 기반으로 단일 결과를 반환하려는 경우가 가끔 있습니다. 예를 들어 저장 프로시저를 호출하고 사용자가 입력 또는 선택한 입력을 제공하도록 Excel 워크시트, 웹 애플리케이션 또는 보고서를 설정할 수 있습니다.

이 섹션에서는 다음 두 저장 프로시저를 사용하여 단일 예측을 만드는 방법을 알아봅니다.

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy)는 scikit-learn 모델을 사용하는 단일 행 채점을 위해 설계되었습니다.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy)는 revoscalepy 모델을 사용하는 단일 행 채점을 위해 설계되었습니다.
+ 아직 모델을 학습시키지 않은 경우 [5부](python-taxi-classification-train-model.md)로 돌아가세요.

두 모델 모두 승객 수, 주행 거리 등 일련의 단일 값을 입력으로 사용합니다. 테이블 반환 함수 `fnEngineerFeatures`는 입력의 위도 및 경도 값을 새 기능인 직접 거리로 변환하는 데 사용됩니다. [4부](python-taxi-classification-create-features.md)에는 이 테이블 반환 함수에 대한 설명이 포함되어 있습니다.

두 저장 프로시저 모두 Python 모델을 기반으로 점수를 만듭니다.

> [!NOTE]
>
> 외부 애플리케이션에서 저장 프로시저를 호출할 때 Python 모델에 필요한 모든 입력 기능을 제공해야 합니다. 오류를 방지하려면 데이터 형식 및 데이터 길이의 유효성을 검사하는 것 외에도 입력 데이터를 Python 데이터 형식으로 캐스팅하거나 변환해야 할 수도 있습니다.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

**scikit-learn** 모델을 사용하여 채점을 수행하는 저장 프로시저의 코드를 잠시 검토해 보세요.

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)
probList = []
probList.append((mod.predict_proba(X)[0])[1])

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

다음 저장 프로시저는 **revoscalepy** 모델을 사용하여 채점을 수행합니다.

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
  '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from revoscalepy.functions.RxPredict import rx_predict;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)

probArray = rx_predict(mod, X)

probList = []
probList = probArray["tipped_Pred"].values

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>모델에서 점수 생성

저장 프로시저를 만든 후에는 두 모델 중 하나를 기반으로 간편하게 점수를 생성할 수 있습니다. 새 **쿼리** 창을 열고, 각 기능 열에 대한 매개 변수를 입력하거나 붙어넣으면 됩니다. 이러한 기능 열에 필요한 7개 값은 순서대로 다음과 같습니다.

+ *passenger_count*
+ *trip_distance*
+ *trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. **revoscalepy** 모델을 사용하여 예측을 생성하려면 다음 명령문을 실행합니다.
  
   ```sql
   EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

2. **scikit-learn** 모델을 사용하여 점수를 생성하려면 다음 명령문을 실행합니다.

   ```sql
   EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

두 프로시저의 출력은 매개 변수 또는 기능이 지정된 택시 운행에서 팁이 지불될 확률입니다.

## <a name="conclusions"></a>결론

이 자습서 시리즈에서는 저장 프로시저에 포함된 Python 코드를 사용하는 방법을 배웠습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]과 통합되므로 훨씬 간편하게 예측용 Python 모델을 배포하고, 모델 재학습을 엔터프라이즈 데이터 워크플로의 일부로 통합할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + 일괄 처리 채점을 위한 저장 프로시저 만들기 및 사용
> + 단일 행 채점을 위한 저장 프로시저 만들기 및 사용

Python에 대한 자세한 내용은 [SQL Server의 Python 확장](../concepts/extension-python.md)을 참조하세요.
