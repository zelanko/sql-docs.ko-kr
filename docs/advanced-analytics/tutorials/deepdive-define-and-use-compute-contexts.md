---
title: 계산 컨텍스트 (SQL과 R 심층 분석)를 사용 및 정의 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb559b0acfc77ddb7e48cc0b3cacf76d421481ac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202345"
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>계산 컨텍스트 (SQL과 R 심층 분석)를 사용 및 정의
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 단원에서는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수 SQL Server에 대 한 계산 컨텍스트를 정의 하 고 다음 로컬 컴퓨터 대신 서버에서 복잡 한 계산을 실행할 수 있습니다. 

RevoScaleR은 Hadoop, Spark, 또는 데이터베이스 내에서 R 코드를 실행할 수 있도록 여러 계산 컨텍스트를 지원 합니다. SQL Server에 대 한 서버를 정의 하 고 로컬 컴퓨터와 원격 실행 컨텍스트 간에 연결 및 전달 개체는 데이터베이스를 만드는 작업을 처리 하는 함수입니다.

SQL Server를 만드는 함수를 사용 하 여 상황에 맞는 다음 정보를 계산 합니다.

- 에 대 한 연결 문자열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스
- 출력 처리 방법 지정
- 추적을 사용 하거나 추적 수준을 지정 하는 선택적 인수
- 공유 데이터 디렉터리의 선택적 사양

## <a name="create-and-set-a-compute-context"></a>만들기 및 계산 컨텍스트를 설정 합니다.

1. 계산이 수행 되는 인스턴스에 대 한 연결 문자열을 지정 합니다.  앞에서 만든 연결 문자열을 다시 사용할 수 있습니다. 다른 서버에는 계산을 이동 하거나 일부 작업을 수행 하는 다른 로그인을 사용 하려는 경우 다른 연결 문자열을 만들 수 있습니다.

    **SQL 로그인 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **Windows 인증 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. 출력 처리 방법을 지정합니다. 다음 코드에서는 워크스테이션의 R 세션이 항상 R 작업 결과를 기다리지만, 원격 계산의 콘솔 출력을 반환하지 않도록 지정합니다.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 에 대한 **wait** 인수는 다음 옵션을 지원합니다.
  
    -   **TRUE**. 작업 차단으로 구성 되 고 완료 되었거나 실패 될 때까지 반환 하지 않습니다.  자세한 내용은 참조 [분산 및 학습 서버 컴퓨터에에서 병렬 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)합니다.
  
    -   **FALSE**. 작업은 비차단로 구성 및 즉시 반환 하므로 다른 R 코드 실행을 계속할 수 있습니다. 그러나 비차단 모드에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 클라이언트 연결을 유지해야 합니다.

3. 원격 및 로컬 R 세션에서 공유 사용을 위해 로컬 디렉터리의 위치를 지정할 수는 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 및 해당 계정.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 공유에 대 한 특정 디렉터리를 수동으로 만들 하려는 경우에 다음과 같은 줄을 추가할 수 있습니다.

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    폴더를 공유 하는 데 현재 사용 중인을 확인 하려면 실행 `rxGetComputeContext()`, 세부 정보에 대 한 현재 계산 컨텍스트를 반환 하는 합니다. 자세한 내용은 [ScaleR reference](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/)(ScaleR 참조)를 참조하세요.

4. 모든 변수를 준비 하지 제공 하 고에 대 한 인수는 **RxInSqlServer** 를 만드는 생성자는 *컨텍스트 개체를 계산*합니다.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    에 대 한 구문 **RxInSqlServer** 의 거의 동일는 **RxSqlServerData** 데이터 원본을 정의 하려면 이전에 사용 하는 함수입니다. 하지만 다음과 같은 점에서 중요한 차이가 있습니다.
      
    - [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)함수를 사용하여 정의한 데이터 원본 개체는 데이터가 저장되는 위치를 지정합니다.
    
    - 함수를 사용 하 여 계산 컨텍스트를 정의 하는 반면, [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 집계 및 기타 계산이 수행 된 것을 표시 합니다.
    
    계산 컨텍스트 정의는 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 계산에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의하지만 계산 컨텍스트를 SQL Server로 변경하지 않고 SQL Server 컴퓨터에서 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다.

## <a name="enable-tracing-on-the-compute-context"></a>계산 컨텍스트에서 추적 사용

때로는 작업이 로컬 컨텍스트에서 작동하지만 원격 계산 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석하거나 성능을 모니터링하려는 경우 계산 컨텍스트에서 추적을 사용하도록 설정하여 런타임 문제 해결을 지원할 수 있습니다.

1. 동일한 연결 문자열을 사용하는 새 계산 컨텍스트를 만듭니다. 이 때 **RxInSqlServer** 생성자에 *traceEnabled*와 *traceLevel* 인수를 추가합니다.

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

2. 계산 컨텍스트를 변경하려면 [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 함수를 사용하고 이름으로 컨텍스트를 지정합니다.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 이 자습서에서는 추적을 사용하지 않도록 설정한 계산 환경을 사용하십시오.
    > 
    > 그러나 추적을 사용하려는 경우 네트워크 연결에 따라 사용자의 경험에 영향을 미칠 수 있습니다. 또한 추적 지원 옵션의 성능 테스트가 일부 작업에 대해 수행되었음에 유의하십시오.

사용 하는 방법을 알아보려면 다음 단계에서는 서버에서 R 코드를 실행 하거나 로컬 컨텍스트를 계산 합니다.

## <a name="next-step"></a>다음 단계

[R 스크립트 만들기 및 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>이전 단계

[SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
