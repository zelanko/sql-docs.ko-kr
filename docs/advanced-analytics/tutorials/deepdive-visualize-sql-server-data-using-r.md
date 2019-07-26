---
title: RevoScaleR rxHistogram을 사용 하 여 SQL Server 데이터 시각화
description: SQL Server에서 R 언어를 사용 하 여 데이터를 시각화 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: dab52381def03394fc8c1bf0836c9c1a1a9f8e92
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469653"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>R을 사용 하 여 SQL Server 데이터 시각화 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이 단원에서는 R 함수를 사용 하 여 성별 *creditLine* 열의 값 분포를 확인 합니다.

> [!div class="checklist"]
> * 히스토그램 입력에 대해 최소-최대 변수 만들기
> * **RevoScaleR** 에서 **rxhistogram** 을 사용 하 여 히스토그램에서 데이터 시각화
> * 기본 R 배포에 포함 된 **격자** 의 **levelplot** 를 사용 하 여 산 점도로 시각화

이 단원에서 설명 하는 것 처럼 오픈 소스 함수와 Microsoft 전용 함수를 동일한 스크립트에서 결합할 수 있습니다.

## <a name="add-maximum-and-minimum-values"></a>최댓값 및 최솟값 추가하기

이전 단원에서 계산 된 요약 통계를 기반으로 추가 계산을 위해 데이터 원본에 삽입할 수 있는 데이터에 대 한 몇 가지 유용한 정보를 발견 했습니다. 예를 들어 최솟값 및 최댓값은 히스토그램을 계산하는 데에 사용될 수 있습니다. 이 연습에서는 **RxSqlServerData** 데이터 원본에 높은 값과 낮은 값을 추가 합니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 이전 단원에서 만든 변수 *ccColInfo* 를 사용 하 여 데이터 원본의 열을 정의 합니다.
  
   원래 정의를 재정의 하는 열 컬렉션에 새 계산 열 (*Numtrans*, *Numintl트랜잭션*및 *creditLine*)을 추가 합니다. 아래 스크립트는 **Rxsummary**의 메모리 내 출력을 저장 하는 sumout에서 얻은 최소값과 최대값을 기반으로 하는 요소를 추가 합니다. 
  
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
  
    이제 sqlFraudDS 데이터 원본에는 *ccColInfo*를 사용 하 여 추가 된 새 열이 포함 됩니다.
  
이 시점에서 수정하면 R의 데이터 원본에만 영향을 끼칩니다. 즉 어떤 데이터도 아직 데이터베이스 테이블에 기록되지 않았습니다. 그러나 sumOut 변수에 캡처된 데이터를 사용 하 여 시각화 및 요약을 만들 수 있습니다. 

> [!TIP]
> 사용 중인 계산 컨텍스트를 잊은 경우 **Rxget계산 econtext ()** 를 실행 합니다. 반환 값이 "RxLocalSeq Compute Context" 라면 로컬 계산 환경을 사용하고 있음을 나타냅니다.

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
 
3. 동일한 데이터 원본을 사용 하 고 있으므로 결과는 정확히 동일 하지만 두 번째 단계에서는 원격 서버에서 계산이 수행 됩니다. 그런 다음 결과가 로컬 워크스테이션에 반환되어 그려집니다.
   
  ![히스토그램 결과](media/rsql-sue-histogramresults.jpg "히스토그램 결과")


## <a name="visualize-with-scatter-plots"></a>산 점도를 사용 하 여 시각화

분산형 플롯은 두 변수 간의 관계를 비교 하기 위해 데이터 탐색 중에 자주 사용 됩니다. **RevoScaleR** 함수에서 제공 하는 입력을 사용 하 여이 용도로 기본 제공 R 패키지를 사용할 수 있습니다.

1. [Rxcube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) 함수를 호출 하 여 *Numtrans* 및 *numintl트랜잭션*의 모든 조합에 대해 *fraudRisk* 의 평균을 계산 합니다.
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    그룹 평균을 계산하는 데 사용되는 그룹을 지정하려면 `F()` 표기법을 사용합니다. 이 예제의 `F(numTrans):F(numIntlTrans)`는 `numTrans` 및 `numIntlTrans` 변수를 각 정숫값에 따라 범주 변수로 처리하는 것을 의미합니다.
  
    **rxCube**는 기본적으로 *rxCube 개체*를 반환합니다. 이 개체는 교차 집계를 나타냅니다. 
  
2. [Rxresultsdf](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 함수를 호출 하 여 R의 표준 그리기 함수 중 하나에서 쉽게 사용할 수 있는 데이터 프레임으로 결과를 변환 합니다.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 함수는 *returnDataFrame* = **TRUE** 라는 선택적인 인수를 갖습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    그러나 **Rxresultsdf** 의 출력은 클리너 이며 원본 열의 이름을 유지 합니다. 다음에를 `head(cube1)` 실행 하여출력을비교할수있습니다.`head(cubePlot)`
  
3. 모든 R 배포판에 포함 된 **격자** 패키지의 **levelplot** 함수를 사용 하 여 열 지도를 만듭니다.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **결과**
  
    ![산점도 결과](media/rsql-sue-scatterplotresults.jpg "산점도 결과")
  
이 빠른 분석에서 트랜잭션 수와 국제 트랜잭션 수를 모두 사용 하 여 사기 위험이 증가할 수 있음을 확인할 수 있습니다.

**Rxcube** 함수 및 일반적인은 크로스탭에 대 한 자세한 내용은 [RevoScaleR를 사용 하 여 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터를 사용 하 여 R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)