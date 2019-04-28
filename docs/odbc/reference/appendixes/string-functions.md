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
manager: craigg
ms.openlocfilehash: 948e22d9a4514e4ed7b211398ac28a7338b1c0ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735151"
---
# <a name="string-functions"></a>문자열 함수
다음 표에서 문자열 조작 함수를 나열합니다. 응용 프로그램에서 호출 하 여 드라이버에서 지원 되는 문자열 함수를 확인할 수 있습니다 **SQLGetInfo** 사용 하 여는 *정보 유형* SQL_STRING_FUNCTIONS입니다.  
  
## <a name="remarks"></a>Remarks  
 로 표시 된 인수 *string_exp* 열의 이름일 수는 *문자 문자열 리터럴*, 또는 다른 스칼라 함수, SQL_CHAR, SQL_로 기본 데이터 형식을 나타낼 수 있는 결과를 VARCHAR 또는 SQL_LONGVARCHAR 합니다.  
  
 로 표시 된 인수 *character_exp* 는 가변 길이 문자 문자열입니다.  
  
 로 표시 된 인수 *시작*를 *길이*, 또는 *개수* 수는 *숫자 리터럴* 또는 다른 스칼라 함수의 결과 위치는 SQL_TINYINT, SQL_SMALLINT, 또는 SQL_INTEGER 내부 데이터 형식이 나타낼 수 있습니다.  
  
 여기에 나열 된 문자열 함수는 1부터 시작 합니다. 즉, 문자열의 첫 번째 문자는 문자 1입니다.  
  
 SQL-92에 맞게 ODBC 3.0에서 BIT_LENGTH "," CHAR_LENGTH "," CHARACTER_LENGTH "," OCTET_LENGTH, "및" 위치 문자열 스칼라 함수가 추가 되었습니다.  
  
|기능|Description|  
|--------------|-----------------|  
|**ASCII(** _string_exp_ **)**  (ODBC 1.0)|가장 왼쪽 문자의 ASCII 코드 값을 반환 합니다 *string_exp* 정수입니다.|  
|**BIT_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|문자열 식의 길이(비트)를 반환합니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동 하지 않습니다, 없습니다 암시적으로 변환 됩니다 따라서 *string_exp* 대신 문자열에 지정 되 고 모든 데이터 형식 (내부) 크기를 반환 합니다.|  
|**CHAR (** _코드_ **)** (ODBC 1.0)|가 ASCII 문자 코드에 지정 된 값 반환 *코드*합니다. 변수의 *코드* 0에서 255 사이 여야 합니다. 그렇지 않으면 반환 값은 데이터 원본에 따라 결정 됩니다.|  
|**CHAR_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|문자열 식이 문자 데이터 형식의; 이면 문자열 식의 문자에서 길이 반환 합니다. 문자열 식 (가장 작은 정수 비트 8로 나눈 수 보다 작지 않음)의 바이트 길이 반환 합니다. (이 함수는 CHARACTER_LENGTH 함수와 동일 하 게 합니다.)|  
|**CHARACTER_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|문자열 식이 문자 데이터 형식의; 이면 문자열 식의 문자에서 길이 반환 합니다. 문자열 식 (가장 작은 정수 비트 8로 나눈 수 보다 작지 않음)의 바이트 길이 반환 합니다. (이 함수는 CHAR_LENGTH 함수와 동일 하 게 합니다.)|  
|**CONCAT(** _string_exp1_,_string_exp2_**)**  (ODBC 1.0)|연결한 결과인 문자열을 반환 *string_exp2* 하 *string_exp1*합니다. 결과 문자열은 DBMS에 종속됩니다. 예를 들어 열을 나타내는 *string_exp1* 반환 NULL이 아니지만 SQL Server는 반환 된 NULL이 아닌 문자열을 NULL 값을 DB2에 포함 되어 있습니다.|  
|**DIFFERENCE(** _string_exp1_,_string_exp2_**)**  (ODBC 2.0)|에 대해 SOUNDEX 함수에서 반환 되는 값 사이의 차이 나타내는 정수 값을 반환 *string_exp1* 하 고 *string_exp2*합니다.|  
|**INSERT(** _string_exp1_, *start*, *length*, _string_exp2_**)**  (ODBC 1.0)|문자를 반환 합니다. 문자열 위치 *길이* 문자에서 삭제 되었습니다 *string_exp1*부터 *시작*, 및 위치 *string_exp2* 에 삽입 되었음을 *string_exp를* 부터 *시작*합니다.|  
|**LCASE (** _string_exp_ **)** (ODBC 1.0)|문자열을 반환 *string_exp*, 모든 대문자를 소문자로 변환 합니다.|  
|**왼쪽 (** _string_exp_하십시오 _개수_**)** (ODBC 1.0)|가장 왼쪽에 있는 반환 *개수* 자의 *string_exp*합니다.|  
|**LENGTH(** _string_exp_ **)** (ODBC 1.0)|에 있는 문자의 수를 반환 *string_exp를* 후행 공백을 제외 합니다.<br /><br /> **길이** 만 문자열을 허용 합니다. 따라서에서는 암시적으로 변환 *string_exp* 문자열 및 (내부의 크기가 아니라 데이터 형식)이이 문자열의 길이 반환 합니다.|  
|**LOCATE(** _string_exp1_, *string_exp2*[, *start*]**)** (ODBC 1.0)|첫 번째로 나타나는 시작 위치를 반환 *string_exp1* 내 *string_exp2*합니다. 처음으로 검색 *string_exp1* 의 첫 번째 문자 위치를 사용 하 여 시작 *string_exp2* 하지 않는 한 선택적 인수 *시작*를 지정 합니다. 하는 경우 *시작* 지정 된 경우의 값으로 표시 되는 문자 위치를 사용 하 여 검색을 시작할 *시작*합니다. 첫 번째 문자 위치 *string_exp2* 값 1로 표시 됩니다. 하는 경우 *string_exp1* 에 없는 *string_exp2*, 값 0이 반환 됩니다.<br /><br /> 응용 프로그램 찾기 스칼라 함수를 호출할 수 있으면를 *string_exp1*를 *string_exp2*, 및 *시작* 인수 드라이버 반환 SQL_FN_STR_LOCATE 때  **SQLGetInfo** 로 호출 되는 *옵션* SQL_STRING_FUNCTIONS입니다. 응용 프로그램에만 사용 하 여 찾기 스칼라 함수 호출 수를 *string_exp1* 하 고 *string_exp2* 인수 드라이버 반환 SQL_FN_STR_LOCATE_2 때 **SQLGetInfo**로 호출 되는 *옵션* SQL_STRING_FUNCTIONS입니다. 두 가지 또는 세 개의 인수를 사용 하 여 찾기 함수 호출을 지 원하는 드라이버 SQL_FN_STR_LOCATE 및 SQL_FN_STR_LOCATE_2 모두 반환 합니다.|  
|**LTRIM(** _string_exp_ **)** (ODBC 1.0)|문자를 반환 *string_exp*를 사용 하 여 선행 공백을 제거 합니다.|  
|**OCTET_LENGTH(** _string_exp_ **)** (ODBC 3.0)|문자열 식의 길이(바이트)를 반환합니다. 결과는 비트 수를 8로 나눈 값보다 큰 수 중 가장 작은 정수입니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동 하지 않습니다, 없습니다 암시적으로 변환 됩니다 따라서 *string_exp* 대신 문자열에 지정 되 고 모든 데이터 형식 (내부) 크기를 반환 합니다.|  
|**POSITION(** _character_exp_ **IN** _character_exp_**)** (ODBC 3.0)|두 번째 문자 식에서 첫 번째 문자 식의 위치를 반환합니다. 결과 구현 시 정의 된 전체 자릿수 및 소수 자릿수가 0 사용 하 여 정확한 숫자입니다.|  
|**반복 (** _string_exp를_ _개수_**)** (ODBC 1.0)|반환 문자열 *string_exp* 반복 *개수* 시간입니다.|  
|**REPLACE(** _string_exp1_, *string_exp2*, _string_exp3_**)** (ODBC 1.0)|검색 *string_exp1* 의 foroccurrences *string_exp2*를 바꾸고 *string_exp3*합니다.|  
|**오른쪽 (** _string_exp_하십시오 _개수_**)** (ODBC 1.0)|맨 오른쪽 반환 *개수* 자의 *string_exp*합니다.|  
|**RTRIM(** _string_exp_ **)** (ODBC 1.0)|문자를 반환 *string_exp* 후행 공백을 제거 합니다.|  
|**SOUNDEX(** _string_exp_ **)** (ODBC 2.0)|데이터 원본에 따라 결정을 나타내는 문자열의 단어 소리 반환 *string_exp*합니다. SQL Server는 4 자리 SOUNDEX 코드를 반환 하는 예를 들어, Oracle에는 각 단어의 발음 표현을 반환합니다.|  
|**공간 (** _개수_ **)** (ODBC 2.0)|구성 된 문자열을 반환 *개수* 공간입니다.|  
|**부분 문자열 (** _string_exp_하십시오 *시작*, 길이 **)** (ODBC 1.0)|파생 되는 문자열을 반환 *string_exp*에서 시작 하 여 지정 된 문자 위치 *시작* 에 대 한 *길이* 문자입니다.|  
|**UCASE(** _string_exp_ **)** (ODBC 1.0)|문자열을 반환 *string_exp*, 모든 소문자를 대문자로 변환 합니다.|
