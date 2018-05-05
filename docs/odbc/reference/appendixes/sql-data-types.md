---
title: SQL 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba122ccbc873603b434a8541fe44aee10a5104e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-data-types"></a>SQL 데이터 형식
각 DBMS 자체 SQL 형식을 정의합니다. 각 ODBC 드라이버 관련된 DBMS 정의 하는 SQL 데이터 유형만 표시 합니다. ODBC 정의 SQL 형식 식별자에 드라이버를 매핑하는 방법에 대 한 정보 DBMS SQL가 입력 하 고 호출을 통해 반환 되는 드라이버 매핑되는 방법을 DBMS SQL 형식 자체 드라이버별 SQL 유형 식별자 **SQLGetTypeInfo**합니다. 열 및 매개 변수를 호출 하 여 데이터 형식을 설명 하는 경우 또한 드라이버 SQL 데이터 형식을 반환 **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, 및 **SQLSpecialColumns**합니다.  
  
> [!NOTE]  
>  SQL 데이터 형식은 구현 설명자의 SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 포함 됩니다. SQL 데이터 형식의 특징 구현 설명자의 SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, 및 SQL_DESC_OCTET_LENGTH 필드에 포함 되어 있습니다. 자세한 내용은 참조 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 이 부록의 뒷부분에 나오는 합니다.  
  
 지정된 된 드라이버 및 데이터 원본에서는이 부록의 내용에 정의 된 모든 SQL 데이터 형식을 반드시 지원 하지 않습니다. SQL 데이터 형식에 대 한 드라이버의 지원 드라이버를 준수 하는 SQL 92의 수준에 따라 달라 집니다. 응용 프로그램이 드라이버에서 지원 되는 SQL 92 문법의 수준을 확인, 호출 **SQLGetInfo** SQL_SQL_CONFORMANCE 정보 유형을 사용 합니다. 또한 지정된 된 드라이버 및 데이터 원본 추가, 드라이버별 SQL 데이터 형식을 지원할 수 있습니다. 응용 프로그램이 호출, 어떤 데이터 형식에서 드라이버를 확인 하려면 지원 **SQLGetTypeInfo**합니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오. 특정 데이터 원본에서 데이터 형식에 대 한 정보를 해당 데이터 원본에 대 한 설명서를 참조 하십시오.  
  
> [!IMPORTANT]  
>  이 부록 전체 표에서 지침 및 일반적으로 사용 하는 표시 이름, 범위 및 SQL 데이터 형식의 제한 됩니다. 지정된 된 데이터 원본과 나열 된 데이터 형식 중 일부만 지원할 수도 있습니다 및 지원 되는 데이터 형식의 특성 나열 된 것과 다를 수 있습니다.  
  
 다음 표에서 모든 SQL 데이터 형식에 대 한 유효한 SQL 유형 식별자를 나열합니다. 표에 나와 이름 및 SQL 92에서 해당 데이터 형식을 설명 (있는 경우).  
  
|SQL 유형 식별자 [1]|일반적인 SQL 데이터<br /><br /> [2] 유형|일반적인 형식 설명|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|고정된 문자열 길이의 문자열을 문자 *n*합니다.|  
|SQL_VARCHAR|VARCHAR (*n*)|최대 문자열 길이가 가변 길이 문자열 *n*합니다.|  
|SQL_LONGVARCHAR|LONG VARCHAR|가변 길이 문자 데이터입니다. 최대 길이 데이터 소스에 따라 다릅니다. [9]|  
|SQL_WCHAR|WCHAR (*n*)|고정된 문자열 길이의 유니코드 문자열 *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|유니코드 가변 길이 문자열 최대 문자열 길이 *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|유니코드 가변 길이 문자 데이터입니다. 최대 길이 데이터 소스에 따라 다릅니다.|  
|SQL_DECIMAL|10 진수 (*p*,*s*)|서명 됨, 정확한 숫자 값의 전체 자릿수가 이상 *p* 와 소수 자릿수 *s입니다.* (최대 전체 자릿수는 드라이버 정의 합니다.) (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|숫자 (*p*,*s*)|서명 됨, 정확한 숫자 값 전체 자릿수가 *p* 와 소수 자릿수 *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|정확한 숫자 값을 정밀도 5 및 배율 0 (서명: –32,768 < = *n* < = 32, 767 서명 되지 않은: 0 < = *n* < 65, 535 =) [3].|  
_INTEGER|INTEGER|정확한 숫자 값을 정밀도 10 및 배율 0 (서명: 있음 < = *n* < [31]-2 = 1, 서명 되지 않은: 0 < = *n* < = 2 [32]-1) [3].|  
|SQL_REAL|REAL|서명 됨, 이진 정밀도 이며 24와 숫자 값 (0 또는 10[38]) 절대값 10 [–38].|  
|SQL_FLOAT|FLOAT (*p*)|서명 됨, 이진 정밀도를 가진 숫자 값 이상 *p*합니다. (최대 전체 자릿수는 드라이버 정의 합니다.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|서명 됨, 이진 전체 자릿수가 53 인 숫자 값 (0 또는 10[308]) 절대값 10 [–308].|  
|SQL_BIT|BIT|단일 비트 이진 데이터입니다. [8]|  
|SQL_TINYINT|TINYINT|정확한 숫자 값을 정밀도 3 고 배율 0 (서명:-128 < = *n* < = 서명 되지 않은 127: 0 < = *n* < = 255) [3].|  
_BIGINT|bigint|정밀도 19 (부호 있음) 하는 경우 숫자 값 또는 20 (부호 없음) 하는 경우 및 0의 크기를 조정 (서명: – 2 [63] < = *n* < [63]-2 = 1, 서명 되지 않은: 0 < = *n* < = 2 [64]-1) [3], [9].|  
|SQL_BINARY|이진 (*n*)|고정 길이 이진 데이터 *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY (*n*)|가변 길이 이진 데이터의 최대 길이 *n*합니다. 최대는 사용자가 설정 됩니다. [9]|  
|SQL_LONGVARBINARY|LONG VARBINARY|가변 길이 이진 데이터입니다. 최대 길이 데이터 소스에 따라 다릅니다. [9]|  
|SQL_TYPE_DATE [6]|DATE|연도, 월 및 날짜 필드, 일반 달력 규칙을 준수 합니다. (참조 [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)이 부록의 뒷부분에 나오는.)|  
|SQL_TYPE_TIME [6]|시간 (*p*)|시간, 분, 및 00부터 59까지 분을 00에서 23 사이의 유효한 값의 시간에 대 한 유효한 값 및 61에 00의 시간 (초)에 대 한 유효한 값이 있는 두 번째 필드를 선택 합니다. 정밀도 *p* 초 전체 자릿수를 나타냅니다.|  
|SQL_TYPE_TIMESTAMP [6]|타임 스탬프 (*p*)|연도, 월, 일, 시간, 분 및 날짜 및 시간 데이터 형식에 대해 정의 된 대로 유효한 값을 가진 두 번째 필드|  
_TYPE_UTCDATETIME|시간|연도, 월, 일, 시, 분, 초, utchour, 및 utcminute 필드입니다. Utchour 및 utcminute 필드에는 1/10 마이크로초의 정밀도 있습니다.|  
|SQL_TYPE_UTCTIME|UTCTIME|시간, 분, 초, utchour, 및 utcminute 필드입니다. Utchour 및 utcminute 필드는 1/10 마이크로초 정밀도...|  
|SQL_INTERVAL_MONTH [7]|간격이 월 (*p*)|두 날짜 사이의 개월 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_YEAR [7]|간격 연도 (*p*)|두 날짜; 사이의 년 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|간격 연도 (*p*)을 월|년 및; 두 날짜 사이의 개월 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY [7]|간격 날짜 (*p*)|두 날짜 사이의 일 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_HOUR [7]|간격 시간 (*p*)|두 시간의 날짜/시간; *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_MINUTE [7]|간격은 1 분 (*p*)|두 간격 (분) 날짜/시간입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_SECOND [7]|간격 두 번째 (*p*,*q*)|두 시간 (초) 날짜/시간; *p* 은 전체 자릿수를 유도 하는 간격 및 *q* 간격 초 전체 자릿수입니다.|  
_INTERVAL_DAY_TO_HOUR [7]|간격 날짜 (*p*) 시간|두 날짜/시간 날짜/시간; *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|간격 날짜 (*p*) 분|일/시간/분 두 수가 날짜/시간; *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|간격 날짜 (*p*) 두 번째 (*q*)|일/시간/분/초 두 수가 날짜/시간; *p* 은 전체 자릿수를 유도 하는 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|간격 시간 (*p*) 분|두 시간/분 수 날짜/시간; *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|간격 시간 (*p*) 두 번째 (*q*)|두 시간/분/초 수 날짜/시간입니다. *p* 은 전체 자릿수를 유도 하는 간격 및 *q* 간격 초 전체 자릿수입니다.|  
_INTERVAL_MINUTE_TO_SECOND [7]|간격은 1 분 (*p*) 두 번째 (*q*)|두 분/초 수 날짜/시간; *p* 은 전체 자릿수를 유도 하는 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_GUID|GUID|고정된 길이 GUID입니다.|  
  
 [1]이를 호출 하 여 DATA_TYPE 열에 반환 된 값은 **SQLGetTypeInfo**합니다.  
  
 [2]이를 호출 하 여 이름 및 매개 변수 만들기 열에 반환 된 값은 **SQLGetTypeInfo**합니다. 이름 열을 지정은 반환-예를 들어 CHAR-반면 만들기 PARAMS 열 전체 자릿수, 소수 자릿수 및 길이 같은 생성 매개 변수는 쉼표로 구분 된 목록을 반환 합니다.  
  
 [3] 응용 프로그램 사용 **SQLGetTypeInfo** 또는 **SQLColAttribute** 특정 데이터 형식이 나 결과 집합의 특정 열 서명 된 인지 확인할 수 있습니다.  
  
 [4] SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식을 해당 정밀도 여부 에서만 다릅니다. 10 진수의 전체 자릿수 (*p*,*s*) 되는 구현에서 정의 된 10 진수 정밀도 됩니다 이상 *p*반면, 숫자의 전체 자릿수 (*p* ,*s*)과 정확히 일치 *p*합니다.  
  
 [5]에 따라 구현, 24 또는 53 SQL_FLOAT 정밀도 될 수 있습니다: 데이터 형식을 SQL_FLOAT SQL_REAL; 같습니다 24 인 경우 53 이면 SQL_FLOAT 데이터 형식이 SQL_DOUBLE와 동일 합니다.  
  
 [ODBC 3에서 6]*.x*, SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP, 되는 SQL date, time 및 timestamp 데이터 형식은 ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP 데이터 형식이 됩니다.  
  
 [7] 간격 SQL 데이터 형식에 대 한 자세한 내용은 참조는 [Interval 데이터 형식을](../../../odbc/reference/appendixes/interval-data-types.md) 이 부록의 뒷부분에 나오는 섹션.  
  
 [8] SQL_BIT 데이터 형식이 s Q l-92에 다른 비트 형식 특성에 있습니다.  
  
 [9]이 데이터 형식은 SQL 92에 해당 하는 데이터 형식을 있습니다.  
  
 이 섹션에서는 다음 예제를 제공 합니다.  
  
-   [SQLGetTypeInfo 결과 집합의 예](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
