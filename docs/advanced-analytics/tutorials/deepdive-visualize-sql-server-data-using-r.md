---
title: RevoScaleR rxHistogram-SQL Server Machine Learning을 사용 하 여 SQL Server 데이터 시각화
description: SQL Server에서 R 언어를 사용 하 여 데이터를 시각화 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4092de07d19d4d33bd56025076e606269c2b04e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962150"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>R (RevoScaleR 및 SQL Server 자습서)를 사용 하 여 SQL Server 데이터 시각화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단원에서는를 사용 하 여 R 함수에 있는 값의 분포를 확인 합니다 *creditLine* 성별 열입니다.

> [!div class="checklist"]
> * 히스토그램 입력에 대 한 최소-최대 변수 만들기
> * 사용 하 여 히스토그램 데이터 시각화 **rxHistogram** 에서 **RevoScaleR**
> * 사용 하 여 산 점도 사용 하 여 시각화 **levelplot** 에서 **격자** 기본 R 배포에 포함

이 단원 에서처럼 동일한 스크립트에서 오픈 소스 및 Microsoft 특정 함수를 결합할 수 있습니다.

## <a name="add-maximum-and-minimum-values"></a>최댓값 및 최솟값 추가하기

이전 단원에서 계산된 된 요약 통계에 따라 추가 계산에 대 한 데이터 소스에 삽입할 수 있는 데이터에 대 한 유용한 정보를 발견 했습니다. 예를 들어 최솟값 및 최댓값은 히스토그램을 계산하는 데에 사용될 수 있습니다. 이 연습에서는 높고 낮은 값을 추가 합니다 **RxSqlServerData** 데이터 원본입니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 변수를 사용 하 여 *ccColInfo* 데이터 원본의 열을 정의 하는 이전 단원에서 만든 합니다.
  
   새 계산된 열 추가 (*numTrans*, *numIntlTrans*, 및 *creditLine*) 원래 정의 재정의 하는 열 컬렉션입니다. 아래 스크립트의 출력을 메모리에 저장 되어 있는 sumOut에서 가져온 최소 및 최대 값을 기반으로 하는 요소를 추가 **rxSummary**합니다. 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. 열 목록을 업데이트했으므로 다음 명령문을 실행해 앞에서 업데이트한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본을 생성하십시오.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    이제 sqlFraudDS 데이터 소스에 사용 하 여 추가 된 새 열에 포함 *ccColInfo*합니다.
  
이 시점에서 수정하면 R의 데이터 원본에만 영향을 끼칩니다. 즉 어떤 데이터도 아직 데이터베이스 테이블에 기록되지 않았습니다. 그러나 시각화 및 요약을 만들려면 sumOut 변수에서 캡처한 데이터를 사용할 수 있습니다. 

> [!TIP]
> 사용 중인 계산 컨텍스트가 어느를 잊은 경우 실행할 **rxGetComputeContext()** 합니다. 반환 값이 "RxLocalSeq Compute Context" 라면 로컬 계산 환경을 사용하고 있음을 나타냅니다.

## <a name="visualize-data-using-rxhistogram"></a>RxHistogram을 사용해 데이터 시각화하기

1. 다음 R 코드를 사용하여 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 함수를 호출하고 수식과 데이터 원본을 그 인수로 전달합니다. 먼저 이 코드를 로컬로 실행해서 예상 결과 및 걸리는 시간을 확인할 수 있습니다.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    내부적으로 **rxHistogram** 은 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 패키지에 포함된 **rxCube** 함수를 호출합니다. **rxCube**는 수식에 명시된 변수에 대해 하나의 열을 포함하는 단일 목록(혹은 데이터 프레임)과 수를 나타내는 열을 반환합니다.
    
2. 이제 계산 환경을 원격 SQL Server 컴퓨터로 설정하고 **rxHistogram**을 다시 실행합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 결과 동일 하므로 동일한 데이터 원본을 사용 하는 두 번째 단계에서는 계산 원격 서버에서 수행 됩니다. 그런 다음 결과가 로컬 워크스테이션에 반환되어 그려집니다.
   
  ![히스토그램 결과](media/rsql-sue-histogramresults.jpg "히스토그램 결과")


## <a name="visualize-with-scatter-plots"></a>산 점도 사용 하 여 시각화

산 점도 두 변수 간의 관계를 비교할 데이터 탐색 하는 동안 자주 사용 됩니다. 제공 하는 입력을 사용 하 여이 작업을 위해 기본 제공 R 패키지를 사용할 수 있습니다 **RevoScaleR** 함수입니다.

1. 호출을 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) 의 평균을 계산 하는 함수 *fraudRisk* 조합 마다 *numTrans* 하 고 *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    그룹 평균을 계산하는 데 사용되는 그룹을 지정하려면 `F()` 표기법을 사용합니다. 이 예제의 `F(numTrans):F(numIntlTrans)`는 `numTrans` 및 `numIntlTrans` 변수를 각 정숫값에 따라 범주 변수로 처리하는 것을 의미합니다.
  
    **rxCube**는 기본적으로 *rxCube 개체*를 반환합니다. 이 개체는 교차 집계를 나타냅니다. 
  
2. 호출 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) R의 표준 그리기 함수 중 하나에서 쉽게 사용할 수 있는 데이터 프레임으로 결과 변환 하는 함수입니다.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 함수는 *returnDataFrame* = **TRUE** 라는 선택적인 인수를 갖습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    그러나 출력 **rxResultsDF** 깨끗 하며 원본 열의 이름을 유지 합니다. 실행할 수 있습니다 `head(cube1)` 뒤에 `head(cubePlot)` 출력을 비교 합니다.
  
3. 사용 하 여 열 지도 **levelplot** 에서 작동 합니다 **격자** 모든 R 배포에 포함 된 패키지.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **결과**
  
    ![산점도 결과](media/rsql-sue-scatterplotresults.jpg "산점도 결과")
  
이 빠른 분석에서 트랜잭션 수와 국제 트랜잭션 수를 사용 하 여 사기 위험을 증가 함을 확인할 수 있습니다.

에 대 한 자세한 내용은 합니다 **rxCube** 함수와 크로스탭 일반적으로 볼 수 [RevoScaleR를 사용 하 여 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터를 사용 하 여 R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)