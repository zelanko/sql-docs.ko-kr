---
title: SQRT(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 06e899be27df88a628f8e45493452a66739f30a4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428180"
---
# <a name="sqrt-ssis-expression"></a>SQRT(SSIS 식)
  숫자 식의 제곱근을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 임의의 숫자 데이터 형식을 갖는 숫자 식입니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 DT_R8  
  
## <a name="remarks"></a>설명  
 인수가 Null이면 SQRT 결과도 Null입니다.  
  
 인수가 음수 값이면 SQRT가 실패합니다.  
  
 인수는 제곱근 연산 전에 DT_R8 데이터 형식으로 캐스팅됩니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴의 제곱근을 반환합니다. 반환 결과는 12입니다.  
  
```  
SQRT(144)  
```  
  
 이 예에서는 **Value1** 열과 **Value2** 열의 값을 뺀 결과인 식의 제곱근을 반환합니다.  
  
```  
SQRT(Value1 - Value2)  
```  
  
 이 예에서는 두 변수에 SQUARE 함수를 적용한 후 합계의 제곱근을 계산하여 삼각형의 3번째 변의 길이를 반환합니다. **Side1** 에 3이 포함되어 있고 **Side2** 에 4가 포함되어 있으면 SQRT 함수는 5를 반환합니다.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  식에서 변수 이름에는 항상 \@ 접두사가 포함되어 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
