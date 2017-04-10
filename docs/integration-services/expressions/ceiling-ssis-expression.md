---
title: "CEILING(SSIS 식) | Microsoft Docs"
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
  - "식보다 크거나 같은 최소 정수"
  - "CEILING 함수 [SSIS]"
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# CEILING(SSIS 식)
  숫자 식보다 크거나 같은 최소 정수를 반환합니다.  
  
## 구문  
  
```  
  
CEILING(numeric_expression)  
```  
  
## 인수  
 *numeric_expression*  
 유효한 숫자 식입니다.  
  
## 결과 형식  
 함수에 전달된 숫자 식의 데이터 형식입니다.  
  
## 주의  
 인수가 Null이면 CEILING 결과도 Null입니다.  
  
## 식 예  
 이 예에서는 양수, 음수 및 0 값에 CEILING 함수를 적용합니다.  
  
```  
CEILING(123.74)  
```  
  
 124.00을 반환합니다.  
  
```  
CEILING(-124.27)  
```  
  
 -124.00을 반환합니다.  
  
```  
CEILING(0.00)  
```  
  
 0.00을 반환합니다.  
  
## 관련 항목:  
 [FLOOR&#40;SSIS 식&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  