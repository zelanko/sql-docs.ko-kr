---
title: FINDSTRING(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7efc711e97abde1d33a7dd4194bd2953b959ef6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769179"
---
# <a name="findstring-ssis-expression"></a>FINDSTRING(SSIS 식)
  문자 식에서 지정한 문자열 발생 위치를 반환합니다. 반환 결과는 항목의 인덱스(1부터 시작)입니다. 문자열 매개 변수는 문자 식으로 계산되고 발생 빈도 매개 변수는 정수여야 합니다. 문자열을 찾을 수 없는 경우 반환 값은 0입니다. 문자열이 발생 인수에 지정된 횟수보다 적게 발생하는 경우에도 반환 값이 0입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 검색 위치를 나타내는 문자열입니다.  
  
 *searchstring*  
 검색할 문자열입니다.  
  
 *occurrence*  
 보고할 *searchstring* 발생을 지정하는 부호 있는 정수 또는 부호 없는 정수입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_I4  
  
## <a name="remarks"></a>설명  
 FINDSTRING은 DT_WSTR 데이터 형식에서만 실행됩니다.  문자열 리터럴인*character_expression* 및 *searchstring* 인수나 DT_STR 데이터 형식의 데이터 열은 FINDSTRING 연산이 수행되기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 *character_expression* 또는 *searchstring* 이 Null이면 FINDSTRING은 Null을 반환합니다.  
  
 *occurrence* 인수의 값이 1이면 첫 번째 발생의 인덱스를 가져오고 값이 2이면 두 번째 발생의 인덱스를 가져옵니다.  
  
 *occurrence* 는 0보다 큰 정수여야 합니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴을 사용합니다. 값 11을 반환합니다.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 이 예에서는 문자열 리터럴을 사용합니다. "NY" 문자열이 두 번만 발생하므로 반환 결과가 0입니다.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 이 예에서는 **Name** 열을 사용합니다. 
  **Name** 열에서 값 n의 위치가 반환됩니다. 반환 결과는 **Name**열의 값에 따라 달라집니다. **Name** 열에 Anderson이 포함된 경우 함수는 8을 반환합니다.  
  
```  
FINDSTRING(Name,"n", 2)   
```  
  
 이 예에서는 **Name** 열과 **Size** 열을 사용합니다. **Name** 열에서 **Size** 값의 가장 왼쪽 문자 위치가 반환됩니다. 반환 결과는 열 값에 따라 달라집니다. **Name** 이 Mountain,500Red,42이고 **Size** 가 42이면 반환 결과는 17입니다.  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>참고 항목  
 [REPLACE&#40;SSIS 식&#41;](replace-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
