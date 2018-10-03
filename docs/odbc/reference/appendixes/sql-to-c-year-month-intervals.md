---
title: 'SQL c: 연-월 간격을 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49cc98fefe9fd67cdc315f80015d2b0dbb6ebd11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762441"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL에서 C로: 연-월 간격
년-월 간격 ODBC SQL 데이터 형식에 대 한 식별자.  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 다음 표에서 ODBC C 데이터 형식은 연도-월 간격 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|[A] SQL_C_INTERVAL_MONTH<br /><br /> [A] SQL_C_INTERVAL_YEAR<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|잘리지 후행 필드 부분<br /><br /> 잘린 후행 필드 부분<br /><br /> 원본에서 데이터를 저장할 만큼 충분히 크지 않습니다 대상의 전체 자릿수를 유도|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|간격 정밀도 단일 필드 및 잘림 없이 데이터 변환 되었습니다.<br /><br /> 간격 정밀도 단일 필드 및 잘린 전체<br /><br /> 단일 필드 간격 정밀도가 없습니다.|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터의 바이트 길이<br /><br /> C 데이터 형식의 크기|n/a<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_CHAR|문자 바이트 길이 < *BufferLength*<br /><br /> (소수) 달리 전체 자릿수 < *BufferLength*<br /><br /> (소수) 달리 전체 자릿수 > = *BufferLength*|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *BufferLength*<br /><br /> (소수) 달리 전체 자릿수 < *BufferLength*<br /><br /> (소수) 달리 전체 자릿수 > = *BufferLength*|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 SQL 형식 [a]는 연도-월 간격 연도-월 간격 C 형식으로 변환할 수 있습니다.  
  
 [b] 이면 간격 정밀도 (연도 또는 월 중 하나) 단일 필드 간격 SQL 형식 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG, 또는 SQL_C_NUMERIC)에 있는 정확한 숫자를 변환할 수 있습니다.  
  
 기본 SQL 유형 간격의 변환이 해당 C 간격 데이터 형식입니다. 응용 프로그램이 다음 열 또는 매개 변수를 바인딩합니다 (또는 카드가의 적절 한 레코드에 SQL_DESC_DATA_PTR 필드가 설정) 초기화 SQL_INTERVAL_STRUCT 구조를 가리키도록 (합니다 로SQL_INTERVAL_STRUCT구조에대한포인터를전달하거나*TargetValuePtr* 호출에서 인수 **SQLGetData**).
