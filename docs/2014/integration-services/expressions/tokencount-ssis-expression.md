---
title: TOKENCOUNT(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c0efed1-c2b3-4f20-a3a1-ad91283b7c0a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d449e6245b779fd281fc9c8f047a9eb352d56846
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822767"
---
# <a name="tokencount-ssis-expression"></a>TOKENCOUNT(SSIS 식)
  지정된 구분 기호로 구분된 토큰을 포함하는 문자열의 토큰 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
TOKENCOUNT(character_expression, delimiter_string)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 구분 기호로 구분된 토큰이 포함된 문자열입니다.  
  
 *delimiter_string*  
 구분 기호 문자가 포함된 문자열입니다. 예를 들어 "; ,"에는 세미콜론, 공백 및 쉼표의 세 구분 문자가 포함되어 있습니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 다음 설명은 TOKEN 함수에 적용됩니다.  
  
-   구분 기호 문자열은 하나 이상의 구분 기호 문자를 포함할 수 있습니다.  
  
-   선행 구분 기호는 생략합니다.  
  
-   TOKENCOUNT는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 TOKEN 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다.  
  
-   character_expression이 null인 경우 TOKENCOUNT는 0(영)을 반환합니다.  
  
-   변수 및 열을 이 식의 인수로 사용할 수 있습니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 문자열에 토큰 3개가 있으므로 TOKENCOUNT 함수에서 3을 반환합니다. "01", "12", "2011"입니다.  
  
```  
TOKENCOUNT("01/12/2011", "/")  
```  
  
 다음 예제에서는 토큰 4개("a", "little", "white", "dog")가 있으므로 TOKENCOUNT 함수에서 4를 반환합니다.  
  
```  
TOKENCOUNT("a little white dog"," ")  
```  
  
 다음 예에서 TOKENCOUNT 함수는 1을 반환합니다. 이 함수는 입력 문자열에서 구분 기호를 구문 분석하고 문자열에 구분 기호가 없으므로 전체 문자열을 첫 번째 토큰으로 추가합니다.  
  
```  
TOKENCOUNT("a little white dog","|")  
```  
  
 다음 예에서 TOKENCOUNT 함수는 4를 반환합니다. 이 예의 구분 기호 문자열에는 구분 기호가 5개 포함되어 있습니다. 입력 문자열에는 "a", "little", "white", "dog"의 4개 토큰이 포함되어 있습니다.  
  
```  
TOKENCOUNT("a:little|white dog","| ,.:")  
```  
  
 다음 예에서 TOKENCOUNT 함수는 4를 반환합니다. 모든 선행 공백 문자는 무시합니다.  
  
```  
TOKENCOUNT("        a little white dog", " ")  
```  
  
## <a name="see-also"></a>관련 항목  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
