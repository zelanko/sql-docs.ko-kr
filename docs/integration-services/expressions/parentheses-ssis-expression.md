---
title: "()(괄호)(SSIS 식) | Microsoft Docs"
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
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ae024cc0a4d8a492175ac992ed82eed34956848
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
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
 *expression*의 데이터 형식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 괄호를 사용하여 연산자의 우선 순위을 수정하는 방법을 보여 줍니다. 첫 번째 식은 100으로 계산되고 두 번째 식은 31로 계산됩니다.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
