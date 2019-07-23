---
title: '&amp; (비트 AND)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8ecc406d7eb0f1d66c0117e062528bed0247a679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034082"
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp; (비트 AND)(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  두 정수 값의 비트 AND 연산을 수행합니다. 그런 후 첫 번째 피연산자의 각 비트를 두 번째 피연산자의 해당 비트와 비교합니다. 두 비트가 모두 1이면 해당 결과 비트가 1로 설정되고, 그렇지 않으면 해당 결과 비트가 0으로 설정됩니다.  
  
 두 조건이 모두 부호 있는 정수 유형이거나 또는 부호 없는 정수 유형이어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression1, integer_expression2*  
 부호가 있거나 부호가 없는 정수 데이터 형식의 유효한 식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 둘 중 한 조건이 Null이면 식 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 **NumberA** 열과 **NumberB**열 사이에 비트 AND 연산을 수행합니다. **NumberA** 열에는 3(0000011)이 포함되고 **NumberB** 열에는 7(00000111)이 포함됩니다.  
  
```  
NumberA & NumberB  
```  
  
 식은 3(00000011)으로 계산됩니다.  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 이 예에서는 **ReorderPoint** 열과 **SafetyStockLevel** 열 사이에 비트 AND 연산을 수행합니다.  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 **ReorderPoint** 가 10이고 **SafetyStockLevel** 이 8이면 식은 8(00001000)로 계산됩니다.  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 이 예에서는 두 정수 사이에 비트 AND 연산을 수행합니다.  
  
```  
3 & 5   
```  
  
 식은 1(00000001)로 계산됩니다.  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>참고 항목  
 [&&&#40;논리적 AND&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
