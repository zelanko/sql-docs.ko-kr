---
title: RevoScaleR를 사용 하 여 SQL Server와 XDF 파일 간에 데이터 이동
description: SQL Server에서 XDF 및 R 언어를 사용 하 여 데이터를 이동 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4109399386f119123591bb917f81290eebe7476e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469717"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server와 XDF 파일 간에 데이터 이동 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이 단계에서는 XDF 파일을 사용 하 여 원격 및 로컬 계산 컨텍스트 간에 데이터를 전송 하는 방법에 대해 알아봅니다. XDF 파일에 데이터를 저장 하면 데이터에 대 한 변환을 수행할 수 있습니다.

완료 되 면 파일의 데이터를 사용 하 여 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만듭니다. [Rxdatastep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수는 데이터에 변환을 적용 하 고 데이터 프레임 및 .xdf 파일 간에 변환을 수행할 수 있습니다.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF 파일에서 SQL Server 테이블 만들기

이 연습에서는 신용 카드 사기 데이터를 다시 사용 합니다. 이 시나리오에서는 California, Oregon 및 Washington 주의 사용자에 대한 몇 가지 추가 분석을 수행하라는 요청을 받았습니다. 보다 효율적으로 이러한 상태에 대 한 데이터를 로컬 컴퓨터에 저장 하 고 성별, 카드 소유자, 주 및 잔액의 변수만 사용 하도록 결정 했습니다.

1. 앞에서 만든 `stateAbb` 변수를 다시 사용 하 여 포함할 수준을 식별 하 고 새 `statesToKeep`변수에 씁니다.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **결과**
    
    CA|또는|WA
    ----|----|----
    5|38|48
    
2. 쿼리를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용 하 여 SQL Server에서 가져올 데이터를 정의 합니다.  나중에이 변수를 **Rximport**에 대 한 *indata* 인수로 사용 합니다.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    줄 바꿈 또는 탭 등의 숨겨진 문자가 쿼리에 없는지 확인합니다.
  
3. 그런 다음 R의 데이터로 작업할 때 사용할 열을 정의 합니다. 예를 들어 작은 데이터 집합에는 세 가지 상태에 대 한 데이터만 반환 하기 때문에 세 개의 요소 수준만 필요 합니다.  `statesToKeep` 변수를 적용 하 여 포함할 올바른 수준을 식별 합니다.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 로컬 컴퓨터에서 모든 데이터를 사용할 수 있도록 하려면 계산 컨텍스트를 **로컬**으로 설정 합니다.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [Rximport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 함수는 지원 되는 모든 데이터 원본의 데이터를 로컬 xdf 파일로 가져올 수 있습니다. 데이터의 로컬 복사본을 사용 하는 것은 데이터에 대해 다양 한 분석을 수행 하지만 동일한 쿼리를 반복 해 서 실행 하지 않으려는 경우에 편리 합니다.

5. **RxSqlServerData**에 인수로 이전에 정의 된 변수를 전달 하 여 데이터 원본 개체를 만듭니다.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. **Rximport** 를 호출 하 여 현재 작업 디렉터리에 있는 `ccFraudSub.xdf`라는 파일에 데이터를 씁니다.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    Rximport 함수에서  반환 되는  `ccFraud.xdf` 개체는디스크에로컬로저장된데이터파일을나타내는경량RxXdfData데이터원본개체`localDs` 입니다.
  
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

8. 이제 SQL Server의 원본 데이터를 사용 하는 것 처럼 다양 한 R 함수를 호출 하 여 **Localds** 개체를 분석할 수 있습니다. 예를 들어 성별을 기준으로 요약할 수 있습니다.
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>다음 단계

이 단원에서는 **RevoScaleR** 및 SQL Server에 대 한 여러 부분으로 구성 된 자습서 시리즈를 마칩니다. 여기에서는 다양 한 데이터 관련 및 계산 개념을 소개 하 여 사용자 고유의 데이터와 프로젝트 요구 사항에 맞게 이동 하기 위한 토대를 제공 합니다.

**RevoScaleR**에 대 한 지식을 활용 위해 R 자습서 목록으로 돌아와서 누락 된 연습을 단계별로 진행할 수 있습니다. 또는 일반 작업에 대 한 자세한 내용은 목차의 방법 문서를 참조 하세요.

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](sql-server-r-tutorials.md)