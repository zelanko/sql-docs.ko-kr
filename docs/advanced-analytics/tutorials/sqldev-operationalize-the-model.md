---
title: R 모델-SQL Server Machine Learning을 사용 하 여 4 단원 예측 가능한 결과
description: SQL Server에 포함 된 R 스크립트를 운영 하는 방법을 보여 주는 자습서 저장 프로시저 T-SQL 함수를 사용 하 여
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4e74f587177c31f55c952eb06ccb8a7e8960c93a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511590"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>4단원: 저장된 프로시저에 포함 된 R을 사용 하 여 예측을 실행 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 새 관찰에 대해 모델을 사용 하 여 잠재적인 결과 예측 하 배웁니다. 모델은 다른 응용 프로그램에서 직접 호출할 수 있는 저장된 프로시저에 래핑됩니다. 이 연습에서는 점수 매기기를 수행 하는 여러 방법을 보여 줍니다.

- **일괄 처리 점수 매기기 모드**: 저장된 프로시저에 대 한 입력으로 선택 쿼리를 사용 합니다. 저장 프로시저는 입력된 사례(case)에 해당하는 관측 표를 반환합니다.

- **개별 점수 매기기 모드**: 개별 매개 변수 값 집합을 입력으로 전달 합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

먼저 점수 매기기의 일반적인 작동 방식을 살펴보겠습니다.

## <a name="basic-scoring"></a>기본 점수 매기기

저장된 프로시저 **RxPredict** 저장된 프로시저에서 RevoScaleR rxPredict 호출을 래핑하는 기본 구문을 보여 줍니다.

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ SELECT 문은 데이터베이스에서 직렬화된 모델을 가져와서, R을 사용한 추가 처리를 위해 R 변수 `mod`에 그 모델을 저장합니다.

+ 새로운 점수매기기 사례는 저장 프로시저의 첫 번째 매개변수인 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 지정된 `@inquery` 쿼리에서 가져옵니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다. 이 데이터 프레임에 전달 되는 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 함수 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), 점수를 생성 합니다.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    data.frame에 단일 행이 포함될 수 있으므로 일괄 처리 또는 단일 점수 매기기에 동일한 코드를 사용할 수 있습니다.
  
+ `rxPredict` 함수에 의해 번환되는 값은 운전자가 임의의 팁을 얻을 확률을 나타내는 **float**입니다.

## <a name="batch-scoring-a-list-of-predictions"></a>일괄 처리 (예측 목록)을 점수 매기기

더 일반적인 시나리오는 일괄 처리 모드에서 여러 관찰에 대 한 예측을 생성 하는 것입니다. 이 단계에서는 일괄 처리 점수 매기기의 작동 방식을 확인해 보겠습니다.

1.  입력된 데이터를 사용 하 여 작동 한 정하여를 가져와서 시작 합니다. 이 쿼리는 승객 수 및 예측을 수행하는 데 필요한 다른 특성과 함께 "상위 10개"의 여정 목록을 만듭니다.
  
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
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. 호출할 저장된 프로시저를 만듭니다 **RxPredictBatchOutput** 에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  변수에 쿼리 텍스트를 입력하고 저장 프로시저에 매개변수로 전달합니다.

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
저장 프로시저는 상위 10개 여정 각각에 대한 예측을 나타내는 일련의 값을 반환합니다. 그러나, 상위 여정은 운전자가 팁을 얻지 못할 수도 있는 비교적 여행 거리가 짧은 단일 승객 여행이기도 합니다.
  

> [!TIP]
> 
> "yes-tip" 및 "no-tip" 결과만 반환하는 대신 예측에 대한 확률 점수를 반환하고 _Score_ 열 값에 WHERE 절을 적용하여 점수를 0.5 또는 0.7과 같은 임계 값을 사용한 "팁을 줄 가능성이 높음" 또는 "주지 않을 가능성이 있음"으로 분류 할 수 있습니다.  이 단계는 저장 프로시저에 포함되지 않지만 쉽게 구현할 수 있습니다.

## <a name="single-row-scoring-of-multiple-inputs"></a>여러 입력의 단일 행 점수 매기기

여러 입력 값을 전달 하 고 해당 값을 기반으로 하는 단일 예측을 가져오는 찾으려는 경우가 있습니다. 예를 들어, Excel 워크시트, 웹 응용 프로그램 또는 Reporting Services 보고서를 저장된 프로시저를 호출 하 여 형식화 되거나 이러한 응용 프로그램에서 사용자가 선택한 입력을 제공 하 고 설정할 수 있습니다.

이 섹션에서는 승객 수, 여정 거리 등의 여러 개의 입력을 사용 하는 저장된 프로시저를 사용 하 여 단일 예측을 만드는 방법을 알아봅니다. 저장된 프로시저는 이전에 저장 된 R 모델을 기반으로 점수를 만듭니다.
  
외부 응용 프로그램에서 저장 프로시저를 호출하는 경우 데이터가 R 모델의 요구 사항과 일치하는지 확인합니다. 여기에는 입력 데이터를 R 데이터 형식으로 캐스팅 또는 변환할 수 있는지 확인, 데이터 형식 및 데이터 길이의 유효성 검사 등이 포함될 수 있습니다. 

1. 저장된 프로시저를 만듭니다 **RxPredictSingleRow**합니다.
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```

2. 수동으로 값을 제공하여 시험해 보세요.
  
    새 **쿼리** 창을 열고 저장 프로시저를 호출하여 각 매개변수의 값을 제공합니다.  매개변수는 모델에서 사용하는 특성 열을 나타내며 필수 항목입니다.

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    또는 [저장 프로시저 매개변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters)에서 지원되는 짧은 형식을 사용하십시오.
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 결과 임을 팁을 받을 확률이 낮은 (영) 이러한 상위 10 개의 여정에서 비교적 짧은 거리에 따라 단일 승객 여정 모두 때문입니다.

## <a name="conclusions"></a>결론

이것으로 자습서를 마칩니다. 이것으로 자습서를 마칩니다. 저장 프로시저에 R 코드를 포함하는 방법을 배웠으므로 이러한 연습을 확장하여 자신의 모델을 빌드할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 과의 통합으로 예측을 위해 R 모델을 배포하고 엔터프라이즈 데이터 워크플로의 일부로 모델 재교육을 통합하는 것이 훨씬 쉬워졌습니다.

## <a name="previous-lesson"></a>이전 단원

[3단원: 학습 및 T-SQL을 사용 하 여 R 모델을 저장 합니다.](sqldev-train-and-save-a-model-using-t-sql.md)
