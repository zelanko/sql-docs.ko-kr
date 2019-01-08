---
title: LOWER(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0acb81035013b1599c4e454d4ce268dd98efe1d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770605"
---
# <a name="lower-ssis-expression"></a>LOWER(SSIS 식)
  대문자를 소문자로 변환한 후에 문자 식을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 소문자로 변환할 문자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 LOWER는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 LOWER가 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 인수가 Null이면 LOWER 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴을 소문자로 변환합니다. 반환 결과는 "new york"입니다.  
  
```  
LOWER("New York")  
```  
  
 이 예에서는 첫 문자를 제외하고 **Color** 입력 열의 모든 문자를 소문자로 변환합니다. Color가 YELLOW이면 반환 결과는 "Yellow"입니다. 자세한 내용은 [SUBSTRING&#40;SSIS 식&#41;](substring-ssis-expression.md)을 참조하세요.  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 이 예에서는 **CityName** 변수 값을 소문자로 변환합니다.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>관련 항목  
 [UPPER&#40;SSIS 식&#41;](upper-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
