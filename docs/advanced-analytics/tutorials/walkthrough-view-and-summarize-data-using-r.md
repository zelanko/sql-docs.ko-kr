---
title: "R를 사용한 데이터 관찰 및 요약 | Microsoft Docs"
ms.date: 11/10/2017
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 91e936b3d972e0819622304fda2827d4f4674a82
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="view-and-summarize-data-using-r"></a>R를 사용한 데이터 관찰 및 요약
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이제 R 코드를 사용 하 여 동일한 데이터를 작업 하겠습니다. 이 단원에서는에 포함 된 함수를 사용 하는 방법을 배웁니다는 **RevoScaleR** 패키지 합니다.

데이터 개체를 만들고 요약을 생성하고 모델을 작성하는 데 필요한 모든 코드를 포함하는 R 스크립트가 이 연습과 함께 제공됩니다. R 스크립트 파일 **RSQL_RWalkthrough.R**은 스크립트 파일을 설치한 위치에서 찾을 수 있습니다.

+ R에 익숙한 경우 스크립트를 한 번에 실행할 수 있습니다.
+ RevoScaleR을 사용 하는 방법을 사용자에 게이 자습서 여 한 줄씩 스크립트를 통해 이동 합니다.
+ 스크립트의 개별 줄을 실행하려면 파일의 줄을 하나 이상 강조 표시하고 Ctrl+Enter를 누르면 됩니다.

> [!TIP]
> 나중에 연습의 나머지 단계를 완료하려는 경우 R 작업 영역을 저장합니다.  이런 방식으로 데이터 개체 및 기타 변수 준비가 다시 사용 합니다.

## <a name="define-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트를 정의 합니다.

Microsoft R을 사용 하면 손쉽게 데이터를 가져올 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 코드에서 사용 하도록 합니다. 프로세스는 다음과 같습니다.
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 만들기
- 필요한 데이터가 있는 쿼리를 정의하거나 테이블 또는 뷰를 지정합니다.
- R 코드를 실행할 때 사용할 하나 이상의 계산 컨텍스트 정의
- 필요에 따라 원본에서 읽는 동안 데이터 원본에 적용 되는 변환을 정의합니다

다음 단계는 R 코드의 모든 부분이 R 환경에서 실행 해야 합니다. 모든 RevoScaleR 패키지 뿐만 아니라 기본 사용할 수 있는 경량 R 도구 집합이 포함 하기 때문에 Microsoft R Client를 사용 했습니다.

1. 경우는 **RevoScaleR** 패키지 로드 되지 않았으면, R 코드의이 줄을 실행 합니다.

    ```R
    library("RevoScaleR")
    ```

     인용 부호는 권장이 경우 선택 사항입니다.
     
     오류가 발생 하는 경우 R 개발 환경을 RevoScaleR 패키지를 포함 하는 라이브러리를 사용 하 고 있는지 확인 합니다. 와 같은 명령을 사용 하 여 `.libPaths()` 현재 라이브러리 경로 볼 수 있습니다.

2. SQL Server에 대 한 연결 문자열을 만들고 R 변수에 저장 _connStr_합니다.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=Your_Database_Name;Uid=Your_User_Name;Pwd=Your_Password"
    ```

    서버 이름에 대 한 인스턴스 이름을 사용 하 여 수 또는 네트워크에 따라 이름을 정규화 해야 할 수 있습니다.

    Windows 인증에 대 한 구문은 조금 다릅니다.
    
    ```R
    connStr <- "Driver=SQL Server;Server=SQL_instance_name;Database=database_name;Trusted_Connection=Yes"
    ```

    다운로드할 수 있는 R 스크립트에는 SQL 로그인만 사용됩니다. 일반적으로 R 코드에서 암호를 저장 되지 않도록 설정할 수 있는 경우 Windows 인증을 사용 하는 것이 좋습니다. 그러나을 보장 하기 위해이 자습서의 코드는 Github에서 다운로드할 코드와 일치 하는지에서는 SQL 로그인이 연습의 나머지 부분에 대 한 합니다.

3. 새에 사용할 변수를 정의 _계산 컨텍스트_합니다. 계산 컨텍스트 개체를 만든 후에 SQL Server 인스턴스에 R 코드를 실행 하려면 사용할 수 있습니다.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R에서는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 R 개체를 직렬화할 때 임시 디렉터리를 사용합니다.  *sqlShareDir*로 사용되는 로컬 디렉터리를 지정하거나 기본값을 사용할 수 있습니다.
  
    - *sqlWait*을 사용하여 R이 서버의 결과를 기다릴지 여부를 지정합니다.  대기 vs. 비 대기 작업에 대한 논의는 [Microsoft R에서 ScaleR을 사용한 분산과 병렬 컴퓨팅](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing) 을 참조합니다.

  
    - *sqlConsoleOutput* 인수를 사용해서 R 콘솔에 출력되지 않도록 지정합니다.


4. [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) 생성자를 호출하여 이전에 정의된 변수와 연결 문자열로 계산 컨텍스트 개체를 만들고 R 변수 *sqlcc* 에 새로운 개체로 저장합니다.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 기본적으로 계산 컨텍스트는 로컬이므로 명시적으로 *활성* 계산 컨텍스트를 설정해야 합니다.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` 는 이전에 활성 계산 컨텍스트를 사용할 수 있도록 보이지 않게 반환합니다.
    + `rxGetComputeContext` 는 활성 계산 컨텍스트를 반환합니다.
    
    계산 컨텍스트 설정은 **RevoScaleR** 패키지의 함수를 사용하는 연산에만 영향을 줍니다. 오픈 소스 R 연산이 수행되는 방식에는 영향을 미치지 않습니다.

## <a name="create-a-data-source-using-rxsqlserver"></a>RxSqlServer를 사용한 데이터 원본 생성

Microsoft R에서 *데이터 소스* 는 RevoScaleR 함수를 사용하여 만드는 개체입니다. 데이터 원본 개체는 모델 훈련 또는 특성 추출과 같은 작업에 사용할 데이터 집합을 지정합니다. 다양한 원본으로부터 데이터를 얻을 수 있습니다. 현재 지원 되는 소스 목록은 [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 를 참조합니다.

이전에 우리는 연결 문자열을 정의하고 R 변수에 그 정보를 저장했습니다. 해당 연결 정보를 재사용해서 가져올 데이터를 지정할 수 있습니다.

1. SQL 쿼리를 문자열 변수로 저장합니다. 쿼리는 모델 훈련용 데이터를 정의합니다.

    ```R
    sampleDataQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    좀 더 빠르게 실행 하는 TOP 절을 사용 했습니다 하지만 쿼리에 의해 반환 되는 실제 행 순서에 따라 달라질 수 있습니다. 따라서 요약 결과가 아래에 나열 된 다른 수도 있습니다. TOP 절을 제거 하려면 자유롭게 합니다.

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
  
    + *rowsPerRead* 인수는 메모리 사용량 관리와 효율적인 계산을 위해 중요한 부분입니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 대부분의 향상된 분석 함수들은 데이터를 청크(chunk)로 처리하고 중간 결과를 누적하면서 모든 데이터를 읽은 후에 최종 계산을 반환합니다.  *rowsPerRead* 매개 변수를 추가하여 각 청크에서 처리할 데이터 행 수를 조절할 수 있습니다.  이 매개 변수의 값이 너무 크면 그만큼 큰 데이터 청크를 효율적으로 처리할 수 있는 메모리가 부족해서 데이터 접근 속도가 느려질 수 있습니다.  일부 시스템에서는 *rowsPerRead* 를 지나치게 작은 값으로 설정하는 것도 성능을 저하시킬 수 있습니다.

3. 이 시점에서 *inDataSource* 개체를 만들었지만 데이터는 포함되지 않았습니다. [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 또는 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) 같은 함수를 실행하기 전까지 SQL 쿼리로부터 로컬 환경으로 데이터를 가져오지 않습니다.

    하지만 이제 데이터 개체를 정의했으므로 다른 함수에 인수로 사용할 수 있습니다.

## <a name="use-the-sql-server-data-in-r-summaries"></a>SQL Server 데이터를 사용 하 여 R 요약에서

이 섹션에서는 적용 해 보도록에서 제공 하는 함수 중 몇 가지 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 해당 지원 원격 계산 컨텍스트. 데이터 원본에 R 함수를 적용 하 여 있습니다 수 탐색, 요약 및 차트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다.

1. 함수 호출 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) 데이터 원본과 해당 데이터 형식에서 변수의 목록을 가져올 수 있습니다.

    **rxGetVarInfo** 유용한 함수는;을 데이터 프레임에서 호출할 수 있습니다 또는 원격 데이터 개체의 데이터 집합이 최대값 및 최소값 등의 정보를 가져오려는 값, 데이터 형식 및 요소 열에는 수준 수입니다.
    
    모든 종류의 데이터 입력, 기능 변환 또는 기능 엔지니어링 후에는 이 함수를 실행하는 것이 좋습니다. 이렇게 하면 모델에 사용 하려는 기능에서 필요한 데이터의 모든 입력 이며 오류가 발생 하지 않도록 확인할 수 있습니다.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **결과**
    
    ```
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

2. 이제, RevoScaleR 함수를 호출 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) 개별 변수에 대 한 자세한 통계를 가져올 합니다.

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

    이러한 경우 결과 rxSummary 함수 성공적으로 실행 하는 경우 나타납니다 목록 다음에 통계의 범주별으로 보여 줍니다. 

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>빅 데이터 보너스 연습

모든 행을 사용하는 새로운 쿼리 문자열을 정의하세요. 이 실험을 위해 새 데이터 원본 개체를 설정하는 것을 권장합니다. 처리량에 미치는 영향을 보기 위해 *rowsToRead* 매개변수를 바꾸어볼 수도 있습니다.

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

## <a name="next-lesson"></a>다음 단원

[SQL 및 R을 사용하여 그래프와 플롯 만들기](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>이전 단원

[SQL을 사용한 데이터 탐색](walkthrough-view-and-explore-the-data.md)
