---
title: SQL에서 C 데이터 형식으로 데이터를 변환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe89608061d82cf54a16394e5ce1a8f901e23523
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="converting-data-from-sql-to-c-data-types"></a>SQL에서 C 데이터 형식으로 데이터를 변환
응용 프로그램 호출 하는 경우 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData**, 드라이버는 데이터 원본에서 데이터를 검색 합니다. 하는 경우 필요에 따라 데이터를 변환할 드라이버 검색 하 고 데이터 형식으로 지정 된 데이터 형식에서는 *TargetType* 인수 **SQLBindCol** 또는 **SQLGetData 합니다.** 마지막으로, 데이터에서 가리키는 위치에 저장 된 *TargetValuePtr* 인수에 **SQLBindCol** 또는 **SQLGetData** (및는 카드가의 SQL_DESC_DATA_PTR 필드가).  
  
 다음 표에서 ODBC SQL에서 지원 되는 변환은 데이터 형식을 ODBC C 데이터 형식에를 보여 줍니다. 채워진된 원이 나타냅니다 SQL 데이터 형식에 대 한 기본 변환 (C 데이터 형식에 데이터 변환할 때의 값 *TargetType* SQL_C_DEFAULT는). 흰색 원 변환이 지원된를 나타냅니다.  
  
 ODBC 3에 대 한*.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버, 드라이버 관련 데이터 형식이 지원 되지 않는 변환 합니다.  
  
 변환된 된 데이터의 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.  
  
 다음 섹션의 표에서 드라이버나 데이터 원본 변환 하는 과정은 데이터 소스에서 검색 된 데이터에 설명 드라이버가 지 원하는 ODBC SQL 데이터 유형 으로부터의 모든 ODBC C 데이터 형식 변환을 지 원하는 데 필요 합니다. 테이블의 첫 번째 열을 지정된 된 ODBC SQL 데이터 형식에 대 한 법적 입력된 값을 나열 합니다는 *TargetType* 인수 **SQLBindCol** 및 **SQLGetData**합니다. 두 번째 열에서 자주 사용 하는 테스트의 결과 나열는 *BufferLength* 인수에 지정 된 **SQLBindCol** 또는 **SQLGetData**, 드라이버를 수행 하는 데이터를 변환할 수 있는지 여부를 결정 합니다. 각 결과 대 한 세 번째 및 네 번째 열 목록으로 지정 된 버퍼에 배치 하는 값은 *TargetValuePtr* 및 *StrLen_or_IndPtr* 에 지정 된 인수가 **SQLBindCol** 또는 **SQLGetData** 후 드라이버는 데이터를 변환 하려고 했습니다. (의 *StrLen_or_IndPtr* 인수는 카드가의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다.) 마지막 열을 나열 하 여 각 결과 대해 반환 된 SQLSTATE **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData**합니다.  
  
 경우는 *TargetType* 인수 **SQLBindCol** 또는 **SQLGetData** 지정된 된 ODBC SQL 데이터 형식에 대 한 테이블에 표시 되지는 ODBC C 데이터 형식에 대 한 식별자가 포함 된  **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData** SQLSTATE 07006 반환 (제한 된 데이터 형식 특성 위반). 경우는 *TargetType* 인수 지정 드라이버별 SQL 데이터 형식에서 ODBC C 데이터 형식으로 변환 하는 식별자가 포함 되며 드라이버에 의해이 변환은 지원 되지 않습니다 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData** SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않음).  
  
 드라이버에 의해 지정 된 버퍼 SQL_NULL_DATA 테이블에 표시 되지 않는 있지만 반환 하는 *StrLen_or_IndPtr* 인수 SQL 데이터 값이 NULL입니다. 에 대 한 설명은 사용 *StrLen_or_IndPtr* 검색 데이터를 여러 번 호출 하면 참조는 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)함수 설명 합니다. 문자 수에 반환 되는 SQL 데이터를 C 문자 데이터로 변환 되 면 \* *StrLen_or_IndPtr* null 종료 바이트를 포함 하지 않습니다. 경우 *TargetValuePtr* null 포인터가 **SQLGetData** SQLSTATE HY009 반환 (null 포인터를 잘못 사용), **SQLBindCol**,이 열을 바인딩 해제 합니다.  
  
 다음 조건 및 규칙은 테이블에 사용 됩니다.  
  
-   **데이터의 바이트 길이** 에 반환할 수 있는 C 데이터의 바이트 수는 **TargetValuePtr*여부는 응용 프로그램에 반환 하기 전에 데이터는 잘립니다. 문자열 데이터에 대 한 null 종결 문자에 대 한 공간을 포함 되지 않습니다.  
  
-   **문자 바이트 길이** 를 문자 형식 데이터를 표시 하는 데 필요한 바이트의 총 수입니다. 이 섹션에서 각 C 데이터 형식에 대해 정의 된 대로 [표시 크기](../../../odbc/reference/appendixes/display-size.md)제외 하 고 문자 바이트 길이 바이트 단위로 표시 크기는 문자 수입니다.  
  
-   에 단어 *기울임꼴* 함수 인수 또는 SQL 문법의 요소를 나타냅니다. 문법 요소 구문에 대 한 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL에서 C로: 문자](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL에서 C로: 숫자](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL에서 C로: 비트](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL에서 C로: 이진](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL에서 C로: 날짜](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL에서 C로: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL에서 C로: 시간](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL에서 C로: 타임스탬프](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL에서 C로: 연-월 간격](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL에서 C로: 날짜-시간 간격](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL에서 C로 데이터 변환 예제](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
