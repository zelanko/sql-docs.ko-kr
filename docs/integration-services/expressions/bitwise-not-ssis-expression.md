---
title: "~(비트 Not)(SSIS 식) | Microsoft Docs"
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
  - "비트 NOT(~)"
  - "~(비트 NOT)"
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# ~(비트 Not)(SSIS 식)
  정수의 비트 부정을 수행합니다. 이 연산자는 부호 있는 정수 또는 부호 없는 정수 데이터 형식에 적용할 수 있습니다.  
  
## 구문  
  
```  
  
~integer_expression  
  
```  
  
## 인수  
 *integer_expression*  
 정수 데이터 형식의 유효한 식입니다. *integer*_*expression*은 비트 연산을 위해 이진수로 변환되는 정수입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## 결과 형식  
 *integer_expression*의 데이터 형식을 반환합니다.  
  
## 주의  
 InclusionThresholdSetting  
  
## 식 예  
 이 예에서는 숫자 170(0000 0000 1010 1010)에 비트 ~(NOT) 연산을 수행합니다. 숫자는 부호 있는 정수입니다.  
  
```  
  
~ 170  
```  
  
 식은 -170(1111111101010101)으로 계산됩니다.  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## 관련 항목:  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  