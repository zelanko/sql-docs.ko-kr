---
title: 보기 및 R 함수-SQL Server Machine Learning을 사용 하 여 SQL Server 데이터 요약
description: 시각화 및 R 함수를 사용 하 여 SQL Server에서 데이터베이스 내 분석에 대 한 통계 요약을 생성 하는 방법을 보여주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 368caa21545e534c393aca29ce8fd3a59f9d9837
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644562"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>보기 및 R (연습)를 사용 하 여 SQL Server 데이터를 요약 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는 함수에 **RevoScaleR** 패키지 하 고 다음 작업을 단계별로 안내 합니다.

> [!div class="checklist"]
> * SQL Server에 연결
> * 필요한 데이터 가지는 쿼리를 정의하거나 테이블 또는 뷰를 지정하기
> * R 코드를 실행할 때 사용할 하나 이상의 계산 컨텍스트 정의하기
> * 선택적으로, 데이터를 읽는 동안 원본에 적용할 변환을 정의

## <a name="define-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트 정의

클라이언트 워크스테이션에서 R 환경에서 다음 R 명령문을 실행 합니다. 이 섹션에서는 가정를 [Microsoft R Client를 사용 하 여 데이터 과학 워크스테이션](../r/set-up-a-data-science-client.md)이므로 모든 RevoScaleR 패키지 뿐만 아니라 R 도구의 간단한 기본 집합을 포함 합니다. 예를 들어이 섹션에서 R 스크립트를 실행 하려면 Rgui.exe를 사용할 수 있습니다.

1. **RevoScaleR** 패키지가 로드되지 않은 경우, 아래 R 코드를 실행합니다.

    ```R
    library("RevoScaleR")
    ```

     인용 부호는 선택 사항이나 이 경우에는 권장됩니다.
     
     오류가 발생한다면 R 개발 환경이 RevoScaleR 패키지를 포함한 라이브러리를 사용하는지 확인합니다. 현재 라이브러리 경로를 보려면 `.libPaths()` 같은 명령을 사용합니다.

2. SQL Server에 대한 연결 문자열을 만들고 R 변수 *connStr* 에 저장합니다.

   자리 표시자 "your_server_name" 올바른 SQL Server 인스턴스 이름으로 변경 해야 합니다. 서버 이름으로 인스턴스 이름만 사용할 수도 있고 네트워크에 따라 전체 식별자 이름이 필요할 수도 있습니다.
    
   SQL Server 인증에 대 한 연결 구문은 다음과 같습니다.

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Windows 인증의 경우 구문이 조금 다릅니다.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    일반적으로 R 코드에 암호가 저장되는 것을 피하기 위해 가능한 Windows 인증을 사용하길 권장합니다.

3. 새로운 *계산 컨텍스트* 를 만들 때 사용할 변수를 정의합니다. 계산 컨텍스트 개체를 만든 후에 이를 사용해서 SQL Server 인스턴스에 R 코드를 실행할 수 있습니다.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R에서는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 R 개체를 직렬화할 때 임시 디렉터리를 사용합니다. *sqlShareDir*로 사용되는 로컬 디렉터리를 지정하거나 기본값을 사용할 수 있습니다.
  
    - *sqlWait*을 사용하여 R이 서버의 결과를 기다릴지 여부를 지정합니다.  대기 및 비 대기 작업의 자세한 내용은 참조 하세요. [분산 및 Microsoft R의 RevoScaleR을 사용 하 여 병렬 컴퓨팅](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)합니다.
  
    - *sqlConsoleOutput* 인수를 사용해서 R 콘솔에 출력되지 않도록 지정합니다.

4. [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) 생성자를 호출하여 이전에 정의된 변수와 연결 문자열로 계산 컨텍스트 개체를 만들고 R 변수 *sqlcc* 에 새로운 개체로 저장합니다.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 기본적으로 계산 컨텍스트는 로컬이므로 명시적으로 *활성* 계산 컨텍스트를 설정해야 합니다.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [다음과 같이 rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 반환 하지 이전의 활성 계산 컨텍스트를 시각적으로 사용할 수 있도록
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 활성 계산 컨텍스트를 반환 합니다.
    
    계산 컨텍스트 설정은 영향을 줍니다의 함수를 사용 하는 작업은 **RevoScaleR** 패키지를, 계산 컨텍스트는 오픈 소스 R 작업을 수행 하는 방법은 영향을 주지 않습니다.

## <a name="create-a-data-source-using-rxsqlserver"></a>RxSqlServer를 사용한 데이터 원본 생성

RevoScaleR 등 MicrosoftML, Microsoft R 라이브러리를 사용 하는 경우는 *데이터 원본* 는 RevoScaleR 함수를 사용 하 여 만든 개체입니다. 데이터 원본 개체는 모델 훈련 또는 특성 추출과 같은 작업에 사용할 데이터 집합을 지정합니다. 다양 한 SQL Server를 비롯 한 원본에서에서 데이터를 가져올 수 있습니다. 현재 지원 되는 원본 목록에 대해서 [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)합니다.

이전에 우리는 연결 문자열을 정의하고 R 변수에 그 정보를 저장했습니다. 해당 연결 정보를 재사용해서 가져올 데이터를 지정할 수 있습니다.

1. SQL 쿼리를 문자열 변수로 저장합니다. 쿼리는 모델 훈련용 데이터를 정의합니다.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    더 빠르게 실행 하는 작업을 하기 위해 여기에 TOP 절을 사용 했습니다 하지만 쿼리에 의해 반환 되는 실제 행 순서에 따라 달라질 수 있습니다. 따라서 요약 결과 아래에 나열 된 다른 수도 있습니다. TOP 절을 제거 해도 됩니다.

2. 쿼리 정의를 인수로 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 함수에 전달합니다.

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + *colClasses* 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 R 간에 데이터를 이동할 때 사용할 열 형식을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 R과는 다른 혹은 더 많은 데이터 형식을 사용하므로 중요한 부분입니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md) 을 참조합니다.
  
    + *rowsPerRead* 인수는 메모리 사용량 관리와 효율적인 계산을 위해 중요한 부분입니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 대부분의 향상된 분석 함수들은 데이터를 청크(chunk)로 처리하고 중간 결과를 누적하면서 모든 데이터를 읽은 후에 최종 계산을 반환합니다.  *rowsPerRead* 매개 변수를 추가하여 각 청크에서 처리할 데이터 행 수를 조절할 수 있습니다.  이 매개 변수의 값이 너무 커서, 충분 한 메모리를 효율적으로 이러한 많은 양의 데이터를 처리할 필요가 없기 때문에 데이터 액세스 느려질 수 있습니다.  일부 시스템에서는 *rowsPerRead* 를 지나치게 작은 값으로 설정하는 것도 성능을 저하시킬 수 있습니다.

3. 이 시점에서 *inDataSource* 개체를 만들었지만 데이터는 포함되지 않았습니다. [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 또는 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) 같은 함수를 실행하기 전까지 SQL 쿼리로부터 로컬 환경으로 데이터를 가져오지 않습니다.

    하지만 이제 데이터 개체를 정의했으므로 다른 함수에 인수로 사용할 수 있습니다.

## <a name="use-the-sql-server-data-in-r-summaries"></a>R 요약에서 SQL Server 데이터 사용

이번 섹션에서 원격 계산 컨텍스트를 지원하는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 의 몇 가지 함수를 시도해 보겠습니다. 데이터 소스에 R 함수를 적용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 탐색, 요약, 차트로 작성할 수 있습니다.

1. [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) 함수를 호출하면 데이터 원본에 있는 변수들의 목록과 해당 데이터 형식을 얻을 수 있습니다.

    **rxGetVarInfo** 는 편리한 함수입니다. 데이터 프레임 또는 원격 데이터 개체 내의 데이터 집합에 대해 호출하면 최대값과 최소값, 그 데이터 유형, 인자(factor) 열이 몇 개의 수준(level)으로 되어 있는지 등의 정보를 얻을 수 있습니다.
    
    데이터 입력, 특성 변환 또는 특성 추출(feature engineering) 후에 이 함수를 실행하는 것을 고려하세요. 그렇게 하면 모델에서 사용하려는 모든 특성의 예상 데이터 유형을 확인하고 오류를 피할 수 있습니다.
  
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

2. 이제 RevoScaleR 함수 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) 를 호출해서 개별 변수에 대한 자세한 통계를 얻습니다.

    rxSummary는 R `summary` 요약 함수에 기반하지만 몇 가지 추가 기능과 이점을 가집니다. rxSummary는 다중 계산 컨텍스트로 작동하고 청킹(chunking)을 지원합니다.  또한 값을 변환하거나 인자 수준 기반의 요약에도 rxSummary를 사용할 수 있습니다.
    
    이 예제에서는 승객 수에 따른 요금을 요약합니다.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + rxSummary의 첫 번째 인수는 요약할 수식이나 용어를 지정합니다. 여기서 `F()` 함수는 요약 전에 _passenger\_count_ 값을 인자(factor)로 변환하는데 사용됩니다. 또한 _passenger\_count_ 인자 변수의 최소값(1)과 최대값(6) 또한 지정해야 합니다.
    + 출력할 통계를 지정하지 않으면 기본적으로 rxSummary가 Mean, StDev, Min, Max 그리고 유효 관측 수와 누락 관측 수를 출력합니다(역주. 각각 ValidObs, MissingObs 라는 항목으로 출력됨).
    + 이 예제에는 함수의 시작과 완료 시간을 추적해서 성능을 비교할 수 있는 코드도 포함하고 있습니다.
  
    **결과**

    이와 같은 결과가 나타납니다 rxSummary 함수를 성공적으로 실행 하는 경우 통계 목록을 범주별으로 옵니다. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>빅 데이터 연습

모든 행을 사용하는 새로운 쿼리 문자열을 정의하세요. 이 실험에 대 한 새 데이터 원본 개체를 설정 하는 것이 좋습니다. 처리량에 미치는 영향을 보기 위해 *rowsToRead* 매개변수를 바꾸어볼 수도 있습니다.

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
> 코드를 실행하는 동안 [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) 또는 SQL Profiler 같은 도구를 사용해서 SQL Server 서비스에 어떻게 연결되고 R code가 실행되는지 확인할 수 있습니다.
> 
> SQL Server에서 실행되는 R 작업을 모니터링하는 또 다른 옵션은 [사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 입니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL 및 R을 사용하여 그래프와 플롯 만들기](walkthrough-create-graphs-and-plots-using-r.md)