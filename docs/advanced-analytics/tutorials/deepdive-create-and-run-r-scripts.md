---
title: (SQL과 R 심층 분석) R 스크립트 만들고 실행하기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1ff4b72b535f97ba0132dd5e2712b56f90effb10
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204695"
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>(SQL과 R 심층 분석) R 스크립트 만들고 실행하기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)과 SQL Server를 함께 쓰는 방법에 대한 데이터 과학 심층 분석 자습서의 일부입니다.

앞서 데이터 원본을 설정하고 하나 이상의 계산 환경을 설정했으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 몇 가지 고성능 R 스크립트를 실행할 준비가 되었습니다.  이 단원에서는 아래의 기계 학습 과정을 진행하기 위해 서버 계산 환경을 사용합니다.

- 데이터 시각화 및 몇 가지 요약 통계 생성
- 선형 회귀 모델 만들기
- 로지스틱 회귀 모델 만들기
- 새로운 데이터를 평가하고 점수 히스토그램 만들기

## <a name="change-compute-context-to-the-server"></a>계산 환경을 서버로 변경하기

R 코드를 실행하기 전에 *현재* 또는 *활성* 계산 컨텍스트를 지정해야 합니다.

1. R을 사용하여 이미 정의한 계산 컨텍스트를 활성화하려면 다음과 같이 **rxSetComputeContext** 함수를 사용합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    이 문을 실행한 후에 모든 계산은 *sqlCompute* 매개 변수에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수행됩니다.
  
2. 워크스테이션에서 R 코드를 실행하려는 경우  **local** 키워드를 사용하여 계산 컨텍스트를 다시 로컬 컴퓨터로 전환할 수 있습니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    이 함수에서 지원하는 다른 키워드 목록을 보려면 R 명령줄에서 `help("rxSetComputeContext")` 를 입력합니다.
  
3. 계산 컨텍스트를 지정하면 변경할 때까지 활성 상태로 유지됩니다. 그러나 원격 서버 컨텍스트에서 실행할 수 *없는* 모든 R 스크립트는 로컬로 실행됩니다.

## <a name="compute-some-summary-statistics"></a>몇 가지 요약 통계 계산하기

계산 환경의 작동 방식을 보려면, `sqlFraudDS` 데이터 원본을 이용해 몇 가지 요약 통계를 생성해보십시오.  다시 강조하지만, 데이터 원본 개체는 단지 사용할 데이터를 정의하는 것입니다. 즉, 계산 환경은 바뀌지 않습니다.

+ 로컬로 요약 통계를 계산하려면 **rxSetComputeContext**를 사용하고 _로컬_ 키워드를 지정하십시오.
+ SQL Server 컴퓨터에서 같은 계산을 하려면 앞에서 정의한 SQL 계산 환경으로 전환하십시오.

1. [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)를 수식이나 데이터 원본 등의 필수 인수와 함께 호출하고 그 결과를 `sumOut` 변수에 할당합니다.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어에는 많은 요약 함수가 있지만, **rxSummary**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 포함하는 다양한 원격 계산 환경에서의 실행만 지원합니다. 이와 유사한 함수에 대한 정보는 [RevoScaleR을 사용하여 데이터 요약하기](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)를 참고하십시오.
  
2. 계산이 완료되면 `sumOut` 변수의 내용을 콘솔로 출력할 수 있습니다.
  
    ```R
    sumOut
    ```
  
    > [!NOTE]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 결과가 반환되기 전에 결과를 출력하려고 하지 마세요. 그러지 않으면 오류가 발생할 수 있습니다.

**결과**

*Summary Statistics Results for: ~gender + balance + numTrans +*

 *numIntlTrans + creditLine*

 *Data: sqlFraudDS (RxSqlServerData Data Source)*

 *Number of valid observations: 10000*

 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*

 *balance       4075.0318 3926.558714            0   25626 100000*

 *numTrans        29.1061   26.619923 0     100 10000    0           100000*

 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*

 *creditLine       9.1856    9.870364 1      75 10000    0          100000*

 *성별에 대 한 범주 수*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>최댓값 및 최솟값 추가하기

계산된 요약 통계를 바탕으로 데이터에 대한 몇 가지 유용한 정보를 발견했습니다. 이런 정보는 나중에 수행될 수 있는 계산에 유용하게 사용될 수 있으므로 이를 데이터 원본에 저장하려고 합니다. 예를 들어 최솟값 및 최댓값은 히스토그램을 계산하는 데에 사용될 수 있습니다. 이러한 이유로 **RxSqlServerData** 데이터 원본에 최댓값 및 최솟값을 추가해보겠습니다.

다행히도 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 정수 데이터를 범주 비율 데이터로 효율적으로 변환할 수 있는 최적화된 함수를 제공합니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 앞에서 만든 `ccColInfo` 변수를 사용하여 데이터 원본의 열을 정의합니다.
  
    또한 열 목록에 몇 가지 새로운 계산 열을(`numTrans`, `numIntlTrans`, 및 `creditLine`) 추가하십시오.
  
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
  
    이제 `sqlFraudDS` 데이터 원본은 `ccColInfo`에 들어있던 정보를 이용해 새로운 열을 포함합니다.
  

이 시점에서 수정하면 R의 데이터 원본에만 영향을 끼칩니다. 즉 어떤 데이터도 아직 데이터베이스 테이블에 기록되지 않았습니다. 하지만 시각화 및 요약을 수행하기 위해 `sumOut` 변수에 저장된 데이터를 사용할 수 있습니다. 다음 단계에서 계산 환경을 전환하는 동안 이 작업을 하는 방법에 대해 알아봅니다.

> [!TIP]
> 현재 사용하고 있는 계산 환경을 잊은 경우 `rxGetComputeContext()`를 실행하십시오.  반환 값이 "RxLocalSeq Compute Context" 라면 로컬 계산 환경을 사용하고 있음을 나타냅니다.

## <a name="next-step"></a>다음 단계

[R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>이전 단계

[계산 컨텍스트 정의 및 사용](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
