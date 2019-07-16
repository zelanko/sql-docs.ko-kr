---
title: RevoScaleR rxExec-SQL Server Machine Learning을 사용 하 여 SQL Server에서 사용자 지정 R 함수 실행
description: RevoScaleR 함수를 사용 하 여 SQL Server에서 사용자 지정 R 스크립트를 실행 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c9cb9d84637d20f3f0e73f97fa6565d84d12fb4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961950"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>RxExec를 사용 하 여 SQL Server에서 사용자 지정 R 함수 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

사용자 지정 R 함수를 통해 함수를 전달 하 여 SQL Server의 컨텍스트에서 실행할 수 있습니다 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)에 스크립트를 사용 하려면 모든 라이브러리 서버에도 설치 됩니다 하 고 해당 라이브러리는 기본 호환 가정, R 배포 

합니다 **rxExec** 함수 **RevoScaleR** 필요한 모든 R 스크립트 실행을 위한 메커니즘을 제공 합니다. 또한 **rxExec** 그렇지 않은 경우 기본 R 엔진의 리소스 제약 조건으로 제한 된 스크립트에 확장을 추가 하는 단일 서버에 여러 코어 작업을 명시적으로 분산할 수 있습니다.

이 자습서에서는 원격 서버에서 실행 되는 사용자 지정 R 함수 실행을 보여 주기 위해 시뮬레이션 된 데이터를 사용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server 2017 Machine Learning 서비스 (R)을 통한](../install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server 2016 R Services (In-database)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한을](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [RevoScaleR 라이브러리를 사용 하 여 개발 워크스테이션](../r/set-up-a-data-science-client.md)

클라이언트 워크스테이션에서 R 배포에는 기본 제공 제공 **Rgui** 이 자습서의 R 스크립트를 실행 하는 데 사용할 수 있는 도구입니다. 또한 Visual Studio 용 R 도구 또는 RStudio 같은 IDE를 사용할 수 있습니다.

## <a name="create-the-remote-compute-context"></a>원격 계산 컨텍스트 만들기

클라이언트 워크스테이션에서 R 명령을 실행 합니다. 사용 하는 예를 들어 **Rgui**를이 위치에서 시작 합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 계산이 수행 되는 SQL Server 인스턴스에 대 한 연결 문자열을 지정 합니다. R 통합에 대 한 서버를 구성 해야 합니다. 데이터베이스 이름은이 연습에서는 사용 되지 않지만 연결 문자열 하나 필요로 합니다. 테스트 또는 샘플 데이터베이스에 있는 경우 사용할 수 있습니다.

    **SQL 로그인 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Windows 인증 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 연결 문자열에서 참조 된 SQL Server 인스턴스에 원격 계산 컨텍스트를 만듭니다.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 계산 컨텍스트를 활성화 하 고 개체 정의 확인 하는 단계를 반환 합니다. 계산 컨텍스트 개체의 속성에 표시 됩니다.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>사용자 지정 함수 만들기

이 연습에서는 dice 한 쌍으로 이루어진는 일반적인 카지노 시뮬레이션 하는 사용자 지정 R 함수를 만듭니다. 게임의 규칙 win 또는 손실 결과 결정합니다.

+ 초기 롤에서 7 또는 11을 배포, 이깁니다.
+ 2를 배포, 손실, 3 또는 12입니다.
+ 4, 해당 숫자가 포인트가, 되 5, 6, 8, 9, 또는 10에 있으며 하면 계속 해 서 주사위 (이 경우 게임) 다시 포인트 또는 롤 하는 7, 경우 배포 중 하나를 분실할 때 까지는.

R에서 사용자 지정 함수를 만든 다음 여러 번 실행하면 게임을 쉽게 시뮬레이트할 수 있습니다.

1.  다음 R 코드를 사용하여 사용자 지정 함수를 만듭니다.
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  함수를 실행 하 여 단일 주사위 게임을 시뮬레이션 합니다.
  
    ```R
    rollDice()
    ```
  
    이겼나요, 졌나요?
  
작업 스크립트를 설정 했으므로 사용 하는 방법을 확인해 보겠습니다 **rxExec** 여 이길 확률을 확인할 수 있는 시뮬레이션을 만드는 여러 번 해당 함수를 실행 합니다.

## <a name="pass-rolldice-in-rxexec"></a>RxExec rollDice() 전달

원격 SQL Server의 컨텍스트에서 임의 함수를 실행 하려면 호출을 **rxExec** 함수입니다.

1. 사용자 지정 함수에 인수로 호출 **rxExec**시뮬레이션을 수정 하는 다른 매개 변수를 사용 하 여 함께 합니다.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + *timesToRun* 인수를 사용하여 함수를 실행해야 하는 횟수를 나타냅니다.  이 경우 주사위를 20회 굴립니다.
  
    + *RNGseed* 및 *RNGkind* 인수를 사용하여 난수 생성을 제어할 수 있습니다. *RNGseed* 를 **auto**로 설정하면 병렬 난수 스트림이 각 작업자에 대해 초기화됩니다.
  
2. **rxExec** 함수는 각 실행에 대한 하나의 요소가 포함된 목록을 만듭니다. 그러나 목록이 완성될 때까지 큰 변화는 없습니다. 모든 반복이 완료 되 면, 시작 하는 줄 **길이** 값을 반환 합니다.
  
    그러면 다음 단계로 이동하여 승패 레코드 요약을 가져올 수 있습니다.
  
3. R의 **unlist** 함수를 사용하여 반환된 목록을 벡터로 변환하고 **table** 함수를 사용하여 결과를 요약합니다.
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    결과가 다음과 같이 표시됩니다.
  
     *손실 Win* *12 8*

## <a name="conclusion"></a>결론

이 연습에서는 간단한 경우에 SQL Server에서 실행 되는 R 스크립트에서 임의 R 함수를 통합 하는 데 중요 한 메커니즘을 보여 줍니다. 이 기법을 가능 하 게 요점을 요약 하는 다음과 같습니다.

+ 기계 학습 및 R 통합에 대 한 SQL Server는 구성 해야 합니다. [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) R 기능을 사용 하거나 [SQL Server 2016 R Services (In-database)](../install/sql-r-services-windows-install.md)합니다.

+ 모든 종속성을 포함 하 여 함수에서 사용 되는 오픈 소스 또는 타사 라이브러리는 SQL Server에 설치 되어야 합니다. 자세한 내용은 [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.

+ 확정 된 프로덕션 환경에는 개발 환경에서 스크립트를 이동 하면 방화벽 및 네트워크 제한이 발생할 수 있습니다. 신중 하 게 테스트 스크립트에서 예상 대로 수행할 수 있는지 확인 합니다.

## <a name="next-steps"></a>다음 단계

사용 하 여 더 복잡 한 예제 **rxExec**,이 문서를 참조 하세요. [Foreach 및 rxExec 성긴 수준 병렬 처리](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
