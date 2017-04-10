---
title: "GETUTCDATE(SSIS 식) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "날짜 [Integration Services], GETUTCDATE"
  - "현재 날짜"
  - "UTC 시간"
  - "GETUTCDATE 함수"
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# GETUTCDATE(SSIS 식)
  DT_DBTIMESTAMP 형식을 사용하여 현재 시스템 날짜를 UTC 시간(국제 표준시 또는 그리니치 표준시)으로 반환합니다. GETUTCDATE 함수는 인수가 필요 없습니다.  
  
## 구문  
  
```  
  
GETUTCDATE()  
```  
  
## 인수  
 InclusionThresholdSetting  
  
## 결과 형식  
 DT_DBTIMESTAMP  
  
## 식 예  
 이 예에서는 현재 날짜의 연도가 UTC 시간으로 반환됩니다.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 이 예에서는 **ModifiedDate** 열의 날짜와 현재 UTC 날짜 사이의 일 수가 반환됩니다.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 이 예에서는 현재 UTC 날짜에 3개월을 더합니다.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## 관련 항목:  
 [GETDATE&#40;SSIS 식&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  