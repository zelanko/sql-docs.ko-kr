---
title: RevoScaleR을 사용하여 SQL 데이터 수정
description: SQL Server에서 R 언어, 특히 RevoScaleR 함수를 사용하여 데이터를 쿼리하고 수정하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 9938cdeca70e4fd7a97c9ce8b9d38035022ce714
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470564"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>SQL Server 데이터 쿼리 및 수정(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 3에 해당됩니다.

이전 자습서에서는 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드했습니다. 이 자습서에서는 **RevoScaleR** 을 사용하여 데이터를 탐색하고 수정할 수 있습니다.

> [!div class="checklist"]
> * 변수에 대한 기본 정보 반환
> * 원시 데이터에서 범주별 데이터 만들기

범주별 데이터 또는 *요소 변수* 는 예비 데이터 시각화에 유용합니다. 히스토그램에 대한 입력으로 사용하여 변수 데이터의 모양을 파악할 수 있습니다.

## <a name="query-for-columns-and-types"></a>열 및 형식에 대한 쿼리

R IDE 또는 RGui.exe를 사용하여 R 스크립트를 실행합니다. 

먼저, 열과 해당 데이터 형식 목록을 가져옵니다. [rxGetVarInfo](/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 함수를 사용하여 분석할 데이터 원본을 지정할 수 있습니다. **RevoScaleR** 버전에 따라 [rxGetVarNames](/machine-learning-server/r-reference/revoscaler/rxgetvarnames)를 사용할 수도 있습니다. 
  
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

## <a name="create-categorical-data"></a>범주별 데이터 만들기

모든 변수가 정수로 저장되었지만 일부 변수는 범주 데이터를 나타내며 R에서는 *요소 변수* 라고 합니다. 예를 들어 *주* 열에는 50개 주와 콜롬비아 특별구의 식별자로 사용되는 숫자가 포함되어 있습니다. 데이터를 더 쉽게 이해하려면 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함하는 문자열 벡터를 만든 다음, 이러한 범주 값을 원래 정수 식별자에 매핑합니다. 그런 다음, *colInfo* 인수에서 새 변수를 사용하여 이 열이 요소로 처리되도록 지정합니다. 데이터를 분석하거나 이동할 때마다 약어가 사용되며 열이 요소로 처리됩니다.

열을 요소로 사용하기 전에 열을 약어에 매핑하면 실제로 성능도 향상됩니다. 자세한 내용은 [R 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)를 참조하세요.

1. 먼저 R 변수 *stateAbb* 를 만들고 다음과 같이 추가할 문자열 벡터를 정의합니다.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 다음으로, 범주 수준(주 약어)과 기존 정수 값 간의 매핑을 지정하는 *ccColInfo* 라는 열 정보 개체를 만듭니다.
  
    이 문은 성별 및 카드 소유자에 대한 요소 변수도 만듭니다.
  
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
  
3. 업데이트된 데이터를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본을 만들려면 이전과 같이 **RxSqlServerData** 함수를 호출하되, *colInfo* 인수를 추가합니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - *table* 매개 변수에 대해 앞에서 만든 데이터 원본을 포함하는 *sqlFraudTable* 변수를 전달합니다.
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

이제 지정한 변수 3개(*gender*, *state*, *cardholder*)가 요소로 처리됩니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [컴퓨팅 컨텍스트 정의 및 사용](../../machine-learning/tutorials/deepdive-define-and-use-compute-contexts.md)