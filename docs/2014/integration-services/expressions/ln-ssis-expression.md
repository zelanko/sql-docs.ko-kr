---
title: LN(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 111c97e177f9829309e5fb727a0227b6f2150791
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308063"
---
# <a name="ln-ssis-expression"></a>LN(SSIS 식)
  숫자 식의 자연 로그를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 0과 음수가 아닌 유효한 숫자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 숫자 식은 로그를 계산하기 전에 DT_R8 데이터 형식으로 캐스팅됩니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *numeric_expression* 이 0 또는 음수 값으로 계산되면 반환 결과는 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 사용합니다. 이 함수는 값 3.737766961828337을 반환합니다.  
  
```  
LN(42)  
```  
  
 이 예에서는 열 **Length**를 사용합니다. 열 값이 53.99이면 3.9887988442302가 반환됩니다.  
  
```  
LN(Length)   
```  
  
 이 예에서는 변수 **Length**를 사용합니다. 변수가 숫자 데이터 형식이거나 식이 숫자 데이터 형식으로의 명시적 캐스트를 포함해야 합니다. **Length** 가 234.567이면 함수는 5.45774126708797을 반환합니다.  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>관련 항목  
 [로그 &#40;SSIS 식&#41;](log-ssis-expression.md)   
 [함수 &#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
