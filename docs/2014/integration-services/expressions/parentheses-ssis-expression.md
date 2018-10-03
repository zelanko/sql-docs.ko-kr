---
title: ()(괄호)(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3cfcad949dd07d4eec4513b09a19cf262bd5c787
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101983"
---
# <a name="-parentheses-ssis-expression"></a>()(괄호)(SSIS 식)
  식의 계산 순서를 식별합니다. 괄호로 묶인 식의 계산 우선 순위가 가장 높습니다. 괄호로 묶인 중첩 식은 안에서부터 밖으로 계산됩니다.  
  
 괄호를 사용하면 복잡한 식을 쉽게 이해하는 데에도 도움이 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 *expression*의 데이터 형식입니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 괄호를 사용하여 연산자의 우선 순위을 수정하는 방법을 보여 줍니다. 첫 번째 식은 100으로 계산되고 두 번째 식은 31로 계산됩니다.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [연산자 우선순위 및 결합성](operator-precedence-and-associativity.md)   
 [연산자 &#40;SSIS 식&#41;](operators-ssis-expression.md)  
  
  
