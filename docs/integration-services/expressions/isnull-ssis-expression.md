---
title: "ISNULL(SSIS 식) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Null 값 [Integration Services]"
  - "ISNULL 함수"
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ISNULL(SSIS 식)
  식이 Null인지 여부에 따라 부울 결과를 반환합니다.  
  
## 구문  
  
```  
  
ISNULL(expression)  
```  
  
## 인수  
 *expression*  
 임의 데이터 형식의 유효한 식입니다.  
  
## 결과 형식  
 DT_BOOL  
  
## 식 예  
 이 예에서는 **DiscontinuedDate** 열에 Null 값이 포함되어 있을 경우 TRUE를 반환합니다.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 이 예에서는 **LastName** 열에 Null 값이 포함되어 있을 경우 "Unknown last name"을 반환합니다. 그렇지 않으면 **LastName**이 반환됩니다.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 이 예에서는 **DaysToManufacture** 열에 Null 값이 포함되어 있을 경우 **AddDays**변수 값에 관계없이 항상 TRUE를 반환합니다.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## 관련 항목:  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE&#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  