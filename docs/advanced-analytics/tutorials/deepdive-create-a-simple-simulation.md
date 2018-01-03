---
title: "만들기 (SQL과 R 심층 분석)에 대해 간단한 시뮬레이션 | Microsoft Docs"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 047ce5984129eadde9ef92505b7c5448f7c37d4f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>간단한 시뮬레이션 (SQL과 R 심층 분석) 만들기

이 문서를 사용 하는 방법에는 데이터 과학 심층 분석 자습서의 마지막 단계는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

지금까지 사용 중인 설계 된 R 기능 간의 데이터 이동에 맞게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 계산 컨텍스트 및 합니다. 그러나 사용자 지정 R 함수를 작성하고 서버 컨텍스트에서 실행하려는 경우를 가정해 보세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec [함수를 사용하여](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 컴퓨터 컨텍스트에서 임의 함수를 호출할 수 있습니다. 사용할 수도 있습니다 **rxExec** 코어 단일 서버에서 작업을 명시적으로 배포 합니다.

이 단원에서는 간단한 시뮬레이션을 만들려면 원격 서버를 사용 합니다. 시뮬레이션에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터가 필요하지 않습니다. 예제에서는 사용자 지정 함수를 디자인한 다음 **rxExec** 함수를 사용하여 호출하는 방법만 보여 줍니다.

사용 하 여 보다 복잡 한 예제를 보려면 **rxExec**,이 문서를 참조: [foreach 및 rxExec 세분화 정교 하지 않은 병렬 처리](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>사용자 정의 함수 만들기

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
  
2.  분할의 단일 게임을 시뮬레이트하기 위해 함수를 실행 합니다.
  
    ```R
    rollDice()
    ```
  
    이겼나요, 졌나요?
  
지금 사용 하는 방법을 살펴보겠습니다 **rxExec** 기능을 여러 번 실행 하려면, 달성의 확률을 확인 하는 데 도움이 되는 시뮬레이션을 만들려고 합니다.

## <a name="create-the-simulation"></a>시뮬레이션 만들기

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 컨텍스트에서 임의 함수를 실행하려면 **rxExec** 함수를 호출합니다. 하지만 **rxExec** 코어가 여기 서버 컨텍스트에 SQL Server 컴퓨터에 사용자 지정 함수를 실행 또는 노드에 걸쳐 병렬로 함수의 분산된 실행을 지원 합니다.

1. 사용자 지정 함수에 인수로 호출 **rxExec**시뮬레이션을 수정 하는 다른 매개 변수와 함께 합니다.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - *timesToRun* 인수를 사용하여 함수를 실행해야 하는 횟수를 나타냅니다.  이 경우 주사위를 20회 굴립니다.
  
    - *RNGseed* 및 *RNGkind* 인수를 사용하여 난수 생성을 제어할 수 있습니다. *RNGseed* 를 **auto**로 설정하면 병렬 난수 스트림이 각 작업자에 대해 초기화됩니다.
  
2. **rxExec** 함수는 각 실행에 대한 하나의 요소가 포함된 목록을 만듭니다. 그러나 목록이 완성될 때까지 큰 변화는 없습니다. 모든 반복이 완료되면 `length` 로 시작하는 줄에 값이 반환됩니다.
  
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
  

데이터 파일은 Revolution analytics 웹 사이트에서 사용할 수 있는 10 백만 관찰의 더 큰 데이터 집합을 사용 하 여 이러한 기술은 시험 하려는 경우: [데이터 집합의 인덱스](http://packages.revolutionanalytics.com/datasets)

이 연습에서는 더 큰 데이터 파일을 다시 사용 하려면 데이터를 다운로드 하 고 각 데이터 원본 다음과 같이 수정 합니다.

1. 변수 수정 `ccFraudCsv` 및 `ccScoreCsv` 새 데이터 파일을 가리키도록
2. 참조 하는 테이블의 이름을 변경 *sqlFraudTable* 를`ccFraud10`
3. 참조 하는 테이블의 이름을 변경 *sqlScoreTable* 를`ccFraudScore10`

## <a name="additional-samples"></a>추가 예제

계산 컨텍스트 및 RevoScaler 함수를 전달 하 고 데이터 변환의 사용, 마스터 한 했으므로이 자습서를 확인해 보십시오.

[컴퓨터 학습 서비스에 대 한 R 자습서](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>이전 단계

[SQL Server와 XDF 파일 간에 데이터 이동](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
