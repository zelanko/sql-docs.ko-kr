---
title: 'SQL에서 C로: 년-월 간격 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7412226dd0674022da022b0a0a63e5bf2063cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065040"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL에서 C로: 연-월 간격

년-월 간격 ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

다음 표에서는 연도-월 간격 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  

|C 형식 식별자|테스트|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|후행 필드 부분이 잘리지 않음<br /><br /> 후행 필드 부분이 잘렸습니다.<br /><br /> 대상의 선행 전체 자릿수가 원본의 데이터를 보유할 만큼 크지 않습니다.|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|간격 전체 자릿수가 단일 필드 이며 데이터가 잘리지 않고 변환 되었습니다.<br /><br /> 간격 전체 자릿수는 단일 필드 이며 전체 잘림<br /><br /> 간격 전체 자릿수가 단일 필드가 아닙니다.|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 데이터의 길이 (바이트)<br /><br /> C 데이터 형식의 크기|해당 없음<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|data<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_CHAR|바이트 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 연도-월 간격 SQL 유형을 연도-월 간격 C 유형으로 변환할 수 있습니다.  
  
 [b] 간격 전체 자릿수가 단일 필드 (연도 또는 월 중 하나) 이면 interval SQL 유형을 정확한 숫자 (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG 또는 SQL_C_NUMERIC)로 변환할 수 있습니다.  

## <a name="default-conversions"></a>기본 변환

Interval SQL 형식의 기본 변환은 해당 C interval 데이터 형식입니다. 그런 다음 응용 프로그램은 열 또는 매개 변수를 바인딩하고 (또는 해당 레코드의 해당 레코드에 있는 SQL_DESC_DATA_PTR 필드를 초기화 된 SQL_INTERVAL_STRUCT 구조를 가리키도록 설정 합니다. 또는 SQL_ INTERVAL_STRUCT 구조에 대 한 포인터를 **SQLGetData**호출의 *Targetvalueptr* 인수로 전달 합니다.)
