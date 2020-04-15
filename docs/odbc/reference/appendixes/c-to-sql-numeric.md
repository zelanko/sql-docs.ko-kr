---
title: 'C에서 SQL로: 숫자 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbc0a994ef95f2deca29c8a4cbb06f3167b0433f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304734"
---
# <a name="c-to-sql-numeric"></a>C에서 SQL로: 숫자
숫자 ODBC C 데이터 형식의 식별자는 다음과 같습니다.  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 다음 표에서는 숫자 C 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|숫자 <수 = 열 바이트 길이<br /><br /> 열 바이트 길이를 > 숫자 수|해당 없음<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|문자 수 <= 열 문자 길이<br /><br /> > 열 문자 길이를 > 문자 수|해당 없음<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|잘리지 않고 또는 소수 자릿수로 잘린 데이터 변환<br /><br /> 전체 자릿수 의 잘림으로 변환된 데이터|해당 없음<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|데이터가 변환되는 데이터 형식의 범위 내에 있습니다.<br /><br /> 데이터가 번호가 변환되는 데이터 형식의 범위를 벗어났습니다.|해당 없음<br /><br /> 22003|  
|SQL_BIT|데이터는 0 또는 1입니다.<br /><br /> 데이터가 0보다 크고 2보다 크며 1과 같지 않습니다.<br /><br /> 데이터가 0보다 크거나 2보다 크거나 같습니다.|해당 없음<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|데이터가 잘리지 않습니다.<br /><br /> 데이터가 잘렸습니다.|해당 없음<br /><br /> 22015|  
  
 [a] 이러한 변환은 정확한 숫자 데이터 유형(SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)에 대해서만 지원됩니다. 대략적인 숫자 데이터 유형(SQL_C_FLOAT 또는 SQL_C_DOUBLE)에는 지원되지 않습니다. 정확한 숫자 C 데이터 형식은 간격 정밀도가 단일 필드가 아닌 간격 SQL 유형으로 변환할 수 없습니다.  
  
 [b] "n/a" 케이스의 경우 드라이버가 분수 잘림이 있을 때 선택적으로 SQL_SUCCESS_WITH_INFO 01S07을 반환할 수 있습니다.  
  
 드라이버는 숫자 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시하고 데이터 버퍼의 크기가 숫자 C 데이터 형식의 크기라고 가정합니다. 길이/표시기 값은 **SQLPutData의** *StrLen_or_Ind* 인수와 **SQLBindParameter**에서 *StrLen_or_IndPtr* 인수로 지정된 버퍼에서 전달됩니다. 데이터 버퍼는 **SQLPutData의** *DataPtr* 인수와 **SQLBind매개**변수 매개 변수의 *매개 변수 값 Ptr* 인수로 지정됩니다.
