---
title: "3단원: 데이터 기능 만들기(데이터 과학 종단 간 연습) | Microsoft Docs"
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 3단원: 데이터 기능 만들기(데이터 과학 종단 간 연습)
데이터 엔지니어링은 Machine Learning의 또 다른 중요한 부분입니다. 데이터를 예측 모델링에 사용하기 전에 변환해야 하는 경우가 많습니다. 데이터에 필요한 기능이 없는 경우 기존 값에서 구성할 수 있습니다.  
  
이 모델링 작업의 경우 승하차 위치의 원시 위도 및 경도 값을 사용하는 대신 두 위치 사이의 거리(마일)를 사용하는 것이 좋습니다. 이 기능을 만들려면 [haversine 수식](https://en.wikipedia.org/wiki/Haversine_formula)을 사용하여 두 점 사이의 직접 선형 거리를 계산합니다.  
데이터에서 기능을 만들기 위한 두 가지 방법을 비교합니다.  
  
-   R 및 `rxDataStep` 함수 사용    
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 지정 함수 사용  
  
두 방법 모두, 코드 결과는 새로운 숫자 기능 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 포함하는 `featureDataSource`데이터 원본 개체인 `direct_distance`입니다.  
  
## <a name="creating-features-using-r"></a>R을 사용하여 기능 만들기  

R 언어는 풍부하고 다양한 통계 라이브러리로 잘 알려져 있지만 여전히 사용자 지정 데이터 변환을 만들어야 할 수 있습니다. 

+ 새로운 R 함수 `ComputeDist`를 만들어 위도 및 경도 값으로 지정된 두 점 사이의 선형 거리를 계산합니다.  
+ 함수를 호출하여 앞에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 데이터를 변환하고 새 데이터 원본인 `featureDataSource`에 저장합니다.  

### <a name="create-the-transformation-function"></a>변환 함수 만들기  
1.  사용자 지정 R 보고서 `ComputeDist`를 만듭니다. 이 보고서는 두 쌍의 위도 및 경도 값을 사용하여 그 사이의 선형 거리를 계산합니다.  함수에서 거리(마일)를 반환합니다.
  
    ```R  
    env <- new.env()  
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){  
      R <- 6371/1.609344 #radius in mile  
      delta_lat <- dropoff_lat - pickup_lat  
      delta_long <- dropoff_long - pickup_long  
      degrees_to_radians = pi/180.0  
      a1 <- sin(delta_lat/2*degrees_to_radians)  
      a2 <- as.numeric(a1)^2  
      a3 <- cos(pickup_lat*degrees_to_radians)  
      a4 <- cos(dropoff_lat*degrees_to_radians)  
      a5 <- sin(delta_long/2*degrees_to_radians)  
      a6 <- as.numeric(a5)^2  
      a <- a2+a3*a4*a6  
      c <- 2*atan2(sqrt(a),sqrt(1-a))  
      d <- R*c  
      return (d)  
    }  
    ```  
  
    + 첫 번째 줄에서는 새 환경을 정의합니다. R에서는 환경을 사용하여 네임스페이스를 패키지 등에 캡슐화할 수 있습니다.
    + `search()` 함수를 사용하여 작업 영역의 환경을 볼 수 있습니다. 특정 환경의 개체를 보려면 `ls(<envname>)`를 입력합니다. 
    + `$env.ComputeDistance` 로 시작하는 줄에는 구의 두 점 간 *대권 거리* 를 계산하는 haversine 수식을 정의하는 코드가 포함되어 있습니다.  
 
  
### <a name="apply-the-transformation-function-to-data"></a>데이터에 변환 함수 적용

함수를 정의했으면 데이터에 적용하여 새 기능 열 *direct_distance*를 만듭니다.

1. `RxSqlServerData` 생성자를 사용하여 작업할 데이터 원본을 만듭니다.  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  `rxDataStep` 함수를 호출하여 `env$ComputeDist` 함수를 지정된 데이터에 적용합니다.  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + `rxDataStep` 함수는 제자리에서 데이터를 수정할 수 있습니다. 인수에는 통과할 열의 문자 벡터(*varsToKeep*) 및 변환을 정의하는 목록이 포함됩니다.
    + 변환된 모든 열은 자동으로 출력되므로 *varsToKeep* 인수에 포함할 필요가 없습니다.
    + 또는 *varsToDrop* 인수를 사용하여 지정된 변수를 제외하고 원본의 모든 열이 포함되도록 지정할 수 있습니다.  
  
4.  마지막으로 `rxGetVarInfo`를 호출하여 새 데이터 원본의 스키마를 검사합니다.  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *Results*
    
    *"It takes CPU Time=0.74 seconds, Elapsed Time=35.75 seconds to generate features."*  
    *Var 1: tipped, Type: integer*   
    *Var 2: fare_amount, Type: numeric*   
    *Var 3: passenger_count, Type: numeric*   
    *Var 4: trip_time_in_secs, Type: numeric*   
    *Var 5: trip_distance, Type: numeric*   
    *Var 6: pickup_datetime, Type: character*   
    *Var 7: dropoff_datetime, Type: character*   
    *Var 8: pickup_longitude, Type: numeric*   
    *Var 9: pickup_latitude, Type: numeric*   
    *Var 10: dropoff_longitude, Type: numeric*   
    *Var 11: dropoff_latitude, Type: numeric*   
    *Var 12: direct_distance, Type: numeric*   
  
## <a name="creating-features-using-transact-sql"></a>Transact-SQL을 사용하여 기능 만들기  
이제 R 함수를 사용하여 기능을 만드는 방법을 살펴봤으므로 사용자 지정 SQL 함수 `ComputeDist`를 사용하여 동일한 작업을 수행하겠습니다. SQL 함수 `ComputeDist` 는 기존 `RxSqlServerData` 데이터 개체에 대해 작동하여 기존 위도 및 경도 값에서 새 거리 기능을 만듭니다.  
  
R을 사용할 때와 마찬가지로, 변환 결과는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 개체인 `featureDataSource`에 저장합니다.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용한 기능 엔지니어링은 R보다 빠른 경우가 많습니다. 해당 데이터와 작업에 따라 가장 효율적인 방법을 선택합니다.  

### <a name="define-the-t-sql-custom-function"></a>T-SQL 사용자 지정 함수 정의
  
1.  새 SQL 함수 `fnCalculateDistance`를 정의합니다.  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END  
  
    ```  

    + 이 SQL *사용자 정의 함수* 에 대한 코드는 데이터베이스를 만들고 구성하기 위해 실행한 PowerShell 스크립트의 일부로 제공되었습니다.  함수가 데이터베이스에 이미 있어야 합니다.  존재하지 않는 경우 SQL Server Management Studio를 사용하여 택시 데이터가 저장된 동일한 데이터베이스에 함수를 생성합니다.

2.  함수의 작동 방식을 보려면 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 지원하는 모든 응용 프로그램에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>R에서 SQL 함수 호출

1. R 변수에서 사용자 지정 함수를 호출하는 SQL 문을 저장합니다.  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] 이 쿼리는 앞에서 사용한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리와 약간 다릅니다. 이 연습을 더 빨리 진행하기 위해 더 작은 데이터 샘플을 가져오도록 수정되었습니다.  
  
4.  이제 다음 코드 줄을 사용하여 R 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 호출하고 `featureEngineeringQuery`에서 정의된 데이터에 적용합니다.  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  새 기능을 만들었으므로 이제 `rxGetVarsInfo`를 호출하여 기능 테이블 요약을 만듭니다.  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>R 함수와 SQL 함수 비교

결과적으로, 이 특정 작업의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 방법이 사용자 지정 R 함수보다 더 빠릅니다. 따라서 이후 단계에서 이러한 계산에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용합니다.  

이 데이터를 사용하여 예측 모델을 작성하고 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장하는 방법을 알아보려면 다음 단원을 진행하세요.  
  
## <a name="next-lesson"></a>다음 단원  
[4단원: 모델 작성 및 저장&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>이전 단원  
[2단원: 데이터 보기 및 탐색&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
