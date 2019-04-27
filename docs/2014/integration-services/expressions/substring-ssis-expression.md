---
title: SUBSTRING(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2b749a88a0783e6981cf9fd643412f0ca614e6a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768737"
---
# <a name="substring-ssis-expression"></a>SUBSTRING(SSIS 식)
  문자 식에서 지정된 위치부터 시작하여 지정된 길이만큼 반환합니다. *position* 매개 변수와 *length* 매개 변수는 정수여야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자를 추출할 문자 식입니다.  
  
 *position*  
 하위 문자열이 시작되는 지점을 지정하는 정수입니다.  
  
 *length*  
 부분 문자열의 길이를 문자 수로 지정하는 정수입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 SUBSTRING은 1부터 시작하는 인덱스를 사용합니다. *position* 이 1이면 부분 문자열은 *character_expression*의 첫 번째 문자로 시작합니다.  
  
 SUBSTRING은 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 SUBSTRING이 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 인수가 Null이면 SUBSTRING 결과도 Null입니다.  
  
 식의 모든 인수가 변수와 열을 사용할 수 있습니다.  
  
 *length* 인수는 문자열 길이를 초과할 수 있습니다. 이 경우 문자열의 나머지가 반환됩니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자 4부터 시작하여 문자열 리터럴의 두 문자가 반환됩니다. 반환 결과는 "ph"입니다.  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 이 예에서는 4번째 문자부터 시작하여 문자열 리터럴의 나머지가 반환됩니다. 반환 결과는 "phant"입니다. *length* 인수가 문자열 길이를 초과하는 것은 오류가 아닙니다.  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 이 예에서는 **MiddleName** 열의 첫 문자가 반환됩니다.  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 이 예에서는 *position* 및 *length* 인수에 변수를 사용합니다. **Start** 가 1이고 **Length** 가 5이면 **Name** 열의 처음 5문자가 반환됩니다.  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 이 예에서는 여섯 번째 문자부터 시작하여 **PostalCode** 변수의 마지막 네 문자가 반환됩니다.  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 이 예에서는 문자열 리터럴의 길이가 0인 문자열이 반환됩니다.  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>관련 항목  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
