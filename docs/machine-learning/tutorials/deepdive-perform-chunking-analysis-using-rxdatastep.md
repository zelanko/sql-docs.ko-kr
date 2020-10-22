---
title: RevoScaleR의 청킹 분석
description: 'RevoScaleR 자습서 12: SQL Server에서 R 언어를 사용하여 분산 분석용 데이터를 청크하는 방법입니다.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c636a33632a44e9cc5d1510bb73b5967a68f21ab
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195116"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>rxDataStep을 사용하여 청킹 분석 수행(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 12에 해당됩니다.

이 자습서에서는 기존 R에서처럼 전체 데이터 세트를 메모리로 로드하여 한 번에 처리할 필요 없이 **rxDataStep** 함수를 사용하여 데이터를 청크로 처리합니다. **rxDataStep** 함수는 데이터를 청크로 읽고 각 데이터 청크에 R 함수를 차례로 적용한 다음, 각 청크에 대한 요약 결과를 공통 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 저장합니다. 모든 데이터를 읽으면 결과가 결합됩니다.

> [!TIP]
> 이 자습서에서는 R의 **table** 함수를 사용하여 대체 테이블을 계산합니다. 이 예는 교육용으로만 제공됩니다. 
> 
> 실제 데이터 세트를 테이블 형식으로 표시해야 하는 경우 이러한 종류의 작업에 최적화된 **RevoScaleR**의 **rxCrossTabs** 또는 **rxCube** 함수를 사용하는 것이 좋습니다.

## <a name="partition-data-by-values"></a>값에 따라 데이터 분할

1. 데이터의 각 청크에서 **table** 함수를 호출하는 사용자 지정 R 함수를 만들고 새 함수의 이름을 **ProcessChunk**로 지정합니다.
  
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
  
3. 처리 중인 데이터를 저장할 SQL Server 데이터 원본을 정의합니다. 먼저 SQL 쿼리를 변수에 할당합니다. 그런 다음, 새 SQL Server 데이터 원본의 *sqlQuery* 인수에서 해당 변수를 사용합니다.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 필요에 따라 이 데이터 원본에서 **rxGetVarInfo**를 실행할 수 있습니다. 이 때 단일 열이 포함됩니다. *Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5. 이 요소 변수를 원본 데이터에 적용하기 전에 중간 결과를 저장할 별도의 테이블을 만듭니다. 다시 **RxSqlServerData** 함수를 사용하여 데이터를 정의하고 같은 이름의 모든 기존 테이블을 삭제합니다.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  **rxDataStep** 함수에 대한 *transformFunc* 인수로 사용자 지정 함수 **ProcessChunk** 함수를 사용해 이 함수를 호출하여 읽은 데이터를 변환합니다.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  **ProcessChunk**의 중간 결과를 보려면 **rxImport**의 결과를 변수에 할당한 다음, 결과를 콘솔에 출력합니다.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **일부 결과**

    | 행 \# |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
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

10. 중간 결과 테이블을 제거하려면 **rxSqlServerDropTable**을 호출합니다.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server용 R 자습서](./r-tutorials.md)