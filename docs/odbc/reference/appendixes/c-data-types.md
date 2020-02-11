---
title: C 데이터 형식 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fe4383e397c0fd06197be2ff25e6dbb876f6c0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037773"
---
# <a name="c-data-types"></a>C 데이터 형식
ODBC C 데이터 형식은 응용 프로그램에 데이터를 저장 하는 데 사용 되는 C 버퍼의 데이터 형식을 지정 합니다.  
  
 모든 드라이버는 모든 C 데이터 형식을 지원 해야 합니다. 모든 드라이버가 지원 되는 SQL 형식을 변환할 수 있는 모든 C 형식을 지원 해야 하 고 모든 드라이버가 하나 이상의 문자 SQL 유형을 지 원하는 경우이 기능이 필요 합니다. 문자 SQL 형식은 모든 C 형식으로 변환 될 수 있으므로 모든 드라이버가 모든 C 형식을 지원 해야 합니다.  
  
 C 데이터 형식은 **SQLBindCol** 및 **SQLGetData** 함수에서 *TargetType* 인수와 *ValueType* 인수를 사용 하 여 **SQLBindParameter** 함수에 지정 됩니다. **SQLSetDescField** 를 호출 하 여 SQLSetDescRec 또는 apd의 SQL_DESC_CONCISE_TYPE 필드를 설정 하거나, *형식* 인수 (필요한 경우 *하위* 형식 인수)를 사용 하 여 **** 를 호출 하 고 *DescriptorHandle* 인수를 사용 하거나 apd의 핸들에 설정 하 여 지정할 수도 있습니다.  
  
 다음 표에서는 C 데이터 형식에 대 한 유효한 형식 식별자를 보여 줍니다. 테이블에는 각 식별자에 해당 하는 ODBC C 데이터 형식 및이 데이터 형식의 정의가 나열 됩니다.  
  
|C 형식 식별자|ODBC C typedef|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLDOUBLE|double|  
|SQL_C_BIT|SQLCHAR|부호 없는 문자|  
|SQL_C_STINYINT [j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT [j]|SQLCHAR|부호 없는 문자|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|unsigned _int64 [h]|  
|SQL_C_BINARY|SQLCHAR|unsigned char *|  
|SQL_C_BOOKMARK [i]|책갈피|unsigned long int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|  
|모든 C interval 데이터 형식|SQL_INTERVAL_STRUCT|이 부록의 뒷부분에 나오는 [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md) 섹션을 참조 하세요.|  
  
 **C 형식 식별자** SQL_C_TYPE_DATE [C]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **C 형식**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 형식 식별자** SQL_C_TYPE_TIME [C]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **C 형식**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 형식 식별자** SQL_C_TYPE_TIMESTAMP [C]  
  
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
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
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
  
 [a] 날짜/시간 C 데이터 형식의 연도, 월, 일, 시, 분 및 초 필드 값이 양력의 제약 조건을 준수 해야 합니다. 이 부록 뒷부분에 나오는 [양력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) 을 참조 하세요.  
  
 [b] 분수 필드의 값은 billionths의 수이 고 범위는 0에서 999999999 (1 10억 보다 작음)입니다. 예를 들어 반 초에 대 한 분수 필드의 값은 5억이 고, 1 초 (1 밀리초)는 100만이 고, 1 1/1000000 (마이크로초)은 1000이 고 천만 (1 나노초)의 경우는 1입니다.  
  
 ODBC 2의 [c]. *x*, C 날짜, 시간 및 타임 스탬프 데이터 형식은 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP입니다.  
  
 [d] ODBC 2.x*응용 프로그램* 은 SQL_C_BOOKMARK 아닌 SQL_C_VARBOOKMARK를 사용 해야 합니다. Odbc*3.x 응용 프로그램이* odbc 2와 함께 작동 하는 경우 *x* 드라이버의 ODBC*3.x 드라이버 관리자* 는 SQL_C_VARBOOKMARK를 SQL_C_BOOKMARK에 매핑합니다.  
  
 [e] 숫자는 little endian 모드에서 (가장 왼쪽 바이트는 최하위 바이트) SQL_NUMERIC_STRUCT 구조의 *val* 필드에 확장 된 정수로 저장 됩니다. 예를 들어 소수 자릿수가 4 인 숫자 10.001 밑수는 100010의 정수로 확장 됩니다. 이는 16 진수 형식의 186AA 이므로 SQL_NUMERIC_STRUCT의 값은 "AA 86 01 00 00 ... 00 "SQL_MAX_NUMERIC_LEN **#define**에서 정의한 바이트 수를 포함 합니다.  
  
 **SQL_NUMERIC_STRUCT**에 대 한 자세한 내용은 [방법: SQL_NUMERIC_STRUCT를 사용 하 여 숫자 데이터 검색](retrieve-numeric-data-sql-numeric-struct-kb222831.md)을 참조 하세요.  
  
 [f] 응용 프로그램의 입력에 사용 되는 SQL_C_NUMERIC 데이터 형식의 전체 자릿수 및 소수 자릿수 필드 및 응용 프로그램에 대 한 드라이버의 출력입니다. 드라이버가 SQL_NUMERIC_STRUCT에 숫자 값을 기록 하는 경우 해당 드라이버 고유의 기본값을 *전체 자릿수* 필드의 값으로 사용 하 고, *크기 조정* 필드에 대 한 응용 프로그램 설명자의 SQL_DESC_SCALE 필드 (기본값은 0)의 값을 사용 합니다. 응용 프로그램은 응용 프로그램 설명자의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드를 설정 하 여 전체 자릿수 및 소수 자릿수에 대 한 고유한 값을 제공할 수 있습니다.  
  
 [g] 부호 필드는 양수 이면 1이 고 음수 이면 0입니다.  
  
 [h] _int64 일부 컴파일러에서 제공 되지 않을 수 있습니다.  
  
 [i] _SQL_C_BOOKMARK은 ODBC 3.x에서 더 이상 사용 되지*않습니다.*  
  
 [j] _SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT는 ODBC에서 부호 있는 형식 및 부호 없는 형식 (SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG 및 SQL_C_ULONG, SQL_C_STINYINT 및 SQL_C_UTINYINT로 대체 되었습니다. Odbc 3.*x* 드라이버는 odbc 2에서 작동 해야 합니다. *x* 응용 프로그램은 SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT를 지원 해야 합니다. 호출 되는 경우 드라이버 관리자는 드라이버를 통해 해당 응용 프로그램을 전달 합니다.  
  
 [k] SQL_C_GUID SQL_CHAR 또는 SQL_WCHAR으로만 변환할 수 있습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [64비트 정수 구조](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
