---
title: RIGHT(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e8d1cfdda299c786aa926aad26f724009a683ec
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796113"
---
# <a name="right-ssis-expression"></a>RIGHT(SSIS 식)
  지정한 문자 식의 오른쪽에서부터 지정한 개수의 문자를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자를 추출할 문자 식입니다.  
  
 *integer_expression*  
 반환할 문자 수를 나타내는 정수 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *integer_expression* 이 *character_expression*의 길이보다 큰 경우 함수는 *character_expression*을 반환합니다.  
  
 *integer_expression* 이 0인 경우 함수는 길이가 0인 문자열을 반환합니다.  
  
 *integer_expression* 이 음수인 경우 함수는 오류를 반환합니다.  
  
 *integer_expression* 인수는 변수와 열을 사용할 수 있습니다.  
  
 RIGHT는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 RIGHT가 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 두 인수 중 하나가 Null이면 RIGHT 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 문자열 리터럴을 사용합니다. 반환 결과는 `"Bike"`입니다.  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 다음 예에서는 `Times` 열의 오른쪽부터 `Name` 변수에 지정한 문자 수만큼의 부분을 반환합니다. `Name` 이 `Touring Front Wheel` 이고 `Times` 가 5이면 반환 결과는 `"Wheel"`입니다.  
  
```  
RIGHT(Name, @Times)  
```  
  
 또한 다음 예에서는 `Times` 열의 오른쪽부터 `Name` 변수에 지정한 문자 수만큼의 부분을 반환합니다. `Times` 데이터 형식이 정수가 아니고 DT_I2 데이터 형식으로의 명시적 캐스트가 식에 포함되어 있습니다. `Name` 이 `Touring Front Wheel` 이고 `Times` 가 `4.32`인 경우 RIGHT 함수가 값 4.32를 4로 변환하고 오른쪽에서부터 4개 문자를 반환하므로 반환 결과는 `"heel"` 입니다.  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>관련 항목  
 [LEFT&#40;SSIS 식&#41;](left-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
