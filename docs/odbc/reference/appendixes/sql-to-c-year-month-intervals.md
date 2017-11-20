---
title: "C: 년-월 간격으로 SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 991dd021935617a9c0bfbe87ecf7be35d35938c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-year-month-intervals"></a>C: 년-월 간격으로 SQL
년-월 간격 ODBC SQL 데이터 형식에 대 한 식별자는.  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 다음 표에서 ODBC C 데이터 형식에는 년-월 간격 SQL 데이터를 변환 될 수 있습니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|잘리지 후행 필드 부분<br /><br /> 잘린 후행 필드 부분<br /><br /> 원본에서 데이터를 보유할 만큼 크지 않습니다 대상의 전체 자릿수를 유도|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|간격 정밀도 단일 필드 였으며 잘림 없이 데이터 변환<br /><br /> 간격 정밀도 단일 필드 및 잘린 전체<br /><br /> 간격 정밀도 단일 필드 없습니다.|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터의 바이트 길이<br /><br /> C 데이터 형식의 크기|n/a<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_CHAR|문자 바이트 길이 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 > = *BufferLength*|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 < *BufferLength*<br /><br /> (소수) 대비 전체 자릿수 > = *BufferLength*|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] A 년-월 간격 SQL 형식의 년-월 C 간격 유형으로 변환할 수 있습니다.  
  
 [b] 이면 간격 정밀도 (연도 또는 월 중 하나)는 단일 필드는 정확한 숫자 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG, 또는 SQL_C_NUMERIC)에 SQL 유형 간격을 변환할 수 있습니다.  
  
 해당 C 간격 데이터 형식을 SQL 유형 간격의 기본 변환이 됩니다. 응용 프로그램이 다음 열 또는 매개 변수를 바인딩합니다 (또는 카드가의 적절 한 레코드에 SQL_DESC_DATA_PTR 필드가 설정) 초기화 SQL_INTERVAL_STRUCT 구조를 가리키도록 (SQL_ INTERVAL_STRUCT 구조는 로에대한포인터를전달하거나*TargetValuePtr* 인수에 대 한 호출에 **SQLGetData**).

