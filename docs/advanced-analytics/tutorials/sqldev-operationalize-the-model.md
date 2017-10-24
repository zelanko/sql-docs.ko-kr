---
title: "6 단원: R 모델을 운용 | Microsoft Docs"
ms.custom: 
ms.date: 08/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0fbdebc582650b0bd524d583d936848ae42e5f6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-operationalize-the-r-model"></a>6 단원: R 모델을 운용

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 방법을 배웁니다 *운영 화* 저장된 프로시저를 사용 하 여 모델입니다. 이 저장 프로시저를 다른 응용 프로그램에서 직접 호출하여 새 관찰을 예측할 수 있습니다. 이 연습에서는 저장된 프로시저에서 R 모델을 사용 하 여 점수 매기기를 수행 하는 두 가지를 보여 줍니다.

- **일괄 처리 점수 매기기 모드**: SELECT 쿼리 저장된 프로시저에 대 한 입력으로 사용 합니다. 저장 프로시저에서 입력 사례에 해당하는 관찰 테이블을 반환합니다.

- **개별 점수 매기기 모드**: 개별 매개 변수 값 집합을 입력으로 전달합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

먼저 점수 매기기의 일반적인 작동 방식을 살펴보겠습니다.

## <a name="basic-scoring"></a>기본 점수 매기기

저장 프로시저 _PredictTip_ 은 예측 호출을 저장 프로시저에 래핑하는 기본 구문을 보여 줍니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
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

- SELECT 문은 데이터베이스에서 직렬화된 모델을 가져와서 R을 사용한 추가 처리를 위해 R 변수 `mod` 에 모델을 저장합니다.

- 점수 매기기에 대 한 새 사례에서 가져온는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 지정 된 쿼리 `@inquery`, 저장된 프로시저에 대 한 첫 번째 매개 변수입니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다. 이 데이터 프레임은 점수를 생성하는 R의 `rxPredict` 함수에 전달됩니다.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    data.frame에 단일 행이 포함될 수 있으므로 일괄 처리 또는 단일 점수 매기기에 동일한 코드를 사용할 수 있습니다.
  
-   반환한 값은 `rxPredict` 함수는는 **float** 드라이버 시간 관계의 끝을 가져옴을 확률을 나타내는입니다.

## <a name="batch-scoring"></a>일괄 처리 점수 매기기

이제 일괄 처리 점수 매기기의 작동 방식을 살펴보겠습니다.

1.  먼저 사용할 작은 입력 데이터 집합을 가져오겠습니다. 이 쿼리는 승객 수 및 예측을 수행하는 데 필요한 다른 기능과 함께 "상위 10개"의 여정 목록을 만듭니다.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count,
        a.trip_time_in_secs AS trip_time_in_secs, 
        a.trip_distance AS trip_distance, 
        a.dropoff_datetime AS dropoff_datetime, 
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    FROM
    (
        SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
         dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a
    LEFT OUTERJOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b
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

    이 쿼리는 저장된 프로시저에 대 한 입력으로 사용할 수 _PredictTipBatchMode_다운로드의 일부로 제공 합니다.

2. 저장된 프로시저의 코드를 검토 하는 데 1 분 소요 _PredictTipBatchMode_ 에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model
      FROM nyc_taxi_models);
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
    ```

3.  변수에 쿼리 텍스트를 입력 하 고 저장된 프로시저에 매개 변수로 전달 합니다.

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='
    select top 10 a.passenger_count as passenger_count,
        a.trip_time_in_secs as trip_time_in_secs,
        a.trip_distance as trip_distance,
        a.dropoff_datetime as dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance
    from
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
        from nyctaxi_sample
    )a  
    LEFT OUTER JOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample  
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b 
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. 저장된 프로시저는 일련의 10 가지와 각각에 대 한 예측을 나타내는 값을 반환 합니다. 그러나 상위 trips 드라이버가 팁은 발생할 가능성이 있지 않으면는 비교적 짧은 여행 거리 하 여 단일 승객 trips 됩니다.
  

> [!TIP]
> 
> 단순히 팁 있음/팁 없음 결과를 반환하는 대신 예측의 확률 점수를 반환한 다음 _Score_ 열 값에 WHERE 절을 적용하여 0.5 또는 0.7과 같은 임계값을 사용해서 "팁 가능성 높음" 또는 "팁 가능성 낮음"으로 점수를 분류할 수도 있습니다. 이 단계는 저장 프로시저에 포함되어 있지 않지만 쉽게 구현할 수 있습니다.

## <a name="single-row-scoring"></a>단일 행의 점수 매기기

응용 프로그램의 개별 값을 전달하고 해당 값을 기반으로 하여 단일 결과를 가져오려는 경우도 있습니다. 예를 들어 저장 프로시저를 호출하고 사용자가 입력 또는 선택한 입력을 제공하도록 Excel 워크시트, 웹 응용 프로그램 또는 Reporting Services 보고서를 설정할 수 있습니다.

이 섹션에서는 저장된 프로시저를 사용 하 여 단일 예측을 만드는 방법을 배웁니다.

1. 다운로드의 일부로 포함된 저장 프로시저 _PredictTipSingleMode_의 코드를 검토합니다.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
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
    ```
  
    - 이 저장 프로시저는 승객 수, 여정 거리 등의 여러 단일 값을 입력으로 사용합니다.
  
        외부 응용 프로그램에서 저장 프로시저를 호출하는 경우 데이터가 R 모델의 요구 사항과 일치하는지 확인합니다. 여기에는 입력 데이터를 R 데이터 형식으로 캐스팅 또는 변환할 수 있는지 확인, 데이터 형식 및 데이터 길이의 유효성 검사 등이 포함될 수 있습니다. 자세한 내용은 [R 데이터 형식 사용](https://msdn.microsoft.com/library/mt590948.aspx)을 참조하세요.
  
    -   저장 프로시저는 저장된 R 모델을 기반으로 하여 점수를 만듭니다.
  
2. 수동으로 값을 제공하여 실험해 보세요.
  
    새 **쿼리** 창과 각 매개 변수에 값을 제공 하는 저장된 프로시저를 호출 합니다. 매개 변수는 모델에 사용 되는 기능 열을 나타내고 필요.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance float = 2.5,
    @trip_time_in_secs int = 631,
    @pickup_latitude float = 40.763958,
    @pickup_longitude float = -73.973373,
    @dropoff_latitude float =  40.782139,
    @dropoff_longitude float = 73.977303
    ```

    에 대 한 지원 짧은이 양식을 사용 하 여 또는 [매개 변수는 저장된 프로시저를](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 결과 모두에 단일 승객 trips 비교적 짧은 거리에 따라 이후 팁 가져오기의 확률 이러한 상위 10 개의 trips에서 매우 느리게 임을 나타냅니다.

## <a name="conclusions"></a>결론

이것으로 자습서를 마칩니다. 저장된 프로시저에 R 코드를 포함 하는 방법을 배웠습니다, 했으므로 자신만의 모델을 작성 하는 이러한 사례를 확장할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 과 통합되어 보다 쉽게 예측에 대한 R 모델을 배포하고 모델 다시 학습을 엔터프라이즈 데이터 워크플로의 일부로 통합할 수 있습니다.

## <a name="previous-lesson"></a>이전 단원

[5 단원: 학습 및 T-SQL을 사용 하 여 R 모델을 저장 합니다.](../r/sqldev-train-and-save-a-model-using-t-sql.md)

