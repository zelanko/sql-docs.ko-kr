---
title: SQL에서 C 데이터 유형으로 데이터 변환 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284753"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>데이터를 SQL에서 C 데이터 형식으로 변환
응용 프로그램이 **SQLFetch,** **SQLFetchScroll**또는 **SQLGetData를**호출하면 드라이버는 데이터 원본에서 데이터를 검색합니다. 필요한 경우 드라이버가 검색한 데이터 형식의 데이터를 **SQLBindCol** 또는 **SQLGetData의** *TargetType* 인수에 의해 지정된 데이터 유형으로 변환합니다. 마지막으로 **SQLBindCol** 또는 **SQLGetData(ARD의** SQL_DESC_DATA_PTR 필드)에서 *TargetValuePtr* 인수가 가리키는 위치에 데이터를 저장합니다.  
  
 다음 표에서는 ODBC SQL 데이터 형식에서 ODBC C 데이터 유형으로의 지원되는 변환을 보여 주며, 이 에 대한 변환을 보여 주실 수 있습니다. 채워진 원은 SQL 데이터 *형식(TargetType* 값이 SQL_C_DEFAULT 때 데이터가 변환되는 C 데이터 형식)에 대한 기본 변환을 나타냅니다. 속이 빈 원은 지원되는 변환을 나타냅니다.  
  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램의 경우 드라이버 별 데이터 형식의 변환이 지원되지 않을 수 있습니다.  
  
 변환된 데이터의 형식은 Windows® 국가 설정의 영향을 받지 않습니다.  
  
 다음 섹션의 표에서는 드라이버 또는 데이터 원본이 데이터 원본에서 검색된 데이터를 변환하는 방법을 설명합니다. 드라이버는 지원하는 ODBC SQL 데이터 형식의 모든 ODBC C 데이터 유형으로의 변환을 지원해야 합니다. 지정된 ODBC SQL 데이터 형식의 경우 테이블의 첫 번째 열에는 **SQLBindCol** 및 **SQLGetData**에서 *TargetType* 인수의 법적 입력 값이 나열됩니다. 두 번째 열에는 테스트 의 결과가 나열되며, 종종 **SQLBindCol** 또는 **SQLGetData에**지정된 *BufferLength* 인수를 사용하여 드라이버가 데이터를 변환할 수 있는지 여부를 결정합니다. 각 결과에 대해 세 번째 및 네 번째 열에는 *TargetValuePtr에서* 지정한 버퍼에 배치된 값과 드라이버가 데이터를 변환하려고 시도한 후 **SQLBindCol** 또는 **SQLGetData에** 지정된 *인수를 StrLen_or_IndPtr* 나열합니다. StrLen_or_IndPtr *인수는* ARD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당합니다.) 마지막 열에는 **SQLFetch, SQLFetchScroll**또는 **SQLGetData**에 의해 각 결과에 대해 반환된 **SQLSTATE가**나열됩니다.  
  
 **SQLBindCol** 또는 **SQLGetData의** *TargetType* 인수에 지정된 ODBC SQL 데이터 형식에 대한 테이블에 표시되지 않은 ODBC C 데이터 형식에 대한 식별자가 포함된 경우 **SQLFetch스크롤** **또는** **SQLGetData는** SQLSTATE 07006(제한된 데이터 형식 특성 위반)을 반환합니다. *TargetType* 인수에 드라이버 별 SQL 데이터 형식에서 ODBC C 데이터 형식으로의 변환을 지정하는 식별자가 포함되어 있고 이 변환이 드라이버, **SQLFetch**, **SQLFetchScroll**또는 **SQLGetData에서** 지원되지 않는 경우 SQLState HYC00(선택적 기능이 구현되지 않음).  
  
 테이블에는 표시되지 않지만 SQL 데이터 값이 NULL일 때 StrLen_or_IndPtr *인수에* 의해 지정된 버퍼에서 SQL_NULL_DATA 반환합니다. 데이터를 검색하기 위해 여러 번 호출할 때 *StrLen_or_IndPtr* 사용에 대한 설명은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)함수 설명을 참조하십시오. SQL 데이터가 문자 C 데이터로 변환되는 경우 \* *StrLen_or_IndPtr* 반환되는 문자 수에는 null-termination 바이트가 포함되지 않습니다. *TargetValuePtr이* null 포인터인 경우 **SQLGetData는** SQLSTATE HY009(null 포인터의 잘못된 사용)를 반환합니다. **SQLBindCol에서는**열을 바인딩 해제합니다.  
  
 다음 용어 및 규칙은 표에 사용됩니다.  
  
-   **데이터 바이트 길이는** **TargetValuePtr에서*반환할 수 있는 C 데이터의 바이트 수로, 데이터가 응용 프로그램에 반환되기 전에 잘릴지 여부입니다. 문자열 데이터의 경우 null 종료 문자에 대한 공백은 포함되지 않습니다.  
  
-   **문자 바이트 길이는** 데이터를 문자 형식으로 표시하는 데 필요한 총 바이트 수입니다. 이는 [표시 크기](../../../odbc/reference/appendixes/display-size.md)섹션의 각 C 데이터 형식에 대해 정의된 대로이지만, 표시 크기가 문자에 있는 동안 문자 바이트 길이가 바이트에 있는 경우를 제외합니다.  
  
-   *기울임꼴의* 단어는 SQL 문법의 함수 인수 또는 요소를 나타냅니다. 문법 요소의 구문은 [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조하십시오.  
  
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
