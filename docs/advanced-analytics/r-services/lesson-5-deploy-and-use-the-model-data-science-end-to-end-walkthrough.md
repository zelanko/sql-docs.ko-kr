---
title: "5단원: 모델 배포 및 사용(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 5단원: 모델 배포 및 사용(데이터 과학 종단 간 연습)
이 단원에서는 지속형 모델을 저장 프로시저에 래핑하여 프로덕션 환경에서 R 모델을 사용합니다. 그러면 R 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 지원하는 모든 응용 프로그래밍 언어(예: C#, Java, Python 등)에서 저장 프로시저를 호출하여 모델을 통해 새로운 관찰을 예측할 수 있습니다.  
  
점수 매기기를 위해 모델을 호출할 수 있는 다음 두 가지 방법이 있습니다.  
  
-   **일괄 처리 점수 매기기 모드** - SELECT 쿼리의 입력에 따라 여러 예측을 만들 수 있습니다.  
  
-   **개별 점수 매기기 모드** - 개별 사례에 대한 기능 값 집합을 저장 프로시저에 전달하여 한 번에 하나씩 예측을 만들 수 있습니다. 저장 프로시저는 단일 예측이나 다른 값을 결과로 반환합니다.  
  
개별 점수 매기기 및 일괄 처리 점수 매기기 방법을 둘 다 사용하여 예측을 만드는 방법을 알아보겠습니다.  
  
## <a name="batch-scoring"></a>일괄 처리 점수 매기기  
1단원에서 PowerShell 스크립트를 처음 실행할 때 생성된 저장 프로시저를 편리하게 사용할 수 있습니다. 이 저장 프로시저는 다음을 수행합니다.  
  
-   입력 데이터 집합을 SQL 쿼리로 가져오기    
-   이전 단원에서 저장한 학습된 로지스틱 회귀 모델 호출    
-   기사가 팁을 받을 확률 예측  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>PredictTipBatchMode 저장 프로시저 사용

1. 저장 프로시저 *PredictTipBatchMode*를 정의하는 스크립트를 잠시 살펴보세요. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 모델을 조작할 수 있는 방법의 여러 측면을 보여 줍니다.  
  
    ```tsql  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]   
    @input nvarchar(max)  
    AS  
    BEGIN  
  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
         @script = N'  
           mod <- unserialize(as.raw(model));  
           print(summary(mod))  
           OutputDataSet<-rxPredict(modelObject = mod, 
               data = InputDataSet, 
               outData = NULL, 
               predVarNames = "Score", type = "response", 
               writeModelVars = FALSE, overwrite = TRUE);  
           str(OutputDataSet)  
           print(OutputDataSet)',  
      @input_data_1 = @input,  
      @params = N'@model varbinary(max)',  
      @model = @lmodel2  
      WITH RESULT SETS ((Score float));  
    END    
    ```  

    + 저장된 모델을 호출하는 SELECT 문을 확인하세요. **varbinary (max)**형식의 열을 사용하여 학습된 모든 모델을 SQL 테이블에 저장할 수 있습니다. 이 코드에서는 테이블에서 모델을 검색하고 SQL 변수 _@lmodel2_에 저장한 다음 시스템 저장 프로시저 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 *mod* 매개 변수로 전달합니다.
    + 점수 매기기에 사용되는 입력 데이터는 저장 프로시저에 문자열로 전달됩니다.  
  
        이 특정 모델에 대한 입력 데이터를 정의하려면 유효한 데이터를 반환하는 쿼리를 만듭니다. 데이터가 데이터베이스에서 검색되고 *InputDataSet*이라는 데이터 프레임에 저장됩니다. 이 데이터 프레임의 모든 행은 일괄 처리 점수 매기기에 사용됩니다.
        + *InputDataSet*은 [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저에 대한 입력 데이터의 기본 이름입니다. 필요한 경우 다른 변수 이름을 정의할 수 있습니다.
        + 점수를 생성하기 위해 저장 프로시저가 **RevoScaleR** 라이브러리에서*rxPredict* 함수를 호출합니다.
    + 저장 프로시저의 반환 값인 *Score*는 기사가 팁을 받을 예상 확률입니다.  
  
2.  필요한 경우 반환된 값에 일종의 필터를 쉽게 적용하여 반환 값을 "yes - tip" 또는 "no tip" 그룹으로 분류할 수 있습니다.  예를 들어 확률이 0.5 미만이면 팁이 없을 가능성이 큽니다.  
  
3.  일괄 처리 모드에서 저장 프로시저를 호출합니다.  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>단일 행 점수 매기기  

쿼리를 사용하여 저장된 R 모델에 입력 값을 전달하는 대신 저장 프로시저에 대한 인수로 기능을 제공할 수도 있습니다.  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>PredictTipSingleMode 저장 프로시저 사용
1.  데이터베이스에 이미 만들어진 저장 프로시저 *PredictTipSingleMode*에 대한 다음 코드를 검토해 보세요.  
  
    ```tsql  
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
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  

      EXEC sp_execute_external_script @language = N'R',  @script = N'  
            mod <- unserialize(as.raw(model));  
            print(summary(mod))  
            OutputDataSet<-rxPredict(
                     modelObject = mod, 
                     data = InputDataSet, 
                     outData = NULL,   
                     predVarNames = "Score", 
                     type = "response", 
                     writeModelVars = FALSE, 
                     overwrite = TRUE);  
            str(OutputDataSet)  
            print(OutputDataSet)  
            ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
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
    ```  
  
    이 저장 프로시저는 승객 수, 여정 거리 등의 기능 값을 입력으로 사용하고 저장된 R 모델을 통해 이러한 기능의 점수를 매긴 다음 점수를 출력합니다.  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>저장 프로시저를 호출하고 매개 변수 전달

1. SQL Server Management Studio에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**를 사용하여 저장 프로시저를 호출하고 필요한 입력을 전달합니다. .  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    여기서 전달되는 값은 각각 _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_및 _dropoff_longitude_변수에 사용됩니다.  
  
2.  R 코드에서 이 동일한 호출을 실행하려면 전체 저장된 프로시저 호출이 포함된 R 변수를 정의하면 됩니다. 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    여기서 전달되는 값은 각각 _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_및 _dropoff_longitude_변수에 사용됩니다.  
  
### <a name="generate-scores"></a>점수 생성

1. **RODBC** 패키지의 *sqlQuery* 함수를 호출하고 저장 프로시저 호출이 포함된 문자열 변수 및 연결 문자열을 전달합니다.  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    **RODBC**에 대한 자세한 내용은 [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery)를 참조하세요.  
  
## <a name="conclusion"></a>결론  
이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하고 학습된 R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하는 방법을 배웠으므로 이 데이터 집합을 기반으로 하여 몇 가지 추가 모델을 비교적 쉽게 만들 수 있습니다. 예를 들어 다음과 같은 모델을 만들어 볼 수 있습니다.  
  
-   팁 금액을 예측하는 회귀 모델    
-   팁이 많은지, 보통인지, 작은지를 예측하는 다중 클래스 분류 모델입니다.  

또한 이러한 추가 샘플 및 리소스 중 일부를 확인하는 것이 좋습니다. 
+ [데이터 과학 시나리오 및 솔루션 템플릿](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [데이터베이스 내 고급 분석](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R - 데이터 분석 살펴보기](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [추가 리소스](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>이전 단원  
[4단원: 모델 작성 및 저장&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
