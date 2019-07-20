---
title: RevoScaleR rxDataStep을 사용 하 여 청크 분석 수행
description: SQL Server에서 R 언어를 사용 하 여 분산 분석용 데이터를 청크 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3026fa03ff654079e355364587d694c9c3fe127f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344721"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep을 사용 하 여 청크 분석 수행 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이 단원에서는 **Rxdatastep** 함수를 사용 하 여 전체 데이터 집합을 메모리에 로드 하 고 기존 R 처럼 한 번에 처리 하도록 하는 대신 데이터를 청크로 처리 합니다. **Rxdatastep** 함수는 데이터를 청크로 읽어 오고 각 데이터 청크에 대해 차례로 R 함수를 적용 한 다음 각 청크에 대 한 요약 결과를 공통 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 저장 합니다. 모든 데이터를 읽으면 결과가 결합 됩니다.

> [!TIP]
> 이 단원에서는 R의 **테이블** 함수를 사용 하 여 대체 테이블을 계산 합니다. 이 예는 교육용 으로만 제공 됩니다. 
> 
> 실제 데이터 집합을 표로 해야 하는 경우이 작업을 위해 최적화 된 **RevoScaleR**에서 **RxCrossTabs** 또는 **rxcube** 함수를 사용 하는 것이 좋습니다.

## <a name="partition-data-by-values"></a>값으로 데이터 분할

1. 데이터의 각 청크에 R **테이블** 함수를 호출 하는 사용자 지정 r 함수를 만들고 새 함수 **processchunk**이름을 지정 합니다.
  
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

2. 컴퓨팅 컨텍스트를 서버로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
3. 처리 중인 데이터를 보관할 SQL Server 데이터 원본을 정의 합니다. 먼저 SQL 쿼리를 변수에 할당합니다. 그런 다음 새 SQL Server 데이터 원본의 *sqlQuery* 인수에서 해당 변수를 사용 합니다.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 필요에 따라이 데이터 원본에서 **Rxgetvarinfo** 를 실행할 수 있습니다. 이 시점에는 단일 열이 포함 되어 있습니다. *Var 1: DayOfWeek, Type: factor, 사용할 수 있는 요소 수준 없음*
     
5. 이 요소 변수를 원본 데이터에 적용하기 전에 중간 결과를 저장할 별도의 테이블을 만듭니다. **RxSqlServerData** 함수를 사용 하 여 데이터를 정의 하 고 같은 이름의 기존 테이블을 모두 삭제 합니다.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  사용자 지정 함수 **Processchunk** 를 호출 하 여 데이터를 읽을 때 **Rxdatastep** 함수의 *transformFunc* 인수로 사용 하 여 변환 합니다.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  **Processchunk**의 중간 결과를 보려면 **rximport** 의 결과를 변수에 할당 한 다음 결과를 콘솔에 출력 합니다.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **일부 결과**

    |      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
    | --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
    | 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
    | 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 모든 청크의 최종 결과를 컴퓨팅하려면 열의 합계를 구한 다음 결과를 콘솔에 표시합니다.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

    **결과**

    1  |   2  |   3  |   4  |   5  |   6  |   7
    ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
    97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 중간 결과 테이블을 제거 하려면 **rxSqlServerDropTable**를 호출 합니다.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](sql-server-r-tutorials.md)