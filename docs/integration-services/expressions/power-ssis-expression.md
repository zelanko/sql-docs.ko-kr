---
title: POWER(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eecca6cd0e18a8a7ced8190756abea2d18d4ca2a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="power-ssis-expression"></a>POWER(SSIS 식)
  숫자 식의 거듭제곱을 반환합니다. 거듭제곱 매개 변수는 정수여야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 유효한 숫자 식입니다.  
  
 *power*  
 유효한 숫자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 *numeric_expression* 및 *power* 인수는 거듭제곱을 계산하기 전에 DT_R8 데이터 형식으로 캐스팅됩니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *numeric_expression* 이 0이고 *power* 가 음수이면 식 계산기는 오류를 반환하고 반환 결과를 Null로 설정합니다.  
  
 *numeric_expression* 또는 *power* 의 계산 결과를 알 수 없는 경우 반환 결과는 Null입니다.  
  
 *power* 인수는 분수일 수 있습니다. 예를 들어 값 0.5를 거듭제곱으로 사용할 수 있습니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 사용합니다. 이 함수는 4의 3 거듭제곱을 계산하여 64를 반환합니다.  
  
```  
POWER(4,3)  
```  
  
 이 예에서는 **Length** 열과 **DimensionCount** 변수를 사용합니다. **Length** 가 8이고 **DimensionCount** 가 2이면 반환 결과는 64입니다.  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
