---
title: 'SQL에서 C까지: 주간 간격 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296473"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL에서 C로: 날짜-시간 간격

낮 간격 ODBC SQL 데이터 형식의 식별자는 다음과 같습니다.

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

다음 표에서는 주간 간격 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.

|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|모든 낮 시간 C 간격 유형|잘린 후행 필드 부분<br /><br /> 후행 필드 부분 잘린<br /><br /> 대상의 선행 정밀도는 원본에서 데이터를 보유할 만큼 크지 않습니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|간격 정밀도는 단일 필드였으며 데이터는 잘리지 않고 변환되었습니다.<br /><br /> 간격 정밀도는 단일 필드이고 잘린 소수<br /><br /> 간격 정밀도는 단일 필드였고 전체 필드가 잘렸습니다.<br /><br /> 간격 정밀도가 단일 필드가 아니었습니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터 길이<br /><br /> 데이터 길이<br /><br /> C 데이터 형식의 크기|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_CHAR|문자 바이트 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 일 간격 SQL 형식은 모든 일 시간 간격 C 유형으로 변환할 수 있습니다.  
  
 [b] 간격 정밀도가 단일 필드(일, 시간, 분 또는 초 중 하나)인 경우 간격 SQL 형식을 정확한 숫자(SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)로 변환할 수 있습니다.  
  
INTERVAL SQL 형식의 기본 변환은 해당 C 간격 데이터 형식입니다. 그런 다음 응용 프로그램은 열 또는 매개 변수(또는 ARD의 적절한 레코드에서 SQL_DESC_DATA_PTR 필드를 설정)를 바인딩하여 초기화된 SQL_INTERVAL_STRUCT 구조를 가리키거나 **SQLGetData**호출에서 *targetValuePtr* 인수로 SQL_ INTERVAL_STRUCT 구조에 대한 포인터를 전달합니다.  
  
다음 예제에서는 SQL_INTERVAL_DAY_TO_MINUTE 형식의 열에서 SQL_INTERVAL_STRUCT 구조로 데이터를 전송하여 DAY_TO_HOUR 간격으로 다시 돌아오는 방법을 보여 줍니다.  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
