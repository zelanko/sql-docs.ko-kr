---
title: '* (곱하기)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8d322ff646d4908f968c068def3d2ca10d4c6a15
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86905130"
---
# <a name="-multiply-ssis-expression"></a>*(곱하기)(SSIS 식)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  두 숫자 식을 곱합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression1, numeric_expression2*  
 숫자 데이터 형식의 유효한 식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
 두 피연산자 중 하나가 Null이면 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 곱합니다.  
  
```  
5 * 6.09  
```  
  
 이 예에서는 **ListPrice** 열의 값에 10%를 곱합니다.  
  
```  
ListPrice * .10  
```  
  
 이 예에서는 **ListPrice** 열에서 식 결과를 뺍니다. 변수 **Discount%** 는 이름에 % 문자가 포함되어 있으므로 대괄호로 묶어야 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)를 참조하세요.  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
