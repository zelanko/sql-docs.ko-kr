---
title: 문자열 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302844"
---
# <a name="string-functions"></a>문자열 함수
다음 표에는 문자열 조작 기능이 나열되어 있습니다. 응용 프로그램은 *정보 유형의* SQL_STRING_FUNCTIONS **사용하여 SQLGetInfo를** 호출하여 드라이버에서 지원하는 문자열 함수를 확인할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 *string_exp* 로 표시된 인수는 열의 이름, *문자 문자열 리터럴*또는 기본 데이터 형식을 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR 나타낼 수 있는 다른 스칼라 함수의 결과일 수 있습니다.  
  
 *character_exp* 로 표시된 인수는 가변 길이 문자열입니다.  
  
 *시작,* *길이*또는 *개수로* 표시된 인수는 *숫자 리터럴이거나* 기본 데이터 형식을 SQL_TINYINT, SQL_SMALLINT 또는 SQL_INTEGER 나타낼 수 있는 다른 스칼라 함수의 결과일 수 있습니다.  
  
 여기에 나열된 문자열 함수는 1기반입니다. 즉, 문자열의 첫 번째 문자는 문자 1입니다.  
  
 BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH 및 위치 문자열 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**아시이(string_exp)** _string_exp_ **)** (ODBC 1.0)|*string_exp* 가장 왼쪽 문자의 ASCII 코드 값을 정수로 반환합니다.|  
|**BIT_LENGTH(string_exp)** _string_exp_ **)** (ODBC 3.0)|문자열 식의 길이(비트)를 반환합니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동하지 않으므로 *string_exp* 문자열로 암시적으로 변환하지 않고 대신 주어진 데이터 형식의 (내부) 크기를 반환합니다.|  
|**CHAR** _(코드)_ **)** (ODBC 1.0)|*코드에*의해 지정된 ASCII 코드 값이 있는 문자를 반환합니다. *코드* 값은 0에서 255 사이여야 합니다. 그렇지 않으면 반환 값은 데이터 원본에 따라 다릅니다.|  
|**CHAR_LENGTH(string_exp)** _string_exp_ **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식인 경우 문자열 식의 문자 길이를 반환합니다. 그렇지 않으면 문자열 식의 바이트 로 길이를 반환합니다(가장 작은 정수는 8로 나눈 비트 수보다 작을 수 있음). 이 함수는 CHARACTER_LENGTH 함수와 동일합니다.|  
|**CHARACTER_LENGTH(string_exp)** _string_exp_ **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식인 경우 문자열 식의 문자 길이를 반환합니다. 그렇지 않으면 문자열 식의 바이트 로 길이를 반환합니다(가장 작은 정수는 8로 나눈 비트 수보다 작을 수 있음). 이 함수는 CHAR_LENGTH 함수와 동일합니다.|  
|**CONCAT** _(string_exp1,__string_exp2)_**)** (ODBC 1.0)|*string_exp1* *string_exp2* 연결한 결과인 문자열을 반환합니다. 결과 문자열은 DBMS에 종속됩니다. 예를 들어 *string_exp1* 나타내는 열에 NULL 값이 포함된 경우 DB2는 NULL을 반환하지만 SQL Server는 NULL이 아닌 문자열을 반환합니다.|  
|**차이(string_exp1,** _string_exp1__string_exp2)_**)** (ODBC 2.0)|*string_exp1* 및 *string_exp2*대해 SOUNDEX 함수에서 반환된 값 간의 차이를 나타내는 정수 값을 반환합니다.|  
|**INSERT** _(string_exp1,_ *시작,* *길이,* _string_exp2)_**)** (ODBC 1.0)|string_exp1 *시작부터* *길이* 문자가 삭제된 문자 *start*문자열을 반환하고 string_exp2 *string_exp* 삽입된 *string_exp2* *위치(시작부터)를*반환합니다.|  
|**LCASE(string_exp)** _string_exp_ **)** (ODBC 1.0)|모든 대문자가 소문자로 변환된 *string_exp*동일한 문자열을 반환합니다.|  
|**왼쪽(string_exp,** _string_exp_ _개수)_**)** (ODBC 1.0)|*string_exp*가장 왼쪽 *카운트* 문자를 반환합니다.|  
|**길이(string_exp)** _string_exp_ **)** (ODBC 1.0)|후행 공백을 제외한 *string_exp* 문자 수를 반환합니다.<br /><br /> **길이는** 문자열만 허용합니다. 따라서 *암시적으로 string_exp* 문자열로 변환하고 이 문자열의 길이를 반환합니다(데이터 형식의 내부 크기).|  
|**위치(string_exp1** _string_exp1_, *string_exp2* *[시작]***(ODBC** 1.0)|*string_exp2*내에서 *string_exp1* 처음 발생하는 시작 위치를 반환합니다. *선택적* 인수인 *start를*지정하지 않는 한 *string_exp1* 첫 번째 발생에 대한 검색은 string_exp2 첫 번째 문자 위치로 시작됩니다. *시작을* 지정하면 검색은 *시작*값으로 표시된 문자 위치로 시작합니다. *string_exp2* 첫 번째 문자 위치는 값 1로 표시됩니다. *string_exp2*내에 *string_exp1* 찾을 수 없는 경우 값 0이 반환됩니다.<br /><br /> 응용 프로그램이 *string_exp1*, *string_exp2*및 시작 인수를 사용하여 LOCATE 스칼라 함수를 호출하고 인수를 *시작할* 수 있는 경우 **SQLGetInfo가** SQL_STRING_FUNCTIONS *옵션으로* 호출될 때 드라이버는 SQL_FN_STR_LOCATE 반환합니다. 응용 프로그램이 *string_exp1* 및 *string_exp2* 인수만 사용하여 LOCATE 스칼라 함수를 호출할 수 있는 경우 **SQLGetInfo가** SQL_STRING_FUNCTIONS *옵션으로* 호출될 때 드라이버는 SQL_FN_STR_LOCATE_2 반환합니다. 두 개 또는 세 개의 인수로 LOCATE 함수호출을 지원하는 드라이버는 SQL_FN_STR_LOCATE SQL_FN_STR_LOCATE_2 모두 반환합니다.|  
|**LTRIM(string_exp)** _string_exp_ **)** (ODBC 1.0)|선행 공백이 제거된 *string_exp*문자를 반환합니다.|  
|**OCTET_LENGTH(string_exp)** _string_exp_ **)** (ODBC 3.0)|문자열 식의 길이(바이트)를 반환합니다. 결과는 비트 수를 8로 나눈 값보다 큰 수 중 가장 작은 정수입니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동하지 않으므로 *string_exp* 문자열로 암시적으로 변환하지 않고 대신 주어진 데이터 형식의 (내부) 크기를 반환합니다.|  
|**위치(character_exp** _character_exp_ **IN** _character_exp)_**)** (ODBC 3.0)|두 번째 문자 표현식에서 첫 번째 문자 표현식의 위치를 반환합니다. 그 결과 구현 정의 정밀도와 배율이 0인 정확한 숫자가 생성됩니다.|  
|**반복(string_exp,** _string_exp,_ _개수)_**)** (ODBC 1.0)|반복 카운트 *시간으로* 구성된 string_exp 문자 문자열을 *반환합니다.*|  
|**교체(string_exp1,** _string_exp1_ *string_exp2,* _string_exp3)_**)** (ODBC 1.0)|*string_exp2* *string_exp1* 검색하고 *string_exp3*.|  
|**오른쪽(string_exp,** _string_exp_ _개수)_**)** (ODBC 1.0)|*string_exp*가장 적합한 *카운트* 문자를 반환합니다.|  
|**RTRIM(string_exp)** _string_exp_ **)** (ODBC 1.0)|후행 공백이 제거된 *string_exp* 문자를 반환합니다.|  
|**사운드렉스(string_exp)** _string_exp_ **)** (ODBC 2.0)|*string_exp*단어의 소리를 나타내는 데이터 원본 종속 문자열을 반환합니다. 예를 들어 SQL Server는 4자리 SOUNDEX 코드를 반환합니다. 오라클은 각 단어의 발음 표현을 반환합니다.|  
|_공간(개수)_ **)** (ODBC 2.0) **SPACE(**|*카운트* 공백으로 구성된 문자 문자열을 반환합니다.|  
|**서브스트링(string_exp,** _string_exp_ *시작,***길이)** (ODBC 1.0)|*길이* 문자에 대해 *시작에* 의해 지정된 문자 위치에서 시작하여 *string_exp*파생된 문자 문자열을 반환합니다.|  
|**UCASE** _(string_exp)_ **)** (ODBC 1.0)|모든 소문자가 대문자로 변환된 *string_exp*동일한 문자열을 반환합니다.|
