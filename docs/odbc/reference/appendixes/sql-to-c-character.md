---
title: 'SQL에서 C까지: 문자 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296673"
---
# <a name="sql-to-c-character"></a>SQL에서 C로: 문자

문자 ODBC SQL 데이터 형식의 식별자는 다음과 같습니다.

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

다음 표에서는 문자 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  

|C 유형 식별자|테스트|대상 밸류프트|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|*버퍼길이<* 데이터의 바이트 길이<br /><br /> 데이터 >바이트 길이 = *버퍼길이*|데이터<br /><br /> 잘린 데이터|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_WCHAR|*버퍼길이* < 데이터의 문자 길이<br /><br /> >데이터의 문자 길이 = *버퍼길이*|데이터<br /><br /> 잘린 데이터|문자로 된 데이터 길이<br /><br /> 문자로 된 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_TINYINT SQL_C_STINYINT SQL_C_SHORT SQL_C_SLONG SQL_C_SLONG SQL_C_SLONG SQL_C_SLONG SQL_C_SHORT SQL_C_SSHORT SQL_C_LONG SQL_C_ULONG SQL_C_USHORT SQL_C_SSHORT SQL_C_UBIGINT SQL_C_SBIGINT SQL_C_UTINYINT SQL_C_UTINYINT SQL_C_UTINYINT SQL_C_NUMERIC.|잘림 없이 변환된 데이터[b]<br /><br /> 소수 자릿수의 잘림으로 변환된 데이터[a]<br /><br /> 데이터를 변환하면 전체(소수와 는 반대)가 손실됩니다[a]<br /><br /> 데이터는 숫자 *리터럴이*아닙니다[b]|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 바이트 수<br /><br /> C 데이터 형식의 바이트 수<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|데이터가 변환되는 데이터 형식의 범위 내에 있습니다[a]<br /><br /> 데이터가 변환되는 데이터 형식의 범위를 벗어났습니다[a]<br /><br /> 데이터는 숫자 *리터럴이*아닙니다[b]|데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|데이터는 0 또는 1입니다.<br /><br /> 데이터가 0보다 크고 2보다 크며 1과 같지 않습니다.<br /><br /> 데이터가 0보다 크거나 2보다 크거나 같습니다.<br /><br /> 데이터는 숫자 *리터럴이* 아닙니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|1[b]<br /><br /> 1[b]<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 잘린 데이터|바이트 내 데이터 길이<br /><br /> 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_TYPE_DATE|데이터 값은 유효한 *날짜 값*[a]<br /><br /> 데이터 값은 유효한 *타임스탬프 값입니다.* 시간 부분은 0[a]<br /><br /> 데이터 값은 유효한 *타임스탬프 값입니다.* 시간 부분은 영해가 아닌 [a],[c]<br /><br /> 데이터 값이 유효한 *날짜 값* 또는 *타임스탬프 값이*아닙니다[a]|데이터<br /><br /> 데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 해당 없음<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|데이터 값은 유효한 *시간 값이며 소수 초 값은 0*[a]<br /><br /> 데이터 값은 유효한 *타임스탬프 값 또는 유효한 시간 값입니다.* 분수 초 부분은 0[a],[d]<br /><br /> 데이터 값은 유효한 *타임스탬프 값입니다.* 분수 초 부분은 영해가 아닙니다[a],[d],[e]<br /><br /> 데이터 값이 유효한 *시간 값* 또는 *타임스탬프 값이*아닙니다[a]|데이터<br /><br /> 데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 해당 없음<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|데이터 값은 유효한 *타임스탬프 값 또는 유효한 시간 값입니다.* 잘린 되지 않는 분수 초 부분[a]<br /><br /> 데이터 값은 유효한 *타임스탬프 값 또는 유효한 시간 값입니다.* 잘린 분수 초 부분[a]<br /><br /> 데이터 값은 유효한 *날짜 값*[a]<br /><br /> 데이터 값은 유효한 *시간 값[a]*<br /><br /> 데이터 값이 유효한 *날짜 값,* *시간 값*또는 *타임스탬프 값*[a] 아닙니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 데이터[f]<br /><br /> 데이터[g]<br /><br /> 정의되지 않음|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 해당 없음<br /><br /> 해당 없음<br /><br /> 22018|  
|모든 C 간격 유형|데이터 값은 유효한 *간격 값입니다.* 잘림 없음<br /><br /> 데이터 값은 유효한 *간격 값입니다.* 하나 이상의 후행 필드 잘림<br /><br /> 데이터는 유효한 간격입니다. 선행 필드 상당한 정밀도가 손실됩니다.<br /><br /> 데이터 값이 유효한 간격 값이 아닙니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 [c] *타임스탬프 값의* 시간 부분이 잘립니다.  
  
 [d] *타임스탬프 값의* 날짜 부분은 무시됩니다.  
  
 [e] 타임스탬프의 소수 초 부분이 잘립니다.  
  
 [f] 타임스탬프 구조의 시간 필드가 0으로 설정됩니다.  
  
 [g] 타임스탬프 구조의 날짜 필드가 현재 날짜로 설정됩니다.  

**추가 공간**

SQL 문자 데이터가 다음 유형 중 으로 변환될 때 선행 및 후행 공백은 무시됩니다.

- date
- numeric
- time
- timestamp
- 간격 C 데이터
