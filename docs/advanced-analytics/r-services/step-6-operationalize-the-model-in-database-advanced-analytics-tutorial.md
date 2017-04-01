---
title: "6단계: 모델 운영화(데이터베이스 내 고급 분석 자습서) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 6단계: 모델 운영화(데이터베이스 내 고급 분석 자습서)
이 단계에서는 저장 프로시저를 사용하여 모델을 *운영화*하는 방법을 알아봅니다. 이 저장 프로시저를 다른 응용 프로그램에서 직접 호출하여 새 관찰을 예측할 수 있습니다.  
  
이 단계에서는 저장 프로시저에서 R 모델을 호출하는 두 가지 방법을 알아봅니다.  
  
-   **일괄 처리 점수 매기기 모드**: SELECT 쿼리를 사용하여 여러 행의 데이터를 제공합니다. 저장 프로시저에서 입력 사례에 해당하는 관찰 테이블을 반환합니다.  
  
-   **개별 점수 매기기 모드**: 개별 매개 변수 값 집합을 입력으로 전달합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.  
  
먼저 점수 매기기의 일반적인 작동 방식을 살펴보겠습니다.  
  
## 기본 점수 매기기  
저장 프로시저 _PredictTip_은 예측 호출을 저장 프로시저에 래핑하는 기본 구문을 보여 줍니다.  
  
```  
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
  
-   SELECT 문은 데이터베이스에서 직렬화된 모델을 가져와서 R을 사용한 추가 처리를 위해 R 변수 `mod`에 모델을 저장합니다.  
  
-   점수를 매길 새 사례는 저장 프로시저에 대한 첫 번째 매개 변수인 `@inquery`에 지정된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 가져옵니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다. 이 데이터 프레임은 점수를 생성하는 R의 `rxPredict` 함수에 전달됩니다.  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    data.frame에 단일 행이 포함될 수 있으므로 일괄 처리 또는 단일 점수 매기기에 동일한 코드를 사용할 수 있습니다.  
  
-   `rxPredict` 함수에서 반환되는 값은 금액에 관계없이 팁을 받을 확률을 나타내는 **float**입니다.  
  
## SELECT 쿼리를 사용하는 일괄 처리 점수 매기기  
이제 일괄 처리 점수 매기기의 작동 방식을 살펴보겠습니다.  
  
1.  먼저 사용할 작은 입력 데이터 집합을 가져오겠습니다.  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    이 쿼리는 승객 수 및 예측을 수행하는 데 필요한 다른 기능과 함께 "상위 10개"의 여정 목록을 만듭니다.  
  
 **결과**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
이 쿼리를 다운로드의 일부로 제공된 저장 프로시저 _PredictTipBatchMode_에 대한 입력으로 사용합니다.  
  
2.  먼저 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 저장 프로시저 _PredictTipBatchMode_의 코드를 검토합니다.  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
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
    ```  
  
3.  예측을 만들려면 변수에 쿼리 텍스트를 제공하고 다음과 같이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 저장 프로시저에 매개 변수로 전달합니다.  
  
    ```  
    -- Specify input query  
  
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
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  저장 프로시저에서 각 "상위 10개의 여정"에 대한 예측을 나타내는 일련의 값을 반환합니다. 다시 입력 값을 살펴보면 "상위 10개의 여정"은 모두 여정 거리가 비교적 짧은 단일 승객 여정입니다. 데이터에 따르면 이러한 여정에서 기사가 팁을 받을 가능성은 매우 낮습니다.  
  
    단순히 팁 있음/팁 없음 결과를 반환하는 대신 예측의 확률 점수를 반환한 다음 _Score_ 열 값에 WHERE 절을 적용하여 0.5 또는 0.7과 같은 임계값을 사용해서 "팁 가능성 높음" 또는 "팁 가능성 낮음"으로 점수를 분류할 수도 있습니다. 이 단계는 저장 프로시저에 포함되어 있지 않지만 쉽게 구현할 수 있습니다.  
  
## 개별 행 점수 매기기  
응용 프로그램의 개별 값을 전달하고 해당 값을 기반으로 하여 단일 결과를 가져오려는 경우도 있습니다. 예를 들어 저장 프로시저를 호출하고 사용자가 입력 또는 선택한 입력을 제공하도록 Excel 워크시트, 웹 응용 프로그램 또는 Reporting Services 보고서를 설정할 수 있습니다.  
  
이 섹션에서는 저장 프로시저를 사용하여 단일 예측을 만드는 방법을 알아봅니다.  
  
1.  다운로드의 일부로 포함된 저장 프로시저 _PredictTipSingleMode_의 코드를 검토합니다.  
  
    ```  
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
  
    -   이 저장 프로시저는 승객 수, 여정 거리 등의 여러 단일 값을 입력으로 사용합니다.  
  
        외부 응용 프로그램에서 저장 프로시저를 호출하는 경우 데이터가 R 모델의 요구 사항과 일치하는지 확인합니다. 여기에는 입력 데이터를 R 데이터 형식으로 캐스팅 또는 변환할 수 있는지 확인, 데이터 형식 및 데이터 길이의 유효성 검사 등이 포함될 수 있습니다. 자세한 내용은 [R 데이터 형식 사용](https://msdn.microsoft.com/library/mt590948.aspx)을 참조하세요.  
  
    -   저장 프로시저는 저장된 R 모델을 기반으로 하여 점수를 만듭니다.  
  
2.  수동으로 값을 제공하여 실험해 보세요.  
  
    새 **쿼리** 창을 열고 각 기능 열에 대한 매개 변수를 입력하여 저장 프로시저를 호출합니다.  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    이러한 기능 열의 값은 순서대로 다음과 같습니다.  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  결과는 모두 비교적 짧은 거리의 단일 승객 여정인 이러한 상위 10개의 여정에서 팁을 받을 확률이 매우 낮음을 나타냅니다.  
  
## 결론  
이 자습서에서는 저장 프로시저에 포함된 R 코드를 사용하는 방법을 배웠습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]과 통합되어 보다 쉽게 예측에 대한 R 모델을 배포하고 모델 다시 학습을 엔터프라이즈 데이터 워크플로의 일부로 통합할 수 있습니다.  
  
  
## 이전 단계  
[4단계: T-SQL을 사용하여 데이터 기능 만들기](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 참고 항목  
[SQL 개발자를 위한 데이터베이스 내 고급 분석&#40;자습서&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
