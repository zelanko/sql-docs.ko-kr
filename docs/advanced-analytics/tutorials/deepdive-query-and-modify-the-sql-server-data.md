---
title: SQL Server 데이터 (SQL 및 R 심층 분석) 쿼리 및 수정 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 57fff9b8ddfd6507876bd6eb174a127d70d0b916
ms.sourcegitcommit: aa9d2826e3c451f4699c0e69c9fcc8a2781c6213
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45975652"
---
# <a name="query-and-modify-the-sql-server-data-sql-and-r-deep-dive"></a>SQL Server 데이터 (SQL 및 R 심층 분석) 쿼리 및 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)과 SQL Server를 함께 쓰는 방법에 대한 데이터 과학 심층 분석 자습서의 일부입니다.

이제 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 불러왔으므로 앞서 만든 데이터 원본을 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 R 함수에 대한 인수로 사용하여 변수에 대한 기본 정보를 가져오고 요약 및 히 스토그램을 생성할 수 있습니다.

이 단계에서는 간단한 분석을 수행한 다음 데이터를 강화하도록 데이터 원본을 다시 사용합니다.

## <a name="query-the-data"></a>데이터를 쿼리 합니다.

먼저, 열과 해당 데이터 형식 목록을 가져옵니다.

1.  [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 함수를 사용하여  분석하려는 데이터 원본을 지정합니다.

    RevoScaleR의 버전에 따라 사용할 수도 있습니다 [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames)합니다. 
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **결과**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender, Type: integer*
    
    *Var 3: state, Type: integer*
    
    *Var 4: cardholder, Type: integer*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*


## <a name="modify-metadata"></a>메타 데이터 수정하기

모든 변수가 정수로 저장 되지만 일부 변수 라고 하는 범주 데이터를 나타내며 *요소 변수* R에서 예를 들어 열 *상태* 50 개 주와 콜롬비아 특별구의 식별자로 사용 하는 숫자를 포함 합니다.  데이터를 더 쉽게 이해하기 위해 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함 하는 문자열 벡터를 만들고 이러한 범주 값을 원래 정수 식별자에 매핑됩니다. 새 변수를 사용 하 여는 *colInfo* 인수에는이 열이 요소로 처리 되도록 지정 합니다. 를 데이터를 분석 하거나 이동할 때마다 약어가 사용 되 고 열 요소로 처리 됩니다.

열을 요인으로 사용하지 말고 약어에 매핑하는 것은 실제로 성능 향상의 요인이 됩니다. 자세한 내용은 [R 및 데이터 최적화](..\r\r-and-data-optimization-r-services.md)를 참조하세요.

1. 먼저 R 변수 *stateAbb*를 만들고 다음과 같이 추가할 문자열 벡터를 정의합니다.
  
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
  
3. 업데이트된 데이터를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본을 만들려면 이전과 같이 **RxSqlServerData** 함수를 호출하되, *colInfo* 인수를 추가합니다.
  
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
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender 2 factor levels: Male Female*
    
    *Var 3: state 51 factor levels: AK AL AR AZ CA ...  VT WA WI WV WY*
    
    *Var 4: cardholder 2 factor levels: Principal Secondary*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

이제 지정한 변수 3개(_gender_, _state_, _cardholder_)가 요인으로 처리됩니다.

## <a name="next-step"></a>다음 단계

[계산 컨텍스트 정의 및 사용](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>이전 단계

[RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
