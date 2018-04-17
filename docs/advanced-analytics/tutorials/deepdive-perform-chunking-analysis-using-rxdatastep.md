---
title: RxDataStep (SQL과 R 심층 분석)를 사용 하 여 청크 분석을 수행 합니다. | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5db0acfb90c200442489cd7c3ec464223195eec6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>RxDataStep (SQL과 R 심층 분석)를 사용 하 여 청크 분석 수행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 단원에서는 사용 하 여는 **rxDataStep** 전체 데이터 집합의 메모리에 로드 하 고 기존의 오른쪽에서와 같이 한 번에 처리 될 필요 하지 않고 데이터 청크를 처리 하려면 함수 **rxDataStep** 함수 읽는 데이터 청크를 차례로 데이터의 각 청크를 R 함수를 적용 하 고 다음에 공통 각 청크에 요약 결과 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다. 모든 데이터를 읽을 때 결과가 결합 됩니다.

> [!TIP]
> 이 단원에서는 사용 하 여 대체 테이블을 계산에서 `table` R에서 함수 이 예제에서는 지침만 제공 하기 위한 것입니다. 
> 
> 실제 데이터 집합을 표로 해야 할 경우 사용 하는 것이 좋습니다는 **rxCrossTabs** 또는 **rxCube** 함수가 **RevoScaleR**,이 대 한 일종의 최적화 작업입니다.

## <a name="partition-data-by-values"></a>값으로 데이터 분할

1. R을 호출 하는 사용자 지정 R 함수를 만들 `table` 데이터의 각 청크에서 작동 하 고 새 함수 이름을 `ProcessChunk`합니다.
  
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
    rxSetComputeContext( sqlCompute )
    ```
  
3. 처리 중인 데이터를 보관할 SQL Server 데이터 원본을 정의 합니다. 먼저 SQL 쿼리를 변수에 할당합니다. 그런 다음에 해당 변수를 사용 하 여는 *sqlQuery* 새의 인수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다.
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. 실행할 수 있습니다 **rxGetVarInfo** 이 데이터 원본에 있습니다. 이 시점에서 단일 열을 포함: *Var 1: DayOfWeek, 유형:을 고려 하 고 사용 가능한 비율 수준이 없습니다.*
     
5. 이 요소 변수를 원본 데이터에 적용하기 전에 중간 결과를 저장할 별도의 테이블을 만듭니다. 다시 방금는 RxSqlServerData 함수를 사용 하면 makign 같은 이름의 기존 테이블을 삭제 하 시겠습니까 데이터를 정의 합니다.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  사용자 정의 함수를 호출 `ProcessChunk` 읽을 때로 사용 하 여 데이터를 변환 하는 *transformFunc* 인수에는 **rxDataStep** 함수입니다.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  중간 결과를 보려면 `ProcessChunk`, 결과를 할당 **rxImport** 변수에 한 다음 콘솔에 결과 출력 합니다.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

**일부 결과**

|      |    1.  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| 1. | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 모든 청크의 최종 결과를 계산하려면 열의 합계를 구한 다음 결과를 콘솔에 표시합니다.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

 **결과**
  1.  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 호출 하는 중간 결과 테이블을 제거 하려면 **rxSqlServerDropTable**합니다.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>다음 단계

[로컬 계산 컨텍스트에서 데이터 분석](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>이전 단계

[rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
