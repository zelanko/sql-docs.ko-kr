---
title: rxExec를 사용하는 사용자 지정 R 함수
description: 시뮬레이션된 데이터를 사용하여 원격 서버에서 실행되는 사용자 지정 R 함수를 실행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6c8fab6b5ecc6a548c5213f4401494f6803acc42
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178790"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>rxExec(SQL Server 및 RevoScaleR 자습서)를 사용하여 SQL Server에서 사용자 지정 R 함수 실행
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 14에 해당됩니다.

이 자습서에서는 시뮬레이션된 데이터를 사용하여 원격 서버에서 실행되는 사용자 지정 R 함수를 실행하는 방법을 보여줍니다.

[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)를 통해 함수를 전달하여 SQL Server 컨텍스트에서 사용자 지정 R 함수를 실행할 수 있습니다.이 경우 스크립트에 필요한 모든 라이브러리도 서버에 설치되고 해당 라이브러리가 R의 기본 배포판과 호환된다고 가정합니다. 

**RevoScaleR**의 **rxExec** 함수는 필요한 R 스크립트를 실행할 수 있는 메커니즘을 제공합니다. 또한 **rxExec**는 단일 서버의 여러 코어에 작업을 명시적으로 배포하여 네이티브 R 엔진의 리소스 제약 조건으로 제한되는 스크립트에 규모를 추가할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server Machine Learning Services(R 포함)](../install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server 2016 R Services(데이터베이스 내)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [RevoScaleR 라이브러리를 사용하는 개발 워크스테이션](../r/set-up-a-data-science-client.md)

클라이언트 워크스테이션의 R 배포판은 이 자습서에서 R 스크립트를 실행하는 데 사용할 수 있는 기본 제공 **Rgui** 도구를 제공합니다. RStudio 또는 Visual Studio용 R 도구와 같은 IDE를 사용할 수도 있습니다.

## <a name="create-the-remote-compute-context"></a>원격 컴퓨팅 컨텍스트 만들기

클라이언트 워크스테이션에서 다음 R 명령을 실행합니다. 예를 들어 **Rgui**를 사용하는 경우 다음 위치에서 시작합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 계산이 수행되는 SQL Server 인스턴스에 대한 연결 문자열을 지정합니다. 해당 서버는 R 통합용으로 구성되어야 합니다. 이 연습에서는 데이터베이스 이름이 사용되지 않지만 연결 문자열에는 데이터베이스 이름이 필요합니다. 테스트 또는 샘플 데이터베이스가 있는 경우 해당 데이터베이스를 사용하면 됩니다.

    **SQL 로그인 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Windows 인증 사용**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 연결 문자열에서 참조하는 SQL Server 인스턴스에 대한 원격 컴퓨팅 컨텍스트를 만듭니다.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 컴퓨팅 컨텍스트를 활성화한 다음, 확인 단계로 개체 정의를 반환합니다. 컴퓨팅 컨텍스트 개체의 속성이 표시 됩니다.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>사용자 지정 함수 만들기

이 연습에서는 주사위 한 쌍을 굴리는 일반적인 카지노를 시뮬레이션하는 사용자 지정 R 함수를 만듭니다. 게임의 규칙에 따라 승패가 결정됩니다.

+ 처음 굴릴 때 7 또는 11이 나오면 이깁니다.
+ 2, 3 또는 12가 나오면 집니다.
+ 4, 5, 6, 8, 9 또는 10이 나오면 해당 숫자가 포인트가 되고, 다시 포인트를 얻거나(이기는 경우) 7이 나올 때까지(지는 경우) 계속해서 주사위를 굴립니다.

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
  
2.  함수를 실행하여 단일 주사위 게임을 시뮬레이션합니다.
  
    ```R
    rollDice()
    ```
  
    이겼나요, 졌나요?
  
이제 제대로 작동하는 스크립트가 만들어졌으므로 **rxExec**를 통해 함수를 여러 번 실행하여 이길 확률을 확인하는 데 도움이 되는 시뮬레이션을 만드는 방법을 살펴보겠습니다.

## <a name="pass-rolldice-in-rxexec"></a>rxExec에 rollDice() 전달

원격 SQL Server 컨텍스트에서 임의 함수를 실행하려면 **rxExec** 함수를 호출합니다.

1. 시뮬레이션을 수정하는 다른 몇 가지 매개 변수와 함께 **rxExec**에 대한 인수로 사용자 지정 함수를 호출합니다.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + *timesToRun* 인수를 사용하여 함수를 실행해야 하는 횟수를 나타냅니다.  이 경우 주사위를 20회 굴립니다.
  
    + *RNGseed* 및 *RNGkind* 인수를 사용하여 난수 생성을 제어할 수 있습니다. *RNGseed* 를 **auto**로 설정하면 병렬 난수 스트림이 각 작업자에 대해 초기화됩니다.
  
2. **rxExec** 함수는 각 실행에 대한 하나의 요소가 포함된 목록을 만듭니다. 그러나 목록이 완성될 때까지 큰 변화는 없습니다. 모든 반복이 완료되면 **length**로 시작하는 줄에 값이 반환됩니다.
  
    그러면 다음 단계로 이동하여 승패 레코드 요약을 가져올 수 있습니다.
  
3. R의 **unlist** 함수를 사용하여 반환된 목록을 벡터로 변환하고 **table** 함수를 사용하여 결과를 요약합니다.
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    결과가 다음과 같이 표시됩니다.
  
     *Loss  Win* *12  8*

## <a name="conclusion"></a>결론

이 연습은 간단하지만 SQL Server에서 실행되는 R 스크립트에서 임의의 R 함수를 통합하는 데 중요한 메커니즘을 보여줍니다. 이 기법을 가능하게 하는 핵심 요소를 요약하면 다음과 같습니다.

+ 기계 학습 및 R 통합용으로 SQL Server를 구성해야 합니다. R 기능이 포함된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server 2016 R Services(데이터베이스 내)](../install/sql-r-services-windows-install.md)

+ 모든 종속 항목을 포함하여 함수에 사용되는 오픈 소스 또는 타사 라이브러리를 SQL Server에 설치해야 합니다. 자세한 내용은 [새 R 패키지 설치](../package-management/install-additional-r-packages-on-sql-server.md)를 참조하세요.

+ 개발 환경에서 강화된 프로덕션 환경으로 스크립트를 이동하면 방화벽과 네트워크 제한 사항이 발생할 수 있습니다. 신중하게 테스트하여 스크립트가 예상대로 작동할 수 있는지 확인합니다.

## <a name="next-steps"></a>다음 단계

**rxExec**를 사용하는 더 복잡한 예는 다음 문서를 참조하세요. [foreach 및 rxExec를 사용하는 대략적인 미세 병렬 처리](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
