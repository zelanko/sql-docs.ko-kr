---
title: Python 모델을 사용 하 여 잠재적 결과 예측
description: T-sql 함수를 사용 하 여 SQL Server 저장 프로시저에 포함 된 PYthon 스크립트를 운영 하는 방법을 보여 주는 자습서
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 275981cbd4543263507415b5e7ba783f1ecbd8e5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345847"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>저장 프로시저에 포함 된 Python을 사용 하 여 예측 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)자습서의 일부입니다. 

이 단계에서는 이전 단계에서 학습 하 고 저장 한 모델을 *운영* 하는 방법을 알아봅니다.

이 시나리오에서 운영 화은 점수 매기기를 위해 프로덕션에 모델을 배포 하는 것을 의미 합니다. 저장 프로시저에 Python 코드를 포함할 수 있기 때문에 SQL Server와 통합 하면이 작업을 매우 쉽게 수행할 수 있습니다. 새 입력을 기반으로 모델에서 예측을 가져오려면 응용 프로그램에서 저장 프로시저를 호출 하 고 새 데이터를 전달 하면 됩니다.

이 단원에서는 Python 모델을 기반으로 하는 예측을 만드는 두 가지 방법, 즉 일괄 처리 점수 매기기 및 행별로 행 기준 점수 매기기 방법을 보여 줍니다.

- **일괄 처리 점수 매기기:** 입력 데이터의 여러 행을 제공 하려면 SELECT 쿼리를 저장 프로시저에 인수로 전달 합니다. 그러면 입력 사례에 해당 하는 관찰 테이블이 생성 됩니다.
- **개별 점수 매기기:** 개별 매개 변수 값 집합을 입력으로 전달 합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

점수 매기기에 필요한 모든 Python 코드는 저장 프로시저의 일부로 제공 됩니다.

## <a name="batch-scoring"></a>일괄 처리 채점

처음 두 개의 저장 프로시저는 저장 프로시저에서 Python 예측 호출을 래핑하는 기본 구문을 보여 줍니다. 두 저장 프로시저 모두 입력으로 데이터 테이블이 필요 합니다.

- 사용할 정확한 모델의 이름은 저장 프로시저에 대 한 입력 매개 변수로 제공 됩니다. 저장 프로시저는 저장 프로시저의 SELECT 문을 사용 하 여 `nyc_taxi_models`데이터베이스 테이블에서 serialize 된 모델을 로드 합니다.
- 직렬화 된 모델은 python을 사용 하 여 `mod` 추가 처리를 위해 python 변수에 저장 됩니다.
- 점수가 매겨진 새 사례는에 [!INCLUDE[tsql](../../includes/tsql-md.md)] `@input_data_1`지정 된 쿼리에서 가져옵니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다.
- 두 저장 프로시저는의 `sklearn` 함수를 사용 하 여 정확도 메트릭 (곡선 아래의 영역)을 계산 합니다. 대상 레이블 ( _크리스마스_ 열)도 제공 하는 경우에만 cc와 같은 정확도 메트릭을 생성할 수 있습니다. 예측에는 대상 레이블 (변수 `y`)이 필요 하지 않지만 정확도 메트릭 계산은 필요 합니다.

    따라서 점수를 매길 데이터의 대상 레이블이 없는 경우에는 저장 프로시저를 수정 하 여이 계산을 제거 하 고 기능 (저장 프로시저의 변수 `X` )에서 팁 확률만 반환할 수 있습니다.

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

다음 T-sql 문을 실행 하 여 저장 프로시저를 만듭니다. 이 저장 프로시저에는 해당 패키지와 관련 된 함수를 사용 하기 때문에 scikit 패키지를 기반으로 하는 모델이 필요 합니다.

+ 입력을 포함 하는 데이터 프레임은 로지스틱 `predict_proba` 회귀 `mod`모델의 함수에 전달 됩니다. 함수 `predict_proba` (`probArray = mod.predict_proba(X)`)는 팁 (임의 금액)이 지정 될 확률을 나타내는 **float** 를 반환 합니다.

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

이 저장 프로시저는 동일한 입력을 사용 하며 이전 저장 프로시저와 동일한 종류의 점수를 만들지만 SQL Server machine learning과 함께 제공 되는 **revoscalepy** 패키지의 함수를 사용 합니다.

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

## <a name="run-batch-scoring-using-a-select-query"></a>SELECT 쿼리를 사용 하 여 일괄 처리 점수 매기기 실행

저장 프로시저 **PredictTipSciKitPy** 및 **Predicttiprxpy** 에는 두 개의 입력 매개 변수가 필요 합니다. 

- 점수 매기기를 위한 데이터를 검색 하는 쿼리입니다.
- 학습 된 모델의 이름

이러한 인수를 저장 프로시저에 전달 하 여 특정 모델을 선택 하거나 점수 매기기에 사용 되는 데이터를 변경할 수 있습니다.

1. 점수 매기기에 **scikit** 모델을 사용 하려면 모델 이름과 쿼리 문자열을 입력으로 전달 하 여 저장 프로시저 **PredictTipSciKitPy**를 호출 합니다.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    저장 프로시저는 입력 쿼리의 일부로 전달 된 각 트립에 대해 예측 확률을 반환 합니다. 
    
    SSMS (SQL Server Management Studio)를 사용 하 여 쿼리를 실행 하는 경우 확률은 **결과** 창에 테이블로 표시 됩니다. **메시지** 창은 값 0.56를 사용 하 여 정확도 메트릭 (지 각 또는 곡선 아래의 영역)을 출력 합니다.

2. 점수 매기기에 **revoscalepy** 모델을 사용 하려면 모델 이름과 쿼리 문자열을 입력으로 전달 하 여 **저장 프로시저를**호출 합니다.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>단일 행 점수 매기기

때로는 일괄 처리 점수 매기기 대신 단일 사례를 전달 하 고, 응용 프로그램에서 값을 가져오고, 해당 값을 기반으로 단일 결과를 반환할 수 있습니다. 예를 들어 저장 프로시저를 호출 하 고 사용자가 입력 하거나 선택한 입력으로 전달 하도록 Excel 워크시트, 웹 응용 프로그램 또는 보고서를 설정할 수 있습니다.

이 섹션에서는 두 개의 저장 프로시저를 호출 하 여 단일 예측을 만드는 방법을 배웁니다.

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) 는 scikit 모델을 사용 하 여 단일 행 점수 매기기를 위해 설계 되었습니다.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) 는 revoscalepy 모델을 사용 하 여 단일 행 점수 매기기를 위해 설계 되었습니다.
+ 아직 모델을 학습 하지 않은 경우 [5 단계로](sqldev-py5-train-and-save-a-model-using-t-sql.md)돌아갑니다.

두 모델은 모두 승객 수, 거리 등과 같은 일련의 단일 값을 입력으로 사용 합니다. 테이블 반환 함수 `fnEngineerFeatures`는 입력의 위도 및 경도 값을 직접 거리의 새 기능으로 변환 하는 데 사용 됩니다. [4 단원](sqldev-py4-create-data-features-using-t-sql.md) 에는이 테이블 반환 함수에 대 한 설명이 포함 되어 있습니다.

두 저장 프로시저는 모두 Python 모델을 기반으로 점수를 만듭니다.

> [!NOTE]
> 
> 외부 응용 프로그램에서 저장 프로시저를 호출할 때 Python 모델에 필요한 모든 입력 기능을 제공 하는 것이 중요 합니다. 오류를 방지 하려면 데이터 형식 및 데이터 길이의 유효성을 검사 하는 것 외에도 입력 데이터를 Python 데이터 형식으로 캐스팅 하거나 변환 해야 할 수 있습니다.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

**Scikit** 모델을 사용 하 여 점수 매기기를 수행 하는 저장 프로시저의 코드를 검토해 보십시오.

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

다음 저장 프로시저는 **revoscalepy** 모델을 사용 하 여 점수 매기기를 수행 합니다.

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

저장 프로시저를 만든 후에는 두 모델을 기준으로 점수를 쉽게 생성할 수 있습니다. 새 **쿼리** 창을 열고 각 기능 열에 대해 매개 변수를 입력 하거나 붙여 넣습니다. 이러한 기능 열에 대 한 7 가지 필수 값은 다음과 같습니다.
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. **Revoscalepy** 모델을 사용 하 여 예측을 생성 하려면 다음 문을 실행 합니다.
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. **Scikit** 모델을 사용 하 여 점수를 생성 하려면 다음 문을 실행 합니다.

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

두 절차의 출력은 지정 된 매개 변수 또는 기능을 사용 하 여 taxi 여행에 대 한 팁이 지불 될 확률입니다.

## <a name="conclusions"></a>결론

이 자습서에서는 저장 프로시저에 포함 된 Python 코드를 사용 하는 방법을 알아보았습니다. 와 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 통합을 통해 예측을 위해 Python 모델을 훨씬 쉽게 배포 하 고 엔터프라이즈 데이터 워크플로의 일부로 모델 재 학습을 통합할 수 있습니다.

## <a name="previous-step"></a>이전 단계

[Python 모델 학습 및 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>참조

[SQL Server의 Python 확장](../concepts/extension-python.md)
