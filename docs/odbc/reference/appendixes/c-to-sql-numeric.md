---
title: 'C에서 SQL로: Numeric | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6dc440e27b362fef9c9794cf0005c6af0b435efc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019311"
---
# <a name="c-to-sql-numeric"></a>C에서 SQL로: 숫자
숫자 ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
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
  
 다음 표에서는 숫자 C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|숫자 <= 열 바이트 길이<br /><br /> 숫자 > 열 바이트 길이|해당 없음<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|문자 수 <= 열 문자 길이<br /><br /> 문자 수 > 열 문자 길이|해당 없음<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|잘림 없이 또는 소수 자릿수로 잘린 데이터 변환<br /><br /> 전체 자릿수가 잘린 상태로 변환 된 데이터|해당 없음<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|데이터가 변환 되는 데이터 형식의 범위 내에 있습니다.<br /><br /> 데이터가 숫자가 변환 되는 데이터 형식의 범위를 벗어났습니다.|해당 없음<br /><br /> 22003|  
|SQL_BIT|데이터가 0 또는 1입니다.<br /><br /> 데이터가 0 보다 크고 2 보다 작고 1과 같지 않습니다.<br /><br /> 데이터가 0 보다 작거나 2 보다 크거나 같습니다.|해당 없음<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|데이터가 잘리지 않습니다.<br /><br /> 데이터가 잘렸습니다.|해당 없음<br /><br /> 22015|  
  
 [a] 이러한 변환은 정확한 숫자 데이터 형식 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)에 대해서만 지원 됩니다. 근사 숫자 데이터 형식 (SQL_C_FLOAT 또는 SQL_C_DOUBLE)에서는 지원 되지 않습니다. 정확한 숫자 C 데이터 형식은 간격의 전체 자릿수가 단일 필드가 아닌 interval SQL 형식으로 변환할 수 없습니다.  
  
 [b] "n/a"의 경우, 드라이버는 소수 잘림이 있는 경우 선택적으로 SQL_SUCCESS_WITH_INFO 및 01S07를 반환할 수 있습니다.  
  
 이 드라이버는 숫자 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 숫자 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
