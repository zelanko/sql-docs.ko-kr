---
title: "새 데이터의 점수 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83beab637e3740dc41706c34ccfacffe985f2957
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="score-new-data"></a>새 데이터 점수 매기기

이제 예측에 사용할 수 있는 모델을 만들었으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 제공하여 몇 가지 예측을 생성합니다.

로지스틱 회귀 분석 모델 *logitObj*를 사용하여 입력으로 같은 독립 변수를 사용하는 다른 데이터 집합에 대한 점수를 만듭니다.

> [!NOTE]
> 이러한 단계 중 일부를 수행하려면 DDL 관리자 권한이 필요합니다.

## <a name="generate-and-save-scores"></a>생성 하 고 점수를 저장 합니다.
  
1. 앞에서 설정한 데이터 원본 *sqlScoreDS*를 업데이트하여 필요한 열 정보를 추가합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 결과가 손실되지 않도록 새 데이터 원본 개체를 만들고 이 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 새 테이블을 채웁니다.
  
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
  
    -  함수 rxSqlServerTableExists ODBC 드라이버를 쿼리하고 테이블이 있는 경우, false를 반환 하지 않으면 TRUE를 반환 합니다.
    -  함수 rxSqlServerDropTable 함수는 DDL을 실행 하 고 테이블을 성공적으로 삭제, FALSE 그렇지 않은 경우 TRUE를 반환 합니다.
  
5. 이제 **rxPredict** 함수를 사용하여 점수를 만들어 데이터 원본 *sqlScoreDS*에 정의된 새 테이블에 저장할 준비가 되었습니다.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    RxPredict 함수는 다른 함수에서 원격 연산 컨텍스트로 실행할 수 있도록 지원입니다. RxLinMod, rxLogit, 또는 rxGlm를 사용 하 여 만든 모델에서 점수를 만들려는 rxPredict 함수를 사용할 수 있습니다.
  
    - 여기서는 *writeModelVars* 매개 변수가 **TRUE** 로 설정되었습니다. 이 경우 예측에 사용된 변수가 새 테이블에 포함됩니다.
  
    - *predVarNames* 매개 변수는 결과를 저장할 변수를 지정합니다. 여기서 새 변수 *ccFraudLogitScore*를 전달합니다.
  
    - *형식* rxPredict에 대 한 매개 변수는 방법을 정의 하며 예측을 계산 합니다. **response** 키워드를 지정하여 response 변수의 눈금에 따라 점수를 생성하거나, **link** 키워드를 사용하여 기본 link 함수에 따라 점수를 생성합니다(이 경우 로지스틱 눈금에 대해 예측이 수행됨).

6. 잠시 후 Management Studio에서 테이블 목록을 새로 고쳐 새 테이블 및 해당 데이터를 확인할 수 있습니다.

7. 출력 예측에 변수를 더 추가하려면 *extraVarsToWrite* 인수를 사용하면 됩니다.  예를 들어 다음 코드에서 *custID* 변수는 점수 매기기 데이터 테이블에서 예측의 출력 테이블에 추가됩니다.
  
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

새 테이블이 만들어진 후 10,000개의 예측 점수 히스토그램을 계산하여 표시합니다. 하위 및 상위 값을 지정하면 계산 속도가 더 빨라지므로 데이터베이스에서 해당 값을 가져와 작업 데이터에 추가합니다.

1. 데이터베이스를 쿼리하여 하위 및 상위 값을 가져오는 새 데이터 원본 *sqlMinMax*를 만듭니다.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     이 예제에서 RxSqlServerData 데이터 원본 개체를 사용 하 여 SQL 쿼리, 함수 또는 저장된 프로시저를 기반으로 임의의 데이터 집합을 정의 하는 것이 얼마나 쉬운지 참조할 수 있으며 다음에 R 코드를 사용 하 여 키를 누릅니다. 변수는 데이터 원본 정의; 실제 값을 저장 하지 않습니다. rxImport와 같은 함수에서 사용 하는 경우에 값을 생성 하는 쿼리가 실행 됩니다.
      
2. 계산 컨텍스트 간에 공유할 수 있는 데이터 프레임에서 값을 정렬할 rxImport 함수를 호출 합니다.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **결과**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 이제는 최대값과 최소값을 사용할 수 값을 사용 하 여 점수 데이터 소스를 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 마지막으로, 점수 데이터 원본 개체를 사용하여 점수 매기기 데이터를 가져오고 계산하여 히스토그램을 표시합니다. 필요한 경우 계산 컨텍스트를 설정하는 코드를 추가합니다.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **결과**
  
    ![R에서 생성된 복잡한 히스토그램](media/rsql-sue-complex-histogram.png "R에서 생성된 복잡한 히스토그램")
  
## <a name="next-step"></a>다음 단계

[R을 사용 하 여 데이터를 변환 합니다.](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>이전 단계

[모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)


