---
title: SQL Server 및 XDF 파일 (SQL과 R 심층 분석) 간 데이터 이동 | Microsoft Docs
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
ms.openlocfilehash: fc0370401338cf5332c57f7db8f62dbbba79d982
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>SQL Server 및 XDF 파일 (SQL과 R 심층 분석) 간 데이터 이동
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 단계에서는 파일을 사용 하는 XDF 원격 및 로컬 컴퓨팅 컨텍스트 간에 데이터를 전송할 방법을 배웁니다. 데이터 파일에에서 저장할 XDF 데이터에서 변환을 수행할 수 있습니다.

파일에 데이터를 사용 하 여 새을 만들고 완료 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 함수 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 고.xdf 파일 및 데이터 프레임 간의 변환을 수행 하는 데이터에 변환을 적용할 수 있습니다.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF 파일에서 SQL Server 테이블 만들기

이 연습에서는 신용 카드 사기 데이터 다시 합니다. 이 시나리오에서는 California, Oregon 및 Washington 주의 사용자에 대한 몇 가지 추가 분석을 수행하라는 요청을 받았습니다. 보다 효율적으로 결정 로컬 컴퓨터에만 이러한 상태에 대 한 데이터를 저장 하 고 변수 성별, 카드 소유자, 상태 및 잔액으로 작업 합니다.

1. 다시 사용 된 `stateAbb` 변수를 포함 하 고, 새 변수를 쓸 수준 식별 이전 만든 `statesToKeep`합니다.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **결과**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. SQL server에서를 통해 해제 하려는 데이터 정의 사용 하 여는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다.  나중에으로이 변수를 사용 하는 *inData* 에 대 한 인수 **rxImport**합니다.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    줄 바꿈 또는 탭 등의 숨겨진 문자가 쿼리에 없는지 확인합니다.
  
3. R에서 데이터로 작업할 때 사용할 열을 다음으로 정의 예를 들어 더 작은 데이터 집합에 필요한 세 개의 요소 수준, 쿼리만 세 가지 상태에 대 한 데이터를 반환 하기 때문에 합니다.  적용 된 `statesToKeep` 변수를 포함 하도록 올바른 수준 식별 합니다.
  
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
    
    [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 함수 로컬 XDF 파일에 지원 되는 데이터 소스에서 데이터를 가져올 수 있습니다. 하지만 동일한 쿼리를 반복 해 실행 되지 않도록 데이터에 대해 많은 다르게 분석 하려는 경우 데이터의 로컬 복사본을 사용 하는 것이 편리 합니다.

5. 이전에 인수로 정의 된 변수를 전달 하 여 데이터 원본 개체를 만들 **RxSqlServerData**합니다.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 호출 **rxImport** 라는 파일에 데이터를 쓸 `ccFraudSub.xdf`, 현재 작업 디렉터리에 있습니다.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    `localDs` 에서 반환 된 개체는 **rxImport** 함수는는 간단한 **RxXdfData** 나타내는 데이터 원본 개체는 `ccFraud.xdf` 데이터 파일을 디스크에 로컬로 저장 합니다.
  
7. XDF 파일에 대해 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 를 호출하여 데이터 스키마가 같은지 확인합니다.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **결과**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. 이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원본 데이터와 마찬가지로 다양한 R 함수를 호출하여 `localDs` 개체를 분석할 수 있습니다. 예를 들어 성별 요약할 수 있습니다.
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

이제 계산 컨텍스트 사용 및 다양한 데이터 원본 작업 방법을 익혔으므로 재미있는 작업을 시도해 보겠습니다. 다음 및 최종 단원에서는 원격 서버의 사용자 지정 R 함수를 실행 하는 간단한 시뮬레이션을 만들 수 있습니다.

## <a name="next-step"></a>다음 단계

[간단한 시뮬레이션 만들기](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>이전 단계

[로컬 계산 컨텍스트에서 데이터 분석](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



