---
title: LEN(SSIS 식) | Microsoft Docs
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
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e0158fef91845d189e9caa0647e23999ab27900
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195603"
---
# <a name="len-ssis-expression"></a>LEN(SSIS 식)
  문자 식에 포함된 문자의 수를 반환합니다. 문자열에 선행 및 후행 공백이 포함되어 있으면 공백도 개수에 포함됩니다. LEN은 싱글바이트 및 더블바이트 문자의 동일한 문자열에 대해 같은 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 계산할 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 *character_expression* 인수는 DT_WSTR, DT_TEXT, DT_NTEXT 또는 DT_IMAGE 데이터 형식일 수 있습니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *character_expression* 이 문자열 리터럴 또는 DT_STR 데이터 형식의 데이터 열인 경우 LEN이 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 LEN 함수로 전달된 인수가 DT_TEXT, DT_NTEXT 또는 DT_IMAGE와 같은 BLOB(Binary Large Object Block) 데이터 형식이면 1바이트 개수가 반환됩니다.  
  
 인수가 Null이면 LEN 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴의 길이를 반환합니다. 반환 결과는 12입니다.  
  
```  
LEN("Ball Bearing")  
```  
  
 이 예에서는 **FirstName** 열과 **LastName** 열의 값 길이의 차이를 반환합니다.  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 시스템 변수 **MachineName**을 사용하여 컴퓨터 이름의 길이를 반환합니다.  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>관련 항목  
 [함수 &#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
