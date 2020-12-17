---
title: 'R 자습서: 데이터 살펴보기'
description: SQL Server에서 데이터베이스 내 분석을 위해 R 함수를 사용하여 통계 요약을 시각화하고 생성하는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 0e746113d49c3cfa419a51826405bc993d90c51c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470044"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>R을 사용하여 SQL Server 데이터 보기 및 요약(연습)
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

이 단원에서는 **RevoScaleR** 패키지의 기능을 소개하고 다음 작업을 단계별로 안내합니다.

> [!div class="checklist"]
> * SQL Server에 연결
> * 필요한 데이터가 있는 쿼리를 정의하거나 테이블 또는 뷰를 지정합니다.
> * R 코드를 실행할 때 사용할 하나 이상의 컴퓨팅 컨텍스트 정의
> * 필요한 경우 원본에서 읽는 동안 데이터 원본에 적용되는 변환을 정의합니다.

## <a name="define-a-sql-server-compute-context"></a>SQL Server 컴퓨팅 컨텍스트 정의

클라이언트 워크스테이션의 R 환경에서 다음 R 문을 실행합니다. 이 섹션에서는 [Microsoft R Client가 있는 데이터 과학 워크스테이션](../r/set-up-a-data-science-client.md)을 사용한다고 가정합니다. 이 워크스테이션에는 모든 RevoScaleR 패키지 뿐만 아니라 기본 경량 R 도구 세트가 포함되어 있기 때문입니다. 예를 들어, Rgui.exe를 사용하여 이 섹션에서 R 스크립트를 실행할 수 있습니다.

1. **RevoScaleR** 패키지를 아직 로드하지 않은 경우 다음 R 코드 줄을 실행합니다.

    ```R
    library("RevoScaleR")
    ```

     큰따옴표는 선택 사항이지만 이 경우에는 사용하는 것이 좋습니다.
     
     오류가 발생할 경우 R 개발 환경에서 RevoScaleR 패키지가 포함된 라이브러리를 사용하고 있는지 확인합니다. `.libPaths()`와 같은 명령을 사용하여 현재 라이브러리 경로를 표시합니다.

2. SQL Server에 대한 연결 문자열을 만들고 R 변수 *connStr* 에 저장합니다.

   자리 표시자 "your_server_name"을 유효한 SQL Server 인스턴스 이름으로 변경해야 합니다. 서버 이름에는 인스턴스 이름만 사용할 수 있으며, 네트워크에 따라 이름을 정규화해야 할 수도 있습니다.
    
   SQL Server 인증의 경우 연결 구문은 다음과 같습니다.

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Windows 인증의 경우 구문은 약간 다릅니다.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    일반적으로 R 코드에 암호를 저장하지 않도록 가능한 경우 Windows 인증을 사용하는 것이 좋습니다.

3. 새 *컴퓨팅 컨텍스트* 를 만들 때 사용할 변수를 정의합니다. 컴퓨팅 컨텍스트 개체를 만든 후에는 이 개체를 사용하여 SQL Server 인스턴스에서 R 코드를 실행할 수 있습니다.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R에서는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 R 개체를 직렬화할 때 임시 디렉터리를 사용합니다. *sqlShareDir* 로 사용되는 로컬 디렉터리를 지정하거나 기본값을 적용할 수 있습니다.
  
    - *sqlWait* 를 사용하여 서버에서 R에서 결과를 대기할지 여부를 지정합니다.  대기 중인 작업 및 대기 중이 아닌 작업에 대한 자세한 내용은 [Microsoft R의 RevoScaleR을 사용한 분산 및 병렬 컴퓨팅](/r-server/r/how-to-revoscaler-distributed-computing)을 참조하세요.
  
    - *sqlConsoleOutput* 인수를 사용하여 R 콘솔의 출력을 표시하지 않도록 지정합니다.

4. [RxInSqlServer](/r-server/r-reference/revoscaler/rxinsqlserver) 구문을 호출하여 이미 정의된 변수 및 연결 문자열로 컴퓨팅 컨텍스트 개체를 만들고 새 개체를 R 변수 *sqlcc* 에 저장합니다.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 기본적으로 컴퓨팅 컨텍스트는 로컬이므로 *활성 컴퓨팅 컨텍스트* 를 명시적으로 설정해야 합니다.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)는 이전에 활성화된 컴퓨팅 컨텍스트를 사용할 수 있도록 보이지 않게 반환합니다.
    + [rxGetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)는 활성 컴퓨팅 컨텍스트를 반환합니다.
    
    컴퓨팅 컨텍스트 설정은 **RevoScaleR** 패키지의 함수를 사용하는 작업에만 영향을 줍니다. 컴퓨팅 컨텍스트는 오픈 소스 R 작업의 수행 방식에는 영향을 주지 않습니다.

## <a name="create-a-data-source-using-rxsqlserver"></a>RxSqlServer를 사용하여 데이터 원본 만들기

RevoScaleR 및 MicrosoftML과 같은 Microsoft R 라이브러리를 사용하는 경우 *데이터 원본* 은 RevoScaleR 함수를 사용하여 만든 개체입니다. 데이터 원본 개체는 모델 학습 또는 기능 추출을 비롯하여 태스크에 사용하려는 일부 데이터 세트를 지정합니다. SQL Server를 포함하는 다양한 원본에서 데이터를 가져올 수 있습니다. 현재 지원되는 원본 목록은 [RxDataSource](/r-server/r-reference/revoscaler/rxdatasource)를 참조하세요.

이전에는 연결 문자열을 정의하고 해당 정보를 R 변수에 저장했습니다. 해당 연결 정보를 다시 사용하여 가져올 데이터를 지정할 수 있습니다.

1. SQL 쿼리를 문자열 변수로 저장합니다. 이 쿼리는 모델 학습을 위한 데이터를 정의합니다.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    여기서는 TOP 절을 사용하여 작업을 더 빠르게 실행했지만 쿼리에 의해 반환되는 실제 행은 순서에 따라 달라질 수 있습니다. 따라서 요약 결과도 아래에 나열된 것과 다를 수 있습니다. TOP 절은 얼마든지 제거해도 됩니다.

2. 쿼리 정의를 인수로 [RxSqlServerData](/r-server/r-reference/revoscaler/rxsqlserverdata) 함수에 전달합니다.

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + *colClasses* 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 과 R 간에 데이터를 이동할 때 사용할 열 형식을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 R과 다른 데이터 형식 및 더 많은 데이터 형식을 사용하므로 이 인수가 중요합니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.
  
    + *rowsPerRead* 인수는 메모리 사용량 및 효율적인 계산을 관리하는 데 중요합니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 대부분의 향상된 분석 함수는 데이터를 청크로 처리하고 중간 결과를 누적하며, 모든 데이터를 읽은 후 최종 계산을 반환합니다.  *rowsPerRead* 매개 변수를 추가하면 처리를 위해 각 청크로 읽어오는 데이터 행 수를 제어할 수 있습니다.  이 매개 변수의 값이 너무 크면 큰 데이터 청크를 효율적으로 처리할 수 있는 메모리가 없기 때문에 데이터 액세스 속도가 느려질 수 있습니다.  일부 시스템에서는 *rowsPerRead* 를 과도하게 작은 값으로 설정하는 경우에도 성능이 저하될 수 있습니다.

3. 이때는 *inDataSource* 개체를 만들었지만 이 개체에는 데이터가 들어 있지 않습니다. [rxImport](/r-server/r-reference/revoscaler/rxdatastep) 또는 [rxSummary](/r-server/r-reference/revoscaler/rxsummary)와 같은 함수를 실행할 때까지 SQL 쿼리의 데이터가 로컬 환경으로 이동되지 않습니다.

    그러나 이제 데이터 개체를 정의했으므로 다른 함수의 인수로 사용할 수 있습니다.

## <a name="use-the-sql-server-data-in-r-summaries"></a>R에서 SQL Server 데이터 사용 요약

이 섹션에서는 원격 컴퓨팅 컨텍스트를 지원하는, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공하는 여러 함수를 사용해 보겠습니다. 데이터 원본에 R 함수를 적용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 살펴보고, 요약하고, 차트로 작성할 수 있습니다.

1. [rxGetVarInfo](/r-server/r-reference/revoscaler/rxgetvarinfo) 함수를 호출하여 데이터 원본의 변수 목록과 해당 데이터 형식을 가져옵니다.

    **rxGetVarInfo** 는 편리한 함수입니다. 원격 데이터 개체의 모든 데이터 프레임 또는 데이터 세트에서 호출하여 최댓값 및 최솟값, 데이터 형식, 요소 열의 수준 수 등의 정보를 가져올 수 있습니다.
    
    모든 종류의 데이터 입력, 기능 변환 또는 기능 엔지니어링 후에는 이 함수를 실행하는 것이 좋습니다. 이렇게 하면 모델에 사용하려는 모든 기능이 필요한 데이터 형식인지 확인하여 오류를 방지할 수 있습니다.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **결과**
    
    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. 이제 RevoScaleR 함수 [rxSummary](/r-server/r-reference/revoscaler/rxsummary)를 호출하여 개별 변수에 대한 자세한 통계를 가져옵니다.

    rxSummary는 R `summary` 함수를 기준으로 하지만 몇 가지 추가 기능과 이점도 제공합니다. rxSummary는 여러 컴퓨팅 컨텍스트에서 작동하며 청크를 지원합니다.  RxSummary를 사용하여 값을 변환하거나 요소 수준에 따라 요약할 수도 있습니다.
    
    이 예제에서는 승객 수에 따라 운임을 요약합니다.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + rxSummary에 대한 첫 번째 인수는 요약 기준으로 사용할 수식 또는 기간을 지정합니다. 여기서는 요약하기 전에 `F()` 함수를 사용하여 _passenger\_count_ 의 값을 요소로 변환합니다. 또한 _passenger\_count_ 요소 변수에 대한 최솟값(1)과 최댓값(6)을 지정해야 합니다.
    + 통계 출력을 지정하지 않을 경우 기본적으로 rxSummary는 Mean, StDev, Min, Max, 유효한 관찰 수 및 누락된 관찰 수를 출력합니다.
    + 이 예제에는 성능을 비교할 수 있도록 함수가 시작 및 완료되는 시간을 추적하는 일부 코드도 포함되어 있습니다.
  
    **결과**

    rxSummary 함수가 성공적으로 실행되면 다음과 같은 결과가 표시된 다음, 범주별 통계 목록이 표시됩니다. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>빅 데이터에 대한 보너스 연습

모든 행을 포함하는 새 쿼리 문자열을 정의해 봅니다. 이 실험을 위해 새 데이터 원본 개체를 설정하는 것이 좋습니다. *rowsToRead* 매개 변수를 변경하여 처리량에 미치는 영향을 확인할 수도 있습니다.

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> 이 작업을 실행하는 동안 [프로세스 탐색기](/sysinternals/downloads/process-explorer) 또는 SQL Profiler와 같은 도구를 사용하여 연결되는 방법과 SQL Server 서비스를 사용하여 R 코드를 실행하는 방법을 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 그래프 및 플롯 만들기](walkthrough-create-graphs-and-plots-using-r.md)