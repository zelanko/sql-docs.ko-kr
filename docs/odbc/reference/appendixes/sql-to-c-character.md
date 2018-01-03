---
title: "C: 문자로 SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be915f119f34ed84bc732239acd7386ea671bb66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-character"></a>SQL에서 c: 문자
문자 형식은 ODBC SQL 데이터에 대 한 식별자:  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 다음 표에서 ODBC C 데이터 형식 문자 SQL 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|데이터의 바이트 길이 < *BufferLength*<br /><br /> 데이터의 바이트 길이 > = *BufferLength*|data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|문자 데이터의 길이 < *BufferLength*<br /><br /> 문자 데이터의 길이 > = *BufferLength*|data<br /><br /> 잘린된 데이터|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이|n/a<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|데이터 잘림 [b] 없이 변환<br /><br /> 데이터 잘림 [a] 소수 자릿수로 변환<br /><br /> 데이터 변환 [a] (소수) 대비 전체 자릿수 손실 될 수 있습니다.<br /><br /> 데이터를 한 *숫자 리터럴*[b].|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 바이트 수<br /><br /> C 데이터 형식의 바이트 수<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|데이터는 숫자를 변환 하는 데이터 형식 범위 내에서 [a]<br /><br /> 데이터 숫자를 변환 하는 데이터 형식의 범위를 벗어났습니다 [a]<br /><br /> 데이터를 한 *숫자 리터럴*[b].|data<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|n/a<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|데이터는 0 또는 1<br /><br /> 데이터 0, 2, 보다 작음 및 1과 같지 않은 보다 큽니다.<br /><br /> 데이터는 0 보다 작거나 또는 2 보다 크거나<br /><br /> 데이터를 한 *숫자 리터럴*|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|1 [b]<br /><br /> 1 [b]<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 길이|n/a<br /><br /> 01004|  
|SQL_C_TYPE_DATE|데이터 값은 올바른 *날짜 값*[a]<br /><br /> 데이터 값은 올바른 *타임 스탬프 값*; 시간 부분은 0은 [a]<br /><br /> 데이터 값은 올바른 *타임 스탬프 값*; 시간 부분을 0이 아닌 [a], [c + +]<br /><br /> 데이터 값이 유효한 *날짜 값* 또는 *타임 스탬프 값*[a]|data<br /><br /> data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 정의되지 않음|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|데이터 값은 올바른 *시간 값과 값 0은 소수 자릿수 초가*[a]<br /><br /> 데이터 값은 올바른 *타임 스탬프 값 또는 시간 값이 유효한*; 소수 자릿수 초 부분은 0 [a], [d]<br /><br /> 데이터 값은 올바른 *타임 스탬프 값*; 소수 자릿수 초 부분을 0이 아닌 [a], [d] [e]<br /><br /> 데이터 값이 유효한 *시간 값* 또는 *타임 스탬프 값*[a]|data<br /><br /> data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 정의되지 않음|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|데이터 값은 올바른 *타임 스탬프 값 또는 시간 값이 유효한*; 소수 자릿수 초 부분 잘리지 [a]<br /><br /> 데이터 값은 올바른 *타임 스탬프 값 또는 시간 값이 유효한*; 소수 자릿수 초 부분 잘림 [a]<br /><br /> 데이터 값은 올바른 *날짜 값*[a]<br /><br /> 데이터 값은 올바른 *시간 값*[a]<br /><br /> 데이터 값이 유효한 *날짜 값*, *시간 값*, 또는 *타임 스탬프 값*[a]|data<br /><br /> 잘린된 데이터<br /><br /> 데이터 [f]<br /><br /> 데이터 [g]<br /><br /> 정의되지 않음|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|모든 C 간격 유형|데이터 값은 올바른 *간격 값*; 없는 잘림<br /><br /> 데이터 값은 올바른 *간격 값*; 하나 이상의 후행 필드의 잘림<br /><br /> 데이터는 유효 간격; 필드 중요 한 전체 자릿수를 유도 하는 것은 손실<br /><br /> 데이터 값이 유효한 간격 값|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a]의 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버를 가정 하는 크기 **TargetValuePtr* C 데이터 형식 크기입니다.  
  
 [b] C 데이터 형식에 해당 크기입니다.  
  
 [c]의 시간 부분에서 *타임 스탬프 값* 잘립니다.  
  
 [d]에서 날짜 부분의 *타임 스탬프 값* 는 무시 됩니다.  
  
 [e] 타임 스탬프의 소수 자릿수 초 부분이 잘립니다.  
  
 [f] 타임 스탬프 구조의 시간 필드를 0으로 설정 됩니다.  
  
 [g] 타임 스탬프 구조의 날짜 필드를 현재 날짜로 설정 됩니다.  
  
 숫자 문자 SQL 데이터를 변환, 날짜, 시간, 타임 스탬프 또는 데이터 간격 C 선행 공백과 후행 공백은 무시 됩니다.
