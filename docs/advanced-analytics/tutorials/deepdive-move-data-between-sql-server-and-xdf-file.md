---
title: SQL Server와 RevoScaleR-SQL Server Machine Learning을 사용 하 여 XDF 파일 간에 데이터 이동
description: XDF 및 R 언어를 사용 하 여 SQL Server에서 데이터를 이동 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d0f097c64d48a3a2e87f01965914b3100c8a28dc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645212"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server와 XDF 파일 (SQL Server 및 RevoScaleR 자습서) 간 데이터 이동
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단계에서는 원격 및 로컬 계산 컨텍스트 간에 데이터를 전송 하는 데 XDF 파일을 사용 하는 방법을 알아봅니다. XDF 파일에서 데이터를 저장 하기를 사용 하면 데이터에서 변환을 수행할 수 있습니다.

파일에 데이터를 사용 하 여 새 작업을 완료 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 함수 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 데이터 변환을 적용할 수 있습니다 하 고 데이터 프레임 및.xdf 파일 간의 변환을 수행 합니다.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF 파일에서 SQL Server 테이블 만들기

이 연습에서는 하면 신용 카드 사기 데이터 다시 사용합니다. 이 시나리오에서는 California, Oregon 및 Washington 주의 사용자에 대한 몇 가지 추가 분석을 수행하라는 요청을 받았습니다. 더 효율적인 하기로 로컬 컴퓨터에 이러한 상태에 대 한 데이터를 저장 하 고 변수 성별, 카드 소유자, 상태 및 분산을 사용 하 여 작업 합니다.

1. 다시 사용 합니다 `stateAbb` 변수를 포함 하 여 새 변수를 쓸 수준을 식별 앞에서 만든 `statesToKeep`합니다.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **결과**
    
    CA|또는|WA
    ----|----|----
    5|38|48
    
2. SQL Server에서 가져올 하려는 데이터 정의 사용 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다.  이 변수를 사용 하는 나중에 *inData* 에 대 한 인수가 **rxImport**합니다.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    줄 바꿈 또는 탭 등의 숨겨진 문자가 쿼리에 없는지 확인합니다.
  
3. 다음으로, R에서 데이터로 작업할 때 사용할 열을 정의 예를 들어, 더 작은 데이터 집합에 필요한 세 개의 요소 수준만 쿼리가 세 개의 상태에 대 한 데이터를 반환 하기 때문에.  적용 된 `statesToKeep` 포함할 올바른 수준을 식별 하는 변수입니다.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 계산 컨텍스트를 설정 **로컬**, 로컬 컴퓨터에서 사용 가능한 모든 데이터를 필요 하기 때문입니다.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    합니다 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 함수를 로컬 XDF 파일에 지원 되는 데이터 원본에서 데이터를 가져올 수 있습니다. 데이터의 로컬 복사본을 사용 하 여 데이터에 대해 다양 한 분석을 수행 하려고 하지만 계속 해 서 동일한 쿼리를 실행 하지 않으려는 경우 유용 합니다.

5. 에 대 한 인수로 이전에 정의 된 변수를 전달 하 여 데이터 원본 개체를 만듭니다 **RxSqlServerData**합니다.
  
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
  
    합니다 `localDs` 에서 반환 된 개체를 **rxImport** 함수는 경량 **RxXdfData** 나타내는 데이터 원본 개체는 `ccFraud.xdf` 디스크에 로컬로 저장 된 데이터 파일.
  
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

8. 이제 분석에 다양 한 R 함수를 호출할 수 있습니다 합니다 **localDs** SQL Server의 원본 데이터와 마찬가지로 개체입니다. 예를 들어 성별 요약할 수 있습니다.
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>다음 단계

이 단원에서 다중 파트 자습서 시리즈를 마무리 **RevoScaleR** 및 SQL Server입니다. 다양 한 관련 된 데이터 및 계산 개념, 사용자 고유의 데이터 및 프로젝트 요구 사항 진행 하기 위한 기초를 제공을 소개 있습니다.

지식의 **RevoScaleR**를 하지 않았을 수 있습니다 모든 연습을 단계별로 R 자습서 목록으로 돌아갈 수 있습니다. 또는 일반 작업에 대 한 정보에 대 한 테이블에서 방법 문서를 검토 합니다.

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](sql-server-r-tutorials.md)