---
title: 새 데이터 (SQL과 R 심층 분석) 점수를 매깁니다. | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2de06b0159c432ac1d53d9e51bbdf0cd820efd7a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202335"
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>새 데이터 (SQL과 R 심층 분석) 점수를 매깁니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 단계에서는 앞에서 만든 입력으로 동일한 독립 변수를 사용 하는 다른 데이터 집합에 대 한 점수를 작성 하는 로지스틱 회귀 모델을 사용 합니다.

> [!NOTE]
> 다음이 단계 중 일부에 대 한 DDL 관리자 권한이 필요합니다.

## <a name="generate-and-save-scores"></a>생성 하 고 점수를 저장 합니다.
  
1. 이전에 설정 하는 데이터 원본을 업데이트 `sqlScoreDS`, 필요한 열 정보를 추가 합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 결과 손실 하지 않으려면 하 게 하려면 새 데이터 원본 개체를 만듭니다. 그런 다음 새 데이터 원본 개체를 사용 하 여 새 테이블에 채우기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    이때 테이블은 만들어지지 않았습니다. 이 문은 데이터의 컨테이너를 정의할 뿐입니다.
     
3. 현재 계산 컨텍스트를 확인하고, 필요한 경우 계산 컨텍스트를 서버로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 결과를 생성하는 예측 함수를 실행하기 전에 기존 출력 테이블이 있는지 확인해야 합니다. 그렇지 않으면 새 테이블을 작성 하려고 할 때 오류가 발생할 것 있습니다.
  
    이렇게 하려면 **rxSqlServerTableExists** 및 **rxSqlServerDropTable**함수를 호출하여 테이블 이름을 입력으로 전달합니다.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  **rxSqlServerTableExists** 함수는 ODBC 드라이버를 쿼리하고, 테이블이 있으면 TRUE를 반환하고 없으면 FALSE를 반환합니다.
    -  함수 **rxSqlServerDropTable** DDL을 실행 하 고 TRUE 테이블이 있는 경우 성공적으로 삭제 FALSE 그렇지 않으면 반환 합니다.
    - 두 함수를 볼 수 있습니다에 대 한 참조: [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. 사용할 준비가 되었습니다. 이제는 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 함수를 점수를 생성 하 고 데이터 원본에 정의 된 새 테이블에 저장할 `sqlScoreDS`합니다.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 함수는 원격 계산 컨텍스트에서의 실행을 지원하는 또 다른 함수입니다. **rxPredict** 함수를 사용하여 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)또는 [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)을 통해 만든 모델에서 점수를 만들 수 있습니다.
  
    - 여기서는 *writeModelVars* 매개 변수가 **TRUE** 로 설정되었습니다. 이 경우 예측에 사용된 변수가 새 테이블에 포함됩니다.
  
    - *predVarNames* 매개 변수는 결과를 저장할 변수를 지정합니다. 새 변수를 전달 하는 여기 `ccFraudLogitScore`합니다.
  
    - *rxPredict* 에 대한 **type** 매개 변수는 예측 계산 방법을 정의합니다. 키워드 지정 **응답** 응답 변수의 배율에 따라 점수를 생성 합니다. 키워드를 사용 또는 **링크** 는 쿼리에서 기본 링크 함수에 따라 점수를 생성할 예측 로지스틱 눈금을 사용 하 여 생성 됩니다.

6. 잠시 후 Management Studio에서 테이블 목록을 새로 고쳐 새 테이블 및 해당 데이터를 확인할 수 있습니다.

7. 출력 예측에 변수를 더 추가하려면 *extraVarsToWrite* 인수를 사용합니다.  예를 들어 다음 코드에서는 변수에서에서 `custID` 점수 매기기 데이터 테이블에서 예측의 출력 테이블에 추가 됩니다.
  
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

## <a name="display-scores-in-a-histogram"></a>히스토그램에 표시 점수

새 테이블을 만든 후 계산 표시 하는 10, 000 예측 점수 막대 그래프. 낮은 임계값과 높은 값을 지정 하므로 데이터베이스에서 해당 권한을 받아야, 경우 작업 데이터에 추가할 계산이 빠릅니다.

1. 새 데이터 원본을 만들고 `sqlMinMax`, 낮은 임계값과 높은 값을 가져올 데이터베이스를 쿼리 하는 합니다.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     이 예제에서는 **RxSqlServerData** 데이터 원본 개체를 사용하여 SQL 쿼리, 함수 또는 저장 프로시저를 기반으로 임의 데이터 세트를 정의한 다음, 이를 R 코드에서 사용하기가 얼마나 쉬운지를 확인할 수 있습니다. 변수는 실제 값을 저장하는 것이 아니라 데이터 원본 정의를 저장할 뿐입니다. 쿼리는 **rxImport**와 같은 함수에서 변수를 사용할 때만 실행되어 값을 생성합니다.
      
2. 호출 된 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 계산 컨텍스트 간에 공유할 수 있는 데이터 프레임의 끝에 있는 함수입니다.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **결과**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 이제는 최대값과 최소값을 사용할 수 값을 사용 하 여 생성 된 점수에 대 한 다른 데이터 소스를 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 데이터 원본 개체를 사용 하 여 `sqlOutScoreDS` 하는 점수를 얻을 계산 하 고 막대 그래프를 표시 합니다. 필요한 경우 계산 컨텍스트를 설정하는 코드를 추가합니다.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **결과**
  
    ![R에서 생성된 복잡한 히스토그램](media/rsql-sue-complex-histogram.png "R에서 생성된 복잡한 히스토그램")
  
## <a name="next-step"></a>다음 단계

[R을 사용하여 데이터 변환](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>이전 단계

[모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)


