---
title: '|(포괄적 비트 OR)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6cdfd0f591bbfa9e4c2729346e36bfe6f43ef597
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>|(포괄적 비트 OR)(SSIS 식)
  두 정수 값의 비트 OR 연산을 수행합니다. 그런 후 첫 번째 피연산자의 각 비트를 두 번째 피연산자의 해당 비트와 비교합니다. 두 비트 중 하나가 1이면 해당 결과 비트가 1로 설정되고, 그렇지 않으면 해당 결과 비트가 0으로 설정됩니다.  
  
 두 조건이 모두 부호 있는 정수 데이터 형식이거나 두 조건이 모두 부호 없는 정수 데이터 형식이어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression1 ,integer_ expression2*  
 부호가 있거나 부호가 없는 정수 데이터 형식의 유효한 식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 둘 중 한 조건이 Null이면 식 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 변수 **NumberA** 와 **NumberB**사이에 포괄적 비트 OR 연산을 수행합니다. **NumberA** 에는 3(00000011)이 포함되고 **NumberB** 에는 9(00001001)가 포함됩니다.  
  
```  
@NumberA | @NumberB  
```  
  
 식은 11(00001011)로 계산됩니다.  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 이 예에서는 **ReorderPoint** 열과 **SafetyStockLevel** 열 사이에 포괄적 비트 OR 연산을 수행합니다.  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 **ReorderPoint** 가 10이고 **SafetyStockLevel** 이 8이면 식은 10(00001010)으로 계산됩니다.  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 이 예에서는 두 정수 사이에 포괄적 비트 OR 연산을 수행합니다.  
  
```  
3 | 5   
```  
  
 식은 7(00000111)로 계산됩니다.  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>참고 항목  
 [&#124;&#124;&#40;논리적 OR&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^&#40;배타적 비트 OR&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
