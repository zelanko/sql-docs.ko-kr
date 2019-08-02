---
title: RevoScaleR rxExec를 사용 하 여 SQL Server에서 사용자 지정 R 함수 실행
description: RevoScaleR 함수를 사용 하 여 SQL Server에서 사용자 지정 R 스크립트를 실행 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 439b21bce4e081025db1db53ab44498415ca44af
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715410"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>RxExec를 사용 하 여 SQL Server에서 사용자 지정 R 함수 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[Rxexec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)를 통해 함수를 전달 하 여 SQL Server 컨텍스트에서 사용자 지정 R 함수를 실행할 수 있습니다 .이 경우 스크립트에 필요한 라이브러리도 서버에 설치 되 고 해당 라이브러리는 R의 기본 배포와 호환 된다고 가정 합니다. 

**RevoScaleR** 의 **rxexec** 함수는 필요한 R 스크립트를 실행 하기 위한 메커니즘을 제공 합니다. 또한 **Rxexec** 는 단일 서버의 여러 코어에 작업을 명시적으로 배포 하 여 네이티브 R 엔진의 리소스 제약 조건으로 제한 되는 스크립트에 확장을 추가할 수 있습니다.

이 자습서에서는 시뮬레이션 된 데이터를 사용 하 여 원격 서버에서 실행 되는 사용자 지정 R 함수를 실행 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server Machine Learning Services (R 포함](../install/sql-machine-learning-services-windows-install.md) ) 또는 [SQL Server 2016 R 서비스 (데이터베이스 내)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [RevoScaleR 라이브러리를 사용 하는 개발 워크스테이션](../r/set-up-a-data-science-client.md)

클라이언트 워크스테이션의 R 배포는이 자습서에서 R 스크립트를 실행 하는 데 사용할 수 있는 기본 제공 **Rgui** 도구를 제공 합니다. RStudio 또는 Visual Studio용 R 도구와 같은 IDE를 사용할 수도 있습니다.

## <a name="create-the-remote-compute-context"></a>원격 계산 컨텍스트 만들기

클라이언트 워크스테이션에서 다음 R 명령을 실행 합니다. 예를 들어 **Rgui**를 사용 하는 경우이 위치에서 시작 합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 계산이 수행 되는 SQL Server 인스턴스에 대 한 연결 문자열을 지정 합니다. R 통합을 위해 서버를 구성 해야 합니다. 이 연습에서는 데이터베이스 이름이 사용 되지 않지만 연결 문자열에는 데이터베이스가 필요 합니다. 테스트 또는 예제 데이터베이스가 있는 경우이를 사용할 수 있습니다.

    **SQL 로그인 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Windows 인증 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 연결 문자열에서 참조 하는 SQL Server 인스턴스에 대 한 원격 계산 컨텍스트를 만듭니다.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 계산 컨텍스트를 활성화 한 다음 확인 단계로 개체 정의를 반환 합니다. 계산 컨텍스트 개체의 속성이 표시 됩니다.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>사용자 지정 함수 만들기

이 연습에서는 분석 한 쌍으로 구성 된 공통 카지노을 시뮬레이트하는 사용자 지정 R 함수를 만듭니다. 게임의 규칙에 따라 win 또는 손실 결과가 결정 됩니다.

+ 초기 롤업에 7 또는 11을 롤백하여 승리 합니다.
+ Roll 2, 3 또는 12는 손실 됩니다.
+ Roll a 4, 5, 6, 8, 9 또는 10은 해당 숫자를 점으로 이동 하 고, 점 (이 경우에는 win) 또는 roll a 7을 모두 분실 한 경우에도 계속 해 서 롤링 됩니다.

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
  
2.  함수를 실행 하 여 단일 주사위 게임을 시뮬레이트합니다.
  
    ```R
    rollDice()
    ```
  
    이겼나요, 졌나요?
  
이제 작동 스크립트가 있으므로 **Rxexec** 를 사용 하 여 함수를 여러 번 실행 하 여 win의 확률을 결정 하는 데 도움이 되는 시뮬레이션을 만드는 방법을 알아보겠습니다.

## <a name="pass-rolldice-in-rxexec"></a>RxExec의 Pass rollDice ()

원격 SQL Server 컨텍스트에서 임의 함수를 실행 하려면 **Rxexec** 함수를 호출 합니다.

1. 시뮬레이션을 수정 하는 다른 매개 변수와 함께 **Rxexec**에 대 한 인수로 사용자 지정 함수를 호출 합니다.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + *timesToRun* 인수를 사용하여 함수를 실행해야 하는 횟수를 나타냅니다.  이 경우 주사위를 20회 굴립니다.
  
    + *RNGseed* 및 *RNGkind* 인수를 사용하여 난수 생성을 제어할 수 있습니다. *RNGseed* 를 **auto**로 설정하면 병렬 난수 스트림이 각 작업자에 대해 초기화됩니다.
  
2. **rxExec** 함수는 각 실행에 대한 하나의 요소가 포함된 목록을 만듭니다. 그러나 목록이 완성될 때까지 큰 변화는 없습니다. 모든 반복이 완료 되 면 **길이가** 로 시작 하는 줄은 값을 반환 합니다.
  
    그러면 다음 단계로 이동하여 승패 레코드 요약을 가져올 수 있습니다.
  
3. R의 **unlist** 함수를 사용하여 반환된 목록을 벡터로 변환하고 **table** 함수를 사용하여 결과를 요약합니다.
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    결과가 다음과 같이 표시됩니다.
  
     *손실 Win* *12 8*

## <a name="conclusion"></a>결론

이 연습은 간단 하지만 SQL Server에서 실행 되는 R 스크립트에서 임의의 R 함수를 통합 하는 데 중요 한 메커니즘을 보여 줍니다. 이 기법을 가능 하 게 하는 핵심 요소를 요약 하면 다음과 같습니다.

+ 기계 학습 및 R 통합을 위해 SQL Server를 구성 해야 합니다. R 기능을 사용 하 여 [Machine Learning Services을 SQL Server](../install/sql-machine-learning-services-windows-install.md) 하거나 [2016 r 서비스 (데이터베이스 내)를 SQL Server](../install/sql-r-services-windows-install.md)합니다.

+ 모든 종속성을 포함 하 여 함수에 사용 되는 오픈 소스 또는 타사 라이브러리는 SQL Server에 설치 해야 합니다. 자세한 내용은 [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

+ 개발 환경에서 강화 된 프로덕션 환경으로 스크립트를 이동 하면 방화벽과 네트워크 제한 사항이 발생할 수 있습니다. 신중 하 게 테스트 하 여 스크립트가 예상 대로 수행할 수 있는지 확인 합니다.

## <a name="next-steps"></a>다음 단계

**Rxexec**를 사용 하는 더 복잡 한 예는 다음 문서를 참조 하세요. [Foreach 및 rxExec를 사용 하는 정교 하지 않은 미세 병렬 처리](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
