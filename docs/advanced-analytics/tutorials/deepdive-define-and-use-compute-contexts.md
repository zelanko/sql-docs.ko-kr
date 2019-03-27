---
title: SQL Server Machine Learning-RevoScaleR 계산 컨텍스트 정의 및 사용
description: SQL Server에서 R 언어를 사용 하 여 계산 컨텍스트를 정의 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c0ae593264abad52873cfc152da721b6c0867109
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645090"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>(SQL Server 및 RevoScaleR 자습서) 계산 컨텍스트 정의 및 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이전 단원에서 사용한 **RevoScaleR** 데이터 개체를 검사 하는 함수입니다. 이 단원에서는 합니다 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수를 원격 SQL Server에 대 한 계산 컨텍스트를 정의할 수 있습니다. 원격 계산 컨텍스트를 사용 하 여 서버에서 원격 세션에 로컬 세션에서 R 실행을 이동할 수 있습니다. 

> [!div class="checklist"]
> * 계산 컨텍스트를 원격 SQL Server의 요소에 알아봅니다.
> * 계산 컨텍스트 개체의 추적을 사용 하도록 설정

**RevoScaleR** 여러 계산 컨텍스트를 지원 합니다. Hadoop HDFS 및 SQL Server에서 Spark 데이터베이스입니다. SQL Server에 대 한 합니다 **RxInSqlServer** 함수 서버 연결 및 로컬 컴퓨터와 원격 실행 컨텍스트 간에 개체를 전달에 사용 됩니다.

## <a name="create-and-set-a-compute-context"></a>계산 컨텍스트를 만들고 설정하기

합니다 **RxInSqlServer** SQL Server 계산 컨텍스트를 만드는 함수를 다음 정보를 사용 합니다.

+ 에 대 한 연결 문자열을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스
+ 출력 처리 방법 지정
+ 선택적으로 공유 데이터 디렉터리 지정
+ 추적을 사용 하도록 설정 하거나 추적 수준을 지정 하는 선택적 인수

이 섹션에서는 각 부분을 안내합니다.

1. 계산을 수행할 인스턴스의 연결 문자열을 지정합니다. 앞서 만들었던 연결 문자열을 다시 사용할 수 있습니다.

    **SQL 로그인 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Windows 인증 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 출력 처리 방법을 지정합니다. 다음 스크립트는 다음 작업을 처리 하기 전에 서버에서 R 작업 결과 대 한 대기를 로컬 R 세션을 전달 합니다. 또한 로컬 세션에서 원격 계산의 출력을 표시 하지 않습니다.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 에 대한 **wait** 인수는 다음 옵션을 지원합니다.
  
    -   **TRUE**. 작업 차단으로 구성 되 고 완료 되었거나 실패 했습니다까지 반환 되지 않습니다.  자세한 내용은 [분산 및 Machine Learning Server에서 병렬 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)합니다.
  
    -   **FALSE**. 비차단로 구성 된 작업과 다른 R 코드 실행을 계속할 수 있도록 즉시 반환 합니다. 그러나 비차단 모드에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 클라이언트 연결을 유지해야 합니다.

3. 필요에 따라 로컬 R 세션에서 원격 공유 사용을 위해 로컬 디렉터리의 위치를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터와 해당 계정.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   공유에 대 한 특정 디렉터리를 수동으로 만들려면 하려는 경우에 다음과 같은 줄을 추가할 수 있습니다.

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 인수를 전달 합니다 **RxInSqlServer** 만드는 생성자입니다는 *계산 컨텍스트 개체*합니다.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    구문을 **RxInSqlServer** 의 거의 동일 합니다 **RxSqlServerData** 이전 데이터 원본 정의에 사용 하는 함수입니다. 하지만 다음과 같은 점에서 중요한 차이가 있습니다.
      
    - [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)함수를 사용하여 정의한 데이터 원본 개체는 데이터가 저장되는 위치를 지정합니다.
    
    - 이와 대조적으로, [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)를 통해 정의된 계산 환경은 집계 및 다른 계산이 어디서 수행되는지 가리킵니다.
    
    계산 환경을 정의하는 것은 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 계산에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의해도 계산 환경을 SQL Server로 변경하고 SQL Server에 있는 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다.

5. 원격 계산 컨텍스트를 활성화 합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 해당 속성을 포함 하는 계산 컨텍스트에 대 한 정보를 반환 합니다.

    ```R
    rxGetComputeContext()
    ```

7. 계산 컨텍스트를 로컬 컴퓨터 (다음 단원에서는 원격 계산 컨텍스트를 사용 하는 방법을 보여 줍니다) "local" 키워드를 지정 하 여 다시 설정 합니다.

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 이 함수에서 지원하는 다른 키워드 목록을 보려면 R 명령줄에서 `help("rxSetComputeContext")` 를 입력합니다.

## <a name="enable-tracing"></a>추적을 사용 하도록 설정

때로는 작업이 로컬 컨텍스트에서 작동하지만 원격 컴퓨팅 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석 하거나 성능을 모니터링 하려는 경우에 런타임 문제 해결을 지원 하도록 계산 컨텍스트에서 추적을 설정할 수 있습니다.

1. 동일한 연결 문자열을 사용 하 여 새 계산 컨텍스트를 만들지만 인수를 추가 *traceEnabled* 하 고 *traceLevel* 에 **RxInSqlServer** 생성자입니다.

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

2. 사용 된 [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 이름별 추적이 설정 된 계산 컨텍스트를 지정 하는 함수입니다.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>다음 단계

서버에서 R 코드를 실행 하거나 로컬 계산 컨텍스트를 전환 하는 방법에 알아봅니다.

> [!div class="nextstepaction"]
> [로컬 및 원격 계산 요약 통계 계산 컨텍스트](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)