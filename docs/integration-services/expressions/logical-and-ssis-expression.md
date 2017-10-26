---
title: "&amp;&amp;(논리적 AND) (SSIS 식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a52d1a0bf10aba48b1e628a9253c7f2361f58506
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp;(논리적 AND) (SSIS 식)
  논리적 AND 연산을 수행합니다. 모든 조건이 TRUE이면 식도 TRUE가 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>인수  
 *boolean _expression1, boolean_expression2*  
 TRUE, FALSE 또는 NULL로 계산되는 임의의 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_BOOL  
  
## <a name="remarks"></a>주의  
 다음 표에서는 && 연산자의 결과를 보여 줍니다.  
  
|결과|식|식|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 **StandardCost** 열과 **ListPrice** 열을 사용합니다. **StandardCost** 열의 값이 300보다 작고 **ListPrice** 열의 값이 500보다 크면 TRUE가 됩니다.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 이 예에서는 리터럴 대신 변수 **SPrice** 와 **LPrice** 를 사용합니다.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>관련 항목:  
 [& &#40; 비트 AND &#41; &#40; SSIS 식 &#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [연산자 우선순위 및 결합성](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자 &#40; SSIS 식 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

