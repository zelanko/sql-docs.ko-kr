---
title: SQL에서 C 데이터 형식으로 데이터를 변환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 553596f474cd8e7c4f4c91911b0167d5b1bc0b4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224476"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>데이터를 SQL에서 C 데이터 형식으로 변환
응용 프로그램을 호출할 때 **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLGetData**, 드라이버는 데이터 원본에서 데이터를 검색 합니다. 하는 경우 필요한 데이터를 변환할 드라이버를 검색 하는 것으로 지정 된 데이터 형식으로 데이터 형식에서의 *TargetType* 에서 인수 **SQLBindCol** 또는 **SQLGetData 합니다.** 마지막으로 데이터를 가리키는 위치에 저장 합니다 *TargetValuePtr* 에서 인수 **SQLBindCol** 또는 **SQLGetData** (및는 카드가의 SQL_DESC_DATA_PTR 필드가).  
  
 다음 표에서 ODBC C 데이터 형식으로 데이터 형식을 ODBC SQL에서 지원 되는 변환에 보여 줍니다. 속이 찬된 원에는 SQL 데이터 형식에 대 한 기본 변환을 나타냅니다 (데이터를 변환 되어야 하는 경우 C 데이터 형식 값 *TargetType* SQL_C_DEFAULT 됩니다). 속이 빈 원에 지원 되는 변환을 나타냅니다.  
  
 ODBC 3 *.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버, 드라이버 관련 데이터 형식이 지원 되지 않는 변환 합니다.  
  
 변환 된 데이터의 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.  
  
 다음 섹션의 표에서 드라이버나 데이터 원본 데이터 소스에서 검색 한 데이터 변환 하는 방법 설명 드라이버 지원 되는 ODBC SQL 데이터 유형 으로부터의 모든 ODBC C 데이터 형식 변환을 지원 해야 합니다. 테이블의 첫 번째 열을 지정된 된 ODBC SQL 데이터 형식에 대 한 유효한 입력된 값을 나열 합니다는 *TargetType* 에서 인수 **SQLBindCol** 하 고 **SQLGetData**합니다. 두 번째 열은 자주 사용 하 여 테스트의 결과 나열 합니다 *BufferLength* 에 지정 된 인수 **SQLBindCol** 또는 **SQLGetData**, 드라이버를 수행 하는 데이터를 변환할 수 있는지 여부를 결정 합니다. 각 결과 대 한 세 번째 및 네 번째 열을 목록으로 지정 된 버퍼에 배치 하는 값을 *TargetValuePtr* 하 고 *StrLen_or_IndPtr* 에 지정 된 인수의 **SQLBindCol** 나 **SQLGetData** 후 드라이버는 데이터를 변환 하려고 했습니다. (합니다 *StrLen_or_IndPtr* 인수는 카드가의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다.) 마지막 열을 나열 하 여 각 결과 대 한 반환 된 SQLSTATE **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLGetData**합니다.  
  
 경우는 *TargetType* 에서 인수 **SQLBindCol** 하거나 **SQLGetData** 지정된 된 ODBC SQL 데이터 형식에 대 한 테이블에 표시 되지는 ODBC C 데이터 형식에 대 한 식별자를 포함  **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLGetData** SQLSTATE 07006를 반환 합니다 (제한 된 데이터 형식 특성 위반). 경우는 *TargetType* 드라이버별 SQL 데이터 형식에서 ODBC C 데이터 형식 변환을 지정 하는 식별자를 포함 하는 인수 및 드라이버에 의해이 변환은 지원 되지 않습니다 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData** SQLSTATE HYC00를 반환 합니다 (선택적 기능이 구현 되지 않음).  
  
 지정한 버퍼에서 드라이버 SQL_NULL_DATA 반환 테이블에는 표시 되지 않습니다, 하지만 합니다 *StrLen_or_IndPtr* SQL 데이터 값이 null 인 인수입니다. 사용에 대 한 설명은 *StrLen_or_IndPtr* 데이터를 검색 하려면 여러 호출이 수행 된 경우 표시 된 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)함수 설명 합니다. SQL 데이터 C 문자 데이터를 변환할 문자 수를 반환 \* *StrLen_or_IndPtr* null 종료 바이트는 포함 되지 않습니다. 경우 *TargetValuePtr* 가 null 포인터인 경우 **SQLGetData** SQLSTATE HY009를 반환 합니다 (null 포인터를 잘못 사용), **SQLBindCol**,이 열을 바인딩 해제 합니다.  
  
 다음 조건 및 규칙에는 테이블에 사용 됩니다.  
  
-   **데이터의 바이트 길이** 에서 반환할 사용 가능한 C 데이터의 바이트 수 **TargetValuePtr*응용 프로그램에 반환 되기 전에 데이터가 잘릴 수 있는지 여부입니다. 문자열 데이터에 대 한이 null 종료 문자에 대 한 공간이 포함 되지 않습니다.  
  
-   **문자 바이트 길이** 문자 형식에서 데이터를 표시 하는 데 필요한 바이트의 총 수입니다. 섹션에서 각 C 데이터 형식에 대해 정의 된 대로 이것이 [표시 크기](../../../odbc/reference/appendixes/display-size.md)표시 크기 문자에서는 문자 바이트 길이 (바이트)는, 합니다.  
  
-   에 단어 *기울임꼴* 함수 인수 또는 SQL 문법 요소를 나타냅니다. 문법 요소의 구문에 대 한 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C: SQL Character](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [C: SQL Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [C: SQL Bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [C: SQL 이진 파일](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [C: SQL 날짜](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [C: SQL GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [C: SQL 시간](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [C: SQL 타임 스탬프](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [C: SQL 연도-월 간격](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [C: SQL 날짜-시간 간격](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL에서 C로 데이터 변환 예제](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
