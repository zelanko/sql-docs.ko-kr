---
title: '- (빼기)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 82d268ed8f61085a2a829821ee3d68931f31e680
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161833"
---
# <a name="--subtract-ssis-expression"></a>-(빼기)(SSIS 식)
  첫 번째 숫자 식에서 두 번째 식을 뺍니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression1, numeric_expression2*  
 숫자 데이터 형식의 유효한 식입니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 식이 올바른 순서로 계산되도록 단항 빼기 식을 괄호로 묶으십시오.  
  
## <a name="remarks"></a>Remarks  
 두 피연산자 중 하나가 Null이면 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 뺍니다.  
  
```  
5 - 6.09  
```  
  
 이 예에서는 **ListPrice** 열의 값에서 **StandardCost** 열의 값을 뺍니다.  
  
```  
ListPrice - StandardCost  
```  
  
 이 예에서는 **ListPrice** 열에서 계산된 값을 뺍니다. 변수 **Discount%** 는 이름에 % 문자가 포함되어 있으므로 대괄호로 묶어야 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](identifiers-ssis.md)를 참조하세요.  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>관련 항목  
 [연산자 우선순위 및 결합성](operator-precedence-and-associativity.md)   
 [연산자 &#40;SSIS 식&#41;](operators-ssis-expression.md)  
  
  
