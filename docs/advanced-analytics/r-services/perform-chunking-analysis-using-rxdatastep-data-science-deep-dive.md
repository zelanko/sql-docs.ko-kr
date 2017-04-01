---
title: "RxDataStep을 사용하여 청크 분석 수행(데이터 과학 심층 분석) | Microsoft Docs"
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
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# RxDataStep을 사용하여 청크 분석 수행(데이터 과학 심층 분석)
*rxDataStep* 함수를 사용하면 기존 R에서처럼 전체 데이터 집합을 메모리로 로드하여 한 번에 처리할 필요 없이 데이터를 청크로 처리할 수 있습니다. 데이터를 청크로 읽고 R 함수를 사용하여 차례로 데이터의 각 청크를 처리한 다음 각 청크에 대한 요약 결과를 공통 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 쓰는 방식으로 작업이 진행되기 때문입니다.  
  
이 단원에서는 R의 *table* 함수를 사용하여 대체 테이블을 계산해 이 기법을 연습합니다.  
  
> [!TIP]  
> 이 예제는 교육용으로만 제공됩니다. 실제 데이터 집합을 테이블 형식으로 표시해야 하는 경우 **RevoScaleR**에 기본 제공된 *rxCrossTabs* 또는 *rxCube* 함수(이러한 종류의 작업에 최적화됨)를 사용하는 것이 좋습니다.  
  
## 값에 따라 데이터 분할  
  
1.  먼저 데이터의 각 청크에서 *table* 함수를 호출하는 *ProcessChunk*라는 사용자 지정 R 함수를 만듭니다.  
  
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
 
  
2.  계산 컨텍스트를 서버로 설정합니다.  
  
    ```R  
    rxSetComputeContext( sqlCompute )   
    ```  
  
3.  처리할 데이터를 저장할 SQL Server 데이터 원본을 정의합니다. 먼저 SQL 쿼리를 변수에 할당합니다.   
  
    ```R  
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"   
    ```  

4.  해당 변수를 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본의 *sqlQuery* 인수에 연결합니다.  
  
    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,  
        connectionString = sqlConnString,    
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",   
            levels = as.character(1:7))))    
    ```  
     이 데이터 원본에서 *rxGetVarInfo*를 실행하면 여기에 단일 열 *Var 1: DayOfWeek, Type: factor, no factor levels available*만 포함된 것을 볼 수 있습니다.
     
5.  이 요소 변수를 원본 데이터에 적용하기 전에 중간 결과를 저장할 별도의 테이블을 만듭니다. 다시 *RxSqlServerData* 함수를 사용하여 데이터를 정의하고 같은 이름의 모든 기존 테이블을 삭제합니다.   
  
    ```R  
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)   
    # Check whether the table already exists.  
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }   
    ```  
  
7.  이제 *rxDataStep* 함수에 대한 *transformFunc* 인수로 사용자 지정 *ProcessChunk* 함수를 사용해 이 함수를 호출하여 읽은 데이터를 변환합니다.  
  
    ```R  
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)   
    ```  
  
8.  *ProcessChunk*의 중간 결과를 보려면 *rxImport*의 결과를 변수에 할당한 다음 결과를 콘솔에 출력합니다.  
  
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
  
10. 중간 결과 테이블을 제거하려면 *rxSqlServerDropTable*을 다시 호출합니다.  
  
    ```R  
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)    
    ```  
  
## 다음 단계  
[4단원: 로컬 계산 컨텍스트에서 데이터 분석&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## 이전 단계  
[RxDataStep을 사용하여 새 SQL Server 테이블 만들기&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## 참고 항목  
[데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
