---
title: "문자열 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a9afffd67b839b36e663404048ac741e068b015
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="string-functions"></a>문자열 함수
다음 표에서 문자열 조작 함수를 나열합니다. 응용 프로그램에서 호출 하 여 드라이버를 통해 지원 되는 문자열 함수를 확인할 수 **SQLGetInfo** 와 *정보 유형* SQL_STRING_FUNCTIONS입니다.  
  
## <a name="remarks"></a>주의  
 로 표시 된 인수 *string_exp* 열 이름이 될 수 있습니다는 *문자 문자열 리터럴*, 또는 SQL_CHAR, SQL_로 기본 데이터 형식을 나타낼 수 있는 다른 스칼라 함수, 결과 VARCHAR 또는 SQL_LONGVARCHAR 합니다.  
  
 로 표시 된 인수 *character_exp* 가변 길이 문자 문자열입니다.  
  
 로 표시 된 인수 *시작*, *길이*, 또는 *count* 수는 *숫자 리터럴* 또는 다른 스칼라 함수의 결과 위치는 내부 데이터 형식은 SQL_TINYINT, SQL_SMALLINT, 또는 SQL_INTEGER로 나타낼 수 있습니다.  
  
 여기에 나열 된 문자열 함수는 1부터 시작 합니다. 즉, 문자열의 첫 번째 문자는 문자 1입니다.  
  
 BIT_LENGTH CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH, 위치, 및 문자열 스칼라 함수 s Q l-92에 맞게 ODBC 3.0에서 추가 되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|가장 왼쪽 문자의 ASCII 코드 값을 반환 *string_exp* 나타내는 정수입니다.|  
|**BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|문자열 식의 길이(비트)를 반환합니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동 하지 않습니다, 따라서 convert 암시적으로 하지 것입니다 *string_exp* 문자열 대신에 모든 데이터 형식의 관계에 지정 됩니다 (내부) 크기를 반환 합니다.|  
|**CHAR (** *코드* **)** (ODBC 1.0)|가 ASCII 문자 코드에 지정 된 값 반환 *코드*합니다. 값 *코드* 0에서 255 사이 여야 합니다. 그렇지 않으면 반환 값은 데이터 소스에 따라 다릅니다.|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식의; 문자열 식의 문자 길이 반환 그렇지 않으면 문자열 식 (가장 작은 정수 비트 8로 나눈 값 수가 보다 작지 않음)의 바이트 길이 반환 합니다. (이 함수는 CHARACTER_LENGTH 함수와 같습니다.)|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|문자열 식이 문자 데이터 형식의; 문자열 식의 문자 길이 반환 그렇지 않으면 문자열 식 (가장 작은 정수 비트 8로 나눈 값 수가 보다 작지 않음)의 바이트 길이 반환 합니다. (이 함수는 CHAR_LENGTH 함수와 같습니다.)|  
|**CONCAT (** *string_exp1*,*string_exp2***)** (ODBC 1.0)|연결한 결과인 문자열을 반환 *string_exp2* 를 *string_exp1*합니다. 결과 문자열은 DBMS에 종속됩니다. 예를 들어,으로 표시 되는 열 *string_exp1* 반환 NULL 하지만 SQL Server는 반환 NULL이 아닌 문자열에 NULL 값을 d b 2를 포함 합니다.|  
|**차이 (** *string_exp1*,*string_exp2***)** (ODBC 2.0)|에 대 한 SOUNDEX 함수에서 반환 된 값 간의 차이 나타내는 정수 값을 반환 *string_exp1* 및 *string_exp2*합니다.|  
|**삽입 (** *string_exp1*, *시작*, *길이*, *string_exp2***)** (ODBC 1.0)|문자 반환 문자열 where *길이* 문자에서 삭제 된 *string_exp1*인스턴스에서 시작 *시작*, 위치 및 *string_exp2* 에 삽입 되었음을 *string_exp,* 부터 *시작*합니다.|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|문자열을 반환 *string_exp*, 모든 대 문자가 소문자로 변환 합니다.|  
|**왼쪽 (** *string_exp*, *count***)** (ODBC 1.0)|맨 왼쪽 반환 *count* 자의 *string_exp*합니다.|  
|**길이 (** *string_exp* **)** (ODBC 1.0)|에 있는 문자의 수를 반환 *string_exp,* 후행 공백을 제외 하 고 있습니다.<br /><br /> **길이** 만 문자열을 허용 합니다. 따라서에서는 암시적으로 변환 *string_exp* 을 문자열과이 문자열 (내부의 크기가 아닌 데이터 형식)의 길이 반환 합니다.|  
|**찾습니다 (** *string_exp1*, *string_exp2*[, *시작*]**)** (ODBC 1.0)|첫 번째로 나타나는 항목의 시작 위치 반환 *string_exp1* 내 *string_exp2*합니다. 첫 번째로 나타나는 항목에 대 한 검색 *string_exp1* 에서 첫 번째 문자 위치부터 시작 *string_exp2* 하지 않으면 선택적 인수 *시작*를 지정 합니다. 경우 *시작* 검색의 값이 지정 된 문자 위치부터 지정 된 *시작*합니다. 첫 번째 문자 위치에서 *string_exp2* 값 1로 표시 됩니다. 경우 *string_exp1* 에 없는 *string_exp2*, 값 0이 반환 됩니다.<br /><br /> 응용 프로그램 사용 하 여 찾기 스칼라 함수를 호출할 수는 경우는 *string_exp1*, *string_exp2*, 및 *시작* 인수, 드라이버 반환 SQL_FN_STR_LOCATE 때 ** SQLGetInfo** 로 호출 되는 *옵션* SQL_STRING_FUNCTIONS입니다. 응용 프로그램에만 사용 하 여 찾기 스칼라 함수 호출 수는 *string_exp1* 및 *string_exp2* 인수, 드라이버 반환 SQL_FN_STR_LOCATE_2 때 **SQLGetInfo**로 호출 되는 *옵션* SQL_STRING_FUNCTIONS입니다. 두 개 또는 세 개의 인수를 사용 하 여 찾기 함수 호출을 지원 드라이버 SQL_FN_STR_LOCATE 및 SQL_FN_STR_LOCATE_2 모두 반환 합니다.|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|문자를 반환 *string_exp*, 앞 공백을 제거 합니다.|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|문자열 식의 길이(바이트)를 반환합니다. 결과는 비트 수를 8로 나눈 값보다 큰 수 중 가장 작은 정수입니다.<br /><br /> 문자열 데이터 형식에 대해서만 작동 하지 않습니다, 따라서 convert 암시적으로 하지 것입니다 *string_exp* 문자열 대신에 모든 데이터 형식의 관계에 지정 됩니다 (내부) 크기를 반환 합니다.|  
|**위치 (** *character_exp* **IN** *character_exp***)** (ODBC 3.0)|두 번째 문자 식에서 첫 번째 문자 식의 위치를 반환합니다. 결과 구현에서 정의 된 전체 자릿수 및 소수 자릿수가 0 정확한 숫자입니다.|  
|**반복 (** *string_exp,* *count***)** (ODBC 1.0)|반환 문자열 이루어져 *string_exp* 반복 *count* 시간입니다.|  
|**대체 (** *string_exp1*, *string_exp2*, *string_exp3***)** (ODBC 1.0)|검색 *string_exp1* 의 foroccurrences *string_exp2*, 대체 및 *string_exp3*합니다.|  
|**오른쪽 (** *string_exp*, *count***)** (ODBC 1.0)|맨 오른쪽 반환 *count* 자의 *string_exp*합니다.|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|문자를 반환 *string_exp* 후행 공백을 제거 합니다.|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|데이터 소스에 따라 다릅니다를 나타내는 문자열에 있는 단어의 소리 반환 *string_exp*합니다. SQL Server;는 4 자리 SOUNDEX 코드를 반환 하는 예를 들어 Oracle 각 단어의 발음을 반환합니다.|  
|**공간 (** *count* **)** (ODBC 2.0)|구성 된 문자열을 반환 *count* 공간입니다.|  
|**SUBSTRING (** *string_exp*, *시작*, 길이**)** (ODBC 1.0)|파생 된 문자열을 반환 *string_exp*로 지정 된 문자 위치에서 시작, *시작* 에 대 한 *길이* 문자입니다.|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|문자열을 반환 *string_exp*, 모든 소문자를 대문자로 변환 합니다.|
