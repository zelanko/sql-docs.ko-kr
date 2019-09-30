---
title: TOKEN(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c025eac60079e601d755439573b35257038d9275
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297361"
---
# <a name="token--ssis-expression"></a>TOKEN(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  문자열에서 토큰을 구분하는 지정된 구분 기호와 반환할 토큰을 나타내는 토큰 번호를 기반으로 문자열에서 토큰(부분 문자열)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 구분 기호로 구분된 토큰이 포함된 문자열입니다.  
  
 *delimiter_string*  
 구분 기호 문자가 포함된 문자열입니다. 예를 들어 "; ,"에는 세미콜론, 공백 및 쉼표의 세 구분 문자가 포함되어 있습니다.  
  
 *occurrence*  
 반환될 토큰을 지정하는 부호 있는 또는 부호 없는 정수입니다. 예를 들어 이 매개 변수의 값으로 3을 지정하면 문자열의 세 번째 토큰이 반환됩니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 이 함수는 <character_expression> 문자열을 <delimiter_string>에 지정된 구분 기호로 구분된 토큰 집합으로 분할한 다음 N번째 토큰을 반환합니다. 여기서 N은 \<occurrence> 매개 변수로 지정된 토큰의 발생 횟수입니다. 이 함수의 샘플 사용법은 예 섹션을 참조하십시오.  
  
 다음 설명은 TOKEN 함수에 적용됩니다.  
  
-   구분 기호 문자열은 하나 이상의 구분 기호 문자를 포함할 수 있습니다.  
  
-   \<occurrence> 매개 변수 값이 문자열의 총 토큰 수보다 큰 경우 이 함수는 NULL을 반환합니다.  
  
-   선행 구분 기호는 생략합니다.  
  
-   TOKEN은 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 TOKEN 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다.  
  
-   character_expression이 null인 경우 TOKEN이 null 결과를 반환합니다.  
  
-   식의 모든 인수에 대한 값으로 변수 및 열을 사용할 수 있습니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 TOKEN 함수가 "a"를 반환합니다. "a little white dog" 문자열에는 4개의 토큰 "a", "little", "white", "dog"가 " "(공백 문자)로 구분되어 있습니다. 두 번째 인수인 구분 기호 문자열은 입력 문자열을 토큰으로 분할하는 데 사용되는 한 구분 기호로 공백 문자를 지정합니다. 마지막 인수 1은 첫 번째로 반환될 토큰을 지정합니다. 이 샘플 문자열에서 첫 번째 토큰은 "a"입니다.  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 다음 예에서는 TOKEN 함수가 "dog"를 반환합니다. 이 예의 구분 기호 문자열에는 구분 기호가 5개 포함되어 있습니다. 입력 문자열에는 "a", "little", "white", "dog"의 4개 토큰이 포함되어 있습니다.  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 다음 예에서는 문자열에 99 토큰이 없으므로 TOKEN 함수가 ""(빈 문자열)을 반환합니다.  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 다음 예에서는 TOKEN 함수가 전체 문자열을 반환합니다. 이 함수는 입력 문자열에서 구분 기호를 구문 분석하고 문자열에 구분 기호가 없으므로 전체 문자열을 첫 번째 토큰으로 추가합니다.  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 다음 예에서는 TOKEN 함수가 "a"를 반환합니다. 모든 선행 공백 문자는 무시합니다.  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 다음 예에서는 TOKEN 함수가 날짜 문자열에서 연도를 반환합니다.  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 다음 예에서는 TOKEN 함수가 지정된 경로에서 파일 이름을 반환합니다. 예를 들어 User::Path 값이 "c:\program files\data\myfile.txt"인 경우 TOKEN 함수는 "myfile.txt"를 반환합니다. TOKENCOUNT 함수는 4를 반환하고 TOKEN 함수는 4번째 토큰 "myfile.txt"를 반환합니다.  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
