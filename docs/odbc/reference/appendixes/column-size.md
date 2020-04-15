---
title: 열 크기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306584"
---
# <a name="column-size"></a>열 크기
숫자 데이터 형식의 열(또는 매개 변수) 크기는 열 또는 매개 변수의 데이터 형식또는 데이터의 정밀도에서 사용되는 최대 자릿수로 정의됩니다. 문자 형식의 경우 이 값은 데이터의 문자 길이입니다. 이진 데이터 형식의 경우 열 크기는 데이터의 바이트 길이로 정의됩니다. 시간, 타임스탬프 및 모든 간격 데이터 형식의 경우 이 데이터의 문자 표현에 있는 문자 수입니다. 각 간결한 SQL 데이터 형식에 대해 정의된 열 크기는 다음 표에 나와 있습니다.  
  
|SQL 유형 식별자|열 크기|  
|-------------------------|-----------------|  
|모든 문자 유형[a],[b]|열 또는 매개 변수의 문자에서 정의된 또는 최대 열 크기(SQL_DESC_LENGTH 설명자 필드에 포함됨)입니다. 예를 들어 CHAR(10)으로 정의된 단일 바이트 문자 열의 열 크기는 10입니다.|  
|SQL_DECIMAL SQL_NUMERIC|정의된 숫자 수입니다. 예를 들어 NUMERIC(10,3)으로 정의된 열의 정밀도는 10입니다.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19(서명된 경우) 또는 20(서명되지 않은 경우)|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|모든 이진 유형[a],[b]|열 또는 매개 변수의 바이트로 정의된 길이 또는 최대 길이입니다. 예를 들어, BINARY(10)로 정의된 열의 길이는 10입니다.|  
|SQL_TYPE_DATE[c]|*10(yyy-mm-dd* 형식의 문자 수).|  
|SQL_TYPE_TIME[c]|*8(hh-mm-ss* 형식의 문자 수) 또는 9 + *s(hh:mm:ss*[.fff...] 형식의 문자 수, *초* 정밀도입니다.) *s*|  
|SQL_TYPE_TIMESTAMP|*16(yyy-mm-dd hh:mm* 형식의 문자 수)<br /><br /> *19(yyy-mm-dd* *hh:mm:ss* 형식의 문자 수)<br /><br /> 또는<br /><br /> 20 + *s* *(yyyy-mm-dd hh:mm:mm:ss*[.fff...] 형식의 문자 수, *여기서 s는* 초 정밀도입니다).|  
|SQL_INTERVAL_SECOND|*여기서 p는* 정밀도를 선도하는 간격이고 *s는* 초 정밀도, *p(s* =0) 또는 *ps*+*s*+1(>*s* *0)입니다.* [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|*여기서 p는* 정밀도를 선도하는 간격이고 *s는* 초 정밀도, 9+*p(s* *s*=0) 또는 10+*ps(s* *p*+ *s*>0)입니다. [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|*여기서 p는* 정밀도를 선도하는 간격이고 *s는* 초 정밀도, 6+*p(s* =0) *s*또는 7+*ps(>* *p*+ *0)입니다.* [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|*여기서 p는* 정밀도를 선도하는 간격이고 *s는* 초 정밀도, 3+*p(s* =0) 또는 4+p*p*+*s(s*>0)입니다. *s* *s* [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p는* *여기서 p는* 정밀도를 선도하는 간격입니다. [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3+*p*, *여기서 p는* 정밀도를 선도하는 간격입니다. [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6+*p*, *여기서 p는* 정밀도를 선도하는 간격입니다. [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3+*p*, *여기서 p는* 정밀도를 선도하는 간격입니다. [d]|  
|SQL_GUID|*36(aaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeeeeee* 형식의 문자 수)|  
  
 [a] ODBC 2.0 드라이버에서 **SQLSetParam을** 호출하는 ODBC 1.0 응용 프로그램과 ODBC 1.0 드라이버에서 **SQLBindParameter를** 호출하는 ODBC 2.0 응용 프로그램의 경우 \* *StrLen_or_IndPtr* SQL_LONGVARCHAR 또는 SQL_LONGVARBINARY 형식에 대해 SQL_DATA_AT_EXEC 경우 *ColumnSize는* 이 테이블에 정의된 정밀도가 아닌 전송할 데이터의 총 길이로 설정되어야 합니다.  
  
 [b] 드라이버가 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환합니다.  
  
 [c] **SQLBindParameter의** *ColumnSize* 인수는 이 데이터 형식에 대해 무시됩니다.  
  
 [d] 간격 데이터 형식의 열 길이에 대한 일반 규칙은 이 부록의 이전 참조 [간격 데이터 형식 길이를](../../../odbc/reference/appendixes/interval-data-type-length.md)참조하십시오.  
  
 열(또는 매개 변수) 크기에 대해 반환된 값은 하나의 설명자 필드의 값과 일치하지 않습니다. 값은 다음 표와 같이 데이터 유형에 따라 SQL_DESC_PRECISION 또는 SQL_DESC_LENGTH 필드에서 올 수 있습니다.  
  
|SQL 유형|대응하는 설명자 필드<br /><br /> 열 또는 매개 변수 크기|  
|--------------|--------------------------------------------------------------------|  
|모든 문자 및 이진 형식|LENGTH|  
|모든 숫자 유형|PRECISION|  
|모든 날짜 시간 및 간격 유형|LENGTH|  
|SQL_BIT|LENGTH|
