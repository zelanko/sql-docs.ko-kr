---
description: 'SQL에서 C로: 날짜-시간 간격'
title: 'SQL에서 C로: 날짜-시간 간격 | Microsoft Docs'
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
ms.openlocfilehash: f3c878434a6fc3b2dcbb8b09a4acfb41ecf44a84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429575"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL에서 C로: 날짜-시간 간격

일자 시간 간격 ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.

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

다음 표에서는 날짜/시간 간격 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.

|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|모든 일자 시간 C 간격 유형|후행 필드 부분이 잘리지 않음<br /><br /> 후행 필드 부분이 잘렸습니다.<br /><br /> 대상의 선행 전체 자릿수가 원본의 데이터를 보유할 만큼 크지 않습니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|간격 전체 자릿수가 단일 필드 이며 데이터가 잘리지 않고 변환 되었습니다.<br /><br /> 간격 전체 자릿수가 단일 필드 이며 소수 부분을 잘렸습니다.<br /><br /> 간격 전체 자릿수는 단일 필드 이며 전체 잘림<br /><br /> 간격 전체 자릿수가 단일 필드가 아닙니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터 길이<br /><br /> 데이터 길이<br /><br /> C 데이터 형식의 크기|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_CHAR|바이트 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 날짜-시간 간격 SQL 유형을 일 시간 간격 C 유형으로 변환할 수 있습니다.  
  
 [b] 간격 전체 자릿수가 단일 필드 (일, 시간, 분 또는 초 중 하나) 이면 interval SQL 유형을 정확한 숫자 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)로 변환할 수 있습니다.  
  
Interval SQL 형식의 기본 변환은 해당 C interval 데이터 형식입니다. 그런 다음 응용 프로그램은 열 또는 매개 변수를 바인딩하고 (또는 해당 레코드의 해당 레코드에 있는 SQL_DESC_DATA_PTR 필드를 초기화 된 SQL_INTERVAL_STRUCT 구조를 가리키도록 설정 합니다. 또는 SQL_ INTERVAL_STRUCT 구조에 대 한 포인터를 **SQLGetData**호출의 *Targetvalueptr* 인수로 전달 합니다.)  
  
다음 예에서는 SQL_INTERVAL_DAY_TO_MINUTE 형식의 열에서 SQL_INTERVAL_STRUCT 구조체로 데이터를 전송 하는 방법을 보여 줍니다 .이를 DAY_TO_HOUR 간격으로 다시 제공 합니다.  

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
