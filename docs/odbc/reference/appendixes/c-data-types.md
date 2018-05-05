---
title: C 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08f5738d39c862184d989ed8581e488adb5da1c3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="c-data-types"></a>C 데이터 형식
ODBC C 데이터 형식에는 응용 프로그램에 데이터를 저장 하는 데 사용 되는 C 버퍼의 데이터 형식을 나타냅니다.  
  
 모든 드라이버는 모든 C 데이터 형식을 지원 해야 합니다. 이 모든 드라이버를 지 원하는 SQL 형식을 변환할 수, 일부 C 형식을 지원 해야 하기 때문에 필요 하며 모든 드라이버에서 지 원하는 SQL 형식 문자를 하나 이상. 문자 SQL 형식이 있으며 모든 C 형식으로 변환할 수 있는, 모든 드라이버는 모든 C 형식을 지원 해야 합니다.  
  
 C 데이터 형식에 지정 된 된 **SQLBindCol** 및 **SQLGetData** 함수는 *TargetType* 인수 및는 **SQLBindParameter**작동는 *ValueType* 인수입니다. 호출 하 여 지정 될 수도 있습니다 **SQLSetDescField** 카드가 또는 APD, 또는 호출 하 여 SQL_DESC_CONCISE_TYPE 필드를 설정할 **SQLSetDescRec** 와 *형식* 인수 (및 *하위* 인수가 필요한 경우) 및 *DescriptorHandle* 인수 카드가 또는 APD의 핸들을 설정 합니다.  
  
 다음 표에서 C 데이터 형식에 대 한 올바른 형식 식별자를 나열 합니다. 또한 각 식별자와이 데이터 형식의 정의에 해당 하는 ODBC C 데이터 형식을 나열 합니다.  
  
|C 형식 식별자|ODBC C typedef|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|부호 없는 short int|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|부호 없는 long int|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|부호 없는 문자|  
|SQL_C_STINYINT [j]|SQLSCHAR|서명 된 char|  
|SQL_C_UTINYINT [j]|SQLCHAR|부호 없는 문자|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|부호 없는 _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|책갈피|부호 없는 long int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|모든 C interval 데이터 형식|SQL_INTERVAL_STRUCT|참조는 [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md) 이 부록의 뒷부분에 나오는 섹션.|  
  
 **C 형식 식별자** SQL_C_TYPE_DATE [c + +]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **C 형식**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 형식 식별자** SQL_C_TYPE_TIME [c + +]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **C 형식**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 형식 식별자** SQL_C_TYPE_TIMESTAMP [c + +]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
 **C 형식**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C 형식 식별자** SQL_C_NUMERIC  
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
 **C 형식**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 형식 식별자** SQL_C_GUID  
  
 **ODBC C typedef** SQLGUID  
  
 **C 형식**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 연도, 월, 일, 시, 분, 및 C 날짜/시간 데이터 형식에서 두 번째 필드의 값 일반 달력의 제약 조건에 맞아야 합니다. (참조 [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) 이 부록의 뒷부분에 나오는.)  
  
 [b]에서 분수 필드의 값에는 두 번째 및 범위는 0에서 999999999 (1 1 십억 미만)-billionths의 수입니다. 예를 들어 0.5 초에서 분수 필드의 값은 초의 1 /에 대 한 500,000,000 (1 밀리초)는 두 번째 1000만 분 1에 대 한 1000000 (1 마이크로초) 이며, 1, 000의 billionth에 대 한 초 (1 나노초)은 1입니다.  
  
 [ODBC 2 c]의. *x*, SQL_C_DATE, SQL_C_TIME, 및 SQL_C_TIMESTAMP C date, time 및 timestamp 데이터 형식은 됩니다.  
  
 [d] ODBC 3 *.x* 응용 프로그램 SQL_C_VARBOOKMARK, 하지 SQL_C_BOOKMARK 사용 해야 합니다. ODBC 3 때 *.x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자가 SQL_C_BOOKMARK를 SQL_C_VARBOOKMARK에 매핑합니다.  
  
 [e] 번호에 저장 됩니다는 *val* little endian 모드 (최하위 바이트 되 고 왼쪽에 있는 바이트)의 크기 조정 된 정수로 SQL_NUMERIC_STRUCT 구조체의 필드입니다. 예를 들어, 4, 배율이 10.001 밑수 10 숫자를 정수로 100010의 크기가 조정 됩니다. SQL_NUMERIC_STRUCT 값 "AA 86 01 00 00... 것 이기 때문에 186AA 16 진수 형식 00"는 SQL_MAX_NUMERIC_LEN에 정의 된 바이트 수와 **#define**합니다.  
  
 에 대 한 자세한 내용은 **SQL_NUMERIC_STRUCT**, 참조 [방법: SQL_NUMERIC_STRUCT 사용 하 여 숫자 데이터를 검색](retrieve-numeric-data-sql-numeric-struct-kb222831.md)합니다.  
  
 [SQL_C_NUMERIC 데이터의 전체 자릿수 및 소수 필드 f]에서 areused 응용 프로그램에서 입력 및 출력 드라이버에서 응용 프로그램에 입력합니다. 에 대 한 값으로는 자체 드라이버 관련 기본 드라이버는 SQL_NUMERIC_STRUCT에 숫자 값을 씁니다 때 사용 됩니다는 *정밀도* 필드가, 응용 프로그램 설명자 (의 자릿수가 SQL_DESC_SCALE 필드에 값이 사용 됩니다 기본값이 0)에 대 한는 *배율* 필드입니다. 응용 프로그램의 응용 프로그램 설명자 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드를 설정 하 여 자릿수와 소수 자릿수에 대 한 고유한 값을 제공할 수 있습니다.  
  
 [g]에서 로그인 필드는 1 양수, 음수 이면 0입니다.  
  
 [일부 컴파일러에서 h] _int64를 제공할 수 있습니다.  
  
 [ODBC 3에서 i] _SQL_C_BOOKMARK를 더 이상 사용 되지 *.x*합니다.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT으로 대체 되었습니다 ODBC의 부호 있는 정수와 부호 없는 형식: SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG SQL_C_ULONG, 및 SQL_C_STINYINT 및 SQL_C_UTINYINT 합니다. ODBC 3 *.x* ODBC 2를 사용 해야 하는 드라이버. *x* 호출 될 때 드라이버 관리자를 통해 드라이버에 전달 하기 때문에 응용 프로그램 SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT를 지원 해야 합니다.  
  
 [k] SQL_C_GUID SQL_CHAR 또는 SQL_WCHAR에만 변환할 수 있습니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [64비트 정수 구조](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC의 C 데이터 유형](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
