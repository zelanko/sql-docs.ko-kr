---
title: RevoScaleR를 사용 하 여 SQL Server 데이터 쿼리 및 수정
description: SQL Server에서 R 언어를 사용 하 여 데이터를 쿼리 및 수정 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3fb28d287c7b92e9b399aa7bc0bb606c618eed47
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469793"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>SQL Server 데이터 쿼리 및 수정 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이전 단원에서는 데이터를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 했습니다. 이 단계에서는 **RevoScaleR**를 사용 하 여 데이터를 탐색 하 고 수정할 수 있습니다.

> [!div class="checklist"]
> * 변수에 대 한 기본 정보 반환
> * 원시 데이터에서 범주 데이터 만들기

범주 데이터 또는 *요소 변수*는 예비 데이터 시각화에 유용 합니다. 이를 히스토그램에 대 한 입력으로 사용 하 여 변수 데이터의 모양을 파악할 수 있습니다.

## <a name="query-for-columns-and-types"></a>열 및 형식에 대 한 쿼리

R IDE 또는 RGui .exe를 사용 하 여 R 스크립트를 실행 합니다. 

먼저, 열과 해당 데이터 형식 목록을 가져옵니다. [Rxgetvarinfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 함수를 사용 하 여 분석할 데이터 원본을 지정할 수 있습니다. **RevoScaleR**버전에 따라 [Rxgetvarnames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames)를 사용할 수도 있습니다. 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**결과**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>범주 데이터 만들기

모든 변수가 정수로 저장 되지만 일부 변수는 R에서 *요소 변수* 라고 하는 범주 데이터를 나타냅니다. 예를 들어 열 *상태* 에는 50의 식별자로 사용 되는 숫자와 특별구의 학구가 포함 됩니다. 데이터를 더 쉽게 이해하기 위해 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함 하는 문자열 벡터를 만든 다음 이러한 범주 값을 원래 정수 식별자에 매핑합니다. 그런 다음 *colInfo* 인수에서 새 변수를 사용 하 여이 열이 요소로 처리 되도록 지정 합니다. 데이터를 분석 하거나 이동할 때마다 약어가 사용 되며 열이 요소로 처리 됩니다.

열을 요인으로 사용하지 말고 약어에 매핑하는 것은 실제로 성능 향상의 요인이 됩니다. 자세한 내용은 [R 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)를 참조하세요.

1. 먼저 다음과 같이 R 변수를 만들고 *stateAbb*에 추가할 문자열의 벡터를 정의 합니다.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 다음으로, 범주 수준(주 약어)과 기존 정수 값 간의 매핑을 지정하는 *ccColInfo*라는 열 정보 개체를 만듭니다.
  
    이 문은 성별 및 카드 소유자에 대한 요인 변수도 만듭니다.
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. 업데이트 된 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하는 데이터 원본을 만들려면 이전 처럼 **RxSqlServerData** 함수를 호출 하지만 *colInfo* 인수를 추가 합니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - *table* 매개 변수에 대해 앞에서 만든 데이터 원본을 포함하는 *sqlFraudTable*변수를 전달합니다.
    - *colInfo* 매개 변수에 대해 열 데이터 형식 및 요소 수준을 포함하는 *ccColInfo* 변수를 전달합니다.

4.  이제 **rxGetVarInfo** 함수를 사용하여 새 데이터 원본의 변수를 확인할 수 있습니다.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **결과**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

이제 지정한 변수 3개(*gender*, *state*, *cardholder*)가 요인으로 처리됩니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [계산 컨텍스트 정의 및 사용](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)