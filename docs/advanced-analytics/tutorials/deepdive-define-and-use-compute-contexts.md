---
title: 계산 환경을 정의하고 사용하기 (SQL과 R 심층 분석) | Microsoft Docs
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
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>계산 환경을 정의하고 사용하기 (SQL과 R 심층 분석)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)과 SQL Server를 함께 쓰는 방법에 대한 데이터 과학 심층 분석 자습서의 일부입니다.

이 단원에서는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수에 대해 알아봅니다. 이 함수를 이용해 SQL Server를 위한 계산 환경을 정의하고 로컬 컴퓨터 대신 서버에서 복잡한 계산을 실행할 수 있습니다. 

RevoScaleR은 Hadoop, Spark, 또는 데이터베이스 내에서 R 코드를 실행할 수 있도록 여러 계산 환경을 지원합니다. SQL Server의 경우 서버를 정의하면 함수는 데이터베이스 연결을 만들고 로컬 컴퓨터와 원격 실행 환경간에 개체를 전달하는 작업을 처리합니다.

SQL Server 계산 환경을 생성하는 함수는 다음 정보를 이용합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 연결 문자열
- 출력이 처리되는 방법에 대한 명세
- 추적을 허용하거나 추적 수준을 지정하는 추가적인 인수
- 공유 데이터 디렉터리에 대한 추가적인 명세

## <a name="create-and-set-a-compute-context"></a>계산 환경을 생성하고 설정하기.

1. 계산을 수행할 인스턴스의 연결 문자열을 지정합니다. 앞서 만들었던 연결 문자열을 다시 사용할 수 있습니다. 다른 서버로 계산을 수행하게 하거나 여러 작업을 수행하기 위해 다른 계정을 사용해야 할 때는 다른 연결 문자열을 생성할 수 있습니다.

    **SQL 로그인 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **Windows 인증 사용**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. 출력을 어떻게 처리할지 지정합니다. 다음 코드에서는 워크스테이션의 R 세션이 항상 R 작업 결과를 기다리지만, 원격 계산의 콘솔 출력을 반환하지 않도록 지정합니다.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 에 대한 **wait** 인수는 다음 옵션을 지원합니다.
  
    -   **TRUE**. 작업을 동기 작업으로 설정해 작업이 완료되거나 실패할 때 까지 반환하지 않습니다.  자세한 내용은 [분산 및 학습 서버 컴퓨터에에서 병렬 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)을 참조하십시오.
  
    -   **FALSE**. 작업을 비동기로 설정해 즉시 반환하고 다른 R 코드를 실행할 수 있습니다. 그러나 비동기 상태에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 클라이언트 연결을 유지해야 합니다.

3. 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터와 컴퓨터에 접속된 계정들, 그리고 로컬 R 세션끼리 공유를 하기 위해 로컬 디렉터리의 위치를 지정할 수 있습니다.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 공유를 위한 특정 디렉터리를 수동으로 생성하려면 아래와 같이 줄을 추가할 수 있습니다.

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    어떤 폴더가 공유 디렉터리로 사용되고 있는지 확인하려면 `rxGetComputeContext()`를 실행해 현재 계산 환경에 대한 정보를 알 수 있습니다. 자세한 내용은 [ScaleR reference](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/)(ScaleR 참조)를 참조하세요.

5. 모든 변수를 지정한 후, 변수들을 **RxInSqlServer**의 인수로 사용해 *계산 환경 개체*를 생성하십시오.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    **RxInSqlServer**는 이전에 데이터 원본을 정의하는데 쓰인 **RxSqlServerData**와 유사한 생김새를 가지고 있습니다. 하지만 몇 가지 중요한 차이점이 있습니다.
      
    - [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)함수를 사용하여 정의한 데이터 원본 개체는 데이터가 저장되는 위치를 지정합니다.
    
    - 이와 대조적으로, [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)를 통해 정의된 계산 환경은 집합과 다른 계산이 어디서 수행되는지 가리킵니다.
    
    계산 환경을 정의하는 것은 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 계산에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의하고 계산 환경을 SQL Server로 변경하고 SQL Server에 있는 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다.

## <a name="enable-tracing-on-the-compute-context"></a>계산 컨텍스트에서 추적을 사용 하도록 설정

때로는 작업이 로컬 컨텍스트에서 작동하지만 원격 계산 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석하거나 성능을 모니터링하려는 경우 계산 컨텍스트에서 추적을 사용하도록 설정하여 런타임 문제 해결을 지원할 수 있습니다.

1. 인수를 추가 하지만 동일한 연결 문자열을 사용 하 여 새 계산 컨텍스트를 만들어 *traceEnabled* 및 *traceLevel* 에 **RxInSqlServer** 생성자입니다.

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
    > 이 자습서에 대 한 추적을 설정 하지 않은 계산 컨텍스트를 사용 합니다. 
    > 
    > 그러나 추적을 사용 하려는 경우 유의 경험 네트워크 연결에 의해 영향을 받을 수 있습니다. 또한 유의 해야 하는 모든 작업에 대 한 추적이 설정 된 옵션에 대 한 성능 테스트 되지 않은 때문에 있습니다.

사용 하는 방법을 알아보려면 다음 단계에서는 서버에서 R 코드를 실행 하거나 로컬 컨텍스트를 계산 합니다.

## <a name="next-step"></a>다음 단계

[R 스크립트 만들기 및 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>이전 단계

[SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
