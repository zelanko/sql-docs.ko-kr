---
title: 문자열 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4ec3e05acfd4faaafd38a79e48c67d03d86bd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070170"
---
# <a name="string-functions"></a>문자열 함수
다음 표에서는 문자열 조작 함수를 보여 줍니다. 응용 프로그램은 SQL_STRING_FUNCTIONS *정보 형식* 으로 **SQLGetInfo** 를 호출 하 여 드라이버에서 지원 되는 문자열 함수를 확인할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 *String_exp* 로 표시 되는 인수는 열 이름, *문자 문자열 리터럴*또는 다른 스칼라 함수의 결과 일 수 있습니다 .이 경우 기본 데이터 형식은 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR로 표시 될 수 있습니다.  
  
 *Character_exp* 로 표시 되는 인수는 가변 길이 문자열입니다.  
  
 *시작*, *길이*또는 *개수로* 표시 되는 인수는 *숫자 리터럴이* 나 다른 스칼라 함수의 결과일 수 있습니다. 여기에서 기본 데이터 형식은 SQL_TINYINT, SQL_SMALLINT 또는 SQL_INTEGER으로 표시 될 수 있습니다.  
  
 여기에 나열 된 문자열 함수는 1부터 사용 됩니다. 즉, 문자열의 첫 번째 문자는 문자 1입니다.  
  
 BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH 및 위치 문자열 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가 되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**ASCII (** _string_exp_ **)** (ODBC 1.0)|*String_exp* 에서 가장 왼쪽 문자의 ASCII 코드 값을 정수로 반환 합니다.|  
|**BIT_LENGTH (** _string_exp_ **)** (ODBC 3.0)|문자열 식의 길이(비트)를 반환합니다.<br /><br /> 는 문자열 데이터 형식에 대해서만 작동 하지 않으므로 암시적으로 *string_exp* 문자열로 변환 되지 않고 대신 지정 된 데이터 형식의 (내부) 크기를 반환 합니다.|  
|**CHAR (** _코드_ **)** (ODBC 1.0)|*코드*에 지정 된 ASCII 코드 값을 포함 하는 문자를 반환 합니다. *코드* 의 값은 0에서 255 사이 여야 합니다. 그렇지 않으면 반환 값은 데이터 원본에 따라 달라 집니다.|  
|**CHAR_LENGTH (** _string_exp_ **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식이 면 문자열 식의 문자 길이를 반환 합니다. 그렇지 않으면 문자열 식의 길이 (바이트)를 반환 합니다 (비트 수를 8로 나눈 값 보다 작은 정수). 이 함수는 CHARACTER_LENGTH 함수와 동일 합니다.|  
|**CHARACTER_LENGTH (** _string_exp_ **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식이 면 문자열 식의 문자 길이를 반환 합니다. 그렇지 않으면 문자열 식의 길이 (바이트)를 반환 합니다 (비트 수를 8로 나눈 값 보다 작은 정수). 이 함수는 CHAR_LENGTH 함수와 동일 합니다.|  
|**CONCAT (** _string_exp1_,_string_exp2_**)** (ODBC 1.0)|*String_exp1*에 *string_exp2* 를 연결한 결과인 문자열을 반환 합니다. 결과 문자열은 DBMS에 종속됩니다. 예를 들어 *string_exp1* 표시 된 열에 null 값이 포함 된 경우 DB2는 null을 반환 하지만 SQL SERVER는 null이 아닌 문자열을 반환 합니다.|  
|**차이 (** _string_exp1_,_string_exp2_**)** (ODBC 2.0)|*String_exp1* 및 *string_exp2*에 대 한 SOUNDEX 함수에서 반환 되는 값의 차이를 나타내는 정수 값을 반환 합니다.|  
|**INSERT (** _string_exp1_, *start*, *length*, _string_exp2_**)** (ODBC 1.0)|*시작에서*시작 하 여 *string_exp1*에서 *길이* 문자가 삭제 되 고 *string_exp2* *string_exp* 에 삽입 된 문자열을 반환 *합니다.*|  
|**LCASE (** _string_exp_ **)** (ODBC 1.0)|모든 대문자를 소문자로 변환 하 여 *string_exp*에 있는 문자열과 동일한 문자열을 반환 합니다.|  
|**LEFT (** _string_exp_, _count_**)** (ODBC 1.0)|*String_exp*의 가장 왼쪽 *카운트* 문자를 반환 합니다.|  
|**길이 (** _string_exp_ **)** (ODBC 1.0)|후행 공백을 제외 *하 고 string_exp* 의 문자 수를 반환 합니다.<br /><br /> **길이** 는 문자열만 허용 합니다. 따라서는 *string_exp* 문자열로 암시적으로 변환 하 고이 문자열의 길이 (데이터 형식의 내부 크기는 아님)를 반환 합니다.|  
|**찾기 (** _string_exp1_, *string_exp2*[, *시작*]**)** (ODBC 1.0)|*String_exp2*내에서 *string_exp1* 처음으로 나타나는 시작 위치를 반환 합니다. 첫 번째 *string_exp1* 검색은 *string_exp2* 의 첫 번째 문자 위치에서 시작 하 고, 선택적인 인수인 *시작*이 지정 되지 않은 경우에 시작 합니다. *Start* 를 지정 하면 *start*값으로 표시 되는 문자 위치로 검색이 시작 됩니다. *String_exp2* 에서 첫 번째 문자 위치는 값 1로 표시 됩니다. *String_exp2*내에 *string_exp1* 없는 경우 값 0이 반환 됩니다.<br /><br /> 응용 프로그램에서 *string_exp1*, *string_exp2*및 *시작* 인수를 사용 하 여 찾기 스칼라 함수를 호출할 수 있는 경우 SQL_STRING_FUNCTIONS의 *옵션* 을 사용 하 여 **SQLGetInfo** 를 호출 하면 드라이버가 SQL_FN_STR_LOCATE 반환 됩니다. 응용 프로그램에서 *string_exp1* 및 *string_exp2* 인수만 사용 하 여 찾기 스칼라 함수를 호출할 수 있는 경우 SQL_STRING_FUNCTIONS의 *옵션* 을 사용 하 여 **SQLGetInfo** 를 호출 하면 드라이버가 SQL_FN_STR_LOCATE_2 반환 됩니다. 두 개 또는 세 개의 인수를 사용 하 여 찾기 함수를 호출할 수 있도록 지 원하는 드라이버는 SQL_FN_STR_LOCATE 및 SQL_FN_STR_LOCATE_2를 모두 반환 합니다.|  
|**LTRIM (** _string_exp_ **)** (ODBC 1.0)|선행 공백이 제거 된 *string_exp*의 문자를 반환 합니다.|  
|**OCTET_LENGTH (** _string_exp_ **)** (ODBC 3.0)|문자열 식의 길이(바이트)를 반환합니다. 결과는 비트 수를 8로 나눈 값보다 큰 수 중 가장 작은 정수입니다.<br /><br /> 는 문자열 데이터 형식에 대해서만 작동 하지 않으므로 암시적으로 *string_exp* 문자열로 변환 되지 않고 대신 지정 된 데이터 형식의 (내부) 크기를 반환 합니다.|  
|**POSITION (** _character_exp_ **** _character_exp_**)** (ODBC 3.0)|두 번째 문자 식에서 첫 번째 문자 식의 위치를 반환 합니다. 결과는 구현에서 정의 된 전체 자릿수와 소수 자릿수가 0 인 정확한 숫자입니다.|  
|**REPEAT (** _string_exp,_ _count_**)** (ODBC 1.0)|*String_exp* *반복 횟수* 로 구성 된 문자열을 반환 합니다.|  
|**REPLACE (** _string_exp1_, *string_exp2*, _string_exp3_**)** (ODBC 1.0)|String_exp2 *string_exp1* 검색 하 여 ** *string_exp3*으로 바꿉니다.|  
|**RIGHT (** _string_exp_, _count_**)** (ODBC 1.0)|*String_exp*의 가장 오른쪽 *카운트* 문자를 반환 합니다.|  
|**RTRIM (** _string_exp_ **)** (ODBC 1.0)|후행 공백이 제거 된 *string_exp* 의 문자를 반환 합니다.|  
|**SOUNDEX (** _string_exp_ **)** (ODBC 2.0)|*String_exp*에 있는 단어의 소리를 나타내는 데이터 소스 종속 문자열을 반환 합니다. 예를 들어 SQL Server은 4 자리 SOUNDEX 코드를 반환 합니다. Oracle은 각 단어의 발음을 반환 합니다.|  
|**공간 (** _개수_ **)** (ODBC 2.0)|*개수* 공간으로 구성 된 문자열을 반환 합니다.|  
|**SUBSTRING (** _string_exp_, *start*, length **)** (ODBC 1.0)|*Start* 에 지정 된 문자 위치에서 시작 하 여 *길이* 문자에서 시작 하는 *string_exp*에서 파생 되는 문자열을 반환 합니다.|  
|**UCASE (** _string_exp_ **)** (ODBC 1.0)|모든 소문자가 대문자로 변환 된 *string_exp*의 문자열과 동일한 문자열을 반환 합니다.|
