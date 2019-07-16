---
title: 'C에서 SQL로: 날짜-시간 간격 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3a4df236273b5afcaba78052ac236669bb133f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019371"
---
# <a name="c-to-sql-day-time-intervals"></a>C에서 SQL로: 날짜-시간 간격
날짜-시간 간격 ODBC C 데이터 형식에 대 한 식별자를 다음과 같습니다.  
  
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
  
 다음 표에서 ODBC SQL 데이터 형식을 C 데이터 간격 변환할 수를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)입니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|열의 바이트 길이 > = 문자 바이트 길이<br /><br /> 열의 바이트 길이 < 문자 바이트 길이 [a]<br /><br /> 데이터 값은 리터럴 유효한 간격이 아닙니다.|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|열의 문자 길이 > 데이터의 문자 길이 =<br /><br /> 열의 문자 길이 < [a] 데이터의 길이 문자<br /><br /> 데이터 값은 리터럴 유효한 간격이 아닙니다.|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT [b] SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b] SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL[b]|변환 된 단일 필드 간격의 전체 자릿수는 잘림이 발생 하지<br /><br /> 변환 결과 전체 자릿수는 잘림이 발생 했습니다.|n/a<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|필드의 잘림 없이 데이터 값이 변환 된<br /><br /> 변환 중 데이터 값의 하나 이상의 필드를 잘렸습니다.|n/a<br /><br /> 22015|  
  
 [a] 모든 C는 interval 데이터 형식은 문자 데이터 형식으로 변환할 수 있습니다.  
  
 [b] 이면 간격 구조에 유형 필드는 간격 (SQL_DAY, SQL_HOUR, SQL_MINUTE, 또는 SQL_SECOND) 단일 필드 간격 C 형식 변환할 수 있습니다 (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT 있는 정확한 숫자 를 SQL_DECIMAL, 또는 SQL_NUMERIC).  
  
 기본 C 간격 유형 변환이 해당 날짜-시간 간격 SQL 형식입니다.  
  
 드라이버 C 간격 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 C 간격 데이터 형식의 크기를 가정 합니다. 길이/표시기 값이 전달 합니다 *StrLen_or_Ind* 인수에 **SQLPutData** 에 지정 된 버퍼는 *StrLen_or_IndPtr* 에서인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼를 *DataPtr* 에서 인수 **SQLPutData** 및 *ParameterValuePtr* 인수에서 **SQLBindParameter**.  
  
 다음 예제에서는 SQL_INTERVAL_STRUCT 구조를 데이터베이스 열에 저장 된 데이터 간격 C 전송 하는 방법을 보여 줍니다. 한 DAY_TO_SECOND 간격;을 포함 하는 간격 구조 SQL_INTERVAL_DAY_TO_MINUTE 형식의 데이터베이스 열에 저장 됩니다.  
  
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
