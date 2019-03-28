---
title: RevoScaleR-SQL Server Machine Learning을 사용 하 여 SQL Server 데이터 쿼리 및 수정
description: 쿼리 및 SQL Server에서 R 언어를 사용 하 여 데이터를 수정 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d2768399ecd3d504e5bc51d4c7cbd151488782a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513140"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>SQL Server 데이터 (SQL Server 및 RevoScaleR 자습서) 쿼리 및 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이전 단원에서는 데이터를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 단계에서는 탐색 고 사용 하 여 데이터를 수정할 수 있습니다 **RevoScaleR**:

> [!div class="checklist"]
> * 변수에 대 한 기본 정보를 반환 합니다.
> * 원시 데이터에서 범주 데이터 만들기

범주 데이터 또는 *요소 변수*, 예비 데이터 시각화에 유용 합니다. 변수 데이터 모양을 파악할에 히스토그램에 대 한 입력으로 사용할 수 있습니다.

## <a name="query-for-columns-and-types"></a>열 및 형식에 대 한 쿼리

R 스크립트를 실행 하려면 R IDE 또는 RGui.exe를 사용 합니다. 

먼저, 열과 해당 데이터 형식 목록을 가져옵니다. 함수를 사용할 수 있습니다 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 분석 하려는 데이터 원본을 지정 합니다. 버전에 따라 **RevoScaleR**를 사용할 수도 있습니다 [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames)합니다. 
  
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

모든 변수가 정수로 저장 되지만 일부 변수 라고 하는 범주 데이터를 나타내며 *요소 변수* R에서 예를 들어 열 *상태* 50 개 주와 콜롬비아 특별구의 식별자로 사용 하는 숫자를 포함 합니다. 데이터를 더 쉽게 이해하기 위해 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함 하는 문자열 벡터를 만들고 이러한 범주 값을 원래 정수 식별자에 매핑됩니다. 새 변수를 사용 하 여는 *colInfo* 인수에는이 열이 요소로 처리 되도록 지정 합니다. 를 데이터를 분석 하거나 이동할 때마다 약어가 사용 되 고 열 요소로 처리 됩니다.

열을 요인으로 사용하지 말고 약어에 매핑하는 것은 실제로 성능 향상의 요인이 됩니다. 자세한 내용은 [R 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)를 참조하세요.

1. 먼저 R 변수를 만듭니다 *stateAbb*, 후에 다음과 같이 추가할 문자열 벡터를 정의 하 고 있습니다.
  
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
  
3. 만들려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출이 업데이트 된 데이터를 사용 하는 데이터 원본 합니다 **RxSqlServerData** 이전과 마찬가지로 작동 하지만 추가 *colInfo* 인수.
  
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