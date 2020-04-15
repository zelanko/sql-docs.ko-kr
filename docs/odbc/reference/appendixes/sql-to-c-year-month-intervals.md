---
title: 'SQL에서 C까지: 연도별 간격 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296393"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL에서 C로: 연-월 간격

연도 간격 ODBC SQL 데이터 형식의 식별자는 다음과 같습니다.

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

다음 표에서는 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며, 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  

|C 유형 식별자|테스트|대상 밸류프트|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|잘린 후행 필드 부분<br /><br /> 후행 필드 부분 잘린<br /><br /> 대상의 선행 정밀도는 원본에서 데이터를 보유할 만큼 크지 않습니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|간격 정밀도는 단일 필드였으며 데이터는 잘리지 않고 변환되었습니다.<br /><br /> 간격 정밀도는 단일 필드였고 전체 필드가 잘렸습니다.<br /><br /> 간격 정밀도가 단일 필드가 아니었습니다.|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 바이트 내 데이터 길이<br /><br /> C 데이터 형식의 크기|해당 없음<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_CHAR|문자 바이트 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 연도-월 간격 SQL 형식은 모든 연도 월 간격 C 유형으로 변환할 수 있습니다.  
  
 [b] 간격 정밀도가 단일 필드(연도 또는 월 중 하나)인 경우 간격 SQL 형식을 정확한 숫자(SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)로 변환할 수 있습니다.  

## <a name="default-conversions"></a>기본 전환수

INTERVAL SQL 형식의 기본 변환은 해당 C 간격 데이터 형식입니다. 그런 다음 응용 프로그램은 열 또는 매개 변수(또는 ARD의 적절한 레코드에서 SQL_DESC_DATA_PTR 필드를 설정)를 바인딩하여 초기화된 SQL_INTERVAL_STRUCT 구조를 가리키거나 **SQLGetData**호출에서 *targetValuePtr* 인수로 SQL_ INTERVAL_STRUCT 구조에 대한 포인터를 전달합니다.
