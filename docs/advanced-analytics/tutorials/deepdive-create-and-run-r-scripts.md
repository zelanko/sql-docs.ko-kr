---
title: "만들기 및 R 스크립트 실행 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ff840a886e281fcb1f86fa7f79db6c187538766d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="create-and-run-r-scripts"></a>만들기 및 R 스크립트 실행

이제 데이터 원본을 설정하고 하나 이상의 계산 컨텍스트를 설정했으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 몇 가지 고성능 R 스크립트를 실행할 준비가 되었습니다.  이 단원에서는 서버 계산 컨텍스트를 사용하여 몇 가지 일반적인 Machine Learning 작업을 수행합니다.

- 데이터 시각화 및 몇 가지 요약 통계 생성
- 선형 회귀 모델 만들기
- 로지스틱 회귀 모델 만들기
- 새 데이터 점수 매기기 및 점수 히스토그램 만들기

## <a name="change-compute-context-to-the-server"></a>계산 컨텍스트를 서버로 변경

R 코드를 실행하기 전에 *현재* 또는 *활성* 계산 컨텍스트를 지정해야 합니다.

1. R을 사용하여 이미 정의한 계산 컨텍스트를 활성화하려면 다음과 같이 **rxSetComputeContext** 함수를 사용합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    이 문을 실행하는 즉시 이후의 모든 계산은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlCompute *매개 변수에 지정된* 컴퓨터에서 수행됩니다.
  
2. 워크스테이션에서 R 코드를 실행하려는 경우  **local** 키워드를 사용하여 계산 컨텍스트를 다시 로컬 컴퓨터로 전환할 수 있습니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    이 함수에서 지원하는 다른 키워드 목록을 보려면 R 명령줄에서 `help("rxSetComputeContext")` 를 입력합니다.
  
3. 계산 컨텍스트를 지정하면 변경할 때까지 활성 상태로 유지됩니다. 그러나 원격 서버 컨텍스트에서 실행할 수 *없는* 모든 R 스크립트는 로컬로 실행됩니다.

## <a name="compute-summary-statistics"></a>계산 요약 통계

계산 컨텍스트가 작동하는 방식을 확인하려면 *sqlFraudDS* 데이터 원본을 사용하여 몇 가지 요약 통계를 생성해 보세요.  데이터 원본 개체는 사용할 데이터만 정의하고 계산 컨텍스트를 변경하지는 않는다는 점을 기억하세요.

+ 로컬에서 요약을 수행하려면 **rxSetComputeContext** 를 사용하고 "local" 키워드를 지정합니다.
+ SQL Server 컴퓨터에서 같은 계산을 만들려면 앞에서 정의한 SQL 계산 컨텍스트로 전환합니다.

1. **rxSummary** 함수를 호출하고 수식 및 데이터 원본과 같은 필수 인수를 전달하고 결과를 *sumOut*변수에 할당합니다.
  
    ```R
    sumOut \<- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어 요약에서는 다양 한 기능을 제공 하지만 rxSummary 다양 한 원격 계산 컨텍스트를 포함 하 여 실행을 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  유사한 함수에 대한 자세한 내용은 [ScaleR reference](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) (ScaleR 참조)의 [Data Summaries](https://msdn.microsoft.com/microsoft-r/scaler/scaler)(데이터 요약)를 참조하세요.
  
2. 처리가 완료되면 *sumOut* 변수의 내용을 콘솔에 출력할 수 있습니다.
  
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

## <a name="add-maximum-and-minimum-values"></a>최대값 및 최소값 추가

계산된 요약 통계에 따라 데이터에 대한 몇 가지 유용한 정보를 발견했으며 추가 계산에 사용하기 위해 이 정보를 데이터 원본에 저장하려고 합니다. 예를 들어 히스토그램을 계산 하 고가 및 저가 값 RxSqlServerData 데이터 소스에 추가 하려는 데는 최소 및 최대 값을 사용할 수 있습니다.

다행히 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에는 매우 효율적으로 정수 데이터를 범주 인수 데이터로 변환할 수 있는 최적화된 함수가 포함되어 있습니다.

1. 먼저 몇 가지 임시 변수를 설정합니다.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 앞에서 만든 *ccColInfo* 변수를 사용하여 데이터 원본의 열을 정의합니다.
  
    또한 몇 가지 새로운 계산 열(*numTrans*, *numIntlTrans*및 *creditLine*)을 열 컬렉션에 추가합니다.
  
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
  
3. 열 컬렉션을 업데이트한 후 다음 문을 적용하여 앞에서 정의한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본의 업데이트된 버전을 만들 수 있습니다.
  
    ```R
    sqlFraudDS \<- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    이제 *sqlFraudDS* 데이터 원본에 *ccColInfo*에 추가된 새 열이 포함됩니다.
  
  이러한 수정 내용은 R의 데이터 원본 개체에만 영향을 주고 데이터베이스 테이블에는 아직 새 데이터가 기록되지 않습니다. 그러나 *sumOut* 변수에서 캡처된 데이터를 사용하여 시각화 및 요약을 만들 수 있습니다. 다음 단계에서는 계산 컨텍스트를 전환하는 동안 이 작업을 수행하는 방법을 알아봅니다.

> [!TIP]
> 사용 하는 계산 컨텍스트를 잊은 경우 실행 `rxGetComputeContext()`합니다.  반환 값이 `RxLocalSeq Compute Context` 로컬 계산 컨텍스트에서 실행을 나타냅니다.

## <a name="next-step"></a>다음 단계

[R을 사용 하 여 SQL Server 데이터를 시각화 합니다.](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>이전 단계

[계산 컨텍스트를 사용 및 정의](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

