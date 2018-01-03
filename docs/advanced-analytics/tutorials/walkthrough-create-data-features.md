---
title: "R 및 SQL (연습)를 사용 하 여 데이터 기능 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/23/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 748d9c8c03fc9633b701d30b0b5faba1e7bab5fb
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>R 및 SQL (연습)를 사용 하 여 데이터 기능 만들기

데이터 엔지니어링은 Machine Learning의 중요한 부분입니다. 데이터는 종종 예측 모델링에 사용 하려면 먼저 변환을 필요 합니다. 데이터에 필요한 기능이 없는 경우 기존 값에서 구성할 수 있습니다.

이 모델링 작업의 경우 승하차 위치의 원시 위도 및 경도 값을 사용하는 대신 두 위치 사이의 거리(마일)를 사용하는 것이 좋습니다. 이 기능을 만들려면 사용 하 여 두 점 사이의 선형 직접 거리를 계산에서 [haversine 수식](https://en.wikipedia.org/wiki/Haversine_formula)합니다.

이 단계에서는 데이터에서 기능을 만들기 위한 두 가지 방법을 비교 합니다.

- 사용자 지정 R 함수를 사용 하 여
- 사용자 지정 T-SQL 함수를 사용 하 여[!INCLUDE[tsql](../../includes/tsql-md.md)]

목표는 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원래 열 및 새 숫자 기능을 포함 하는 데이터 집합이 *direct_distance*합니다.

## <a name="featurization-using-r"></a>R을 사용 하 여 기능 생성

R 언어는 풍부하고 다양한 통계 라이브러리로 잘 알려져 있지만 여전히 사용자 지정 데이터 변환을 만들어야 할 수 있습니다.

첫째, 하자 R 방식으로 사용자에 게 익숙한: 랩톱에 데이터를 가져오고 사용자 지정 R 함수를 실행 한 다음 *ComputeDist*, 선형 위도 및 경도 값으로 지정 된 두 점 사이의 거리를 계산 하 합니다.

1. 앞에서 만든 데이터 원본 개체는 상위 1000 행만을 가져옴을 기억 합니다. 모든 데이터를 가져오는 쿼리를 정의 하겠습니다.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 쿼리를 사용 하 여 새 SQL Server 데이터 원본을 만듭니다.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 에 인수로 제공 된 올바른 SELECT 쿼리가 구성 된 쿼리를 수행할 수는 _sqlQuery_ 으로 제공 되는 테이블 개체의 이름 또는 매개 변수는 _테이블_ 매개 변수입니다.
    
    - 테이블에서 예제 데이터를 원하는 경우 사용 해야는 _sqlQuery_ T-SQL TABLESAMPLE 절을 사용 하 여 샘플링 매개 변수를 정의 하 고 설정 하는 매개 변수는 _rowBuffering_ 인수를 FALSE입니다.

3. 사용자 지정 R 함수를 만들려면 다음 코드를 실행 합니다. ComputeDist 위도 및 경도 값의 두 쌍에서 받아서 마일에서 거리를 반환 하 사이의 선형 거리를 계산 합니다.

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

5. 호출 된 [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 하 여 데이터를 엔지니어링 기능 작동 하 고 적용는 `env$ComputeDist` 함수 메모리에 데이터를 합니다.

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
    
    다른 데이터 원본에는 인수를 사용 하 여 *varsToKeep* 및 *varsToDrop*, 있지만 SQL Server 데이터 원본에 대해 지원 되지 않습니다. 따라서이 예제에서는 사용 했습니다는 _변환_ 인수를 통과 열과 변형 된 열이 모두 지정 합니다. 또한 SQL Server에서 실행 컨텍스트, 계산 된 _inData_ 인수에는 SQL Server 데이터 원본만 사용할 수 있습니다.

    위의 코드에서 더 큰 데이터 집합에서 실행 하는 경우 경고 메시지를 만들어 수도 있습니다. 행 수가 수 제한 시간이 설정 된 값 (기본값인 3000000)를 초과 만들어지는 열, rxDataStep 경고를 반환 및 반환 된 데이터 프레임의 행 수가 줄어듭니다. 경고를 제거 하려면 수정할 수 있습니다는 _maxRowsByCols_ rxDataStep 함수의 인수입니다. 그러나 경우 _maxRowsByCols_ 너무 커서 메모리에 데이터 프레임을 로드 하는 경우 문제가 발생할 수 있습니다.

7. 호출할 수 있습니다 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) 변환 된 데이터 원본의 스키마를 검사 합니다.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Transact-SQL을 사용하여 기능 개발

이제는 사용자 지정 SQL 함수를 만들 *ComputeDist*, 사용자 지정 R 함수로 동일한 작업을 수행 합니다.

1. 새로운 사용자 지정 SQL 함수 *fnCalculateDistance*를 정의합니다. 이 사용자 정의 SQL 함수에 대한 코드는 데이터베이스를 만들고 구성하기 위해 실행한 PowerShell 스크립트의 일부로 제공됩니다.  함수가 데이터베이스에 이미 있어야 합니다.

    존재하지 않는 경우 SQL Server Management Studio를 사용하여 택시 데이터가 저장된 동일한 데이터베이스에 함수를 생성합니다.

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

2. 함수의 작동 방식을 보려면 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 지원하는 모든 응용 프로그램에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. 이 함수를 정의 것을 SQL을 사용 하 여 원하는 기능을 작성 및 다음 새 테이블에 직접 값을 삽입 합니다.

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 그러나 R 코드에서 사용자 지정 SQL 함수를 호출 하는 방법을 살펴보겠습니다. 먼저 SQL 기능 생성 쿼리는 R 변수에 저장 합니다.

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
  
5. 다음 코드 줄을 사용하여 R 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 호출하고 *featureEngineeringQuery*에서 정의된 데이터에 적용합니다.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  이제 새로운 기능을 만들었으므로 호출 **rxGetVarsInfo** 기능 테이블에서 데이터의 요약을 만들려고 합니다.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *Results*

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
    > FnCalculateDistance 개체에 대 한 스키마를 확인 합니다. 데이터베이스 소유자가 개체를 만든 로그인 역할 db_datareader에 속하는 경우 로그인 스크립트를 실행 하는 명시적 사용 권한을 부여 해야 합니다.

## <a name="comparing-r-functions-and-sql-functions"></a>R 함수와 SQL 함수 비교

R 코드의 시간을 하는 데 사용 되는 코드의이 부분을 기억?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

SQL 사용자 정의 함수 예제를 사용 하 여 데이터 변환의 소요 시간 SQL 함수를 호출할 때 볼 수는이 시도할 수 있습니다. 또한 rxSetComputeContext 계산 컨텍스트를 전환 하 고 타이밍 비교.

약속 있음에는 네트워크 속도 및 하드웨어 구성에 따라 크게 달라질 수 있습니다. 테스트 구성에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 접근 방식은 사용자 지정 R 함수를 사용 하 여 보다 빠르게 이었습니다. 따라서 사용 하 여 이유임는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이후 단계에서 이러한 계산에 대 한 함수입니다.

> [!TIP]
> 자주 사용 하 여 엔지니어링 기능 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오른쪽 보다 빠를 수 있습니다 T-SQL 빠른 windowing 및 이동 평균을 롤링 같은 일반적인 데이터 과학 계산에 적용할 수 있는 순위 함수를 포함 하는 예를 들어 및  *n* -타일입니다. 해당 데이터와 태스크에 따라 가장 효율적인 방법을 선택합니다.

## <a name="next-lesson"></a>다음 단원

[R 모델을 작성 하 고 SQL에 저장](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[보기 및 R을 사용 하 여 데이터를 요약 합니다.](walkthrough-view-and-summarize-data-using-r.md)

