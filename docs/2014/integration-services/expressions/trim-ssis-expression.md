---
title: TRIM(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- TRIM function
- trailing blanks
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 756d9bd066f4ecbcb1cfb7e43cec8ca7ea2713a6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437070"
---
# <a name="trim-ssis-expression"></a>TRIM(SSIS 식)
  선행 및 후행 공백을 제거하고 문자 식을 반환합니다.  
  
> [!NOTE]  
>  TRIM은 탭이나 줄 바꿈 문자와 같은 공백 문자를 제거하지 않습니다. 유니코드는 많은 다른 공백 유형에 대해 코드 포인트를 제공하지만 이 함수는 유니코드 코드 포인트 0x0020만 인식합니다. DBCS(더블바이트 문자 집합) 문자열이 유니코드로 변환될 때 0x0020이 아닌 공백 문자를 포함할 수도 있는데 이 함수에서는 이러한 공백을 제거할 수 없습니다. 모든 종류의 공백을 제거하려면 스크립트 구성 요소의 스크립트 실행에서 Microsoft Visual Basic .NET Trim 메서드를 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TRIM(character_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 공백을 제거할 문자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>설명  
 인수가 Null이면 TRIM 결과도 Null입니다.  
  
 TRIM은 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 TRIM이 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴에서 선행 및 후행 공백을 제거합니다. 반환 결과는 "New York"입니다.  
  
```  
TRIM("   New York   ")  
```  
  
 이 예에서는 **FirstName** 열과 **LastName** 열의 연결 결과에서 선행 및 후행 공백을 제거합니다. **FirstName** 과 **LastName** 사이의 빈 문자열은 제거되지 않습니다.  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## <a name="see-also"></a>참고 항목  
 [LTRIM&#40;SSIS 식&#41;](trim-ssis-expression.md)   
 [RTRIM&#40;SSIS 식&#41;](rtrim-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
