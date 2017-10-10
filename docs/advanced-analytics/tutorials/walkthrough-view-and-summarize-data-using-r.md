---
title: "보기 및 R (연습)를 사용 하 여 데이터를 요약 합니다. | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/08/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 22
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 8d94b671e88eb512cd763dc7660df6d3ac986370
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="view-and-summarize-data-using-r"></a>보기 및 R을 사용 하 여 데이터를 요약 합니다.

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
    connStrWin <- "Driver=SQL Server;Server=SQL_instance_name;Database=database_name;Trusted_Connection=Yes"
    ```

    다운로드할 수 있는 R 스크립트에는 SQL 로그인만 사용됩니다. 일반적으로 R 코드에서 암호를 저장 되지 않도록 설정할 수 있는 경우 Windows 인증을 사용 하는 것이 좋습니다. 그러나을 보장 하기 위해이 자습서의 코드는 Github에서 다운로드할 코드와 일치 하는지에서는 SQL 로그인이 연습의 나머지 부분에 대 한 합니다.

3. 새에 사용할 변수를 정의 _계산 컨텍스트_합니다. 계산 컨텍스트 개체를 만든 후에 SQL Server 인스턴스에 R 코드를 실행 하려면 사용할 수 있습니다.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R에서는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 R 개체를 직렬화할 때 임시 디렉터리를 사용합니다. *sqlShareDir*로 사용되는 로컬 디렉터리를 지정하거나 기본값을 적용할 수 있습니다.
  
    - 사용 하 여 *sqlWait* 를 서버에서 결과를 기다릴 R을 표시할지 여부를 지정 합니다.  비-대기 작업 및 대기의 논의 알려면 [분산 및 Microsoft R에서 ScaleR와 병렬 컴퓨팅](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)합니다.
  
    - 인수를 사용 하 여 *sqlConsoleOutput* R 콘솔에서 출력 않으려면 나타냅니다.


4. 호출 하 여 [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) 변수와 이미 정의 된 연결 문자열이 사용 하 여 계산 컨텍스트 개체를 만들고 새 개체는 R 변수에 저장 하는 생성자 *sqlcc*합니다.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 기본적으로 계산 컨텍스트는 로컬, 명시적으로 설정 해야 하므로 *활성* 컨텍스트를 계산 합니다.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` 는 이전에 활성화된 계산 컨텍스트를 사용할 수 있도록 보이지 않게 반환합니다.
    + `rxGetComputeContext` 는 활성 계산 컨텍스트를 반환합니다.
    
    계산 컨텍스트 설정은 **RevoScaleR** 패키지의 함수를 사용하는 작업에만 영향을 줍니다. 계산 컨텍스트는 오픈 소스 R 작업의 수행 방식에는 영향을 주지 않습니다.

## <a name="create-a-data-source-using-rxsqlserver"></a>RxSqlServer를 사용 하 여 데이터 원본 만들기

Microsoft R에서는 *데이터 소스* 는 RevoScaleR 함수를 사용 하 여 만드는 개체입니다. 데이터 원본 개체는 모델 학습 또는 기능 추출 하는 등의 작업에 대 한 사용 하려는 데이터의 일부 집합을 지정 합니다. 다양 한 원본;에서 데이터를 가져올 수 있습니다. 현재 지원 되는 소스 목록에 대 한 참조 [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)합니다.

이전 버전, 연결 문자열을 정의 하 고 해당 정보는 R 변수에 저장 합니다. 가져올 데이터 지정 하 고 해당 연결 정보를 다시 사용할 수 있습니다.

1. SQL 쿼리 문자열 변수로 저장 합니다. 쿼리는 모델 학습에 대 한 데이터를 정의 합니다.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

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
    
    + *colClasses* 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 과 R 간에 데이터를 이동할 때 사용할 열 형식을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 R과 다른 데이터 형식 및 더 많은 데이터 형식을 사용하므로 이 인수가 중요합니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)합니다.
  
    + 인수 *rowsPerRead* 메모리 사용량 및 효율적인 계산을 관리 하기 위한 것이 중요 합니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 대부분의 향상된 분석 함수는 데이터를 청크로 처리하고 중간 결과를 누적하며, 모든 데이터를 읽은 후 최종 계산을 반환합니다.  추가 하 여는 *rowsPerRead* 매개 변수를 데이터의 행 수에서 읽어 들이는 처리를 위해 각 청크를 제어할 수 있습니다.  이 매개 변수의 값이 너무 크면 큰 데이터 청크를 효율적으로 처리할 수 있는 메모리가 없기 때문에 데이터 액세스 속도가 느려질 수 있습니다.  일부 시스템 설정에서 *rowsPerRead* 과도 하 게 작은 값으로 성능이 저하을 제공할 수도 있습니다.

3. 만든이 시점에서 *inDataSource* 개체 데이터를 포함 하지 않습니다. 데이터는 추출 되지 SQL 쿼리에서 로컬 환경에 같은 함수를 실행할 때까지 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 또는 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)합니다.

    그러나 데이터 개체를 정의한 했으므로 다른 함수에 대 한 인수로 사용할 수 있습니다.

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

    R에 따라 rxSummary `summary` 작동 하지만 몇 가지 추가 기능 및 장점입니다. rxSummary 여러 계산 컨텍스트에서 작동 하 고 청크를 지원 합니다.  사용할 수도 있습니다를 값을 변환 하거나 요약 rxSummary 수준을 기반으로 요소입니다.
    
    이 예제에서는 승객 수에 따른 요금 크기에 요약 되어 있습니다.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + 수식 또는 요약 하 여 용어 rxSummary 첫 번째 인수를 지정 합니다. 여기서는 `F()` 함수에 값으로 변환 하는 데 사용 됩니다 _승객\_count_ 요소를 요약 하기 전에. 도 지정 해야 (1) 최소값 및 최 댓 값 (6)에 대 한는 _승객\_count_ 변수입니다.
    + 통계를 출력을 지정 하지 않으면 기본적으로 rxSummary 출력 평균, 표준 편차, Min, Max 및 유효 하 고 누락 된 관측 치 수가 합니다.
    + 이 예제에는 성능을 비교할 수 있도록 함수가 시작 및 완료되는 시간을 추적하는 일부 코드도 포함되어 있습니다.
  
    **결과**

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    Name  Mean    StdDev   Min Max ValidObs MissingObs
    fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0
    Statistics by category (6 categories):*
    Category                             F_passenger_count Means    StdDev    Min
    fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5
    fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0
    fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5
    fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5
    fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5
    fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0
    Max ValidObs
    55  666
    52  206
    52   51
    39   21
    64   55
    12    1
    "It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."
    ```

다른 결과 어? TOP 키워드를 사용 하 여 더 작은 쿼리 결과를 가져오지는 동일한 때마다 보장 되지 않으므로입니다.

### <a name="bonus-exercise-on-big-data"></a>빅 데이터 보너스 연습

모든 행이 있는 새 쿼리 문자열을 정의 하십시오. 이 실험에 대 한 새 데이터 원본 개체를 설정 하는 것이 좋습니다. 변경해 볼 수도 있습니다는 *rowsToRead* 처리량에 미치는 영향을 확인 하려면 매개 변수입니다.

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
> 와 같은 도구를 사용 하 여이 실행 되는 동안 [프로세스 탐색기](https://technet.microsoft.com/sysinternals/processexplorer.aspx) 또는 SQL Server 서비스를 사용 하 여 SQL 프로파일러를 연결 생성 되는 방법 참조 및 R 코드를 실행 합니다.
> 
> 이 사용 하 여 SQL Server에서 실행 되는 R 작업을 모니터링 하려면 또 다른 옵션은 [사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)합니다.

## <a name="next-lesson"></a>다음 단원

[R을 사용하여 그래프 및 플롯 만들기](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>이전 단원

[SQL을 사용하여 데이터 탐색](walkthrough-view-and-explore-the-data.md)

