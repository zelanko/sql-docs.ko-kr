---
title: "계산 컨텍스트 정의 및 사용(데이터 과학 심층 분석) | Microsoft Docs"
ms.custom: ""
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 계산 컨텍스트 정의 및 사용(데이터 과학 심층 분석)
복잡한 계산의 일부를 로컬 컴퓨터 대신 서버에서 수행하기로 결정했습니다. 이렇게 하려면 서버에서 R 코드를 실행할 수 있도록 하는 계산 컨텍스트를 만들어야 합니다.  
  
[RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver) 함수는 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 패키지에서 제공하는 향상된 R 함수 중 하나입니다. 이 함수는 데이터베이스 연결을 만들고 로컬 컴퓨터와 원격 실행 컨텍스트 간에 개체를 전달하는 작업을 처리합니다.  
  
이 단계에서는 R 코드에서 *RxInSqlServer* 함수를 사용하여 계산 컨텍스트를 정의하는 방법을 알아봅니다.  


  
## 계산 컨텍스트 만들기 및 설정  
계산 컨텍스트를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 다음과 같은 기본 정보가 필요합니다.  
  
-   인스턴스에 대한 연결 문자열  
-   출력 처리 방법에 대한 사양  
-   추적을 사용하도록 설정하거나 공유 디렉터리를 지정하기 위한 선택적 인수


 이제 시작하겠습니다.

1.  계산이 수행되는 인스턴스에 대한 연결 문자열을 지정합니다.  이는 계산 컨텍스트를 만들기 위해 *RxInSqlServer* 함수에 전달하는 여러 변수 중 하나에 불과합니다. 

    **SQL 로그인 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **Windows 통합 인증 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  출력 처리 방법을 지정합니다. 다음 코드에서는 워크스테이션의 R 세션이 항상 R 작업 결과를 기다리지만, 원격 계산의 콘솔 출력을 반환하지 않도록 지정합니다.  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    *RxInSqlServer*에 대한 *wait* 인수는 다음 옵션을 지원합니다.  
  
    -   **TRUE**. 작업이 차단하며, 완료되거나 실패할 때까지 반환되지 않습니다.  작업 차단 및 비차단에 대한 자세한 내용은 다음을 참조하세요. 
  
    -   **FALSE**. 작업이 차단하지 않으며 즉시 반환되므로 다른 R 코드를 계속 실행할 수 있습니다. 그러나 비차단 모드에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 클라이언트 연결을 유지해야 합니다.  

3. 필요에 따라 로컬 R 세션 및 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터와 해당 계정에서의 공유 사용을 위한 로컬 디렉터리 위치를 지정할 수 있습니다.
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    이 인수에 대한 폴더를 수동으로 지정하는 것보다 기본값을 사용하는 것이 좋습니다. 자세한 내용은 [ScaleR reference](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver)(ScaleR 참조)를 참조하세요.
    
    사용되는 폴더를 알고 싶으면 `rxGetComputeContext`를 실행하여 현재 계산 컨텍스트에 대한 세부 정보를 확인할 수 있습니다. 
  

4.  모든 변수를 준비했으면 `RxInSqlServer` 생성자에 대한 인수로 제공하여 계산 컨텍스트 개체를 정의합니다.  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    *RxInSqlServer*의 구문이 앞에서 데이터 원본을 정의하는 데 사용한 *RxSqlServerData* 함수의 구문과 거의 같다는 것을 알 수 있습니다. 하지만 다음과 같은 점에서 중요한 차이가 있습니다.  
  
    -   *RxSqlServerData* 함수를 사용하여 정의한 데이터 원본 개체는 데이터가 저장되는 위치를 지정합니다.  
  
    -   반면, 계산 컨텍스트(*RxInSqlServer* 함수를 사용하여 정의됨)는 집계 및 기타 계산이 수행되는 위치를 나타냅니다.  
  
    계산 컨텍스트 정의는 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 계산에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의하지만 계산 컨텍스트를 SQL Server로 변경하지 않고 SQL Server 컴퓨터에서 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다. 
  
## 계산 컨텍스트에서 추적 사용  
때로는 로컬 컨텍스트에서 작동하는 작업이 특정 원격 계산 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석하거나 성능을 모니터링하려는 경우 계산 컨텍스트에서 추적을 사용하도록 설정하여 런타임 문제 해결을 지원할 수 있습니다.  
  
1. 같은 연결 문자열을 사용하지만 *RxInSqlServer* 생성자에 *traceEnabled* 및 *traceLevel* 인수를 추가하는 새 계산 컨텍스트를 만듭니다.  
  
    ```R  
    sqlComputeTrace <- RxInSqlServer(   
        connectionString = sqlConnString,        
        #shareDir = sqlShareDir,  
        wait = sqlWait,   
        consoleOutput = sqlConsoleOutput,       
        traceEnabled = TRUE,
        traceLevel = 7)  
    ```  
  
    이 예제에서는 *traceLevel* 속성이 7로 설정되었으며 이는 "모든 추적 정보 표시"를 의미합니다.  

2. 언제든지 이 계산 컨텍스트로 전환하려면 *rxSetComputeContext* 함수를 사용하고 이름으로 컨텍스트를 지정합니다.

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    이 자습서에서는 추적을 사용하도록 설정하지 않은 계산 컨텍스트를 사용합니다. 추적을 사용하도록 설정한 옵션의 성능은 모든 작업에 대해 테스트되지 않았으며 네트워크 연결에 따라 사용자의 경험이 다를 수 있습니다.  
  
원격 계산 컨텍스트를 만들었으므로 이제 서버에서 또는 로컬로 R 코드를 실행하기 위해 계산 컨텍스트를 변경하는 방법을 알아봅니다.  
  
## 다음 단계  
[2단원: R 스크립트 만들기 및 실행&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## 이전 단계  
[SQL Server 데이터 쿼리 및 수정&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## 관련 항목:  
[데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
