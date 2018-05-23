---
title: 6 단원 R 모델을 운용 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1503467f1979e2e123f12227cc92ea975b6cd6a3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-6-operationalize-the-r-model"></a>6단원: R 모델 운용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용하는 방법에 대한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 저장 프로시저를 사용하여 모델을 *운용*하는 방법을 학습합니다. 이 저장 프로시저는 다른 응용 프로그램에서 직접 호출하여 새 관측에 대해 예측할 수 있습니다. 이 연습에서는 저장 프로시저에서 R 모델을 사용하여 채점하는 두 가지 방법을 보여줍니다.

- **일괄 처리 점수 매기기 모드**: 저장 프로시저에 대한 입력으로 SELECT 조회를 사용하십시오. 저장 프로시저는 입력된 사례(case)에 해당하는 관측 표를 반환합니다.

- **개별 점수 매기기 모드**: 개별 매개변수 값 집합을 입력으로 전달합니다. 저장 프로시저에서 단일 행 또는 값을 반환합니다.

먼저 점수 매기기의 일반적인 작동 방식을 살펴보겠습니다.

## <a name="basic-scoring"></a>기본 점수 매기기

_PredictTip_ 저장 프로시저는 예측 호출을 저장 프로시저에 래핑하는 기본 구문을 보여 줍니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max) 
AS 
BEGIN 
  
DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  
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
+ 새로운 점수매기기 사례는 저장 프로시저의 첫 번째 매개변수인 `@inquery`에 지정된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 가져옵니다. 쿼리에서 읽은 데이터는 기본 데이터 프레임인 `InputDataSet`에 저장됩니다. 이 데이터 프레임은 점수를 생성하는 R의 `rxPredict` 함수에 전달됩니다.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    data.frame에 단일 행이 포함될 수 있으므로 일괄 처리 또는 단일 점수 매기기에 동일한 코드를 사용할 수 있습니다.
  
+ `rxPredict` 함수에 의해 번환되는 값은 운전자가 임의의 팁을 얻을 확률을 나타내는 **float**입니다.

## <a name="batch-scoring"></a>일괄 처리 채점

이제 일괄 처리 점수 매기기의 작동 방식을 살펴보겠습니다.

1. 먼저 사용할 작은 입력 데이터 집합을 가져오겠습니다. 이 쿼리는 승객 수 및 예측을 수행하는 데 필요한 다른 특성과 함께 "상위 10개"의 여정 목록을 만듭니다.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **예제 결과**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    이 쿼리는 다운로드의 일부로 제공되는 _PredictTipBatchMode_ 저장 프로시저에 대한 입력으로 사용할 수 있습니다.

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 _PredictTipBatchMode_ 저장 프로시저의 코드를 검토합니다.

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
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

3. 변수에 쿼리 텍스트를 입력하고 저장 프로시저에 매개변수로 전달합니다.

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. 저장 프로시저는 상위 10개 여정 각각에 대한 예측을 나타내는 일련의 값을 반환합니다. 그러나, 상위 여정은 운전자가 팁을 얻지 못할 수도 있는 비교적 여행 거리가 짧은 단일 승객 여행이기도 합니다.
  

> [!TIP]
> 
> "yes-tip" 및 "no-tip" 결과만 반환하는 대신 예측에 대한 확률 점수를 반환하고 _Score_ 열 값에 WHERE 절을 적용하여 점수를 0.5 또는 0.7과 같은 임계 값을 사용한 "팁을 줄 가능성이 높음" 또는 "주지 않을 가능성이 있음"으로 분류 할 수 있습니다. 이 단계는 저장 프로시저에 포함되지 않지만 쉽게 구현할 수 있습니다.

## <a name="single-row-scoring"></a>단일 행의 점수 매기기

때로는 응용 프로그램에서 개별 값을 전달하고 해당 값을 기반으로 단일 결과를 얻고 싶을 수도 있습니다. 예를 들어 저장 프로시저를 호출하고 사용자가 입력하거나 선택한 입력을 제공하도록 Excel 워크 시트, 웹 응용 프로그램 또는 Reporting Services 보고서를 설정할 수 있습니다.

이 섹션에서는 저장 프로시저를 사용하여 단일 예측을 만드는 방법을 설명합니다.

1. 다운로드의 일부로 포함된 _PredictTipSingleMode_ 저장 프로시저의 코드를 검토합니다.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
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
  
    - 이 저장 프로시저는 승객 수, 여정 거리 등의 여러 단일 값을 입력으로 사용합니다.
  
        외부 응용 프로그램에서 저장 프로시저를 호출하는 경우 데이터가 R 모델의 요구 사항과 일치하는지 확인합니다. 여기에는 입력 데이터를 R 데이터 형식으로 변환 또는 변환 데이터 유형 및 데이터 길이의 유효성을 검증할 수 있는지 여부가 포함됩니다. 
  
    -   저장 프로시저는 저장된 R 모델을 기반으로 하여 점수를 만듭니다.
  
2. 수동으로 값을 제공하여 시험해 보세요.
  
    새 **쿼리** 창을 열고 저장 프로시저를 호출하여 각 매개변수의 값을 제공합니다. 매개변수는 모델에서 사용하는 특성 열을 나타내며 필수 항목입니다.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = 73.977303
    ```

    또는 [저장 프로시저 매개변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters)에서 지원되는 짧은 형식을 사용하십시오.
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 결과는 상위 10번의 여정에서 팁을 얻을 확률이 낮다는 것을 의미합니다. 왜냐하면 모두가 비교적 거리가 짧은 단일 승객의 여정이기 때문입니다.

## <a name="conclusions"></a>결론

이것으로 자습서를 마칩니다. 저장 프로시저에 R 코드를 포함하는 방법을 배웠으므로 이러한 연습을 확장하여 자신의 모델을 빌드할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]과의 통합으로 예측을 위해 R 모델을 배포하고 엔터프라이즈 데이터 워크플로의 일부로 모델 재교육을 통합하는 것이 훨씬 쉬워졌습니다.

## <a name="previous-lesson"></a>이전 단원

[5단원: T-SQL을 사용한 R 모델 학습 및 저장](../r/sqldev-train-and-save-a-model-using-t-sql.md)
