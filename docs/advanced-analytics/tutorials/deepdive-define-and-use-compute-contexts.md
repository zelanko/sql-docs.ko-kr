---
title: "계산 컨텍스트 정의 및 사용(데이터 과학 심층 분석) | Microsoft 문서"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a682a40a9a62af3e1ff18ec0cc777ac9c1da7a9e
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="define-and-use-compute-contexts"></a>계산 컨텍스트 정의 및 사용


복잡한 계산의 일부를 로컬 컴퓨터 대신 서버에서 수행해야 한다고 가정해 보겠습니다. 이 작업을 위해 서버에서 R 코드를 실행할 수 있도록 하는 계산 컨텍스트를 만들 수 있습니다.

**RxInSqlServer** 함수는 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 패키지에서 제공하는 향상된 R 함수 중 하나입니다. 이 함수는 데이터베이스 연결을 만들고 로컬 컴퓨터와 원격 실행 컨텍스트 간에 개체를 전달하는 작업을 처리합니다.

이 단계에서는 R 코드에서 **RxInSqlServer** 함수를 사용하여 계산 컨텍스트를 정의하는 방법을 알아봅니다.

계산 컨텍스트를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 다음과 같은 기본 정보가 필요합니다.

- 인스턴스에 대한 연결 문자열
- 출력 처리 방법에 대한 사양
- 추적을 사용하도록 설정하거나 공유 디렉터리를 지정하기 위한 선택적 인수

## <a name="create-and-set-a-compute-context"></a>계산 컨텍스트 만들기 및 설정

1. 계산이 수행되는 인스턴스에 대한 연결 문자열을 지정합니다.  이는 계산 컨텍스트를 만들기 위해 *RxInSqlServer* 함수에 전달하는 여러 변수 중 하나에 불과합니다. 앞에서 만든 연결 문자열을 다시 사용하거나, 계산을 다른 서버로 이동하거나 다른 ID를 사용하려는 경우 다른 연결 문자열을 만들 수 있습니다.

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
  
    *RxInSqlServer* 에 대한 *wait* 인수는 다음 옵션을 지원합니다.
  
    -   **TRUE**. 작업이 차단하며, 완료되거나 실패할 때까지 반환되지 않습니다.  자세한 내용은 참조 [분산 및 Microsoft R에 병렬 컴퓨팅](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)합니다.
  
    -   **FALSE**. 작업이 차단하지 않으며 즉시 반환되므로 다른 R 코드를 계속 실행할 수 있습니다. 그러나 비차단 모드에서도 작업이 실행되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 클라이언트 연결을 유지해야 합니다.

3. 필요에 따라 로컬 R 세션 및 원격  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터와 해당 계정에서의 공유 사용을 위한 로컬 디렉터리 위치를 지정할 수 있습니다.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 공유에 대 한 특정 디렉터리를 수동으로 만들 하려는 경우에 다음과 같은 줄을 추가할 수 있습니다. 폴더를 공유 하는 데 현재 사용 중인을 확인 하려면 실행 `rxGetComputeContext`, 세부 정보에 대 한 현재 계산 컨텍스트를 반환 하는 합니다. 자세한 내용은 [ScaleR reference](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver)(ScaleR 참조)를 참조하세요.

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 모든 변수를 준비 하지 제공 하 고 만드는 데 RxInSqlServer 생성자에 대 한 인수는 *컨텍스트 개체를 계산*합니다.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    RxInSqlServer *에 대 한 구문은 거의 동일한 데이터 원본을 정의 하려면 이전에 사용 되는 RxSqlServerData 함수의 알 수 있습니다. 하지만 다음과 같은 점에서 중요한 차이가 있습니다.
      
    - RxSqlServerData, 함수를 사용 하 여 정의 된 데이터 원본 개체는 데이터가 저장 된 지정 합니다.
    
    - 반면, (RxInSqlServer 함수를 사용 하 여 정의 됨) 계산 컨텍스트로 집계 및 다른 계산을 수행 하려면는 나타냅니다.
    
    계산 컨텍스트 정의는 워크스테이션에서 수행할 수 있는 다른 모든 제네릭 R 계산에 영향을 주지 않으며 데이터의 원본을 변경하지 않습니다. 예를 들어 로컬 텍스트 파일을 데이터 원본으로 정의하지만 계산 컨텍스트를 SQL Server로 변경하지 않고 SQL Server 컴퓨터에서 데이터에 대한 모든 읽기 및 요약을 수행할 수 있습니다.

## <a name="enable-tracing-on-the-compute-context"></a>계산 컨텍스트에서 추적 사용

때로는 작업이 로컬 컨텍스트에서 작동하지만 원격 계산 컨텍스트에서 실행될 때 문제가 발생합니다. 문제를 분석하거나 성능을 모니터링하려는 경우 계산 컨텍스트에서 추적을 사용하도록 설정하여 런타임 문제 해결을 지원할 수 있습니다.

1. 인수를 추가 하지만 동일한 연결 문자열을 사용 하 여 새 계산 컨텍스트를 만들어 *traceEnabled* 및 *traceLevel* 에 *RxInSqlServer* 생성자입니다.

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

2. 계산 컨텍스트를 변경 하려면 rxSetComputeContext 함수를 사용 하 고 이름으로 컨텍스트를 지정 합니다.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 이 자습서에서는 추적을 사용하도록 설정하지 않은 계산 컨텍스트를 사용합니다. 모든 작업에 대 한 추적이 설정 된 옵션에 대 한 성능 테스트 되지 않은 때문입니다.
    > 
    > 그러나 추적을 사용 하려는 경우 유의 경험 네트워크 연결에 의해 영향을 받을 수 있습니다.

원격 계산 컨텍스트를 만들었으므로 이제 서버에서 또는 로컬로 R 코드를 실행하기 위해 계산 컨텍스트를 변경하는 방법을 알아봅니다.

## <a name="next-step"></a>다음 단계

[만들기 및 R 스크립트 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>이전 단계

[쿼리 및 SQL Server 데이터를 수정 합니다.](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)


