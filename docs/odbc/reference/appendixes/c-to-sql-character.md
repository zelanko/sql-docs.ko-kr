---
title: 'C에서 SQL로: 문자 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292034"
---
# <a name="c-to-sql-character"></a>C에서 SQL로: 문자
문자 ODBC C 데이터 형식의 식별자는 다음과 같습니다.  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 다음 표에서는 C 문자 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
> [!NOTE]  
>  문자 C 데이터가 유니코드 SQL 데이터로 변환되는 경우 유니코드 데이터의 길이는 짝수여야 합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|데이터의 바이트 길이 <= 열 길이입니다.<br /><br /> 데이터의 바이트 길이는 열 길이를 >.|해당 없음<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|데이터의 문자 길이 <= 열 길이입니다.<br /><br /> 데이터의 문자 길이는 열 길이를 >.|해당 없음<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|잘리지 않고 변환된 데이터<br /><br /> 소수 자릿수의 잘림으로 변환된 데이터[e]<br /><br /> 데이터를 변환하면 전체(소수와 반대)가 손실됩니다[e]<br /><br /> 데이터 값은 *숫자 리터럴이* 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|데이터가 변환되는 데이터 형식의 범위 내에 있습니다.<br /><br /> 데이터가 번호가 변환되는 데이터 형식의 범위를 벗어났습니다.<br /><br /> 데이터 값은 *숫자 리터럴이* 아닙니다.|해당 없음<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|데이터는 0 또는 1입니다.<br /><br /> 데이터가 0보다 크고 2보다 크며 1과 같지 않습니다.<br /><br /> 데이터가 0보다 크거나 2보다 크거나 같습니다.<br /><br /> 데이터는 숫자 *리터럴이* 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(데이터 바이트 길이) / 2 <= 열 바이트 길이<br /><br /> (바이트 데이터 길이) / 2 > 컬럼 바이트 길이<br /><br /> 데이터 값은 육각형 값이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|데이터 값은 유효한 *ODBC 날짜 리터럴입니다.*<br /><br /> 데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 시간 부분은 0입니다.<br /><br /> 데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 시간 부분은 영하지 않습니다[a]<br /><br /> 데이터 값이 유효한 *ODBC 날짜 리터럴* 또는 *ODBC 타임스탬프 리터럴이* 아닙니다.|해당 없음<br /><br /> 해당 없음<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|데이터 값은 유효한 *ODBC 시간 리터럴입니다.*<br /><br /> 데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 소수 초 부분은 0[b]<br /><br /> 데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 분수 초 부분은 영하지 않습니다[b]<br /><br /> 데이터 값이 유효한 *ODBC 시간 리터럴* 또는 *ODBC 타임스탬프 리터럴이* 아닙니다.|해당 없음<br /><br /> 해당 없음<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 잘린 되지 않는 분수 초 부분<br /><br /> 데이터 값은 유효한 *ODBC-타임스탬프 리터럴입니다.* 분수 초 부분이 잘립니다.<br /><br /> 데이터 값은 유효한 *ODBC 날짜 리터럴*[c]<br /><br /> 데이터 값은 유효한 *ODBC 시간 리터럴*[d]<br /><br /> 데이터 값은 유효한 *ODBC 날짜 리터럴,* *ODBC 시간 리터럴*또는 *ODBC 시간 스탬프 리터럴이* 아닙니다.|해당 없음<br /><br /> 22008<br /><br /> 해당 없음<br /><br /> 해당 없음<br /><br /> 22018|  
|모든 SQL 간격 유형|데이터 값은 유효한 *간격 값입니다.* 잘림이 발생하지 않습니다.<br /><br /> 데이터 값은 유효한 *간격 값입니다.* 필드 중 하나의 값이 잘립니다.<br /><br /> 데이터 값이 유효한 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 타임스탬프의 시간 부분이 잘립니다.  
  
 [b] 타임스탬프의 날짜 부분은 무시됩니다.  
  
 [c] 타임스탬프의 시간 부분이 0으로 설정됩니다.  
  
 [d] 타임스탬프의 날짜 부분이 현재 날짜로 설정됩니다.  
  
 [e] 드라이버/데이터 원본은 변환을 수행하기 전에 전체 문자열이 수신될 때까지 효과적으로 기다립니다(문자 데이터가 **SQLPutData를**호출하여 조각으로 전송되는 경우에도).  
  
 문자 C 데이터가 숫자, 날짜, 시간 또는 타임스탬프 SQL 데이터로 변환되면 선행 및 후행 공백은 무시됩니다.  
  
 문자 C 데이터가 이진 SQL 데이터로 변환되면 각 두 바이트의 문자 데이터가 이진 데이터의 단일 바이트(8비트)로 변환됩니다. 각 두 바이트의 문자 데이터는 육각형 형식의 숫자를 나타냅니다. 예를 들어 "01"은 이진 00000001로 변환되고 "FF"는 이진 1111111111로 변환됩니다.  
  
 드라이버는 항상 헥사데피말 숫자 쌍을 개별 바이트로 변환하고 null 종료 바이트를 무시합니다. 따라서 문자열 문자열의 길이가 홀수인 경우 문자열의 마지막 바이트(있는 경우 null-termination 바이트 제외)는 변환되지 않습니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 문자 C 데이터를 이진 SQL 데이터 형식에 바인딩하지 않는 것이 좋습니다. 이 변환은 일반적으로 비효율적이고 느립니다.
