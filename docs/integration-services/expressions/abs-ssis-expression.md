---
title: "ABS(SSIS 식) | Microsoft Docs"
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
  - "ABS 함수"
  - "절대 양수 값"
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ABS(SSIS 식)
  숫자 식의 절대값을 양수로 반환합니다.  
  
## 구문  
  
```  
  
ABS(numeric_expression)  
```  
  
## 인수  
 *numeric_expression*  
 부호 있는 숫자 식이거나 부호 없는 숫자 식입니다.  
  
## 결과 형식  
 함수에 전달된 숫자 식의 데이터 형식입니다.  
  
## 주의  
 인수가 Null이면 ABS 결과도 Null입니다.  
  
## 식 예  
 이 예에서는 ABS 함수를 양수와 음수에 적용합니다. 둘 다 1.23을 반환합니다.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 이 예에서는 변수 **HighTemperature** 와 **LowTempature**의 값을 빼는 식에 ABS 함수를 적용합니다.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## 관련 항목:  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  