---
title: 'R 자습서: SQL 저장 프로시저에서 예측 실행'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈의 5부에서는 SQL Machine Learning을 통해 T-SQL을 사용하여 SQL 저장 프로시저에 포함된 R 스크립트를 운영합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: 0b32d12a694062e56611abaff18dc4f1e2f23061
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470114"
---
# <a name="r-tutorial-run-predictions-in-sql-stored-procedures"></a>R 자습서: SQL 저장 프로시저에서 예측 실행
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 5부 자습서 시리즈의 5부에서는 4부에서 가능한 결과를 예측하는 모델을 사용하여 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다. 모델은 다른 애플리케이션에서 직접 호출될 수 있는 저장 프로시저에 래핑됩니다.

이 문서에서는 채점을 수행하는 두 가지 방법을 보여 줍니다.

+ **일괄 처리 채점 모드**: 저장 프로시저에 대한 입력으로 SELECT 쿼리를 사용합니다. 저장 프로시저에서 입력 사례에 해당하는 관찰 테이블을 반환합니다.

+ **개별 점수 매기기 모드**: 개별 매개 변수 값 집합을 입력으로 전달합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + 일괄 처리 채점을 위한 저장 프로시저 만들기 및 사용
> + 단일 행 채점을 위한 저장 프로시저 만들기 및 사용

[1부](r-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](r-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성했습니다.

[3부](r-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 배웠습니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만들었습니다.

[4부](r-taxi-classification-train-model.md)에서는 SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시켰습니다.

## <a name="basic-scoring"></a>기본 채점

저장 프로시저 **RPredict** 는 `PREDICT` 호출을 저장 프로시저에 래핑하는 기본 구문을 보여 줍니다.

```sql
CREATE PROCEDURE [dbo].[RPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model));
    print(summary(mod))
    OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
    str(OutputDataSet)
    print(OutputDataSet)
    ',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS (("Score" float));
END
GO
```

+ SELECT 문은 데이터베이스에서 직렬화된 모델을 가져와서 R을 사용한 추가 처리를 위해 R 변수 `mod` 에 모델을 저장합니다.

+ 새로운 채점 사례는 저장 프로시저의 첫 번째 매개 변수인 `@inquery`에 지정된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 가져옵니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다. 이 데이터 프레임은 점수를 생성하는 [PREDICT](/sql/t-sql/queries/predict-transact-sql) 함수에 전달됩니다.
  
  `OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));`
  
  data.frame에 단일 행이 포함될 수 있으므로 일괄 처리 또는 단일 점수 매기기에 동일한 코드를 사용할 수 있습니다.
  
+ `PREDICT` 함수로 반환되는 값은 운전사가 금액에 관계없이 팁을 받게 될 확률을 나타내는 **float** 입니다.

## <a name="batch-scoring-a-list-of-predictions"></a>일괄 채점(예측 목록)

보다 일반적인 시나리오는 일괄 처리 모드에서 여러 관찰에 대한 예측을 생성하는 것입니다. 이 단계에서는 일괄 처리 채점의 작동 방식을 살펴보겠습니다.

1. 사용할 작은 입력 데이터 세트를 가져오는 것으로 시작합니다. 이 쿼리는 승객 수 및 예측을 수행하는 데 필요한 다른 기능과 함께 "상위 10개"의 여정 목록을 만듭니다.
  
   ```sql
   SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
   
   FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

   LEFT OUTER JOIN

   (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

   ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
   AND a.pickup_datetime=b.pickup_datetime
   WHERE b.medallion IS NULL
   ```

   **샘플 결과**

   ```text
   passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime          direct_distance
   1                 283                  0.7            2013-03-27 14:54:50.000   0.5427964547
   1                 289                  0.7            2013-02-24 12:55:29.000   0.3797099614
   1                 214                  0.7            2013-06-26 13:28:10.000   0.6970098661
   ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 **RPredictBatchOutput** 이라는 저장 프로시저를 만듭니다.

   ```sql
   CREATE PROCEDURE [dbo].[RPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
   AS
   BEGIN
   DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
   EXEC sp_execute_external_script 
     @language = N'R',
     @script = N'
       mod <- unserialize(as.raw(model));
       print(summary(mod))
       OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
       str(OutputDataSet)
       print(OutputDataSet)
     ',
     @input_data_1 = @inquery,
     @params = N'@model varbinary(max)',
     @model = @lmodel2
     WITH RESULT SETS ((Score float));
   END
   ```

3. 변수에 쿼리 텍스트를 제공하고 이를 저장 프로시저에 대한 매개 변수로 전달합니다.

   ```sql
   -- Define the input data
   DECLARE @query_string nvarchar(max)
   SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
   
   -- Call the stored procedure for scoring and pass the input data
   EXEC [dbo].[RPredictBatchOutput] @model = 'RTrainLogit_model', @inquery = @query_string;
   ```
  
저장 프로시저에서 각 상위 10개의 여정에 대한 예측을 나타내는 일련의 값을 반환합니다. 하지만 이러한 상위 여정은 이동 거리가 비교적 짧고 단일 승객이 탑승한 여정이며, 운전사가 팁을 받을 가능성이 낮습니다.

> [!TIP]
> 단순히 "팁 있음" 및 "팁 없음" 결과를 반환하는 대신 예측의 확률 점수를 반환한 다음, _Score_ 열 값에 WHERE 절을 적용하여 0.5 또는 0.7과 같은 임계값을 사용해서 "팁 가능성 높음" 또는 "팁 가능성 낮음"으로 점수를 분류할 수도 있습니다. 이 단계는 저장 프로시저에 포함되어 있지 않지만 쉽게 구현할 수 있습니다.

## <a name="single-row-scoring-of-multiple-inputs"></a>여러 입력의 단일 행 채점

일부 경우에는 여러 입력 값을 전달하고 이러한 값을 기준으로 단일 예측을 가져와야 할 수 있습니다. 예를 들어 저장 프로시저를 호출하고 애플리케이션에서 사용자가 입력 또는 선택한 입력을 제공하도록 Excel 워크시트, 웹 애플리케이션 또는 Reporting Services 보고서를 설정할 수 있습니다.

이 섹션에서는 승객 수, 주행 거리 등의 여러 입력을 받아들이는 저장 프로시저를 사용해서 단일 예측을 생성하는 방법을 알아봅니다. 저장 프로시저는 이전에 저장된 R 모델을 기반으로 하여 점수를 만듭니다.
  
외부 애플리케이션에서 저장 프로시저를 호출하는 경우 데이터가 R 모델의 요구 사항과 일치하는지 확인합니다. 여기에는 입력 데이터를 R 데이터 형식으로 캐스팅 또는 변환할 수 있는지 확인, 데이터 형식 및 데이터 길이의 유효성 검사 등이 포함될 수 있습니다.

1. 저장 프로시저 **RPredictSingleRow** 를 만듭니다.
  
   ```sql
   CREATE PROCEDURE [dbo].[RPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
   AS
   BEGIN
   DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
   DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
   EXEC sp_execute_external_script  
     @language = N'R',
     @script = N'  
       mod <- unserialize(as.raw(model));  
       print(summary(mod));  
       OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
       str(OutputDataSet);
       print(OutputDataSet); 
       ',  
     @input_data_1 = @inquery,  
     @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
     WITH RESULT SETS ((Score float));  
   END
   ```

2. 수동으로 값을 제공하여 실험해 보세요.
  
   새 **쿼리** 창을 열고 각 매개 변수 값을 제공하여 저장 프로시저를 호출합니다. 매개 변수는 모델에 사용되며 필수인 기능 열을 나타냅니다.

   ```sql
   EXEC [dbo].[RPredictSingleRow] @model = 'RTrainLogit_model',
   @passenger_count = 1,
   @trip_distance = 2.5,
   @trip_time_in_secs = 631,
   @pickup_latitude = 40.763958,
   @pickup_longitude = -73.973373,
   @dropoff_latitude =  40.782139,
   @dropoff_longitude = -73.977303
   ```

   또는 다음과 같은 더 짧은 지원 양식을 [저장 프로시저에 대한 매개변수](../../relational-databases/stored-procedures/specify-parameters.md)로 사용합니다.
  
   ```sql
   EXEC [dbo].[RPredictSingleRow] 'RTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

3. 모두 주행 거리가 비교적 짧은 단일 승객 여정이기 때문에 결과는 이러한 상위 10개의 여정에서 팁을 받을 확률이 낮음(0)을 나타냅니다.

## <a name="conclusions"></a>결론

지금까지 저장 프로시저에서 R 코드를 포함하는 방법을 배웠으므로, 이제는 이러한 방식을 확장하여 고유 모델을 빌드할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 과 통합되어 보다 쉽게 예측에 대한 R 모델을 배포하고 모델 다시 학습을 엔터프라이즈 데이터 워크플로의 일부로 통합할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + 일괄 처리 채점을 위한 저장 프로시저 만들기 및 사용
> + 단일 행 채점을 위한 저장 프로시저 만들기 및 사용

R에 대한 자세한 내용은 [SQL Server의 R 확장](../concepts/extension-r.md)을 참조하세요.