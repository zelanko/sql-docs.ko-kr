---
title: RevoScaleR rxDataStep-SQL Server Machine Learning을 사용 하 여 청크 분석 수행
description: SQL Server에서 R 언어를 사용 하 여 분산 된 분석을 위해 데이터를 청크 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c5d3b50af1f7db3a39dec0e475aa00582bc77e0a
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596034"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep (RevoScaleR 및 SQL Server 자습서)를 사용 하 여 청크 분석 수행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단원에서는 사용 된 **rxDataStep** 전체 데이터 집합을 메모리로 로드 하 고 기존 R 에서처럼 한 번에 처리를 요구 하는 것이 아니라 프로세스 데이터를 청크로 함수 합니다 **rxDataStep** 함수 읽고 청크의 데이터 차례로 각 데이터 청크에 R 함수를 적용 한 다음 각 청크에 대 한 요약 결과 공용으로 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다. 모든 데이터를 읽을 때 결과가 결합 됩니다.

> [!TIP]
> 이 단원에서는 사용 하 여 대체 테이블을 계산 합니다 **테이블** R에서 함수 이 예제는 교육용 으로만 제공 해야 합니다. 
> 
> 실제 데이터 집합을 표로 나타낼 경우 사용 하는 것이 좋습니다 합니다 **rxCrossTabs** 또는 **rxCube** 함수가 **RevoScaleR**,이 대 한 일종의 최적화 된 작업입니다.

## <a name="partition-data-by-values"></a>값에 따라 데이터 분할

1. R을 호출 하는 사용자 지정 R 함수를 만듭니다 **테이블** 데이터의 각 청크에서 작동 하 고 새 함수 이름을 **ProcessChunk**합니다.
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. 계산 컨텍스트를 서버로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
3. 처리할 데이터를 보관 하는 SQL Server 데이터 원본을 정의 합니다. 먼저 SQL 쿼리를 변수에 할당합니다. 그런 다음 해당 변수를 사용 합니다 *sqlQuery* 새 SQL Server 데이터 원본의 인수입니다.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 필요에 따라 실행할 수 있습니다 **rxGetVarInfo** 이 데이터 원본에 있습니다. 이 시점에서 단일 열을 포함 합니다. *Var 1: DayOfWeek, Type: 비율, 사용 가능한 요소 수준이 없습니다.*
     
5. 이 요소 변수를 원본 데이터에 적용하기 전에 중간 결과를 저장할 별도의 테이블을 만듭니다. 다시 사용 합니다 **RxSqlServerData** 동일한 이름의 기존 테이블을 삭제 하 고 데이터를 정의 하는 함수입니다.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  사용자 지정 함수를 호출 **ProcessChunk** 읽을 때, 그대로 사용 하 여 데이터를 변환 하는 *transformFunc* 인수를 **rxDataStep** 함수입니다.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  중간 결과 보려면 **ProcessChunk**, 결과 할당 **rxImport** 변수에 한 다음 콘솔에 결과 출력 합니다.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **일부 결과**

    |      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
    | --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
    | 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
    | 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 모든 청크의 최종 결과를 계산하려면 열의 합계를 구한 다음 결과를 콘솔에 표시합니다.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

    **결과**

    1  |   2  |   3  |   4  |   5  |   6  |   7
    ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
    97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 중간 결과 테이블을 제거 하려면 호출할 **rxSqlServerDropTable**합니다.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](sql-server-r-tutorials.md)