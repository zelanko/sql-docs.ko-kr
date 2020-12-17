---
title: RevoScaleR을 사용하여 데이터 점수 매기기
description: 이전 자습서에서 만든 로지스틱 회귀 분석 모델을 사용하여 입력과 같은 독립 변수를 사용하는 다른 데이터 세트에 대한 점수를 계산합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 314520a54bb9052fb091932b63b9cf4c817a0f16
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470504"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>새 데이터 점수 매기기(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 8에 해당됩니다.

이 자습서에서는 이전 자습서에서 만든 로지스틱 회귀 분석 모델을 사용하여 입력과 같은 독립 변수를 사용하는 다른 데이터 세트에 대한 점수를 계산합니다.

> [!div class="checklist"]
> * 새 데이터 점수 매기기
> * 점수의 히스토그램 만들기

> [!NOTE]
> 이러한 단계 중 일부를 수행하려면 DDL 관리자 권한이 필요합니다.

## <a name="generate-and-save-scores"></a>점수 생성 및 저장
  
1. 이전 자습서에서 만든 열 정보를 사용하도록 sqlScoreDS 데이터 원본([자습서 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)에서 생성됨)을 업데이트합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 결과가 손실되지 않도록 하려면 새 데이터 원본 개체를 만듭니다. 그런 다음, 새 데이터 원본 개체를 사용하여 RevoDeepDive 데이터베이스에 새 테이블을 채웁니다.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    이때 테이블은 만들어지지 않았습니다. 이 문은 데이터의 컨테이너를 정의할 뿐입니다.
     
3. **rxGetComputeContext()** 를 사용하여 현재 컴퓨팅 컨텍스트를 확인하고, 필요한 경우 컴퓨팅 컨텍스트를 서버로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 예방 차원에서 출력 테이블이 있는지 확인하세요. 이름이 같은 항목이 이미 있으면 새 테이블을 작성하려고 할 때 오류가 발생합니다.
  
    이렇게 하려면 [rxSqlServerTableExists](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 및 [rxSqlServerDropTable](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)함수를 호출하여 테이블 이름을 입력으로 전달합니다.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** 는 ODBC 드라이버를 쿼리하고, 테이블이 있으면 TRUE를 반환하고, 그렇지 않으면 FALSE를 반환합니다.
    + **rxSqlServerDropTable** 은 DDL을 실행하고, 테이블이 성공적으로 삭제되었으면 TRUE를 반환하고, 그렇지 않으면 FALSE를 반환합니다.

5. [rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict)를 실행하여 점수를 만들어 데이터 원본 sqlScoreDS에 정의된 새 테이블에 저장합니다.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 함수는 원격 컴퓨팅 컨텍스트에서의 실행을 지원하는 또 다른 함수입니다. **rxPredict** 함수를 사용하여 [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) 또는 [rxGlm](/machine-learning-server/r-reference/revoscaler/rxglm)을 기반으로 하는 모델에서 점수를 만들 수 있습니다.
  
    - 여기서는 *writeModelVars* 매개 변수가 **TRUE** 로 설정되었습니다. 이 경우 예측에 사용된 변수가 새 테이블에 포함됩니다.
  
    - *predVarNames* 매개 변수는 결과를 저장할 변수를 지정합니다. 여기에 새 변수 `ccFraudLogitScore`를 전달합니다.
  
    - *rxPredict* 에 대한 **type** 매개 변수는 예측 계산 방법을 정의합니다. 응답 변수의 소수 자릿수를 기준으로 점수를 생성하려면 키워드 **응답** 을 지정합니다. 또는 키워드 **link** 를 사용하여 기본 링크 함수를 기반으로 점수를 생성합니다. 이 경우 로지스틱 스케일을 사용하여 예측을 만듭니다.

6. 잠시 후 Management Studio에서 테이블 목록을 새로 고쳐 새 테이블 및 해당 데이터를 확인할 수 있습니다.

7. 출력 예측에 변수를 더 추가하려면 *extraVarsToWrite* 인수를 사용합니다.  예를 들어 다음 코드에서 *custID* 변수는 점수 매기기 데이터 테이블에서 예측의 출력 테이블에 추가됩니다.
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>히스토그램에 점수 표시

새 테이블이 만들어진 후 10,000개의 예측 점수 히스토그램을 컴퓨팅하여 표시합니다. 하위 및 상위 값을 지정하면 계산 속도가 더 빨라지므로 데이터베이스에서 해당 값을 가져와 작업 데이터에 추가합니다.

1. 데이터베이스를 쿼리하여 하위 및 상위 값을 가져오는 새 데이터 원본인 sqlMinMax를 만듭니다.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     이 예제에서는 **RxSqlServerData** 데이터 원본 개체를 사용하여 SQL 쿼리, 함수 또는 저장 프로시저를 기반으로 임의 데이터 세트를 정의한 다음, 이를 R 코드에서 사용하기가 얼마나 쉬운지를 확인할 수 있습니다. 변수는 실제 값을 저장하는 것이 아니라 데이터 원본 정의를 저장할 뿐입니다. 쿼리는 **rxImport** 와 같은 함수에서 변수를 사용할 때만 실행되어 값을 생성합니다.
      
2. [rxImport](/machine-learning-server/r-reference/revoscaler/rximport) 함수를 호출하여 컴퓨팅 컨텍스트 간에 공유할 수 있는 데이터 프레임에 값을 저장합니다.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **결과**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 이제 최댓값과 최솟값을 사용할 수 있으므로 해당 값을 사용하여 생성된 점수에 대한 다른 데이터 원본을 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 데이터 원본 개체 sqlOutScoreDS를 사용하여 점수를 가져오고 히스토그램을 컴퓨팅하여 표시합니다. 필요한 경우 컴퓨팅 컨텍스트를 설정하는 코드를 추가합니다.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **결과**
  
    ![R에서 생성된 복잡한 히스토그램](media/rsql-sue-complex-histogram.png "R에서 생성된 복잡한 히스토그램")
  
## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 데이터 변환](../../machine-learning/tutorials/deepdive-transform-data-using-r.md)