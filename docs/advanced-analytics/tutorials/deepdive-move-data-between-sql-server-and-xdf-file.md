---
title: "SQL Server 및 XDF 파일 간에 데이터를 이동 | Microsoft Docs"
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
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1db44423f71f1808d99a9611062bdc8291640ece
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="move-data-between-sql-server-and-xdf-file"></a>SQL Server와 XDF 파일 간에 데이터 이동

로컬 계산 컨텍스트에서 작업 하는 경우에 액세스할 수 있는 두 로컬 데이터 파일 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 (RxSqlServerData 데이터 원본으로 정의 됨).

이 섹션에서는 데이터 변환을 수행할 수 있도록 데이터를 가져와 로컬 컴퓨터의 파일에 저장하는 방법을 알아봅니다. 완료 되 면 데이터 파일에 데 사용할 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxDataStep를 사용 하 여 테이블입니다.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF 파일에서 SQL Server 테이블 만들기

RxImport 함수를 사용 하면 로컬 XDF 파일에 모든 지원 되는 데이터 원본에서 데이터를 가져올 수 있습니다. 로컬 파일을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장된 데이터에 대해 다양한 분석을 수행하고 동일한 쿼리를 반복해서 실행하지 않으려는 경우에 편리할 수 있습니다.

이 연습에서는 신용 카드 사기 데이터를 다시 사용합니다. 이 시나리오에서는 California, Oregon 및 Washington 주의 사용자에 대한 몇 가지 추가 분석을 수행하라는 요청을 받았습니다. 효율성을 높이기 위해 해당 주에 대한 데이터만 로컬 컴퓨터에 저장하고 성별, 카드 소유자, 주, 잔액 변수를 사용하기로 결정했습니다.

1. 앞에서 만든 *stateAbb* 벡터를 다시 사용하여 포함할 수준을 식별한 다음 콘솔에 새 *statesToKeep*변수를 출력합니다.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **결과**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. 이제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 SQL Server에서 가져올 데이터를 정의합니다.  나중에 이 변수를 *rxImport* 에 대한 *inData*인수로 사용합니다.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    줄 바꿈 또는 탭 등의 숨겨진 문자가 쿼리에 없는지 확인합니다.
  
3. 다음에 R에서 데이터로 작업할 때 사용할 열을 정의 예를 들어 더 작은 데이터 집합에 필요 하면 세 개의 요소 수준, 쿼리는 3 개의 상태에 대 한 데이터를 반환 합니다.  *statesToKeep* 변수를 다시 사용하여 포함할 올바른 수준을 식별할 수 있습니다.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 계산 컨텍스트를 설정 **로컬**로컬 컴퓨터에서 사용할 수 있는 모든 데이터를 원하는 때문에 있습니다.
  
    ```R
    rxSetComputeContext("local")
    ```
  
5. RxSqlServerData에 인수로 정의 된 모든 변수를 전달 하 여 데이터 원본 개체를 만듭니다.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 그런 다음 호출 **rxImport** 라는 파일에 데이터를 쓸 `ccFraudSub.xdf`, 현재 작업 디렉터리에 있습니다.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    *localDs* rxImport 함수에서 반환 된 개체는 디스크에 로컬로 저장 ccFraud.xdf 데이터 파일을 표시 하는 간단한 RxXdfData 데이터 원본 개체입니다.
  
7. 데이터 스키마 동일한 지 확인 하려면 XDF 파일 rxGetVarInfo를 호출 합니다.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **결과**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. 이제 *의 원본 데이터와 마찬가지로 다양한 R 함수를 호출하여* localDs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]개체를 분석할 수 있습니다. 예를 들어
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

이제 계산 컨텍스트 사용 및 다양한 데이터 원본 작업 방법을 익혔으므로 재미있는 작업을 시도해 보겠습니다. 다음 최종 단원에서는 사용자 지정 R 함수를 사용하여 간단한 시뮬레이션을 만들고 원격 서버에서 실행합니다.

## <a name="next-step"></a>다음 단계

[간단한 시뮬레이션을 만들어서](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>이전 단계

[로컬 계산 컨텍스트에서 데이터 분석](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)




