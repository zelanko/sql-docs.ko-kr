---
title: SQUARE(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7b312453000aaf3862eef91c5c660ecf6ecb9cf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52787235"
---
# <a name="square-ssis-expression"></a>SQUARE(SSIS 식)
  숫자 식의 제곱을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 임의의 숫자 데이터 형식을 갖는 숫자 식입니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 인수가 Null이면 SQUARE 결과도 Null입니다.  
  
 인수는 제곱 연산 전에 DT_R8 데이터 형식으로 캐스팅됩니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 12의 제곱을 반환합니다. 반환 결과는 144입니다.  
  
```  
SQUARE(12)  
```  
  
 이 예에서는 두 열의 값을 뺀 결과의 제곱을 반환합니다. **Value1** 이 12이고 **Value2** 가 4이면 SQUARE 함수는 64를 반환합니다.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 이 예에서는 두 변수에 SQUARE 함수를 적용한 후 합계의 제곱근을 계산하여 직각 삼각형의 3번째 변의 길이를 반환합니다. **Side1** 에 3이 포함되어 있고 **Side2** 에 4가 포함되어 있으면 SQRT 함수는 5를 반환합니다.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  식에서 변수 이름에는 항상 \@ 접두사가 포함되어 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
