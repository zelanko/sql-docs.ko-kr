---
description: 데이터를 SQL에서 C 데이터 형식으로 변환
title: 데이터를 SQL에서 C 데이터 형식으로 변환 | Microsoft Docs
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
ms.openlocfilehash: 5c1306564a9e4a5c1cbd9cac74508529a1e6df9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429695"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>데이터를 SQL에서 C 데이터 형식으로 변환
응용 프로그램이 **Sqlfetch**, **sqlfetchscroll**또는 **SQLGetData**를 호출 하면 드라이버는 데이터 원본에서 데이터를 검색 합니다. 필요한 경우 드라이버에서 데이터를 검색 한 데이터 형식에서 **SQLBindCol** 또는 SQLGetData의 *TargetType* 인수에 지정 된 데이터 형식으로 데이터를 변환 합니다 **.** 마지막으로 **SQLBindCol** 또는 **SQLGetData** 의 *targetvalueptr* 인수에서 가리키는 위치에 데이터를 저장 하 고, 해당 하는 SQL_DESC_DATA_PTR 필드를 저장 합니다.  
  
 다음 표에서는 ODBC SQL 데이터 형식에서 ODBC C 데이터 형식으로의 지원 되는 변환을 보여 줍니다. 채워진 원은 SQL 데이터 형식에 대 한 기본 변환 ( *TargetType* 값이 SQL_C_DEFAULT 될 때 데이터가 변환 될 C 데이터 형식)을 나타냅니다. 빈 원은 지원 되는 변환을 나타냅니다.  
  
 *Odbc 2.x 응용 프로그램* 에서 odbc *2.x 드라이버를* 사용 하는 경우 드라이버 특정 데이터 형식에서의 변환이 지원 되지 않을 수 있습니다.  
  
 변환 된 데이터의 형식은 Windows® country 설정의 영향을 받지 않습니다.  
  
 다음 섹션의 표에서는 드라이버 또는 데이터 원본이 데이터 원본에서 검색 된 데이터를 변환 하는 방법에 대해 설명 합니다. 드라이버는 지원 되는 ODBC SQL 데이터 형식에서 모든 ODBC C 데이터 형식으로의 변환을 지원 하기 위해 필요 합니다. 지정 된 ODBC SQL 데이터 형식에 대해 테이블의 첫 번째 열에는 **SQLBindCol** 및 **SQLGetData**의 *TargetType* 인수에 대 한 유효한 입력 값이 나열 됩니다. 두 번째 열은 일반적으로 **SQLBindCol** 또는 **SQLGetData**에 지정 된 *bufferlength* 인수를 사용 하 여 테스트 결과를 나열 합니다 .이는 드라이버에서 데이터를 변환할 수 있는지 여부를 결정 하는 데 사용 됩니다. 각 결과에 대해 세 번째와 네 번째 열은 드라이버에서 데이터 변환을 시도한 후 **SQLBindCol** 또는 **SQLGetData** 에 지정 된 *targetvalueptr* 및 *StrLen_or_IndPtr* 인수로 지정 된 버퍼에 배치 된 값을 나열 합니다. *StrLen_or_IndPtr* 인수는 고의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다. 마지막 열에는 **Sqlfetch**, **Sqlfetchscroll**또는 **SQLGetData**의 각 결과에 대해 반환 되는 SQLSTATE가 나열 됩니다.  
  
 **SQLBindCol** 또는 **sqlgetdata** 의 *TARGETTYPE* 인수에 지정 된 odbc SQL 데이터 형식에 대 한 테이블에 표시 되지 않는 odbc C 데이터 형식에 대 한 식별자가 포함 된 경우 **Sqlfetch**, **Sqlfetchscroll**또는 **SQLGetData** 는 SQLSTATE 07006 (제한 된 데이터 형식 특성 위반)을 반환 합니다. *TargetType* 인수에 드라이버별 SQL 데이터 형식에서 ODBC C 데이터 형식으로의 변환을 지정 하는 식별자가 포함 되어 있고이 변환이 드라이버에서 지원 되지 않는 경우 **sqlfetch**, **SQLFETCHSCROLL**또는 **SQLGetData** 에서 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 합니다.  
  
 테이블에는 표시 되지 않지만 SQL 데이터 값이 NULL 인 경우 드라이버는 *StrLen_or_IndPtr* 인수로 지정 된 버퍼에 SQL_NULL_DATA를 반환 합니다. 여러 번 호출 하 여 데이터를 검색할 때 *StrLen_or_IndPtr* 를 사용 하는 방법에 대 한 설명은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)함수 설명을 참조 하세요. SQL 데이터가 문자 C 데이터로 변환 되 면 StrLen_or_IndPtr에서 반환 된 문자 수에 \* *StrLen_or_IndPtr* null 종료 바이트가 포함 되지 않습니다. *Targetvalueptr* 이 null 포인터인 경우 **SQLGETDATA** 는 SQLSTATE HY009 (Null 포인터 사용이 잘못 됨)를 반환 합니다. **SQLBindCol**에서는 열을 바인딩 해제 합니다.  
  
 테이블에 사용 되는 용어와 규칙은 다음과 같습니다.  
  
-   **데이터의 바이트 길이** 는 응용 프로그램에 반환 되기 전에 데이터를 잘라낼 지 여부에 관계 없이 **Targetvalueptr*에서 반환 하는 데 사용할 수 있는 C 데이터의 바이트 수입니다. 문자열 데이터의 경우 null 종료 문자에 대 한 공간이 포함 되지 않습니다.  
  
-   **문자 바이트 길이** 는 데이터를 문자 형식으로 표시 하는 데 필요한 총 바이트 수입니다. 이는 문자 바이트 길이는 바이트 이지만 표시 크기는 문자 수를 제외 하 고 섹션 [표시 크기](../../../odbc/reference/appendixes/display-size.md)의 각 C 데이터 형식에 대해 정의 된 것입니다.  
  
-   *기울임꼴* 단어는 SQL 문법의 함수 인수나 요소를 나타냅니다. 문법 요소의 구문은 [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조 하세요.  
  
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
