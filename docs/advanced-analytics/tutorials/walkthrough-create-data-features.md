---
title: 'R 자습서: 기능 엔지니어링'
description: 데이터베이스 내 분석을 위해 SQL Server 함수를 사용하여 데이터 기능을 만드는 방법을 보여주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 67d2c0bf73e24bc3f70e94cd6cf7ce94d13e5297
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73723861"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>R 및 SQL Server를 사용하여 데이터 기능 만들기(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터 엔지니어링은 Machine Learning의 중요한 부분입니다. 데이터를 예측 모델링에 사용하려면 먼저 데이터를 변환해야 하는 경우가 자주 있습니다. 데이터에 필요한 기능이 없는 경우 기존 값에서 구성할 수 있습니다.

이 모델링 작업의 경우 승하차 위치의 원시 위도 및 경도 값을 사용하는 대신 두 위치 사이의 거리(마일)를 사용하는 것이 좋습니다. 이 기능을 만들려면 [haversine 수식](https://en.wikipedia.org/wiki/Haversine_formula)을 사용하여 두 점 사이의 직선 거리를 컴퓨팅합니다.

이 단계에서는 데이터로 기능을 만드는 다음 두 가지 방법을 알아봅니다.

> [!div class="checklist"]
> * 사용자 지정 R 함수 사용
> * [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 지정 T-SQL 함수 사용

목표는 원본 열과 새로운 숫자 기능인 *direct_distance*를 포함하는 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 세트를 만드는 것입니다.

## <a name="prerequisites"></a>사전 요구 사항

이 단계는 이 연습의 이전 단계에서 진행 중인 R 세션을 전제로 합니다. 이전 단계에서 만든 연결 문자열과 데이터 원본 개체를 사용합니다. 다음 도구 및 패키지는 스크립트를 실행하는 데 사용됩니다.

+ R 명령을 실행하는 Rgui.exe
+ T-SQL을 실행하는 Management Studio

## <a name="featurization-using-r"></a>R을 사용하여 기능 개발

R 언어는 풍부하고 다양한 통계 라이브러리로 잘 알려져 있지만 여전히 사용자 지정 데이터 변환을 만들어야 할 수 있습니다.

R 사용자에게 익숙한 방식부터 해보겠습니다. 즉, 데이터를 랩톱으로 가져온 다음, 위도 및 경도 값으로 지정된 두 지점 사이의 직선 거리를 계산하는 사용자 지정 R 함수 *ComputeDist*를 실행합니다.

1. 앞에서 만든 데이터 원본 개체는 상위 1000개 행만 가져온다는 사실을 기억하세요. 모든 데이터를 가져오는 쿼리를 정의하겠습니다.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 쿼리를 사용하여 새 데이터 원본 개체를 만듭니다.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)는 _sqlQuery_ 매개 변수의 인수로 제공되는 유효한 SELECT 쿼리로 구성된 쿼리, 또는 _table_ 매개 변수로 제공된 테이블 개체의 이름을 사용할 수 있습니다.
    
    - 테이블의 데이터를 샘플링하려면 _sqlQuery_ 매개 변수를 사용하고, T-SQL TABLESAMPLE 절을 사용하여 샘플링 매개 변수를 정의하고, _rowBuffering_ 인수를 FALSE로 설정해야 합니다.

3. 다음 코드를 실행하여 사용자 지정 R 함수를 만듭니다. ComputeDist는 두 쌍의 위도 및 경도 값을 사용하여 둘 사이의 직선 거리를 계산하고, 거리를 마일 단위로 반환합니다.

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
  
    + 첫 번째 줄에서는 새 환경을 정의합니다. R에서는 환경을 사용하여 네임스페이스를 패키지 등에 캡슐화할 수 있습니다. `search()` 함수를 사용하여 작업 영역의 환경을 볼 수 있습니다. 특정 환경의 개체를 보려면 `ls(<envname>)`를 입력합니다.
    + `$env.ComputeDist` 로 시작하는 줄에는 구의 두 점 간 *대권 거리* 를 계산하는 haversine 수식을 정의하는 코드가 포함되어 있습니다.

4. 함수를 정의했으므로, 데이터에 함수를 적용하여 새 기능 열 *direct_distance*를 만듭니다. 그러나 변환을 실행하기 전에 컴퓨팅 컨텍스트를 로컬로 변경합니다.

    ```R
    rxSetComputeContext("local");
    ```

5. [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 함수를 호출하여 기능 엔지니어링 데이터를 가져오고, `env$ComputeDist` 함수를 메모리의 데이터에 적용합니다.

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

    + rxDataStep 함수는 제자리에서 데이터를 수정하는 다양한 방법을 지원합니다. 자세한 내용은 다음 문서를 참조하세요.  [Microsft R에서 데이터를 변환하고 하위 세트로 만드는 방법](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    그러나 rxDataStep와 관련하여 몇 가지 주의할 사항이 있습니다. 
    
    다른 데이터 원본에서는 *varsToKeep* 및 *varsToDrop* 인수를 사용할 수 있지만, SQL Server 데이터 원본에는 지원되지 않습니다. 따라서 이 예에서는 _transform_ 인수를 사용하여 통과 열과 변환된 열을 모두 지정했습니다. 또한 SQL Server 컴퓨팅 컨텍스트에서 실행하는 경우 _inData_ 인수는 SQL Server 데이터 원본만 사용할 수 있습니다.

    이전 코드를 더 큰 데이터 세트에서 실행하면 경고 메시지가 생성될 수도 있습니다. 행 수와 생성되는 열 수를 곱한 값이 설정된 값(기본값은 3,000,000)을 초과하면 rxDataStep은 경고를 반환하고, 반환된 데이터 프레임의 행 수는 잘립니다. 이 경고를 제거하려면 rxDataStep 함수에서 _maxRowsByCols_ 인수를 수정하면 됩니다. 그러나 _maxRowsByCols_가 너무 크면 데이터 프레임을 메모리에 로드할 때 문제가 발생할 수 있습니다.

7. 원한다면 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)를 호출하여 변환된 데이터 원본의 스키마를 검사할 수 있습니다.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Transact-SQL을 사용하여 기능 개발

이 연습에서는 사용자 지정 R 함수 대신 SQL 함수를 사용하여 동일한 작업을 수행하는 방법에 대해 알아봅니다. 

[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 또는 다른 쿼리 편집기로 전환하여 T-SQL 스크립트를 실행합니다.

1. *fnCalculateDistance*라는 SQL 함수를 사용합니다. 이 함수가 이미 NYCTaxi_Sample 데이터베이스에 있어야 합니다. 개체 탐색기에서 데이터베이스 > NYCTaxi_Sample > 프로그래밍 기능 > 함수 > 스칼라 반환 함수 > dbo.fnCalculateDistance 경로를 탐색하여 이 함수가 있는지 확인합니다.

    이 함수가 없으면 SQL Server Management Studio를 사용하여 NYCTaxi_Sample 데이터베이스에서 함수를 생성합니다.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS decimal(28, 10)
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

2. 함수의 작동 방식을 보려면 Management Studio의 새 쿼리 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 지원하는 아무 애플리케이션으로 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 새 테이블에 직접 값을 삽입하려면(먼저 테이블을 만들어야 함) 테이블 이름을 지정하는 **INTO** 절을 추가하면 됩니다.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. R 코드에서 SQL 함수를 호출할 수도 있습니다. Rgui로 돌아가서 SQL 기능화 쿼리를 R 변수에 저장합니다.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 이 연습을 더 빨리 진행하기 위해 이 쿼리는 더 작은 데이터 샘플을 가져오도록 수정되었습니다. 환경에 따라 모든 데이터를 가져오기 위해 TABLESAMPLE 절을 제거해도 됩니다. 그러나 환경에 따라 전체 데이터 세트를 R에 로드할 수 없는 경우도 있으며, 이 경우 오류가 발생합니다.
  
5. 다음 코드 줄을 사용하여 R 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 호출하고 *featureEngineeringQuery*에서 정의된 데이터에 적용합니다.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  새 기능을 만들었으므로, 이제 **rxGetVarsInfo**를 호출하여 기능 테이블에 데이터 요약을 만듭니다.
  
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
    > 경우에 따라 *'fnCalculateDistance' 개체에 대한 EXECUTE 권한이 거부되었습니다* 같은 오류가 발생할 수 있습니다. 이 경우 사용 중인 로그인에 스크립트를 실행하고 인스턴스가 아닌 데이터베이스에 개체를 만들 권한이 있는지 확인하세요.
    > fnCalculateDistance 개체의 스키마를 확인하세요. 데이터베이스 소유자가 개체를 만들었고 로그인이 db_datareader 역할에 속하는 경우 스크립트를 실행할 수 있는 권한을 로그인에 명시적으로 부여해야 합니다.

## <a name="comparing-r-functions-and-sql-functions"></a>R 함수와 SQL 함수 비교

아래 코드는 R 코드의 시간을 측정하는 데 사용되었습니다.

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

SQL 사용자 지정 함수 예제에서 이 코드를 사용하여 SQL 함수를 호출할 때 데이터 변환에 걸리는 시간을 확인할 수 있습니다. 또한 컴퓨팅 컨텍스트를 rxSetComputeContext로 바꾸고 타이밍을 비교해 볼 수 있습니다.

네트워크 속도 및 하드웨어 구성에 따라 시간이 크게 달라질 수 있습니다. 우리가 테스트한 구성에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 방법이 사용자 지정 R 함수를 사용하는 것보다 빨랐습니다. 따라서 이후 단계에서 이러한 계산에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하고 있습니다.

> [!TIP]
> [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하는 기능 엔지니어링이 R보다 빠른 경우가 매우 많습니다. 예를 들어 T-SQL에는 데이터 과학자가 연속 이동 평균 및 *n*타일과 같은 일반적인 데이터 과학 계산에 적용할 수 있는 빠른 기간 이동 및 순위 함수가 포함되어 있습니다. 해당 데이터와 태스크에 따라 가장 효율적인 방법을 선택합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R 모델을 빌드하여 SQL에 저장](walkthrough-build-and-save-the-model.md)

