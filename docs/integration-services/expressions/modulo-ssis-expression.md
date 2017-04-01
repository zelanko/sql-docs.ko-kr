---
title: "(모듈로)(SSIS 식) | Microsoft Docs"
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
  - "%(모듈로 연산자)"
  - "나누기 연산의 나머지"
  - "모듈로 연산자(%)"
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# (모듈로)(SSIS 식)
  첫 번째 숫자 식을 두 번째 식으로 나눈 다음 나머지의 정수 부분을 제공합니다.  
  
## 구문  
  
```  
  
dividend % divisor  
  
```  
  
## 인수  
 *dividend*  
 나눌 숫자 식입니다. *dividend* 는 임의의 유효한 숫자 식일 수 있습니다. 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *divisor*  
 피제수를 나눌 숫자 식입니다. *divisor* 는 0을 제외한 임의의 유효한 숫자 식일 수 있습니다.  
  
## 결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
## 주의  
 두 식이 모두 부호 있는 정수 또는 부호 없는 정수 데이터 형식이어야 합니다.  
  
 두 피연산자 중 하나가 Null이면 결과도 Null입니다.  
  
 모듈로 0은 사용할 수 없습니다.  
  
## 식 예  
 이 예에서는 두 개의 숫자 리터럴에서 모듈러스를 계산합니다. 결과는 3입니다.  
  
```  
42 % 13  
```  
  
 이 예에서는 **SalesQuota** 열과 하나의 숫자 리터럴에서 모듈러스를 계산합니다.  
  
```  
SalesQuota % 12  
```  
  
 이 예에서는 두 개의 숫자 변수 **Sales$** 와 **Month**에서 모듈러스를 계산합니다. 변수 **Sales$** 는 이름에 $ 문자가 포함되어 있으므로 대괄호로 묶어야 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)를 참조하세요.  
  
```  
@[Sales$] % @Month  
```  
  
 이 예에서는 모듈로 연산자를 사용하여 **Value** 변수가 짝수 또는 홀수인지를 확인하고 조건부 연산자를 사용하여 결과를 설명하는 문자열을 반환합니다. 자세한 내용은 [? :&#40;조건&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/conditional-ssis-expression.md)을 참조하세요.  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## 관련 항목:  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  