---
title: RevoScaleR 및 rxPredict-SQL Server Machine Learning을 사용 하 여 새 데이터 점수 매기기
description: SQL Server에서 R 언어를 사용 하 여 데이터 점수를 매기는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 386daeb62262182d40ea0b15cca3eb9714c23d64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962193"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>점수를 새 데이터 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단계에서는 입력으로 같은 독립 변수를 사용 하는 다른 데이터 집합의 점수를 매길 이전 단원에서 만든 로지스틱 회귀 모델을 사용 합니다.

> [!div class="checklist"]
> * 새 데이터 점수 매기기
> * 점수 히스토그램 만들기

> [!NOTE]
> 다음이 단계 중 일부에 대 한 DDL 관리자 권한이 부여 해야합니다.

## <a name="generate-and-save-scores"></a>생성 하 고 점수를 저장 합니다.
  
1. SqlScoreDS 데이터 원본을 업데이트 (에서 만든 [두 단원](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) 이전 단원에서 만든 열 정보를 사용 합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 결과가 손실 되지 않도록 확인, 새 데이터 원본 개체를 만듭니다. 그런 다음 새 데이터 원본 개체를 사용을 RevoDeepDive 데이터베이스에 새 테이블을 채웁니다.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    이때 테이블은 만들어지지 않았습니다. 이 문은 데이터의 컨테이너를 정의할 뿐입니다.
     
3. 하 여 현재 계산 컨텍스트를 확인할 **rxGetComputeContext()** , 필요한 경우 서버 계산 컨텍스트를 설정 합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 예방 조치로 출력 테이블의 존재 여부를 확인 합니다. 이미 있을 경우 동일한 이름의 새 테이블을 작성 하려고 할 때 오류가 받습니다.
  
    이렇게 하려면 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 및 [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)함수를 호출하여 테이블 이름을 입력으로 전달합니다.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** ODBC 드라이버를 쿼리하고 테이블이 FALSE이 고, 그렇지 경우 TRUE를 반환 합니다.
    + **rxSqlServerDropTable** DDL을 실행 하 고 테이블 되 면 TRUE 삭제 FALSE이 고, 그렇지를 반환 합니다.

5. 실행할 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 점수를 생성 하 여 데이터 원본 sqlScoreDS에 정의 된 새 테이블에 저장 합니다.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 함수는 원격 계산 컨텍스트에서의 실행을 지원하는 또 다른 함수입니다. 사용할 수는 **rxPredict** 기반 모델에서 점수를 작성 하는 함수 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)에 [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit), 또는 [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)합니다.
  
    - 여기서는 *writeModelVars* 매개 변수가 **TRUE** 로 설정되었습니다. 이 경우 예측에 사용된 변수가 새 테이블에 포함됩니다.
  
    - *predVarNames* 매개 변수는 결과를 저장할 변수를 지정합니다. 여기서 새 변수를 전달 하는 `ccFraudLogitScore`합니다.
  
    - *rxPredict* 에 대한 **type** 매개 변수는 예측 계산 방법을 정의합니다. 키워드를 지정 **응답** 응답 변수의 크기에 따라 점수를 생성 합니다. 키워드를 사용 하거나 **링크** 로지스틱 눈금을 사용 하 여 예측은 생성 하는 경우 기본 link 함수에 따라 점수를 생성 합니다.

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

새 테이블을 만든 후에 계산 및 10,000 예측 점수 히스토그램을 표시 합니다. 계산 하위 및 상위 값을 지정, 따라서 데이터베이스에서 해당 및 작업 데이터에 추가할 경우 더 빠릅니다.

1. SqlMinMax 하위 및 상위 값을 가져오기 위해 데이터베이스를 쿼리 하는 새 데이터 원본을 만듭니다.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     이 예제에서는 **RxSqlServerData** 데이터 원본 개체를 사용하여 SQL 쿼리, 함수 또는 저장 프로시저를 기반으로 임의 데이터 세트를 정의한 다음, 이를 R 코드에서 사용하기가 얼마나 쉬운지를 확인할 수 있습니다. 변수는 실제 값을 저장하는 것이 아니라 데이터 원본 정의를 저장할 뿐입니다. 쿼리는 **rxImport**와 같은 함수에서 변수를 사용할 때만 실행되어 값을 생성합니다.
      
2. 호출 된 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 계산 컨텍스트 간에 공유할 수 있는 데이터 프레임에 값을 저장 하는 함수입니다.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **결과**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 이제는 최대값과 최소값을 사용할 수 있는 값을 사용 하 여 생성 된 점수에 대 한 다른 데이터 소스를 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 데이터 원본 개체 sqlOutScoreDS를 사용 하 여 점수를 가져올 계산 하 여 히스토그램을 표시. 필요한 경우 컴퓨팅 컨텍스트를 설정하는 코드를 추가합니다.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **결과**
  
    ![R에서 생성된 복잡한 히스토그램](media/rsql-sue-complex-histogram.png "R에서 생성된 복잡한 히스토그램")
  
## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 데이터 변환](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)