---
title: "만들기 및 R 스크립트 (SQL과 R 심층 분석)를 실행 합니다. | Microsoft Docs"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3f26a5850ffe3245029486a2be4406790e36b6ab
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>만들기 및 R 스크립트 (SQL과 R 심층 분석)를 실행 합니다.

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이제 데이터 원본을 설정하고 하나 이상의 계산 컨텍스트를 설정했으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 몇 가지 고성능 R 스크립트를 실행할 준비가 되었습니다.  이 단원 server 계산 컨텍스트를 사용 하 여 몇 가지 일반적인 시스템 작업 학습을 수행 하려면:

- 데이터 시각화 및 몇 가지 요약 통계 생성
- 선형 회귀 모델 만들기
- 로지스틱 회귀 모델 만들기
- 새 데이터 점수 매기기 및 점수 히스토그램 만들기

## <a name="change-compute-context-to-the-server"></a>계산 서버에는 컨텍스트 변경

R 코드를 실행하기 전에 *현재* 또는 *활성* 계산 컨텍스트를 지정해야 합니다.

1. R을 사용하여 이미 정의한 계산 컨텍스트를 활성화하려면 다음과 같이 **rxSetComputeContext** 함수를 사용합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    이 문을 실행 하는 즉시 모든 이후 계산에 진행는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 지정 된 컴퓨터는 *sqlCompute* 매개 변수입니다.
  
2. 워크스테이션에서 R 코드를 실행하려는 경우  **local** 키워드를 사용하여 계산 컨텍스트를 다시 로컬 컴퓨터로 전환할 수 있습니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    이 함수에서 지원하는 다른 키워드 목록을 보려면 R 명령줄에서 `help("rxSetComputeContext")` 를 입력합니다.
  
3. 계산 컨텍스트를 지정하면 변경할 때까지 활성 상태로 유지됩니다. 그러나 원격 서버 컨텍스트에서 실행할 수 *없는* 모든 R 스크립트는 로컬로 실행됩니다.

## <a name="compute-some-summary-statistics"></a>일부 요약 통계를 계산 합니다.

계산 컨텍스트 작동 방식을 보려면 사용 하 여 일부 요약 통계를 생성을 시도 `sqlFraudDS` 데이터 원본입니다.  기억, 데이터 원본 개체에는 방금; 사용 하는 데이터 정의 계산 컨텍스트를 바뀌지 않습니다.

+ 로컬로 요약을 수행 하려면 **rxSetComputeContext** 지정는 _로컬_ 키워드입니다.
+ SQL Server 컴퓨터에서 같은 계산을 만들려면 앞에서 정의한 SQL 계산 컨텍스트로 전환합니다.

1. 호출 된 [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) 함수 및 수식 및 데이터 원본 등의 필수 인수를 전달 하 고 결과 변수에 할당 `sumOut`합니다.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어 여러 요약 기능을 제공 하지만 **rxSummary** 다양 한 원격 계산 컨텍스트를 포함 하 여 실행을 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 유사한 기능에 대 한 정보를 참조 하십시오. [RevoScaleR을 사용 하 여 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)합니다.
  
2. 처리가 완료 되는 경우의 내용을 인쇄할 수 있습니다는 `sumOut` 콘솔에 변수입니다.
  
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

 *creditLine 9.1856 9.870364 1 75 10000 0 100000*

 *성별에 대 한 범주 수*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>최대 및 최소 값 추가

계산된 요약 통계에 따라 데이터에 대한 몇 가지 유용한 정보를 발견했으며 추가 계산에 사용하기 위해 이 정보를 데이터 원본에 저장하려고 합니다. 예를 들어 히스토그램을 계산 하는 최소 및 최대 값을 사용할 수 있습니다. 이러한 이유로 추가 하 고가 및 저가 값은 **RxSqlServerData** 데이터 원본입니다.

다행히 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 범주 비율 데이터에 정수 데이터를 효율적으로 변환할 수 있는 최적화 된 기능을 포함 합니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 앞에서 만든 `ccColInfo` 변수를 사용하여 데이터 원본의 열을 정의합니다.
  
    또한 일부 새 계산 열을 추가 (`numTrans`, `numIntlTrans`, 및 `creditLine`)을 열 컬렉션입니다.
  
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
  
3. 업데이트 된 버전을 만들려면 다음 문을 적용 열 컬렉션에 있는 업데이트 것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 앞에서 정의한 데이터 원본.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    `sqlFraudDS` 데이터 원본을 사용 하 여 추가 하는 새 열이 포함 이제 `ccColInfo`합니다.
  

수정만 R;에서 데이터 원본 개체에 영향을 줄이 시점에서 새 데이터가 아직 데이터베이스 테이블에 기록 된 했습니다. 그러나에서 수집 된 데이터를 사용할 수는 `sumOut` 변수를 시각화 및 요약을 만듭니다. 다음 단계 계산 컨텍스트를 전환 하는 동안이 작업을 수행 하는 방법에 설명 합니다.

> [!TIP]
> 사용 하는 계산 컨텍스트를 잊은 경우 실행 `rxGetComputeContext()`합니다.  반환 값이 "RxLocalSeq 계산 컨텍스트" 로컬 계산 컨텍스트에서 실행을 나타냅니다.

## <a name="next-step"></a>다음 단계

[R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>이전 단계

[계산 컨텍스트 정의 및 사용](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
