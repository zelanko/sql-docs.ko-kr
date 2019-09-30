---
title: LOG(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2a44d6e7245108c16442e30a67aaea13aae8293
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297504"
---
# <a name="log-ssis-expression"></a>LOG(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  숫자 식의 상용 로그를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 0이 아니거나 음수가 아닌 유효한 숫자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 *숫자 식* 은 로그를 계산하기 전에 DT_R8 데이터 형식으로 캐스팅됩니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *numeric_expression* 이 0 또는 음수 값으로 계산되면 반환 결과는 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 사용합니다. 이 함수는 값 1.988291341907488을 반환합니다.  
  
```  
LOG(97.34)  
```  
  
 이 예에서는 열 **Length**를 사용합니다. 열 값이 101.24이면 2.005352136486217을 반환합니다.  
  
```  
LOG(Length)   
```  
  
 이 예에서는 변수 **Length**를 사용합니다. 변수가 숫자 데이터 형식이거나 식이 숫자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터 형식으로의 명시적 캐스트를 포함해야 합니다. **Length** 가 234.567이면 함수는 2.370266913465859을 반환합니다.  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>참고 항목  
 [EXP&#40;SSIS 식&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN&#40;SSIS 식&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
