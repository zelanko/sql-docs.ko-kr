---
title: 'C에서 SQL까지: 주간 간격 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3f7efb443b442d44a94cfd43629cdaedd6195b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291923"
---
# <a name="c-to-sql-day-time-intervals"></a>C에서 SQL로: 날짜-시간 간격
낮 간격 ODBC C 데이터 형식의 식별자는 다음과 같습니다.  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 다음 표에서는 C 간격 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|열 바이트 길이 >= 문자 바이트 길이<br /><br /> 문자 바이트 길이< 열 바이트 길이[a]<br /><br /> 데이터 값이 유효한 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|열 문자 길이 >= 데이터의 문자 길이<br /><br /> 데이터의 문자 길이< 열 문자 길이[a]<br /><br /> 데이터 값이 유효한 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|단일 필드 간격을 변환하면 전체 숫자가 잘림되지 않았습니다.<br /><br /> 변환결과 전체 숫자가 잘림되었습니다.|해당 없음<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|필드가 잘리지 않고 데이터 값을 변환했습니다.<br /><br /> 변환 하는 동안 하나 이상의 데이터 값 필드가 잘렸습니다.|해당 없음<br /><br /> 22015|  
  
 [a] 모든 C 간격 데이터 형식을 문자 데이터 유형으로 변환할 수 있습니다.  
  
 [b] 간격 구조의 형식 필드가 간격이 단일 필드(SQL_DAY, SQL_HOUR, SQL_MINUTE 또는 SQL_SECOND)인 경우 간격 C 형식은 모든 정확한 숫자(SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL 또는 SQL_NUMERIC)로 변환할 수 있습니다.  
  
 간격 C 형식의 기본 변환은 해당 일 시간 간격 SQL 형식입니다.  
  
 드라이버는 C 간격 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시하고 데이터 버퍼의 크기가 C 간격 데이터 형식의 크기라고 가정합니다. 길이/표시기 값은 **SQLPutData의** *StrLen_or_Ind* 인수와 **SQLBindParameter**에서 *StrLen_or_IndPtr* 인수로 지정된 버퍼에서 전달됩니다. 데이터 버퍼는 **SQLPutData의** *DataPtr* 인수와 **SQLBind매개**변수 매개 변수의 *매개 변수 값 Ptr* 인수로 지정됩니다.  
  
 다음 예제에서는 SQL_INTERVAL_STRUCT 구조에 저장된 C 간격 데이터를 데이터베이스 열로 보내는 방법을 보여 줍니다. 간격 구조에는 DAY_TO_SECOND 간격이 포함됩니다. SQL_INTERVAL_DAY_TO_MINUTE 형식의 데이터베이스 열에 저장됩니다.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
