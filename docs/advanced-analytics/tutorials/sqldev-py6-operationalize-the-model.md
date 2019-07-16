---
title: Python 모델-SQL Server Machine Learning을 사용 하 여 잠재적인 결과 예측
description: SQL Server에 포함 된 PYthon 스크립트를 운영 하는 방법을 보여 주는 자습서 저장 프로시저 T-SQL 함수를 사용 하 여
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e5f88beb2c429091fcea8ce66e4defa291e718d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961840"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>저장된 프로시저에 포함 된 Python을 사용 하 여 예측을 실행 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서에 일부 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 하는 방법을 알아봅니다 *운용* 모델을 학습 하 고 이전 단계에서 저장 합니다.

이 시나리오에서는 운영 화 모델 점수 매기기에 대 한 프로덕션에 배포를 의미 합니다. SQL Server와 통합 하면이 상당히 쉽게 저장된 프로시저에서 Python 코드를 포함할 수 있습니다. 새 입력을 기반으로 모델에서 예측을 구하려면, 응용 프로그램에서 저장된 프로시저를 호출 하 고 새 데이터를 전달 하기만 됩니다.

이 단원에 Python 모델을 기반으로 예측을 만드는 두 가지 방법을 보여 줍니다: 점수 매기기 및 행 단위 점수 매기기 배치 합니다.

- **일괄 처리 점수 매기기:** 여러 행의 입력된 데이터를 제공 하려면 SELECT 쿼리를 저장된 프로시저에 인수로 전달 합니다. 결과 입력된 사례에 해당 하는 관찰 테이블입니다.
- **개별 점수 매기기:** 개별 매개 변수 값 집합을 입력으로 전달 합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

점수 매기기에 필요한 모든 Python 코드는 저장된 프로시저의 일부로 제공 됩니다.

## <a name="batch-scoring"></a>일괄 처리 채점

처음 두 개의 저장된 프로시저는 저장된 프로시저에서 Python 예측 호출을 래핑하는 기본 구문을 보여 줍니다. 모두 저장된 프로시저는 데이터 테이블을 입력으로 필요합니다.

- 저장된 프로시저에 입력된 매개 변수로 사용 하 여 정확한 모델의 이름을 제공 됩니다. 저장된 프로시저는 데이터베이스 테이블에서 직렬화 된 모델을 로드 `nyc_taxi_models`.table, 저장된 프로시저의 SELECT 문을 사용 하 여 합니다.
- 직렬화 된 모델은 Python 변수에 저장 된 `mod` 추가 처리를 위해 Python을 사용 합니다.
- 평가 되어야 하는 새 사례를 얻은 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 지정 된 쿼리 `@input_data_1`합니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다.
- 모두 저장된 프로시저에서 함수를 사용 `sklearn` 는 정확도 메트릭에 AUC (곡선 아래의 영역)을 계산 합니다. 대상 레이블에 제공 하면 AUC 등 정확도 메트릭을 생성할 수만 있습니다 (합니다 _tipped_ 열). 예측 대상 레이블에 필요가 없습니다 (변수 `y`), 정확도 메트릭 계산 않지만 합니다.

    따라서 점수를 매길 데이터에 대 한 대상 레이블 없다면 AUC 계산을 제거 하려면 저장된 프로시저를 수정 하 기능에서 팁 확률만를 반환 (변수 `X` 저장된 프로시저에서).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

저장된 프로시저를 만들 실행 다음 T-SQL 문입니다. 이 저장된 프로시저는 scikit를 기반으로 모델에 필요한-해당 패키지에 특정 함수를 사용 하기 때문에 패키지에 알아봅니다.

+ 입력을 포함 하는 데이터 프레임에 전달 되는 `predict_proba` 로지스틱 회귀 모델의 함수 `mod`합니다. `predict_proba` 함수 (`probArray = mod.predict_proba(X)`)를 반환을 **float** (모든 양의) 팁 지정 될 확률을 나타내는입니다.

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

이 저장된 프로시저 동일한 입력을 사용 하 고 이전 저장된 프로시저와 같은 유형의 점수 만들지만에서 기능을 사용 하는 **revoscalepy** 패키지가 SQL Server machine learning을 통해 제공 합니다.

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

## <a name="run-batch-scoring-using-a-select-query"></a>일괄 처리는 SELECT 쿼리를 사용 하 여 점수 매기기 실행

저장된 프로시저 **PredictTipSciKitPy** 하 고 **PredictTipRxPy** 두 입력 매개 변수가 필요 합니다. 

- 점수 매기기에 대 한 데이터를 검색 하는 쿼리
- 학습된 된 모델의 이름

저장된 프로시저에 이러한 인수에 전달 하 여 특정 모델을 선택할 수도 있고 점수 매기기에 사용 되는 데이터를 변경할 수 있습니다.

1. 사용 하는 **scikit-알아봅니다** 점수 매기기에 모델 저장된 프로시저를 호출할 **PredictTipSciKitPy**모델 이름을 전달 하 고 쿼리 문자열을 입력으로 합니다.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    저장된 프로시저 입력 쿼리의 일환으로 전달 된 각 여정에 대해 예측된 확률을 반환 합니다. 
    
    SSMS (SQL Server Management Studio)를 쿼리를 실행 하는 데 사용 하는 확률을 테이블로 나타납니다 합니다 **결과** 창입니다. 합니다 **메시지** 창 약 0.56 값을 사용 하 여 정확도 메트릭이 (AUC 또는 곡선 아래의 영역)를 출력 합니다.

2. 사용 하는 **revoscalepy** 모델 점수 매기기에 대 한 저장된 프로시저를 호출 합니다 **PredictTipRxPy**모델 이름을 전달 하 고 쿼리 문자열을 입력으로 합니다.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>단일 행 점수 매기기

경우에 따라 일괄 처리 점수 매기기 대신 하려는 단일 대/소문자를 전달할 응용 프로그램에서 값을 가져오고 해당 값을 기반으로 하는 단일 결과 반환 합니다. 예를 들어, Excel 워크시트, 웹 응용 프로그램 또는 보고서 저장 프로시저를 설정할 수 있습니다 및 형식화 된 또는 사용자가 선택한 패스를 입력 합니다.

이 섹션에서는 두 개의 저장된 프로시저를 호출 하 여 단일 예측을 만드는 방법에 알아봅니다.

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) 단일 행을 scikit를 사용 하 여 점수 매기기를 위해 설계 되었습니다-모델에 알아봅니다.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) 단일 행 revoscalepy 모델을 사용 하 여 점수 매기기를 위해 설계 되었습니다.
+ 모델을 아직 학습 하지 않은 경우 돌아갑니다 [5 단계](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

일련의 승객 수, 여정 거리 등의 단일 값을 입력으로 두 모델 수행 합니다. 테이블 반환 함수, `fnEngineerFeatures`, 직접 거리, 새로운 기능에 대 한 입력에서 위도 및 경도 값을 변환 하는 데 사용 됩니다. [4 단원](sqldev-py4-create-data-features-using-t-sql.md) 이 테이블 반환 함수에 대 한 설명을 포함 합니다.

모두 저장된 프로시저에 Python 모델을 기반으로 점수를 만듭니다.

> [!NOTE]
> 
> 외부 응용 프로그램에서 저장된 프로시저를 호출 하는 경우 Python 모델에 필요한 모든 입력된 기능을 제공 하는 것입니다. 오류를 방지 하려면 캐스트 또는 데이터 형식과 데이터 길이 유효성 검사 하는 것 외에도 Python 데이터 형식으로 입력된 데이터를 변환 해야 합니다.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

사용 하 여 점수 매기기를 수행 하는 저장된 프로시저의 코드를 검토 합니다 **scikit-알아봅니다** 모델.

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

다음 저장된 프로시저를 사용 하 여 점수 매기기를 수행 합니다 **revoscalepy** 모델입니다.

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

### <a name="generate-scores-from-models"></a>모델에서 점수를 생성 합니다.

저장된 프로시저를 만든 후 모델 중 하나를 기준으로 점수를 생성 하는 것이 쉽습니다. 새 열 **쿼리** 창과 각 기능 열에 대 한 매개 변수를 입력 하거나 붙여 넣습니다. 7 개의 순서로 이러한 기능 열의 값이 필요 합니다.
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 사용 하 여 예측을 생성 하는 **revoscalepy** 모델에서이 문을 실행 합니다.
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 사용 하 여 점수를 생성 하는 **scikit-알아봅니다** 모델에서이 문을 실행:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

두 절차 모두에서 출력 되 고 지정 된 매개 변수 또는 기능을 사용 하 여 택시 여정에 대해 지불 된 팁의 확률은.

## <a name="conclusions"></a>결론

이 자습서에서는 저장된 프로시저에 포함 된 Python 코드를 사용 하는 방법을 알아보았습니다. 와 통합 [!INCLUDE[tsql](../../includes/tsql-md.md)] 훨씬 쉽게 예측에 대 한 Python 모델을 배포 하는 데는 엔터프라이즈 데이터 워크플로의 일부로 재 학습 모델을 통합 합니다.

## <a name="previous-step"></a>이전 단계

[학습 및 Python 모델을 저장 합니다.](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>참조

[SQL Server의 Python 확장](../concepts/extension-python.md)
