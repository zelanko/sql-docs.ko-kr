---
title: "4단원: 로컬 계산 컨텍스트에서 데이터 분석(데이터 과학 심층 분석) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 4단원: 로컬 계산 컨텍스트에서 데이터 분석(데이터 과학 심층 분석)
일반적으로 서버 컨텍스트를 사용하여 복잡한 R 코드를 실행하는 것이 훨씬 더 빠르지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 가져와 개인 워크스테이션에서 분석하는 것이 더 편리한 경우도 있습니다.  
  
이 섹션에서는 로컬 계산 컨텍스트로 다시 전환하고 컨텍스트 간에 데이터를 이동하여 성능을 최적화하는 방법을 알아봅니다.  
  
## 로컬 요약 만들기  
  
1.  모든 작업을 로컬에서 수행하도록 계산 컨텍스트를 변경합니다.  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 추출하는 경우 각 읽기에서 추출되는 행 수를 늘리면 대체로 성능이 향상됩니다.  이렇게 하려면 데이터 원본에 대한 *rowsPerRead* 매개 변수의 값을 늘립니다.  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    이전에는 *rowsPerRead* 값이 5000으로 설정되었습니다.  
  
3.  이제 새 데이터 원본에 대해 *rxSummary*를 호출합니다.  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    실제 결과는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 컨텍스트에서 *rxSummary*를 실행할 때와 같아야 합니다.  그러나 작업은 더 빠르거나 느릴 수 있습니다. 데이터가 분석을 위해 로컬 컴퓨터로 전송되므로 이러한 작업 속도는 데이터베이스에 대한 연결에 크게 좌우됩니다.  
  

## 다음 단계  
[SQL Server와 XDF 파일 간에 데이터 이동&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## 이전 단계  
[RxDataStep을 사용하여 청크 분석 수행&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
