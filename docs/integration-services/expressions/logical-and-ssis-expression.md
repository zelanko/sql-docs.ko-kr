---
title: '&amp;&amp; (논리적 AND)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cda41d0db42f72b56c84b184138ade1e345fdaa9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71289063"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (논리적 AND)(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>설명  
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
  
## <a name="see-also"></a>참고 항목  
 [&&#40;비트 AND&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
