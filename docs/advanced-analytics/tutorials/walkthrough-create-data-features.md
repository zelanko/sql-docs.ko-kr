---
title: "R 및 SQL (연습)를 사용 하 여 데이터 기능 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/23/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9b447f8c8faa834bea4360844308e468bf15d89c
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>R 및 SQL (연습)를 사용 하 여 데이터 기능 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 엔지니어링은 Machine Learning의 중요한 부분입니다. 데이터는 종종 예측 모델링에 사용 하려면 먼저 변환을 필요 합니다. 데이터에 필요한 기능이 없는 경우 기존 값에서 구성할 수 있습니다.

이번 모델링 작업에서는 승차와 하차 위치에 대한 위도와 경도 값을 사용하는 대신 두 위치 간의 거리(마일)를 사용하는 것이 더 좋을 수 있습니다. 이 특성을 만들려면 [haversine 수식](https://en.wikipedia.org/wiki/Haversine_formula)을 사용하여 두 점 간의 직선 거리를 계산합니다.

이 단계에서는 데이터에서 기능을 만들기 위한 두 가지 방법을 비교 합니다.

- 사용자 지정 R 함수 사용하기
- 사용자 지정 T-SQL 함수를 사용하기 [!INCLUDE[tsql](../../includes/tsql-md.md)]

목표는 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원래 열 및 새 숫자 기능을 포함 하는 데이터 집합이 *direct_distance*합니다.

## <a name="featurization-using-r"></a>R을 사용한 새 특성 추가(Featurization)

R 언어는 풍부하고 다양한 통계 라이브러리로 잘 알려져 있지만 여전히 사용자 정의 데이터 변환을 만들어야 할 수도 있습니다.

첫째, 하자 R 방식으로 사용자에 게 익숙한: 랩톱에 데이터를 가져오고 사용자 지정 R 함수를 실행 한 다음 *ComputeDist*, 선형 위도 및 경도 값으로 지정 된 두 점 사이의 거리를 계산 하 합니다.

1. 앞에서 만든 데이터 원본 개체는 상위 1000 행만을 가져옴을 기억 합니다. 모든 데이터를 가져오는 쿼리를 정의 하겠습니다.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 쿼리를 사용하여 새 SQL Server 데이터 원본을 만듭니다.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 에 인수로 제공 된 올바른 SELECT 쿼리가 구성 된 쿼리를 수행할 수는 _sqlQuery_ 으로 제공 되는 테이블 개체의 이름 또는 매개 변수는 _테이블_ 매개 변수입니다.
    
    - 테이블에서 예제 데이터를 원하는 경우 사용 해야는 _sqlQuery_ T-SQL TABLESAMPLE 절을 사용 하 여 샘플링 매개 변수를 정의 하 고 설정 하는 매개 변수는 _rowBuffering_ 인수를 FALSE입니다.

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
  
    + 첫 번째 줄에서는 새 환경을 정의합니다. R에서는 환경을 사용하여 네임스페이스를 패키지 등에 캡슐화할 수 있습니다.  `search()` 함수를 사용하여 작업 영역의 환경을 볼 수 있습니다. 특정 환경의 개체를 보려면 `ls(<envname>)`를 입력합니다.
    + `$env.ComputeDistance` 로 시작하는 줄에는 구의 두 점 간 *대권 거리* 를 계산하는 haversine 수식을 정의하는 코드가 포함되어 있습니다.

4. 함수 정의 적용할 새 기능 열을 만들기 위해 데이터를 *direct_distance*합니다. 하지만 변환을 실행 하기 전에 로컬 계산 컨텍스트를 변경 합니다.

    ```R
    rxSetComputeContext("local");
    ```

5. [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 함수를 호출하여 특성 엔지니어링 데이터를 가져오고 `env$ComputeDist` 함수를 메모리의 데이터에 적용합니다.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
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

    + RxDataStep 함수는 현재 위치에서 데이터를 수정 하기 위한 다양 한 메서드를 지원 합니다. 자세한 내용은이 문서를 참조 하십시오.: [Microsft R의 데이터 변환 및 부분 집합 하는 방법](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    그러나 몇 가지 사항 rxDataStep에 관한 주목할 만한: 
    
    다른 데이터 원본에서는 *varsToKeep* 과 *varsToDrop*, 인수를 사용할 수 있지만 SQL Server 데이터 원본에는 지원되지 않습니다. 따라서 이 예제에서는 _transform_ 인수를 사용해서 통과(pass-through) 열과 변환 열 모두를 지정했습니다. 또한 SQL Server 계산 컨텍스트에서 실행할 때 _inData_ 인수에는 SQL Server 데이터 원본만 사용할 수 있습니다.

    위의 코드에서 더 큰 데이터 집합에서 실행 하는 경우 경고 메시지를 만들어 수도 있습니다. 행 수가 수 제한 시간이 설정 된 값 (기본값인 3000000)를 초과 만들어지는 열, rxDataStep 경고를 반환 및 반환 된 데이터 프레임의 행 수가 줄어듭니다. 경고를 제거 하려면 수정할 수 있습니다는 _maxRowsByCols_ rxDataStep 함수의 인수입니다. 그러나 경우 _maxRowsByCols_ 너무 커서 메모리에 데이터 프레임을 로드 하는 경우 문제가 발생할 수 있습니다.

7. 선택적으로 변환된 데이터 원본의 스키마를 검사하기 위해 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) 를 호출할 수 있습니다.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Transact-SQL을 사용한 새 특성 추가(featurzation)

이제 사용자 지정 R 함수와 동일한 작업을 수행할 SQL 함수 *ComputeDist*를 만듭니다.

1. 새로운 사용자 지정 SQL 함수 *fnCalculateDistance*를 정의합니다. 이 사용자 정의 SQL 함수에 대한 코드는 데이터베이스를 만들고 구성하기 위해 실행하는 PowerShell 스크립트의 일부로 제공됩니다.  함수는 데이터베이스에 미리 생성해야 합니다.

    존재하지 않으면 SQL Server Management Studio를 사용하여 택시 데이터가 저장된 동일한 데이터베이스에 함수를 생성합니다. (역주. 아래 코드에서 RETURNS 문의 반환 데이터 형식이 생략되어 추가로 지정했습니다).

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

2. 함수가 제대로 작동하는지 보기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 지원하는 응용 프로그램에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다. (역주. 함수 동작 검증이 목적이므로 TOP 절을 추가해서 일부 데이터만 시험하길 권장합니다).

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. 함수를 정의하고 나면 SQL을 사용해서 원하는 특성을 만들고 그 값을 새로운 테이블에 직접 입력하기가 쉬워집니다.

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 그렇지만 R 코드에서 사용자 지정 SQL 함수를 호출하는 방법을 살펴보겠습니다. 먼저 R변수에 SQL 특성 추가 쿼리를 저장합니다.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 이 연습을 더 빨리 하도록 하려면 데이터의 작은 샘플을 얻으려고이 쿼리가 수정 되었습니다. 모든 데이터를 가져오려는 경우에 TABLESAMPLE 절을 제거할 수 있습니다. 그러나 환경에 따라는 오류가 발생 하는 R을 전체 바인딩되 로드 못할 수도 있습니다.
  
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

    *결과*

    ```
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
    > 일부 경우에는 이와 같은 오류가 발생할 수 있습니다: *'fnCalculateDistance' 개체에 대해 EXECUTE 권한이 거부 되었습니다* 그렇다면 사용 하는 로그인에 스크립트를 실행 하 고 데이터베이스에 개체를 만들 수 있는 권한이 있는지 확인 뿐 아니라 인스턴스에서 합니다.
    > FnCalculateDistance 개체에 대한 스키마를 확인합니다. 만일 개체가 데이터베이스 소유자에 의해 생성되었고, 로그인이 db_datareader 역할에 속한다면 스크립트를 실행하기 위해서 명시적으로 사용 권한을 부여해야 합니다.

## <a name="comparing-r-functions-and-sql-functions"></a>R 함수와 SQL 함수 비교

R 코드의 시간을 하는 데 사용 되는 코드의이 부분을 기억?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

이것을 SQL 사용자 지정 함수 예제와 함께 사용해서 SQL 함수 호출 시 데이터 변환 작업이 얼마나 오래 걸리는지 확인할 수 있습니다. 또한 rxSetComputeContext로 계산 컨텍스트를 전환하고 타이밍을 비교해보세요.

네트워크 속도와 하드웨어 구성 등에 따라서 시간이 크게 차이날 수 있습니다. 우리가 시험한 구성에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 방식이 사용자 지정 R 함수보다 더 빨랐음으로 이후 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용합니다.

> [!TIP]
> 자주 사용 하 여 엔지니어링 기능 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오른쪽 보다 빠를 수 있습니다 T-SQL 빠른 windowing 및 이동 평균을 롤링 같은 일반적인 데이터 과학 계산에 적용할 수 있는 순위 함수를 포함 하는 예를 들어 및  *n* -타일입니다. 해당 데이터와 태스크에 따라 가장 효율적인 방법을 선택합니다.

## <a name="next-lesson"></a>다음 단원

[R 모델을 작성하고 SQL Server에 저장하기](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[보기 및 R을 사용 하 여 데이터를 요약 합니다.](walkthrough-view-and-summarize-data-using-r.md)

