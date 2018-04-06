---
title: 쿼리 및 수정 (SQL과 R 심층 분석)에서 SQL Server 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: f860eeaee25f76f4267f1bbee865ed74c12febd9
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="query-and-modify-the-sql-server-data-sql-and-r-deep-dive"></a>쿼리 및 SQL Server 데이터 (SQL과 R 심층 분석)를 수정 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이제 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드했으므로 앞서 만든 데이터 원본을 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 R 함수에 대한 인수로 사용하여 변수에 대한 기본 정보를 가져오고 요약 및 히스토그램을 생성합니다.

이 단계에서는 몇 가지 빠른 분석을 수행한 다음 데이터를 강화하도록 데이터 원본을 다시 사용합니다.

## <a name="query-the-data"></a>데이터 쿼리

먼저, 열과 해당 데이터 형식 목록을 가져옵니다.

1.  함수를 사용 하 여 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 분석 하려는 데이터 원본을 지정 합니다.

    RevoScaleR의 버전을 따라 사용할 수도 있습니다 [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames)합니다. 
  
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


## <a name="modify-metadata"></a>메타 데이터를 수정 합니다.

모든 변수가 정수로 저장되었지만 일부 변수는 범주형 데이터를 나타내며 R에서는 *요인(factor) 변수* 라고 합니다. 예를 들어 *state* 열에는 50개 주와 콜롬비아 특별구에 대한 식별자로 사용되는 숫자가 포함되어 있습니다.   데이터를 더 쉽게 이해하기 위해 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함 하는 문자열 벡터 만들고 원래 정수 식별자에 이러한 범주 값을 매핑합니다. 다음에서 새 변수를 사용 하 여는 *colInfo* 인수를 추가 하는이 열이 처리는 비율을 지정 합니다. 데이터를 분석 하거나 이동할 때마다 약어가 사용 되 고 열을 인수로 처리 됩니다.

을 요소로 사용하기 전에 열을 약어에 매핑하면 실제로 성능도 향상됩니다. 자세한 내용은 [R 및 데이터 최적화](..\r\r-and-data-optimization-r-services.md)를 참조하세요.

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
