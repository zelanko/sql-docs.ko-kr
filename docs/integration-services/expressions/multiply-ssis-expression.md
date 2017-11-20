---
title: "* (곱하기) (SSIS 식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb439e9221a1bcb169776eec1f6251b49ed4b861
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="-multiply-ssis-expression"></a>*(곱하기)(SSIS 식)
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
  
## <a name="remarks"></a>주의  
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
  
## <a name="see-also"></a>관련 항목:  
 [연산자 우선순위 및 결합성](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자 &#40; SSIS 식 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

