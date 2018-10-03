---
title: '&amp;&amp; (논리적 AND)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a59545c26427afa1677eca78e4c00263e663dded
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065537"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (논리적 AND)(SSIS 식)
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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목  
 [& &#40;비트 AND&#41; &#40;SSIS 식&#41;](bitwise-and-ssis-expression.md)   
 [연산자 우선순위 및 결합성](operator-precedence-and-associativity.md)   
 [연산자 &#40;SSIS 식&#41;](operators-ssis-expression.md)  
  
  
