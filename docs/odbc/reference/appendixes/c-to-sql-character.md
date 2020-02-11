---
title: 'C에서 SQL로: 문자 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f30e0cf7622de5124cb151288417bb508354ce0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037722"
---
# <a name="c-to-sql-character"></a>C에서 SQL로: 문자
ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 다음 표에서는 C 문자 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
> [!NOTE]  
>  문자 C 데이터가 유니코드 SQL 데이터로 변환 되는 경우 유니코드 데이터의 길이는 짝수 여야 합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|데이터의 바이트 길이 <= 열 길이입니다.<br /><br /> 열 길이 > 데이터의 바이트 길이입니다.|해당 없음<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|데이터 <의 문자 길이 = 열 길이입니다.<br /><br /> 데이터의 문자 길이 > 열 길이입니다.|해당 없음<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|잘림 없이 변환 된 데이터<br /><br /> 소수 자릿수로 잘린 데이터 변환 [e]<br /><br /> 데이터를 변환 하면 소수 자릿수가 아니라 전체 손실이 발생 합니다. [e]<br /><br /> 데이터 값이 *숫자 리터럴이* 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|데이터가 변환 되는 데이터 형식의 범위 내에 있습니다.<br /><br /> 데이터가 숫자가 변환 되는 데이터 형식의 범위를 벗어났습니다.<br /><br /> 데이터 값이 *숫자 리터럴이* 아닙니다.|해당 없음<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|데이터가 0 또는 1입니다.<br /><br /> 데이터가 0 보다 크고 2 보다 작고 1과 같지 않습니다.<br /><br /> 데이터가 0 보다 작거나 2 보다 크거나 같습니다.<br /><br /> 데이터가 *숫자 리터럴이* 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(데이터의 바이트 길이)/2 <= 열 바이트 길이<br /><br /> (데이터의 바이트 길이)/2 > 열 바이트 길이<br /><br /> 데이터 값이 16 진수 값이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|데이터 값이 올바른 *ODBC 날짜 리터럴입니다* .<br /><br /> 데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 시간 부분이 0입니다.<br /><br /> 데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 시간 부분은 0이 아닙니다. [a]<br /><br /> 데이터 값이 올바른 *ODBC 날짜 리터럴* 또는 *odbc-타임 스탬프-리터럴이* 아닙니다.|해당 없음<br /><br /> 해당 없음<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|데이터 값이 올바른 *ODBC 시간 리터럴입니다* .<br /><br /> 데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 소수 자릿수 초 부분은 0 [b]입니다.<br /><br /> 데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 소수 자릿수 초 부분은 0이 아닙니다. [b]<br /><br /> 데이터 값이 올바른 *ODBC 시간 리터럴* 또는 *odbc-타임 스탬프 리터럴이* 아닙니다.|해당 없음<br /><br /> 해당 없음<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 소수 자릿수 초 부분이 잘리지 않음<br /><br /> 데이터 값이 올바른 *ODBC 타임 스탬프-리터럴*입니다. 소수 자릿수 초 부분이 잘렸습니다.<br /><br /> 데이터 값이 올바른 *ODBC 날짜 리터럴*[c]입니다.<br /><br /> 데이터 값이 올바른 *ODBC 시간 리터럴*[d]입니다.<br /><br /> 데이터 값이 올바른 *ODBC 날짜-리터럴*, *odbc 시간 리터럴*또는 *odbc-타임 스탬프-리터럴이* 아닙니다.|해당 없음<br /><br /> 22008<br /><br /> 해당 없음<br /><br /> 해당 없음<br /><br /> 22018|  
|모든 SQL 간격 유형|데이터 값이 유효한 *간격 값*입니다. 잘림이 발생 하지 않음<br /><br /> 데이터 값이 유효한 *간격 값*입니다. 필드 중 하나의 값이 잘립니다.<br /><br /> 데이터 값이 올바른 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 타임 스탬프의 시간 부분이 잘립니다.  
  
 [b] 타임 스탬프의 날짜 부분은 무시 됩니다.  
  
 [c] 타임 스탬프의 시간 부분은 0으로 설정 됩니다.  
  
 [d] 타임 스탬프의 날짜 부분이 현재 날짜로 설정 됩니다.  
  
 [e] 변환 수행을 시도 하기 전에 전체 문자열을 받을 때까지 ( **Sqlputdata**를 호출 하 여 문자 데이터를 전달 하는 경우에도) 드라이버/데이터 원본은 효과적으로 대기 합니다.  
  
 문자 C 데이터가 숫자, 날짜, 시간 또는 타임 스탬프 SQL 데이터로 변환 되 면 선행 및 후행 공백이 무시 됩니다.  
  
 문자 C 데이터가 이진 SQL 데이터로 변환 되는 경우 두 바이트의 문자 데이터는 이진 데이터의 단일 바이트 (8 비트)로 변환 됩니다. 문자 데이터의 각 두 바이트는 16 진수 형식으로 숫자를 나타냅니다. 예를 들어, "01"은 이진 00000001로 변환 되 고 "FF"는 이진 11111111로 변환 됩니다.  
  
 드라이버는 항상 16 진수 숫자 쌍을 개별 바이트로 변환 하 고 null 종료 바이트를 무시 합니다. 따라서 문자열의 길이가 홀수 이면 문자열의 마지막 바이트 (null 종결 바이트 (있는 경우) 제외)가 변환 되지 않습니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 문자 C 데이터를 이진 SQL 데이터 형식에 바인딩하는 것을 권장 하지 않습니다. 일반적으로 이러한 변환은 비효율적 이며 느립니다.
