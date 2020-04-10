---
title: RevoScaleR을 사용하여 데이터 시각화
description: 'RevoScaleR 자습서 6: SQL Server에서 R 언어를 사용하여 데이터를 시각화하는 방법입니다.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cc97db70461797e2e37614ae33d23ed51b21147
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116726"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>R을 사용하여 SQL Server 데이터 시각화(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 6에 해당됩니다.

이 자습서에서는 R 함수를 사용하여 *creditLine* 열에서 성별에 따른 값 분포를 확인합니다.

> [!div class="checklist"]
> * 히스토그램 입력을 위한 최소-최대 변수 만들기
> * **RevoScaleR**의 **rxHistogram**을 사용하여 히스토그램의 데이터 시각화
> * 기본 R 분포에 포함된 **lattice**에서 **levelplot**을 사용하여 산점도로 시각화

이 자습서에 나와 있는 것처럼 동일 스크립트에서 오픈 소스 및 Microsoft 전용 함수를 결합할 수 있습니다.

## <a name="add-maximum-and-minimum-values"></a>최댓값 및 최솟값 추가

이전 자습서에서 계산된 요약 통계를 기준으로, 추가 계산을 위해 데이터 소스에 삽입할 수 있는 데이터에 대한 유용한 정보가 발견되었습니다. 예를 들어 최솟값 및 최댓값을 사용하여 히스토그램을 계산할 수 있습니다. 이 연습에서는 상위 값 및 하위 값을 **RxSqlServerData** 데이터 소스에 추가합니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 이전 자습서에서 만든 *ccColInfo* 변수를 사용하여 데이터 소스의 열을 정의합니다.
  
   새로 계산된 열(*numTrans*, *numIntlTrans* 및 *creditLine*)을 원래 정의를 재정의하는 열 컬렉션에 추가합니다. 아래 스크립트는 **rxSummary**의 메모리 내 출력을 저장하는 sumOut에서 가져온 최솟값 및 최댓값을 기준으로 요소를 추가합니다. 
  
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
  
3. 열 컬렉션을 업데이트한 후 다음 명령문을 적용하여 앞에서 정의한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본의 업데이트된 버전을 만듭니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    이제 sqlFraudDS 데이터 원본에 *ccColInfo*를 사용하여 추가된 새 열이 포함됩니다.
  
이 시점에서 수정 내용은 R의 데이터 원본 개체에만 영향을 주고 데이터베이스 테이블에는 아직 새 데이터가 기록되지 않습니다. 그러나 sumOut 변수에서 캡처된 데이터를 사용하여 시각화 및 요약을 만들 수 있습니다. 

> [!TIP]
> 사용 중인 계산 컨텍스트가 어느 것인지 잊어버린 경우 **rxGetComputeContext()** 를 실행합니다. "RxLocalSeq 계산 컨텍스트"의 반환 값은 로컬 계산 컨텍스트로 실행 중임을 나타냅니다.

## <a name="visualize-data-using-rxhistogram"></a>rxHistogram을 사용하여 데이터 시각화

1. 다음 R 코드를 사용하여 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 함수를 호출하고 수식 및 데이터 원본을 전달합니다. 처음에 이 코드를 로컬로 실행하여 예상 결과 및 걸리는 시간을 확인할 수 있습니다.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    내부적으로 **rxHistogram** 은 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 패키지에 포함된 **rxCube** 함수를 호출합니다. **rxCube**는 수식에 지정된 각 변수마다 하나의 열과 개수 열이 포함된 단일 목록(또는 데이터 프레임)을 출력합니다.
    
2. 다음으로, 계산 컨텍스트를 원격 SQL Server 컴퓨터로 설정하고 다시 **rxHistogram** 을 실행합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 동일한 데이터 소스를 사용 중이기 때문에 결과가 정확하게 동일하지만, 두 번째 단계에서는 원격 서버에서 계산이 수행됩니다. 그런 다음 결과가 로컬 워크스테이션에 반환되어 그려집니다.
   
  ![히스토그램 결과](media/rsql-sue-histogramresults.jpg "히스토그램 결과")


## <a name="visualize-with-scatter-plots"></a>산점도를 사용하여 시각화

산점도는 데이터 탐색 중 두 변수 사이의 관계를 비교하기 위해 종종 사용됩니다. **RevoScaleR** 함수로 제공된 입력과 함께 이 목적으로 기본 제공 R 패키지를 사용할 수 있습니다.

1. [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) 함수를 호출하여 모든 *numTrans* 및 *numIntlTrans* 조합에 대해 *fraudRisk* 평균을 계산합니다.
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    그룹 평균을 계산하는 데 사용되는 그룹을 지정하려면 `F()` 표기법을 사용합니다. 이 예에서 `F(numTrans):F(numIntlTrans)`는 `numTrans` 및 `numIntlTrans` 변수의 정수가 각 정수 값마다 하나의 수준을 사용하여 범주 변수로 처리되어야 함을 나타냅니다.
  
    **rxCube**의 기본 반환 값은 교차 집계를 나타내는 *rxCube 개체*입니다. 
  
2. [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 함수를 호출하여 R의 표준 그리기 함수 중 하나에서 쉽게 사용할 수 있는 데이터 프레임으로 결과를 변환합니다.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 함수는 결과를 데이터 프레임으로 직접 변환하기 위해 사용할 수 있는 선택적 인수인 *returnDataFrame* = **TRUE**를 포함합니다. 다음은 그 예입니다.
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    하지만 **rxResultsDF** 출력이 더 명확하며 원본 열의 이름을 유지합니다. `head(cubePlot)` 다음에 `head(cube1)`를 실행하여 출력을 비교할 수 있습니다.
  
3. 모든 R 배포에 포함된 **lattice** 패키지에서 **levelplot** 함수를 사용하여 열 지도를 만듭니다.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **결과**
  
    ![scatterplot 결과](media/rsql-sue-scatterplotresults.jpg "scatterplot 결과")
  
이 빠른 분석에서 트랜잭션 수와 국제 트랜잭션 수 둘 다에서 사기 위험이 증가하는 것을 확인할 수 있습니다.

**rxCube** 함수 및 일반적인 크로스탭에 대한 자세한 내용은 [RevoScaleR을 사용한 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)을 참조하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터를 사용하여 R 모델 만들기](../../machine-learning/tutorials/deepdive-create-models.md)