---
title: C 데이터 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292303"
---
# <a name="c-data-types"></a>C 데이터 형식
ODBC C 데이터 형식은 응용 프로그램에 데이터를 저장하는 데 사용되는 C 버퍼의 데이터 형식을 나타냅니다.  
  
 모든 드라이버는 모든 C 데이터 형식을 지원해야 합니다. 모든 드라이버는 변환할 수 있는 모든 C 형식을 지원해야 하며 모든 드라이버는 하나 이상의 문자 SQL 형식을 지원해야 합니다. 문자 SQL 형식은 모든 C 유형으로 변환할 수 있으므로 모든 드라이버는 모든 C 유형을 지원해야 합니다.  
  
 C 데이터 형식은 *TargetType* 인수가 있는 **SQLBindCol** 및 **SQLGetData** 함수와 *ValueType* 인수를 가진 **SQLBindParameter** 함수에 지정됩니다. 또한 **SQLSetDescField를** 호출하여 ARD 또는 APD의 SQL_DESC_CONCISE_TYPE 필드를 설정하거나 **SQLSetDescRec을** *형식* 인수(필요한 경우 *하위 유형* 인수)와 *설명자 핸들* 인수를 ARD 또는 APD의 핸들로 설정하여 지정할 수도 있습니다.  
  
 다음 표에는 C 데이터 형식에 대한 유효한 형식 식별자가 나열되어 있습니다. 또한 표에는 각 식별자와 이 데이터 형식의 정의에 해당하는 ODBC C 데이터 형식도 나열됩니다.  
  
|C 유형 식별자|ODBC C 타입데프|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSmallINT|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|서명되지 않은 _int64[h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK[i]|책갈피|서명되지 않은 긴 int[d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|모든 C 간격 데이터 형식|SQL_INTERVAL_STRUCT|이 부록의 다음 부분인 [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md) 섹션을 참조하십시오.|  
  
 **C 유형 식별자** SQL_C_TYPE_DATE[c]  
  
 **ODBC C 타입데프** SQL_DATE_STRUCT  
  
 **C 형식**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 유형 식별자** SQL_C_TYPE_TIME[c]  
  
 **ODBC C 타입데프** SQL_TIME_STRUCT  
  
 **C 형식**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 유형 식별자** SQL_C_TYPE_TIMESTAMP[c]  
  
 **ODBC C 타입데프** SQL_TIMESTAMP_STRUCT  
  
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
  
 **C 유형 식별자** SQL_C_NUMERIC  
  
 **ODBC C 타입데프** SQL_NUMERIC_STRUCT  
  
 **C 형식**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 유형 식별자** SQL_C_GUID  
  
 **ODBC C 타입데프** SQLGUID  
  
 **C 형식**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 날짜 시간 C 데이터 형식의 연도, 월, 일, 시간, 분 및 두 번째 필드의 값은 [이비인게이지 언리전 달력'의 제약 조건을 준수해야 합니다. (이 부록의 후반부에서 [그레고리오력의 제약 조건을](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) 참조하십시오.)  
  
 [b] 분수 필드의 값은 1초의 수십억 분의 1이며 0에서 999,999,999(10억 미만)의 범위입니다. 예를 들어, 반초 동안 분획 필드의 값은 500,000,000이고, 100분의 1초(1밀리초)는 1,000,000이고, 100분의 1(1마이크로초)은 1,000이고, 1초(1나노초)의 10억 분의 1은 1입니다.  
  
 [c] ODBC 2에서. *x*, C 날짜, 시간 및 타임스탬프 데이터 형식은 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP.  
  
 [d] ODBC 3 *.x* 응용 프로그램은 SQL_C_BOOKMARK 아니라 SQL_C_VARBOOKMARK 사용해야 합니다. ODBC 3 *.x* 응용 프로그램이 ODBC 2에서 작동하는 경우. *x* 드라이버, ODBC 3 *.x* 드라이버 관리자는 SQL_C_BOOKMARK SQL_C_VARBOOKMARK 매핑합니다.  
  
 [e] 숫자는 작은 엔디안 모드에서 배율 정수로 SQL_NUMERIC_STRUCT 구조의 *val* 필드에 저장됩니다(가장 왼쪽바이트는 가장 중요하지 않은 바이트임). 예를 들어 배율이 4인 숫자 10.001 기본 10은 100010의 정수로 배율이 조정됩니다. 이것은 헥사데피말 형식의 186AA이기 때문에 SQL_NUMERIC_STRUCT 값은 "AA 86 01 00 00 ... 00", SQL_MAX_NUMERIC_LEN 의해 정의 된 바이트의 **수와 #define.**  
  
 **SQL_NUMERIC_STRUCT**대한 자세한 내용은 [howto: SQL_NUMERIC_STRUCT 숫자 데이터를 사용하여 검색하는](retrieve-numeric-data-sql-numeric-struct-kb222831.md)것을 참조하십시오.  
  
 [f] SQL_C_NUMERIC 데이터 형식의 정밀도 및 배율 필드는 응용 프로그램의 입력및 드라이버에서 응용 프로그램으로의 출력에 사용됩니다. 드라이버가 SQL_NUMERIC_STRUCT 숫자 값을 쓰면 자체 드라이버별 기본값을 *정밀도* 필드의 값으로 사용하고 *배율 필드에* 대한 응용 프로그램 설명자의 SQL_DESC_SCALE 필드(기본값은 0)에 값을 사용합니다. 응용 프로그램은 응용 프로그램 설명자의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드를 설정하여 정밀도와 확장에 대한 고유한 값을 제공할 수 있습니다.  
  
 [g] 부호 필드는 1이면 양수이고 0인 경우 음수입니다.  
  
 [h] _int64 일부 컴파일러에서 제공되지 않을 수 있습니다.  
  
 [i] _SQL_C_BOOKMARK ODBC 3 *.x에서*더 이상 사용되지 않았습니다.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT ODBC에서 SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG 및 SQL_C_ULONG, SQL_C_STINYINT 및 SQL_C_UTINYINT 서명되지 않은 유형으로 대체되었습니다. ODBC 2와 함께 작동해야 하는 ODBC*3.x* 드라이버입니다. *x* 응용 프로그램은 호출될 때 드라이버 관리자가 드라이버로 전달하기 때문에 SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT 지원해야 합니다.  
  
 [k] SQL_C_GUID SQL_CHAR 또는 SQL_WCHAR 변환할 수 있습니다.  
  
 이 섹션에는 다음 항목이 포함되어 있습니다.  
  
-   [64비트 정수 구조](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
