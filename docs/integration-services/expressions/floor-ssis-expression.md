---
title: "FLOOR(SSIS 식) | Microsoft Docs"
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
  - "식보다 작거나 같은 최대 정수"
  - "FLOOR 함수 [SSIS]"
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# FLOOR(SSIS 식)
  숫자 식보다 작거나 같은 최대 정수를 반환합니다.  
  
## 구문  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## 인수  
 *numeric_expression*  
 유효한 숫자 식입니다.  
  
## 결과 형식  
 인수 식의 숫자 데이터 형식입니다. 결과는 *numeric_expression*과 동일한 데이터 형식으로 계산된 값의 정수 부분입니다.  
  
## 주의  
 인수가 Null이면 FLOOR 결과도 Null입니다.  
  
## 식 예  
 이 예에서는 FLOOR 함수를 양수, 음수 및 0 값에 적용합니다.  
  
```  
FLOOR(123.45)  
```  
  
 123.00을 반환합니다.  
  
```  
FLOOR(-123.45)  
```  
  
 -124.00을 반환합니다.  
  
```  
FLOOR(0.00)  
```  
  
 0.00을 반환합니다.  
  
## 관련 항목:  
 [CEILING&#40;SSIS 식&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  