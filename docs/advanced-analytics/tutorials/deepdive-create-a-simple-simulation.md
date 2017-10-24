---
title: "5단원: 간단한 시뮬레이션 만들기(데이터 과학 심층 분석) | Microsoft 문서"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e5bbd69bba01da2aacd3b8912aebac6b4e1c28a1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-simple-simulation"></a>간단한 시뮬레이션을 만들어서

지금까지 사용 중인 설계 된 R 기능 간의 데이터 이동에 맞게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 계산 컨텍스트 및 합니다. 그러나 사용자 지정 R 함수를 작성하고 서버 컨텍스트에서 실행하려는 경우를 가정해 보세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec **함수를 사용하여** 컴퓨터 컨텍스트에서 임의 함수를 호출할 수 있습니다. 또한 명시적으로 코어에서 단일 서버 노드에서 작업을 분배 rxExec를 사용할 수 있습니다.

이 단원에서는 원격 서버를 사용하여 간단한 시뮬레이션을 만듭니다. 시뮬레이션 요구 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를이 예제에서는 사용자 지정 함수를 디자인 하 고 다음 rxExec 함수를 사용 하 여 호출 하는 방법을 보여 주며 합니다.

RxExec를 사용 하 여 보다 복잡 한 예제는이 문서를 참조: [foreach 및 rxExec 세분화 정교 하지 않은 병렬 처리](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-function"></a>함수 만들기

일반적인 카지노 게임은 다음과 같은 규칙에 따라 한 쌍의 주사위를 굴리는 동작으로 구성됩니다.

- 처음 굴릴 때 7 또는 11이 나오면 이깁니다.
- 2, 3 또는 12가 나오면 집니다.
- 4, 5, 6, 8, 9 또는 10이 나오면 해당 숫자가 포인트가 되고, 다시 포인트를 얻거나(이기는 경우) 7이 나올 때까지(지는 경우) 계속해서 주사위를 굴립니다.

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
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  단일 주사위 게임을 시뮬레이트하려면 함수를 실행합니다.
  
    ```R
    rollDice()
    ```
  
    이겼나요, 졌나요?
  
이제 함수를 여러 번 실행하여 이길 확률을 확인하는 데 도움이 되는 시뮬레이션을 만드는 방법을 살펴보겠습니다.

## <a name="create-the-simulation"></a>시뮬레이션 만들기

컨텍스트에서 임의 함수를 실행 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec 함수를 호출 하면 컴퓨터. RxExec도 지원 하지만 함수의 분산된 실행 병렬로 노드 또는 서버 컨텍스트에서 코어, 여기 있습니다 때 사용 해야 서버에서 사용자 지정 함수를 실행 하기 위해서만 합니다.

1. 시뮬레이션을 수정 하는 몇 가지 다른 매개 변수와 함께 rxExec에 대 한 인수로 사용자 정의 함수를 호출 합니다.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - *timesToRun* 인수를 사용하여 함수를 실행해야 하는 횟수를 나타냅니다.  이 경우 주사위를 20회 굴립니다.
  
    - *RNGseed* 및 *RNGkind* 인수를 사용하여 난수 생성을 제어할 수 있습니다. *RNGseed* 를 **auto**로 설정하면 병렬 난수 스트림이 각 작업자에 대해 초기화됩니다.
  
2. RxExec 함수는 각 실행;에 대해 하나의 요소가 표시 된 목록을 만듭니다. 그러나 많이 발생 하는 목록 완료 될 때까지 표시 되지 않습니다. 모든 반복이 완료되면 `length` 로 시작하는 줄에 값이 반환됩니다.
  
    그러면 다음 단계로 이동하여 승패 레코드 요약을 가져올 수 있습니다.
  
3. R의 `unlist` 함수를 사용하여 반환된 목록을 벡터로 변환하고 `table` 컴퓨터 컨텍스트에서 임의 함수를 호출할 수 있습니다.
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    결과가 다음과 같이 표시됩니다.
  
     *손실 Win* *12 8*

## <a name="conclusions"></a>결론

이 자습서에서는 다음과 같은 태스크를 익혔습니다.
  
-   분석에 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 가져오기
  
-   R에서 데이터 원본 만들기 및 수정
  
-   워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 간에 모델, 데이터 및 그림 전달
  
>  [!TIP]
> 
> 데이터 파일은 Revolution analytics 웹 사이트에서 사용할 수 있는 10 백만 관찰의 더 큰 데이터 집합을 사용 하 여 이러한 기술은 시험 하려는 경우: [데이터 집합의 인덱스](http://packages.revolutionanalytics.com/datasets)
>   
> 이 연습에서는 더 큰 데이터 파일을 다시 사용 하려면 데이터를 다운로드 하 고 각 데이터 원본 다음과 같이 수정 합니다.
>  - 새 데이터 파일을 가리키도록 *ccFraudCsv* 및 *ccScoreCsv* 변수 설정
>  - *sqlFraudTable* 에서 참조된 테이블의 이름을 *ccFraud10*으로 변경
>  - *sqlScoreTable* 에서 참조된 테이블의 이름을 *ccFraudScore10*으로 변경

## <a name="previous-step"></a>이전 단계

[SQL Server 및 XDF 파일 간에 데이터를 이동](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)



