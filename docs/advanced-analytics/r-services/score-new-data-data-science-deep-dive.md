---
title: "새 데이터 점수 매기기(데이터 과학 심층 분석) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 새 데이터 점수 매기기(데이터 과학 심층 분석)
이제 예측에 사용할 수 있는 모델을 만들었으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 제공하여 몇 가지 예측을 생성합니다.  
  
## 새 데이터 점수 매기기  
로지스틱 회귀 분석 모델 *logitObj*를 사용하여 입력으로 같은 독립 변수를 사용하는 다른 데이터 집합에 대한 점수를 만듭니다.  
  
> [!NOTE]  
> 이러한 단계 중 일부를 수행하려면 DDL 관리자 권한이 필요합니다.  
  
1.  앞에서 설정한 데이터 원본 *sqlScoreDS*를 업데이트하여 필요한 열 정보를 추가합니다.  
  
    ```R  
    sqlScoreDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlScoreTable,   
        colInfo = ccColInfo,   
        rowsPerRead = sqlRowsPerRead)    
    ```  
  
2.  결과가 손실되지 않도록 새 데이터 원본 개체를 만들고 이 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 새 테이블을 채웁니다.  
  
    ```R    
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",   
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead )    
    ```  
     이때 테이블은 만들어지지 않았습니다. 이 문은 데이터의 컨테이너를 정의할 뿐입니다.
     
3.  현재 계산 컨텍스트를 확인하고, 필요한 경우 계산 컨텍스트를 서버로 설정합니다.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
4.  결과를 생성하는 예측 함수를 실행하기 전에 기존 출력 테이블이 있는지 확인해야 합니다. 없으면 새 테이블을 작성하려고 할 때 오류가 발생합니다.  
  
    이렇게 하려면 *rxSqlServerTableExists* 및 *rxSqlServerDropTable* 함수를 호출하여 테이블 이름을 입력으로 전달합니다.  
  
    ```R  
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")   
    ```  
  
    -   *rxSqlServerTableExists* 함수는 ODBC 드라이버를 쿼리하고, 테이블이 있으면 TRUE를 반환하고 없으면 FALSE를 반환합니다.    
    -   *rxSqlServerDropTable* 함수는 DDL을 실행하고, 테이블이 삭제되었으면 TRUE를 반환하고 삭제되지 않았으면 FALSE를 반환합니다.   
  
5.  이제 *rxPredict* 함수를 사용하여 점수를 만들어 데이터 원본 *sqlScoreDS*에 정의된 새 테이블에 저장할 준비가 되었습니다.  
  
    ```R  
    rxPredict(modelObject = logitObj,   
        data = sqlScoreDS,        
        outData = sqlServerOutDS,     
        predVarNames = "ccFraudLogitScore",   
          type = "link",      
        writeModelVars = TRUE,        
        overwrite = TRUE)    
    ```  
  
    *rxPredict* 함수는 원격 계산 컨텍스트에서의 실행을 지원하는 또 다른 함수입니다. *rxPredict* 함수를 사용하여 *rxLinMod*, *rxLogit* 또는 *rxGlm*을 통해 만든 모델에서 점수를 만들 수 있습니다.  
  
    -   여기서는 *writeModelVars* 매개 변수가 **TRUE**로 설정되었습니다. 이 경우 예측에 사용된 변수가 새 테이블에 포함됩니다.  
  
    -   *predVarNames* 매개 변수는 결과를 저장할 변수를 지정합니다. 여기서 새 변수 *ccFraudLogitScore*를 전달합니다.  
  
    -   *rxPredict*에 대한 *type* 매개 변수는 예측 계산 방법을 정의합니다. **response** 키워드를 지정하여 response 변수의 눈금에 따라 점수를 생성하거나, **link** 키워드를 사용하여 기본 link 함수에 따라 점수를 생성합니다(이 경우 로지스틱 눈금에 대해 예측이 수행됨).  

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
  
## 히스토그램에 점수 표시  
새 테이블이 만들어진 후 10,000개의 예측 점수 히스토그램을 계산하여 표시합니다. 하위 및 상위 값을 지정하면 계산 속도가 더 빨라지므로 데이터베이스에서 해당 값을 가져와 작업 데이터에 추가합니다.  
  
1.  데이터베이스를 쿼리하여 하위 및 상위 값을 가져오는 새 데이터 원본 *sqlMinMax*를 만듭니다.  
  
    ```R  
    sqlMinMax <- RxSqlServerData(  
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",   
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),   
        connectionString = sqlConnString)    
    ```  
     이 예제에서는 *RxSqlServerData* 데이터 원본 개체를 사용하여 SQL 쿼리, 함수 또는 저장 프로시저를 기반으로 임의 데이터 집합을 정의한 다음 이를 R 코드에서 사용하기가 얼마나 쉬운지를 확인할 수 있습니다. 변수는 실제 값을 저장하는 것이 아니라 데이터 원본 정의를 저장할 뿐입니다. 쿼리는 *rxImport*와 같은 함수에서 변수를 사용할 때만 실행되어 값을 생성합니다.  
      
2.  *rxImport* 함수를 호출하여 계산 컨텍스트 간에 공유할 수 있는 데이터 프레임에 값을 저장합니다.  
  
    ```R  
    minMaxVals <- rxImport(sqlMinMax)   
    minMaxVals <- as.vector(unlist(minMaxVals))  
  
    ```  
     **결과**
 
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3.  이제 최대값과 최소값을 사용할 수 있으므로 해당 값을 사용하여 점수 데이터 원본을 만듭니다.  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",    
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead,   
            colInfo = list(ccFraudLogitScore = list(   
                low = floor(minMaxVals[1]),    
                        high = ceiling(minMaxVals[2]) ) ) )  
  
    ```  

  
4.  마지막으로, 점수 데이터 원본 개체를 사용하여 점수 매기기 데이터를 가져오고 계산하여 히스토그램을 표시합니다. 필요한 경우 계산 컨텍스트를 설정하는 코드를 추가합니다.  
  
    ```R  
    # rxSetComputeContext(sqlCompute)   
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)  
  
    ```  
  
    **결과**  
  
    ![complex histogram created by R](../../advanced-analytics/r-services/media/rsql-sue-complex-histogram.png "complex histogram created by R")  
  
## 다음 단계  
[3단원: R을 사용하여 데이터 변환&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## 이전 단계  
[모델 만들기&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## 관련 항목:  
[데이터 과학 심층 분석: 개요&#40;SQL Server R Services&#41;](http://msdn.microsoft.com/library/mt637368(SQL.130).aspx)  
  
  
  
