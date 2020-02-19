---
title: XDF 파일로 데이터 이동
description: 'RevoScaleR 자습서 13: SQL Server에서 XDF 및 R 언어를 사용하여 데이터를 이동하는 방법입니다.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d55bdf59eef4c8e7baa0553487a92a06e76326a9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947372"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server와 XDF 파일 간에 데이터 이동(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 13에 해당됩니다.

이 자습서에서는 XDF 파일을 사용하여 원격 및 로컬 계산 컨텍스트 사이에 데이터를 전송하는 방법을 알아봅니다. XDF 파일에 데이터를 저장하면 데이터에 대해 변환을 수행할 수 있습니다.

완료되었으면 파일의 데이터를 사용하여 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들 수 있습니다. [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수는 데이터에 변환을 적용할 수 있으며, 데이터 프레임과 .xdf 파일 사이에 변환을 수행합니다.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF 파일에서 SQL Server 테이블 만들기

이 연습에서는 신용 카드 사기 데이터를 다시 사용합니다. 이 시나리오에서는 California, Oregon 및 Washington 주의 사용자에 대한 몇 가지 추가 분석을 수행하라는 요청을 받았습니다. 효율성을 높이기 위해 해당 주에 대한 데이터만 로컬 컴퓨터에 저장하고 성별, 카드 소유자, 주, 잔액 변수만 사용하기로 결정했습니다.

1. 앞에서 만든 `stateAbb` 변수를 다시 사용하여 포함할 수준을 식별하고 이를 새 변수 `statesToKeep`로 작성합니다.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **결과**
    
    CA|또는|WA
    ----|----|----
    5|38|48
    
2. [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 SQL Server에서 가져올 데이터를 정의합니다.  나중에 이 변수를 **rxImport**에 대한 *inData* 인수로 사용합니다.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    줄 바꿈 또는 탭 등의 숨겨진 문자가 쿼리에 없는지 확인합니다.
  
3. 그런 후 R의 데이터를 작업할 때 사용할 열을 정의합니다. 예를 들어 크기가 작은 데이터 세트에서는 쿼리가 3개 상태에 대해서만 데이터를 반환하기 때문에 3개의 요소 수준만 필요합니다.  `statesToKeep` 변수를 적용하여 포함할 올바른 수준을 식별합니다.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 로컬 컴퓨터에서 모든 데이터를 사용할 수 있도록 컴퓨팅 컨텍스트를 **local**로 설정합니다.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 함수는 지원되는 데이터 원본의 데이터를 로컬 XDF 파일로 가져올 수 있습니다. 데이터에 대해 여러 분석을 수행해야 하지만 동일 쿼리를 계속해서 반복적으로 실행하고 싶지 않을 때는 데이터의 로컬 복사본을 사용하는 것이 편리합니다.

5. 이전에 정의된 변수를 **RxSqlServerData**에 인수로 전달하여 데이터 원본 개체를 만듭니다.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 현재 작업 디렉터리에서 **rxImport**를 호출하여 이름이 `ccFraudSub.xdf`인 파일에 데이터를 기록합니다.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    **rxImport** 함수에서 반환된 `localDs` 개체는 디스크에 로컬로 저장된 `ccFraud.xdf` 데이터 파일을 나타내는 경량 **RxXdfData** 데이터 원본 개체입니다.
  
7. XDF 파일에 대해 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 를 호출하여 데이터 스키마가 같은지 확인합니다.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **결과**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. 이제 SQL Server의 원본 데이터와 마찬가지로 다양한 R 함수를 호출하여 **localDs** 개체를 분석할 수 있습니다. 예를 들어 성별을 기준으로 요약할 수 있습니다.
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>다음 단계

이 자습서를 끝으로 **RevoScaleR** 및 SQL Server에 대해 여러 파트로 구성된 자습서 시리즈를 마칩니다. 여기에서는 여러 가지 데이터 관련 및 계산 관련 개념을 소개하고, 사용자의 고유 데이터 및 프로젝트 요구 사항에 맞게 작업을 진행하기 위한 기본 사항들을 살펴봤습니다.

**RevoScaleR**에 대한 지식을 더 넓히기 위해서는 R 자습서 목록으로 돌아가서 누락된 연습을 진행하시기 바랍니다. 또는 목차에서 방법 도움말 문서들을 검토하여 일반적인 작업들에 대한 정보를 확인하세요.

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](sql-server-r-tutorials.md)