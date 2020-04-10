---
title: RevoScaleR 계산 컨텍스트 사용
description: 'RevoScaleR 자습서 4: SQL Server에서 R 언어를 사용하여 컴퓨팅 컨텍스트를 정의하는 방법.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6c93198daa68e252018e5744eeef1a49a2513e60
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116916"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>계산 컨텍스트 정의 및 사용(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 4에 해당됩니다.

이전 자습서에서는 **RevoScaleR** 함수를 사용하여 데이터 개체를 검사했습니다. 이 자습서에서는 원격 SQL Server에 대한 컴퓨팅 컨텍스트를 정의할 수 있게 해주는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수를 소개합니다. 원격 계산 컨텍스트에서는 서버의 로컬 세션에서 원격 세션으로 R 실행을 전환할 수 있습니다. 

> [!div class="checklist"]
> * 원격 SQL Server 계산 컨텍스트에 대한 요소 알아보기
> * 계산 컨텍스트 개체에서 추적 사용

**RevoScaleR**은 Hadoop, Spark on HDFS 및 SQL Server 데이터베이스 내와 같은 여러 계산 컨텍스트를 지원합니다. SQL Server에서 **RxInSqlServer** 함수는 서버 연결과 로컬 컴퓨터와 원격 실행 컨텍스트 사이의 개체 전달을 위해 사용됩니다.

## <a name="create-and-set-a-compute-context"></a>계산 컨텍스트 만들기 및 설정

SQL Server 계산 컨텍스트를 만드는 **RxInSqlServer** 함수는 다음 정보를 사용합니다.

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 연결 문자열
+ 출력 처리 방법 지정
+ 공유 데이터 디렉터리에 대한 선택적 지정
+ 추적을 설정하거나 추적 수준을 지정하는 선택적 인수

이 섹션에서는 각 부분에 대한 연습을 진행합니다.

1. 계산이 수행되는 인스턴스에 대해 연결 문자열을 지정합니다. 이전에 만든 연결 문자열을 다시 사용할 수 있습니다.

    **SQL 로그인 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Windows 인증 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 출력 처리 방법을 지정합니다. 다음 스크립트는 로컬 R 세션이 다음 작업을 처리하기 전에 서버에서 R 작업 결과를 기다리도록 지시합니다. 또한 원격 계산의 결과가 로컬 세션에 표시되지 않도록 방지합니다.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 에 대한 **wait** 인수는 다음 옵션을 지원합니다.
  
    -   **TRUE**. 작업이 차단 작업으로 구성되고 완료 또는 실패할 때까지 반환되지 않습니다.  자세한 내용은 [Machine Learning Server의 분산 및 병렬 계산](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)을 참조하세요.
  
    -   **FALSE**. 작업이 비차단 작업으로 구성되고 즉시 반환되며, 사용자가 다른 R 코드 실행을 계속할 수 있습니다. 그러나 비차단 모드에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 클라이언트 연결을 유지해야 합니다.

3. 필요에 따라 로컬 R 세션 및 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터와 해당 계정에서의 공유 사용을 위한 로컬 디렉터리 위치를 지정합니다.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   공유할 특정 디렉터리를 수동으로 만들려면 다음과 같은 줄을 추가할 수 있습니다.

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. **RxInSqlServer** 생성자에 인수를 전달하여 *계산 컨텍스트 개체*를 만듭니다.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    **RxInSqlServer** 구문은 이전에 데이터 원본을 정의하기 위해 사용한 **RxSqlServerData** 함수의 구문과 거의 동일합니다. 하지만 다음과 같은 점에서 중요한 차이가 있습니다.
      
    - [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)함수를 사용하여 정의한 데이터 원본 개체는 데이터가 저장되는 위치를 지정합니다.
    
    - 반면에 계산 컨텍스트([RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수를 사용하여 정의됨)는 집계 및 기타 컴퓨팅이 수행되는 위치를 나타냅니다.
    
    컴퓨팅 컨텍스트 정의는 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 컴퓨팅에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의하지만 컴퓨팅 컨텍스트를 SQL Server로 변경하지 않고 SQL Server 컴퓨터에서 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다.

5. 원격 계산 컨텍스트를 활성화합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 해당 속성을 포함하여 계산 컨텍스트에 대한 정보를 반환합니다.

    ```R
    rxGetComputeContext()
    ```

7. "로컬" 키워드를 지정하여 컴퓨팅 컨텍스트를 다시 로컬 컴퓨터로 재설정합니다. 다음 자습서에서는 원격 컴퓨팅 컨텍스트 사용에 관해 설명합니다.

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 이 함수에서 지원하는 다른 키워드 목록을 보려면 R 명령줄에서 `help("rxSetComputeContext")` 를 입력합니다.

## <a name="enable-tracing"></a>추적 사용 설정

때로는 작업이 로컬 컨텍스트에서 작동하지만 원격 컴퓨팅 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석하거나 성능을 모니터링하려는 경우 컴퓨팅 컨텍스트에서 추적을 사용하도록 설정하여 런타임 문제 해결을 지원할 수 있습니다.

1. 같은 연결 문자열을 사용하지만 **RxInSqlServer** 생성자에 *traceEnabled* 및 *traceLevel* 인수를 추가하는 새 컴퓨팅 컨텍스트를 만듭니다.

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

2. [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 함수를 사용하여 추적이 사용 설정된 계산 컨텍스트를 이름으로 지정합니다.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>다음 단계

계산 컨텍스트로 전환하여 서버에서 또는 로컬로 R 코드를 실행하는 방법을 알아봅니다.

> [!div class="nextstepaction"]
> [로컬 및 원격 계산 컨텍스트에서 요약 통계 계산](../../machine-learning/tutorials/deepdive-create-and-run-r-scripts.md)