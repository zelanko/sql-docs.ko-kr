---
title: "+(더하기)(SSIS) | Microsoft Docs"
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
  - "+ (더하기)"
  - "더하기 연산자 (+)"
  - "식 추가"
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# +(더하기)(SSIS)
  두 숫자 식을 더합니다.  
  
## 구문  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## 인수  
 *numeric_expression1, numeric_ expression2*  
 숫자 데이터 형식의 유효한 식입니다.  
  
## 결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## 주의  
 두 피연산자 중 하나가 Null이면 결과도 Null입니다.  
  
## 식 예  
 이 예에서는 숫자 리터럴을 추가합니다.  
  
```  
5 + 6.09 + 7.0  
```  
  
 이 예에서는 **VacationHours** 열과 **SickLeaveHours** 열의 값을 더합니다.  
  
```  
VacationHours + SickLeaveHours  
```  
  
 이 예에서는 **StandardCost** 열에 계산된 값을 추가합니다. 변수 **Profit%** 은 이름에 % 문자가 포함되어 있으므로 대괄호로 묶어야 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)를 참조하세요.  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## 관련 항목:  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  