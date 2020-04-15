---
title: 'C에서 SQL까지: 연도별 간격 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306614"
---
# <a name="c-to-sql-year-month-intervals"></a>C에서 SQL로: 연-월 간격
연도 간격 ODBC C 데이터 형식의 식별자는 다음과 같습니다.  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 다음 표에서는 연도별 월 간격 C 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|열 바이트 길이 >= 문자 바이트 길이<br /><br /> 문자 바이트 길이< 열 바이트 길이[a]<br /><br /> 데이터 값이 유효한 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|열 문자 길이 >= 데이터의 문자 길이<br /><br /> 데이터의 문자 길이< 열 문자 길이[a]<br /><br /> 데이터 값이 유효한 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|단일 필드 간격을 변환하면 전체 숫자가 잘림되지 않았습니다.<br /><br /> 변환결과 전체 숫자가 잘림되었습니다.|해당 없음<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|필드가 잘리지 않고 데이터 값을 변환했습니다.<br /><br /> 변환 하는 동안 하나 이상의 데이터 값 필드가 잘렸습니다.|해당 없음<br /><br /> 22015|  
  
 [a] 모든 C 간격 데이터 형식을 문자 데이터 유형으로 변환할 수 있습니다.  
  
 [b] 간격 구조의 형식 필드가 간격이 단일 필드(SQL_YEAR 또는 SQL_MONTH)인 경우 간격 C 형식은 정확한 숫자(SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL 또는 SQL_NUMERIC)로 변환할 수 있습니다.  
  
 간격 C 형식의 기본 변환은 해당 연도 월 간격 SQL 형식입니다.  
  
 드라이버는 C 간격 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시하고 데이터 버퍼의 크기가 C 간격 데이터 형식의 크기라고 가정합니다. 길이/표시기 값은 **SQLPutData의** *StrLen_or_Ind* 인수와 **SQLBindParameter**에서 *StrLen_or_IndPtr* 인수로 지정된 버퍼에서 전달됩니다. 데이터 버퍼는 **SQLPutData의** *DataPtr* 인수와 **SQLBind매개**변수 매개 변수의 *매개 변수 값 Ptr* 인수로 지정됩니다.
