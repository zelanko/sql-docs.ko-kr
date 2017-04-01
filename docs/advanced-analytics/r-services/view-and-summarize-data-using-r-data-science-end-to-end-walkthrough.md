---
title: "R을 사용하여 데이터 보기 및 요약(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# R을 사용하여 데이터 보기 및 요약(데이터 과학 종단 간 연습)
이제 R 코드를 사용하여 동일한 데이터로 작업해 보겠습니다. 또한 **에 포함된** RevoScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 패키지의 함수를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버의 컨텍스트에서 데이터 요약을 생성하고 결과를 다시 R 환경으로 보내는 방법을 알아봅니다.  

데이터 개체를 만들고 요약을 생성하고 모델을 작성하는 데 필요한 모든 코드를 포함하는 R 스크립트가 이 연습과 함께 제공됩니다. R 스크립트 파일 **RSQL_RWalkthrough.R**은 스크립트 파일을 설치한 위치에서 찾을 수 있습니다.  
+ R에 익숙한 경우 스크립트를 한 번에 실행할 수 있습니다.
+ RevoScaleR 사용 방법을 배우는 사용자를 위해 이 자습서에서는 스크립트를 줄 단위로 안내합니다.
+ 스크립트의 개별 줄을 실행하려면 파일의 줄을 하나 이상 강조 표시하고 Ctrl+Enter를 누르면 됩니다.    
  
> [!TIP]  나중에 연습의 나머지 단계를 완료하려는 경우 R 작업 영역을 저장합니다.  이렇게 하면 데이터 개체 및 기타 변수를 다시 사용할 수 있습니다.   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>SQL Server 데이터 원본 및 계산 컨텍스트 정의
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드에서 사용할 데이터를 가져오려면 다음을 수행해야 합니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 만들기  
- 필요한 데이터가 있는 쿼리를 정의하거나 테이블 또는 뷰를 지정합니다.    
- R 코드를 실행할 때 사용할 하나 이상의 계산 컨텍스트 정의    
-   필요에 따라 데이터 원본에 적용할 수 있는 함수 정의  
 

### <a name="load-the-revoscaler-library"></a>RevoScaleR 라이브러리 로드

+  **RevoScaleR** 패키지를 아직 로드하지 않은 경우 다음을 실행합니다.
    ```R
    library("RevoScaleR")`.  
    ```  
    오류가 발생할 경우 R 개발 환경에서 RevoScaleR 패키지가 포함된 라이브러리를 사용하고 있는지 확인합니다. 현재 경로를 보려면 `.libPaths())`와 같은 명령을 사용합니다.  

    **RevoScaleR** 패키지를 처음 사용하는 경우 `help("RevoScaleR")` 또는 `help("RxSqlServerData")`를 입력하여 R 환경에서 온라인 도움말을 확인합니다.  

### <a name="create-connection-strings"></a>연결 문자열 만들기


1. 연결 문자열을 정의합니다. 이 연습에서는 SQL 로그인 예제와 Windows 통합 인증 예제를 둘 다 제공합니다. R 코드에 암호를 저장하지 않도록 가능한 경우 Windows 인증을 사용하는 것이 좋습니다.

    사용하는 계정에는 지정된 데이터베이스에서 데이터를 읽고 새 테이블을 만들 수 있는 권한이 있어야 합니다. SQL Database에 사용자를 추가하고 올바른 사용 권한을 부여하는 방법에 대한 자세한 내용은 [설치 후 서버 구성&#40;SQL Server R Services&#41;](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md)을 참조하세요. 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호를 필요에 따라 편집해야 합니다. 
      
  
### <a name="define-and-set-a-compute-context"></a>계산 컨텍스트 정의 및 설정  

다음으로, SQL Server 컴퓨터에서 R 코드를 실행하도록 지원하는 *계산 컨텍스트*를 정의합니다. 일반적으로 R을 사용하는 경우 모든 작업이 컴퓨터의 메모리에서 실행됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R 작업이 수행되도록 지정하여 일부 태스크를 병렬로 실행하고 서버 리소스를 활용할 수 있습니다.  

기본적으로 계산 컨텍스트는 로컬이므로 작업에 따라 계산 컨텍스트를 명시적으로 설정해야 합니다.  


1.  먼저 계산 컨텍스트를 만드는 사용되는 몇 가지 변수를 정의합니다.  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   R에서는 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 R 개체를 직렬화할 때 임시 디렉터리를 사용합니다. *sqlShareDir*로 사용되는 로컬 디렉터리를 지정하거나 기본값을 적용할 수 있습니다.  
  
    -   *sqlWait*를 사용하여 R에서 결과를 대기할지 여부를 지정합니다.  대기 및 비 대기 작업에 대한 자세한 내용은 [ScaleR 분산 컴퓨팅](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)을 참조하세요.
  
    -   *sqlConsoleOutput* 인수를 사용하여 R 콘솔의 출력을 표시하지 않도록 지정합니다.  
  
2.  이미 정의된 변수 및 연결 문자열을 사용하여 계산 컨텍스트 개체를 만들고 R 변수 *sqlcc*에 저장합니다.  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. 계산 컨텍스트를 설정합니다.
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + `rxSetComputeContext`는 이전에 활성화된 계산 컨텍스트를 사용할 수 있도록 보이지 않게 반환합니다.
   + `rxGetComputeContext`는 활성 계산 컨텍스트를 반환합니다.  
  
    계산 컨텍스트 설정은 **RevoScaleR** 패키지의 함수를 사용하는 작업에만 영향을 줍니다. 계산 컨텍스트는 오픈 소스 R 작업의 수행 방식에는 영향을 주지 않습니다.  
  
### <a name="create-an-rxsqlserver-data-object"></a>RxSqlServer 데이터 개체 만들기  

사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 정의했으므로 해당 데이터 연결 개체를 기준으로 사용하여 다른 데이터 원본을 정의할 수 있습니다. *데이터 원본* 은 교육, 탐색, 점수 매기기 또는 기능 생성과 같은 태스크에 사용할 일부 데이터 집합을 지정합니다.  
    
*RxSqlServer* 함수를 사용하고 연결 문자열 및 가져올 데이터의 정의를 전달하여 SQL Server 데이터 집합을 정의합니다.  
  
1. SQL 문을 문자열 변수로 저장합니다. 이 쿼리는 모델을 학습하는 데 사용할 데이터를 정의합니다.    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. 쿼리 정의를 SQL Server 데이터 원본에 인수로 전달합니다. *colClasses* 인수는 SQL을 매핑하여 반환할 데이터의 스키마를 지정합니다. 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + *colClasses* 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]과 R 간에 데이터를 이동할 때 사용할 열 형식을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 R과 다른 데이터 형식 및 더 많은 데이터 형식을 사용하므로 이 인수가 중요합니다. 자세한 내용은 [R 데이터 형식 사용](../../advanced-analytics/r-services/working-with-r-data-types.md)을 참조하세요.  
  
    + *rowsPerRead* 인수는 메모리 사용량 및 효율적인 계산을 처리하는 데 중요합니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 대부분의 향상된 분석 함수는 데이터를 청크로 처리하고 중간 결과를 누적하며, 모든 데이터를 읽은 후 최종 계산을 반환합니다.  `rowsPerRead` 매개 변수를 추가하면 처리를 위해 각 청크로 읽어오는 데이터 행 수를 제어할 수 있습니다.  이 매개 변수의 값이 너무 크면 큰 데이터 청크를 효율적으로 처리할 수 있는 메모리가 없기 때문에 데이터 액세스 속도가 느려질 수 있습니다.  일부 시스템에서는 `rowsPerRead` 를 너무 작은 값으로 설정하는 경우에도 성능이 저하될 수 있습니다.  

> [!TIP] *inDataSource* 개체가 생성된 후 이 개체를 필요한 횟수만큼 다시 사용하여 사용된 변수 및 데이터에 대한 기본 정보를 가져와 데이터를 조작 및 변환하거나 모델 학습에 사용할 수 있습니다.  그러나 *inDataSource* 개체 자체에는 SQL 쿼리의 데이터가 아직 없습니다. 데이터는 *rxImport* 또는 *rxSummary*와 같은 함수를 실행할 때까지 로컬 환경에 포함되지 않습니다.          
  
## <a name="using-the-sql-server-data-in-r"></a>R에서 SQL Server 데이터 사용  
이제 데이터 원본에 R 함수를 적용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 탐색, 요약 및 차트로 작성할 수 있습니다. 이 섹션에서는 원격 계산 컨텍스트를 지원하는, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 제공하는 여러 함수를 사용해 보겠습니다.  
  
-   `rxGetVarInfo`: 원격 데이터 개체의 모든 데이터 프레임 또는 데이터 집합(또한 일부 목록 및 행렬)에서 이 함수를 사용하여 최대값 및 최소값, 데이터 형식, 요소 열의 수준 수 등의 정보를 가져올 수 있습니다.  
  
    모든 종류의 데이터 입력, 기능 변환 또는 기능 엔지니어링 후에는 이 함수를 실행하는 것이 좋습니다. 이렇게 하면 모델에 사용하려는 모든 기능이 필요한 데이터 형식인지 확인하여 오류를 방지할 수 있습니다.  
 
  
-   `rxSummary`: 이 함수를 사용하여 개별 변수에 대한 자세한 통계를 가져올 수 있습니다. 값을 변환하고, 요소 수준을 사용하여 요약을 계산하고, 다시 사용하기 위해 요약을 저장할 수도 있습니다.  
  
  
### <a name="inspect-variables-in-the-data-source"></a>데이터 원본에서 변수 검사  
    
+ 데이터 원본 `rxGetVarInfo`를 인수로 사용해서  `inDataSource` 함수를 호출하여 데이터 원본의 변수 목록 및 해당 데이터 형식을 가져옵니다.  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    *Results:*  
    *Var 1: tipped, Type: integer*  
    *Var 2: fare_amount, Type: numeric*  
    *Var 3: passenger_count, Type: integer*  
    *Var 4: trip_time_in_secs, Type: numeric, Storage: int64*  
    *Var 5: trip_distance, Type: numeric*  
    *Var 6: pickup_datetime, Type: character*  
    *Var 7: dropoff_datetime, Type: character*  
    *Var 8: pickup_longitude, Type: numeric*  
    *Var 9: pickup_latitude, Type: numeric*  
    *Var 10: dropoff_longitude, Type: numeric*  
  
### <a name="create-a-summary-using-r"></a>R을 사용하여 요약 만들기

+ RevoScaleR 함수 `rxSummary`를 호출하여 승객 수에 따른 요금을 요약합니다. 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + `rxSummary` 에 대한 첫 번째 인수는 요약 기준으로 사용할 수식 또는 기간을 지정합니다. 여기서는 요약하기 전에 `F()` 함수를 사용하여 passenger_count의 값을 요소로 변환합니다.  
    + 통계 출력을 지정하지 않을 경우 기본적으로 `rxSummary` 는 Mean, StDev, Min, Max, 유효한 관찰 수 및 누락된 관찰 수를 출력합니다.  
    + 이 예제에는 성능을 비교할 수 있도록 함수가 시작 및 완료되는 시간을 추적하는 일부 코드도 포함되어 있습니다.  
  
    *Results*  
    *rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)*  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
    *Number of valid observations: 1000*   
    *Name                          Mean    StdDev   Min Max ValidObs MissingObs*  
    *fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0*   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>다음 단계  
[R을 사용하여 그래프 및 그림 생성&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>이전 단원  
[1단원: 데이터 준비&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
