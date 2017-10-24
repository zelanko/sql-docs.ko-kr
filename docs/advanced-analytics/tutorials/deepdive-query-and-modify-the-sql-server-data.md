---
title: "쿼리 및 SQL Server 데이터를 수정 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4970a681733d8920b9eef6b27023f9ae1c7ce981
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="query-and-modify-the-sql-server-data"></a>SQL Server 데이터 쿼리 및 수정

이제 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드했으므로 만든 데이터 원본을 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 R 함수에 대한 인수로 사용하여 변수에 대한 기본 정보를 가져오고 요약 및 히스토그램을 생성합니다.

이 단계에서는 몇 가지 빠른 분석을 수행 하 고 다음 데이터를 강화 하도록 데이터 원본을 다시 사용 합니다.

## <a name="query-the-data"></a>데이터 쿼리

먼저, 열과 해당 데이터 형식 목록을 가져옵니다.

1.  함수를 사용 하 여 **rxGetVarInfo** 분석 하려는 데이터 원본을 지정 합니다.
  
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


## <a name="modify-metadata"></a>메타데이터 수정

모든 변수가 정수로 저장되었지만 일부 변수는 범주 데이터를 나타내며 R에서는 *요소 변수* 라고 합니다. 예를 들어 *주* 열에는 50개 주와 콜롬비아 특별구의 식별자로 사용되는 숫자가 포함되어 있습니다.  데이터를 더 쉽게 이해하려면 숫자를 주 약어 목록으로 바꿉니다.

이 단계에서는 약어를 포함하는 문자열 벡터를 제공한 다음 이러한 범주 값을 원래 정수 식별자에 매핑합니다. 이 변수가 준비된 후 *colInfo* 인수에 이 변수를 사용하여 이 열이 요소로 처리되도록 지정합니다. 그 후에는 이 데이터가 분석되거나 이 데이터를 가져올 때마다 약어가 사용되고 열이 요소로 처리됩니다.

1. 먼저 R 변수 *stateAbb*를 만들고 다음과 같이 추가할 문자열 벡터를 정의합니다.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 다음으로, 범주 수준(주 약어)과 기존 정수 값 간의 매핑을 지정하는 *ccColInfo*라는 열 정보 개체를 만듭니다.
  
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
  
3. 업데이트된 데이터를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본을 만들려면 이전과 같이 *RxSqlServerData* 함수를 호출하되, *colInfo* 인수를 추가합니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - *table* 매개 변수에 대해 앞에서 만든 데이터 원본을 포함하는 *sqlFraudTable*변수를 전달합니다.
    - *colInfo* 매개 변수에 대해 열 데이터 형식 및 요소 수준을 포함하는 *ccColInfo* 변수를 전달합니다.
    - 열을 요소로 사용하기 전에 열을 약어에 매핑하면 실제로 성능도 향상됩니다. 자세한 내용은 [R 및 데이터 최적화](https://msdn.microsoft.com/library/mt723575.aspx)를 참조하세요.
  
4.  이제 새 데이터 원본에 변수를 보려면 함수 rxGetVarInfo를 사용할 수 있습니다.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **결과**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: 2 단계 수준을 성별: 남성 여성*
    
    *Var 3: 51 요소 수준 상태: AK AL AR AZ CA 중... VT WA WI WV WY*
    
    *Var 4: 카드 소유자 2 단계 수준: 보조 보안 주체*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

이제 지정한 변수 3개(_gender_, _state_, _cardholder_)가 요소로 처리됩니다.

## <a name="next-step"></a>다음 단계

[계산 컨텍스트를 사용 및 정의](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>이전 단계

[RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)




