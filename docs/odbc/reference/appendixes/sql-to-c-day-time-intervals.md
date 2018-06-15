---
title: 'C: 날짜-시간 간격으로 SQL | Microsoft Docs'
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
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0155a2ac3d07ce4d31562abdd0094d41467ca192
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910618"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL에서 c: 날짜-시간 간격
주간 시간 간격 ODBC SQL 데이터 형식에 대 한 식별자는.  
  
 SQL_INTERVAL_DAY  
  
 SQL_INTERVAL_DAY_TO_MINUTE  
  
 SQL_INTERVAL_HOUR  
  
 SQL_INTERVAL_DAY_TO_SECOND  
  
 SQL_INTERVAL_MINUTE  
  
 SQL_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_INTERVAL_SECOND  
  
 SQL_INTERVAL_HOUR_TO_SECOND  
  
 SQL_INTERVAL_DAY_TO_HOUR  
  
 SQL_INTERVAL_MINUTE_TO_SECOND  
  
 다음 표에서 ODBC C 데이터 형식에 하루 시간 간격 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|모든 하루 시간 C 간격 유형|잘리지 후행 필드 부분<br /><br /> 잘린 후행 필드 부분<br /><br /> 원본에서 데이터를 보유할 만큼 크지 않습니다 대상의 전체 자릿수를 유도|Data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|데이터의 길이<br /><br /> 데이터의 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22015|  
|[B] [b] [b] [b] [b] [b] [b] [b] SQL_C_BIGINT SQL_C_NUMERIC SQL_C_ULONG SQL_C_SLONG SQL_C_SHORT SQL_C_USHORT SQL_C_UTINYINT SQL_C_STINYINT|간격 정밀도 단일 필드 였으며 잘림 없이 데이터 변환<br /><br /> 간격 정밀도 단일 필드 였으며 잘린 소수 자릿수<br /><br /> 간격 정밀도 단일 필드 및 잘린 전체<br /><br /> 간격 정밀도 단일 필드 없습니다.|Data<br /><br /> 잘린된 데이터<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터의 길이<br /><br /> 데이터의 길이<br /><br /> C 데이터 형식의 크기|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|Data<br /><br /> 정의되지 않음|데이터의 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_CHAR|문자 바이트 길이 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 > = *BufferLength*|Data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
_C_WCHAR|문자 길이 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 > = *BufferLength*|Data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 SQL 유형 [a] A 하루 시간 간격을 일 시간 간격 C 형식으로 변환할 수 있습니다.  
  
 [b] 이면 간격 정밀도 (날짜, 시간, 분 또는 초 중 하나)는 단일 필드는 정확한 숫자 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG, 또는 SQL_C_NUMERIC)에 SQL 유형 간격을 변환할 수 있습니다.  
  
 해당 C 간격 데이터 형식을 SQL 유형 간격의 기본 변환이 됩니다. 응용 프로그램이 다음 열 또는 매개 변수를 바인딩합니다 (또는 카드가의 적절 한 레코드에 SQL_DESC_DATA_PTR 필드가 설정) 초기화 SQL_INTERVAL_STRUCT 구조를 가리키도록 (SQL_ INTERVAL_STRUCT 구조는 로에대한포인터를전달하거나*TargetValuePtr* 인수에 대 한 호출에 **SQLGetData**).  
  
 다음 예제에서는 DAY_TO_HOUR 간격으로 다시 들어올 되도록 SQL_INTERVAL_DAY_TO_MINUTE 유형의 열에서 SQL_INTERVAL_STRUCT 구조로 전송 하는 방법을 보여 줍니다.  
  
```  
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
