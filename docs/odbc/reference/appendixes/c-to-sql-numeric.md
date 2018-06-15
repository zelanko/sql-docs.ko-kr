---
title: 'C에서 SQL로: 숫자 | Microsoft Docs'
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
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b47617c9905571095d09f06aab1ac5cceb9b9eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906988"
---
# <a name="c-to-sql-numeric"></a>C에서 SQL로: 숫자
숫자 ODBC C 데이터 형식에 대 한 식별자는.  
  
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
  
 다음 표에서 ODBC SQL 데이터 형식이 숫자 C 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|자릿수 < = 바이트 길이 열<br /><br /> 자릿수 > 열의 바이트 길이|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|문자 수가 < = 열 문자 길이<br /><br /> 문자 수가 > 열 문자 길이|n/a<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|데이터 잘림 없이 변환 또는와 소수 자릿수 잘립니다.<br /><br /> 데이터 잘림 자릿수로 변환|n/a<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|숫자를 변환 하는 데이터 형식 범위 내에서 데이터를<br /><br /> 데이터는 숫자를 변환 하는 데이터 형식의 범위를 벗어납니다.|n/a<br /><br /> 22003|  
|SQL_BIT|데이터는 0 또는 1<br /><br /> 데이터 0, 2, 보다 작음 및 1과 같지 않은 보다 큽니다.<br /><br /> 데이터는 0 보다 작거나 또는 2 보다 크거나|n/a<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|데이터가 잘리지 않습니다.<br /><br /> 데이터가 잘렸습니다.|n/a<br /><br /> 22015|  
  
 [a] 이러한 변환이 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG, 또는 SQL_C_NUMERIC) 정확한 숫자 데이터 형식에 대해서만 지원 됩니다. 근사 숫자 데이터 형식 (SQL_C_FLOAT 또는 SQL_C_DOUBLE)에 대 한 지원 되지 않습니다. 정확한 숫자 C 데이터 형식은 간격 간격 전체 자릿수가 단일 필드가 아닙니다. SQL 유형으로 변환할 수 없습니다.  
  
 [b] "해당 없음" 사례에 대 한 드라이버를 반환할 수 있습니다 필요에 따라 SQL_SUCCESS_WITH_INFO 및 01S07 소수 잘림 경우.  
  
 드라이버는 숫자 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기는 숫자 C 데이터 형식 크기 있다고 가정 합니다. 에 길이/표시기 값이 전달 되는 *StrLen_or_Ind* 인수 **SQLPutData** 및 지정 된 버퍼는 *StrLen_or_IndPtr* 인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼는 *DataPtr* 인수에 **SQLPutData** 및 *ParameterValuePtr* 인수에 **SQLBindParameter**.
