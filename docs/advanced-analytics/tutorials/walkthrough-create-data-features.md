---
title: R 및 SQL Server 함수-SQL Server Machine Learning을 사용 하 여 데이터 기능 만들기
description: 데이터베이스 내 분석에 대 한 SQL Server 함수를 사용 하 여 데이터 기능을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 527f88ed14adc0140cbca179177e85670f72cafd
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890014"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>R 및 SQL Server (연습)를 사용 하 여 데이터 기능 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 엔지니어링은 기계 학습(Machine Learning)의 중요한 부분입니다. 데이터는 가끔 예측 모델링에 사용하기 위해 사전 변환이 필요하기도 합니다. 기존 데이터에서 필요한 특성이 없는 경우 기존 값에서 가공해낼 수도 있습니다.

이번 모델링 작업에서는 승차와 하차 위치에 대한 위도와 경도 값을 사용하는 대신 두 위치 간의 거리(마일)를 사용하는 것이 더 좋을 수 있습니다. 이 특성을 만들려면 [haversine 수식](https://en.wikipedia.org/wiki/Haversine_formula)을 사용하여 두 점 간의 직선 거리를 계산합니다.

이 단계에서는 데이터에서 기능을 만들기 위한 두 가지 방법을 알아봅니다.

> [!div class="checklist"]
> * 사용자 지정 R 함수 사용하기
> * 사용자 지정 T-SQL 함수를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)]

목표는 원본 열과 더불어 새로운 numeric 특성인  *direct_distance*를 포함하는 새로운[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 집합을 만드는 것입니다. 

## <a name="prerequisites"></a>사전 요구 사항

이 단계에서는이 연습의 이전 단계에 따라 진행 중인 R 세션을 가정 합니다. 이러한 단계에서 만든 연결 문자열 및 데이터 원본 개체를 사용 합니다. 스크립트를 실행 하려면 다음 도구 및 패키지 사용 됩니다.

+ Rgui.exe R 명령을 실행 하려면
+ T-SQL을 실행 하기 위해 management Studio

## <a name="featurization-using-r"></a>R을 사용한 새 특성 추가(Featurization)

R 언어는 풍부하고 다양한 통계 라이브러리로 잘 알려져 있지만 여전히 사용자 정의 데이터 변환을 만들어야 할 수도 있습니다.

우선, R 사용자가 익숙한 방식으로 해 봅니다. 데이터를 랩톱에 가져온 다음 위도와 경도 값으로 지정된 두 점 간의 직선 거리를 계산하는 사용자 지정 R 함수 *ComputeDist*를 실행합니다.

1. 이전에 만든 데이터 원본 개체는 상위 1000개 행만 가져옵니다. 그래서 모든 데이터를 가져오는 쿼리를 정의해 보겠습니다. 

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 쿼리를 사용 하 여 새 데이터 원본 개체를 만듭니다.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 는 _sqlQuery_ 매개변수의 인수로 제공되는 유효한 SELECT 쿼리 혹은 _table_ 매개변수로 제공되는 테이블 개체 이름으로 구성할 수 있습니다. 
    
    - 테이블에서 데이터를 샘플링하고 싶은 경우 _sqlQuery_ T-SQL TABLESAMPLE 절을 사용해서 샘플 매개변수를 정의하며,   _rowBuffering_ 인수를 FALSE로 설정해야 합니다. 

3. 다음 코드를 실행해서 사용자 지정 R 함수를 만듭니다. ComputeDist는 두 쌍의 위도와 경도 값을 받아서 직선 거리를 계산하고 마일 단위 거리를 반환합니다.

    ```R
    env <- new.env();
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
  
    + 첫 번째 줄은 새 환경을 정의합니다.  R에서는 패키지와 같은 이름 공간을 캡슐화하는 데 환경을 사용할 수 있습니다. `search()` 함수를 사용하여 작업 영역의 환경을 볼 수 있습니다.  특정 환경의 개체를 보려면 `ls(<envname>)`를 입력합니다. 
    + `$env.ComputeDist` 로 시작하는 줄에는 haversine 공식을 정의하는 코드가 포함되어 있으며, 구(sphere)의 두 점간 *거리*를 계산합니다.

4. 함수를 정의한 후 새로운 특성 열인 *direct_distance*를 생성하기 위해 함수를 데이터에 적용합니다. 변환을 실행하기 전에 계산 컨텍스트를 로컬로 변경합니다. 

    ```R
    rxSetComputeContext("local");
    ```

5. [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 함수를 호출하여 특성 엔지니어링 데이터를 가져오고 `env$ComputeDist` 함수를 메모리의 데이터에 적용합니다.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + RxDataStep 함수는 데이터를 현재 위치에서 수정하는 다양한 방법을 지원합니다. 자세한 내용은이 문서를 참조 하세요.  [Microsft R에서 데이터를 변환 및 일부 하는 방법](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    그러나 rxDataStep과 관련된 몇 가지 주목할만한 포인트가 있습니다. 
    
    다른 데이터 원본에서는 *varsToKeep* 과 *varsToDrop*, 인수를 사용할 수 있지만 SQL Server 데이터 원본에는 지원되지 않습니다. 따라서 이 예제에서는 _transform_ 인수를 사용해서 통과(pass-through) 열과 변환 열 모두를 지정했습니다. 또한 SQL Server 계산 컨텍스트에서 실행할 때 _inData_ 인수에는 SQL Server 데이터 원본만 사용할 수 있습니다.

    이전 코드는 큰 데이터 집합에서 실행할 때 경고 메시지를 생성할 수도 있습니다. 행과 열의 수가 설정된 값(기본 3,000,000)을 초과하는 경우 rsDataStep은 경고를 반환하고 결과 데이터 프레임의 행 수가 잘립니다. 경고를 제거하려면 rxDataStep 함수의 _maxRowsByCols_ 인수를 수정할 수 있습니다. 그러나 _maxRowsByCols_ 가 너무 큰 경우 데이터 프레임을 메모리로 로드할 때 문제가 발생할 수 있습니다. 

7. 선택적으로 변환된 데이터 원본의 스키마를 검사하기 위해 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) 를 호출할 수 있습니다.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Transact-SQL을 사용한 새 특성 추가(featurzation)

이 연습에서는 사용자 지정 R 함수 대신 SQL 함수를 사용 하 여 동일한 작업을 수행 하는 방법에 알아봅니다. 

전환할 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 또는 T-SQL 스크립트를 실행 하려면 다른 쿼리 편집기.

1. 명명 된 SQL 함수를 사용 하 여 *fnCalculateDistance*합니다. 함수는 NYCTaxi_Sample 데이터베이스에 이미 존재 해야 합니다. 개체 탐색기에서이 경로 이동 하 여 함수가 존재를 확인 합니다. 데이터베이스 > NYCTaxi_Sample > 프로그래밍 기능 > 함수 > 스칼라 반환 함수 > dbo.fnCalculateDistance 합니다.

    함수가 없으면 NYCTaxi_Sample 데이터베이스에 함수를 생성 하려면 SQL Server Management Studio를 사용 합니다.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
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

2. Management studio에서 새 쿼리 창에서 다음을 실행 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지 원하는 응용 프로그램에서 문을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수의 작동 방식을 확인 합니다.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. (먼저 만들어야 있는) 새 테이블에 직접 값을 삽입할 추가할 수 있습니다는 **INTO** 절 테이블 이름을 지정 합니다.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 또한 R 코드에서 SQL 함수를 호출할 수 있습니다. Rgui로 다시 전환 하 고 R 변수에 SQL 기능화 (featurization) 쿼리를 저장 합니다.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 위 쿼리는 연습을 더 빨리하기 위해 더 적은 샘플 데이터를 얻도록 수정되었습니다. 모든 데이터를 가져오려면 TABLESAMPLE 절을 제거할 수 있습니다. 그러나 환경에 따라서는 전체 데이터를 R에 로딩할 수 없어서 오류가 발생할 수 있습니다. 
  
5. 다음 코드 줄을 사용하여 R 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 호출하고 이를 *featureEngineeringQuery*에 정의된 데이터에 적용합니다.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  이제 새 특성이 만들어졌으므로 **rxGetVarsInfo**를 호출하여 특성 테이블에 데이터 요약을 만듭니다.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **결과**

    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > 경우에 따라 다음과 같은 오류가 발생할 수 있습니다. *'FnCalculateDistance' 개체에 EXECUTE 권한이 거부 되었습니다* 그렇다면 사용 중인 로그인에 스크립트를 실행 하 고 인스턴스에서 뿐 아니라 데이터베이스에서 개체를 만들 권한이 있는지 확인 합니다.
    > FnCalculateDistance 개체에 대한 스키마를 확인합니다. 만일 개체가 데이터베이스 소유자에 의해 생성되었고, 로그인이 db_datareader 역할에 속한다면 스크립트를 실행하기 위해서 명시적으로 사용 권한을 부여해야 합니다.

## <a name="comparing-r-functions-and-sql-functions"></a>R 함수와 SQL 함수 비교

R 코드의 시간을 재는 데 사용된 코드 조각을 기억하십니까?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

이것을 SQL 사용자 지정 함수 예제와 함께 사용해서 SQL 함수 호출 시 데이터 변환 작업이 얼마나 오래 걸리는지 확인할 수 있습니다. 또한 rxSetComputeContext로 계산 컨텍스트를 전환하고 타이밍을 비교해보세요.

네트워크 속도와 하드웨어 구성 등에 따라서 시간이 크게 차이날 수 있습니다. 우리가 시험한 구성에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 방식이 사용자 지정 R 함수보다 더 빨랐음으로 이후 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용합니다.

> [!TIP]
> 자주, 사용한 기능 엔지니어링 [!INCLUDE[tsql](../../includes/tsql-md.md)] R. 보다 향상 되는 T-SQL 창 빠른 작업 및 연속 이동 평균와 같은 일반적인 데이터 과학 계산을 적용할 수 있는 순위 함수를 포함 하는 예를 들어, 및 *n*-타일입니다. 해당 데이터와 태스크에 따라 가장 효율적인 방법을 선택합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R 모델을 작성하고 SQL Server에 저장하기](walkthrough-build-and-save-the-model.md)

