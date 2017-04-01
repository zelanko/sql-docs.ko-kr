---
title: "rxImport를 사용하여 메모리에 데이터 로드(데이터 과학 심층 분석) | Microsoft Docs"
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# rxImport를 사용하여 메모리에 데이터 로드(데이터 과학 심층 분석)
*rxImport* 함수를 사용하여 데이터 원본의 데이터를 R 세션 메모리의 데이터 프레임 또는 디스크의 XDF 파일로 이동할 수 있습니다. 파일을 대상으로 지정하지 않으면 데이터는 메모리에 데이터 프레임으로 저장됩니다.  
  
이 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 가져온 다음 *rxImport*를 사용하여 관심 있는 데이터를 로컬 파일에 저장하는 방법을 알아봅니다. 이렇게 하면 데이터베이스를 다시 쿼리하지 않고도 로컬 계산 컨텍스트에서 반복하여 데이터를 분석할 수 있습니다.  
  
## SQL Server에서 로컬 메모리로 데이터 하위 집합 추출  
고위험 개인만 자세히 검사하기로 결정했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원본 테이블은 크기 때문에 고위험 고객에 대한 정보를 가져와 로컬 워크스테이션의 메모리에 있는 데이터 프레임에 로드합니다.  
  
1.  계산 컨텍스트를 로컬 워크스테이션으로 다시 설정합니다.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  *sqlQuery* 매개 변수에 유효한 SQL 문을 제공하는 새 SQL Server 데이터 원본 개체를 만듭니다. 이 예제에서는 위험 점수가 가장 높은 관찰의 하위 집합을 가져옵니다. 이렇게 하면 필요한 데이터만 로컬 메모리에 저장됩니다.  
  
    ```R    
    sqlServerProbDS <- RxSqlServerData(       
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",  
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)   
    ```  
  
3.  *rxImport* 함수를 사용하여 실제로 로컬 R 세션의 데이터 프레임으로 데이터를 로드합니다.  
  
    ```R  
    highRisk <- rxImport(sqlServerProbDS)   
    ```  
     작업에 성공하면 상태 메시지 Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds가 나타납니다. 
   
4.  이제 메모리의 데이터 프레임에 고위험 관찰이 있으므로 다양한 R 함수를 사용하여 데이터 프레임을 조작할 수 있습니다. 예를 들어 고객의 위험 점수를 기준으로 고객 순서를 매긴 다음 가장 위험도가 높은 고객을 출력할 수 있습니다.  
  
    ```R  
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]   
    row.names(orderedHighRisk) <- NULL    
    head(orderedHighRisk)  
  
    ```  
  
 **결과**  
  
 *ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*  
*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*  
*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*  
*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*  
*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*  
*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*  
*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*  
  
## rxImport 대한 자세한 정보  
*rxImport*를 사용하여 데이터 이동은 물론 데이터를 읽는 동안 데이터를 변환할 수도 있습니다. 예를 들어 고정 너비 열에 대해 문자 수를 지정하고, 변수에 대한 설명을 제공하고, 요소 열에 대한 수준을 설정하고, 가져온 후 사용할 새로운 수준을 만들 수 있습니다.  
  
*rxImport* 함수는 가져오는 동안 열에 변수 이름을 할당하지만 *colInfo* 매개 변수를 사용하여 새 변수 이름을 지정하거나 *colClasses* 매개 변수를 사용하여 데이터 형식을 변경할 수 있습니다.  
  
*transforms* 매개 변수에서 추가 작업을 지정하여 읽은 각 데이터 청크에 대한 기본 처리를 수행할 수 있습니다.  
  
## 다음 단계  
[RxDataStep을 사용하여 새 SQL Server 테이블 만들기&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## 이전 단계  
[3단원: R을 사용하여 데이터 변환&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## 관련 항목:  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
