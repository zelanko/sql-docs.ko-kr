---
title: 'SQL에서 C로: 문자 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a649e1ec27261551b7a64e09310ce99b6140a15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056920"
---
# <a name="sql-to-c-character"></a>SQL에서 C로: 문자

ODBC SQL 데이터 형식의 문자에 대 한 식별자는 다음과 같습니다.

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

다음 표에서는 문자 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  

|C 형식 식별자|테스트|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|*Bufferlength* < 데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이 >= *Bufferlength*|data<br /><br /> 잘린 데이터|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)|해당 없음<br /><br /> 01004|  
|SQL_C_WCHAR|데이터의 문자 길이 < *Bufferlength*<br /><br /> 데이터 >의 문자 길이 = *Bufferlength*|data<br /><br /> 잘린 데이터|데이터의 길이 (문자)<br /><br /> 데이터의 길이 (문자)|해당 없음<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|잘림 없이 변환 된 데이터 [b]<br /><br /> 소수 자릿수가 잘린 상태로 변환 된 데이터 [a]<br /><br /> 데이터를 변환 하면 소수 자릿수가 아니라 전체 손실이 발생 합니다. [a]<br /><br /> 데이터가 *숫자 리터럴이*아닙니다. [b]|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 바이트 수<br /><br /> C 데이터 형식의 바이트 수<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|데이터가 변환 되는 데이터 형식의 범위 내에 있는 경우 [a]<br /><br /> 데이터가 변환 되는 데이터 형식의 범위를 벗어났습니다. [a]<br /><br /> 데이터가 *숫자 리터럴이*아닙니다. [b]|data<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|데이터가 0 또는 1입니다.<br /><br /> 데이터가 0 보다 크고 2 보다 작고 1과 같지 않습니다.<br /><br /> 데이터가 0 보다 작거나 2 보다 크거나 같습니다.<br /><br /> 데이터가 *숫자 리터럴이* 아닙니다.|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|1 [b]<br /><br /> 1 [b]<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|data<br /><br /> 잘린 데이터|데이터의 길이 (바이트)<br /><br /> 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_TYPE_DATE|데이터 값이 유효한 *날짜 값*[a]입니다.<br /><br /> 데이터 값이 유효한 *타임 스탬프 값*입니다. 시간 부분이 0 [a]입니다.<br /><br /> 데이터 값이 유효한 *타임 스탬프 값*입니다. 시간 부분은 0이 아닌 [a], [c]입니다.<br /><br /> 데이터 값이 올바른 *날짜 값* 또는 *타임 스탬프 값*이 아닙니다. [a]|data<br /><br /> data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 해당 없음<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|데이터 값이 유효한 *시간 값 이며 소수 자릿수 초 값은 0*[a]입니다.<br /><br /> 데이터 값이 유효한 *타임 스탬프 값 또는 유효한 시간 값*입니다. 소수 자릿수 초 부분은 0 [a], [d]입니다.<br /><br /> 데이터 값이 유효한 *타임 스탬프 값*입니다. 초 소수 부분을 0이 아닌 값으로 [a], [d], [e]<br /><br /> 데이터 값이 유효한 *시간 값* 또는 *타임 스탬프 값*이 아닙니다. [a]|data<br /><br /> data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 해당 없음<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|데이터 값이 유효한 *타임 스탬프 값 또는 유효한 시간 값*입니다. 소수 자릿수 초 부분이 잘리지 않음 [a]<br /><br /> 데이터 값이 유효한 *타임 스탬프 값 또는 유효한 시간 값*입니다. 소수 자릿수 초 부분이 잘렸습니다. [a]<br /><br /> 데이터 값이 유효한 *날짜 값*[a]입니다.<br /><br /> 데이터 값이 유효한 *시간 값*[a]입니다.<br /><br /> 데이터 값이 올바른 *날짜 값*, *시간 값*또는 *타임 스탬프 값*이 아닙니다. [a]|data<br /><br /> 잘린 데이터<br /><br /> 데이터 [f]<br /><br /> 데이터 [g]<br /><br /> 정의되지 않음|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 해당 없음<br /><br /> 해당 없음<br /><br /> 22018|  
|모든 C 간격 유형|데이터 값이 유효한 *간격 값*입니다. 잘림 없음<br /><br /> 데이터 값이 유효한 *간격 값*입니다. 하나 이상의 후행 필드 잘림<br /><br /> 데이터가 유효한 간격입니다. 선행 필드의 큰 전체 자릿수가 손실 됩니다.<br /><br /> 데이터 값이 올바른 간격 값이 아닙니다.|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 [c] *타임 스탬프 값* 의 시간 부분을 자릅니다.  
  
 [d] *타임 스탬프 값* 의 날짜 부분은 무시 됩니다.  
  
 [e] 타임 스탬프의 초 소수 부분을 자릅니다.  
  
 [f] 타임 스탬프 구조의 시간 필드는 0으로 설정 됩니다.  
  
 [g] 타임 스탬프 구조의 날짜 필드를 현재 날짜로 설정 합니다.  

**추가 공백**

SQL 문자 데이터가 다음 형식으로 변환 되 면 선행 공백과 후행 공백은 무시 됩니다.

- date
- numeric
- time
- timestamp
- 간격 C 데이터
