---
title: "C에서 SQL 데이터 형식으로 데이터를 변환 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8f3f8c3c62c7a4d4c6765d52c48d592ff92a21e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="converting-data-from-c-to-sql-data-types"></a>C에서 SQL 데이터 형식으로 데이터를 변환
응용 프로그램 호출 하는 경우 **SQLExecute** 또는 **SQLExecDirect**를 검색 하 여 데이터를 바인딩된 매개 변수 **SQLBindParameter** 의 저장소 위치에서 응용 프로그램입니다. 응용 프로그램 호출 하는 경우 **SQLSetPos**, 드라이버 업데이트에 대 한 데이터를 검색 하거나 연결 된 열에서 작업을 추가할 **SQLBindCol**합니다. 응용 프로그램 실행 시 데이터 매개 변수를 사용 하 여 매개 변수 데이터를 보냅니다 **SQLPutData**합니다. 하는 경우 필요에 따라 드라이버는 데이터 변환에서 지정한 데이터 형식에서는 *ValueType* 인수 **SQLBindParameter** 에서 지정한 데이터 형식으로는 *ParameterType*인수 **SQLBindParameter**, 데이터 원본에는 데이터를 보냅니다.  
  
 다음 표에서 ODBC C에서 지원 되는 변환은 데이터 형식을 ODBC SQL 데이터 형식에를 보여 줍니다. 채워진된 원이 SQL 데이터 형식에 대 한 기본 변환을 나타냅니다 (올 데이터 변환할 때 C 데이터 형식 값 *ValueType* SQL_DESC_CONCISE_TYPE 설명자 필드는 SQL_C_DEFAULT 또는). 흰색 원 변환이 지원된를 나타냅니다.  
  
 변환된 된 데이터의 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.  
  
 ![변환 지원: ODBC C에서 SQL 데이터 형식](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 다음 섹션의 표에서 드라이버나 데이터 원본 변환 하는 과정은 데이터 소스에 전송 된 데이터에 설명 드라이버는 일부 ODBC C 데이터 형식 변환할 때 지원 되는 ODBC SQL 데이터 형식으로 지원 해야 합니다. 테이블의 첫 번째 열을 지정된 된 ODBC C 데이터 형식에 대 한 법적 입력된 값을 나열 합니다는 *ParameterType* 인수 **SQLBindParameter**합니다. 두 번째 열 데이터를 변환할 수 있는 경우를 결정 하는 드라이버 수행 하는 테스트의 결과 나열 합니다. 세 번째 열에서 나열 하 여 각 결과 대해 반환 된 SQLSTATE **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**, 또는 **SQLPutData**합니다. 데이터는 SQL_SUCCESS가 반환 하는 경우에 데이터 원본에 전송 됩니다.  
  
 경우는 *ParameterType* 인수 **SQLBindParameter** 지정된 된 C 데이터 형식에 대 한 테이블에 표시 되지 않는 ODBC SQL 데이터 형식 식별자가 포함 된 **SQLBindParameter**SQLSTATE 07006 반환 (제한 된 데이터 형식 특성 위반). 경우는 *ParameterType* 드라이버 관련 식별자를 포함 하는 인수 및 드라이버 지원 하지 않는 해당 드라이버별 SQL 데이터 형식에 대 한 특정 ODBC C 데이터 형식 변환을 **SQLBindParameter** SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않음).  
  
 경우는 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 에 지정 된 인수가 **SQLBindParameter** 해당 함수가 반환 SQLSTATE HY009, 모두 null 포인터인 (유효 하지 않음 null 포인터 사용)입니다. 응용 프로그램에서 가리키는 길이/표시기 버퍼의 값을 설정 하지만 테이블에 표시 되지 않는 *StrLen_or_IndPtr* 의 인수 **SQLBindParameter** 의 값은 * StrLen_or_IndPtr* 의 인수 **SQLPutData** 을 sql_null_data로 SQL NULL 데이터 값을 지정 합니다. (의 *StrLen_or_IndPtr* 인수 APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다.) 응용 프로그램이 이러한 값을 지정 하는 SQL_NTS의 값을 설정 \* *ParameterValuePtr* 에 **SQLBindParameter** 또는 \* *DataPtr*에 **SQLPutData** 은 null로 끝나는 문자열로 (APD의 SQL_DESC_DATA_PTR 필드가 가리키는 함).  
  
 테이블에는 다음과 같은 용어가 사용 됩니다.  
  
-   **데이터의 바이트 길이** -데이터 원본에 전송 하기 전에 데이터는 잘립니다 여부 데이터 원본으로 전달할 수 있는 SQL 데이터의 바이트 수입니다. 문자열 데이터에 대 한 null 종결 문자에 대 한 공간이 포함 되지 않습니다.  
  
-   **열의 바이트 길이** -데이터 소스에서 데이터를 저장 하는 데 필요한 바이트 수입니다.  
  
-   **문자 바이트 길이** -문자 형식에서 데이터를 표시 하는 데 필요한 바이트의 최대 수입니다. 이 각 SQL 데이터 형식에 대해 정의 된 [표시 크기](../../../odbc/reference/appendixes/display-size.md)문자 바이트 길이 바이트 단위로 표시 크기는 문자에서 제외 하 고 있습니다.  
  
-   **자릿수** -(필요한 경우) 빼기 기호, 소수점 및 지 수를 포함 하 여 숫자를 나타내는 하는 데 사용 되는 문자 수입니다.  
  
-   **에 있는 단어**   
     ***italics*** -SQL 문법의 요소입니다. 문법 요소 구문에 대 한 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C에서 SQL로: 문자](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C에서 SQL로: 숫자](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C에서 SQL로: 비트](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C에서 SQL로: 이진](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C에서 SQL로: 날짜](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C에서 SQL로: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C에서 SQL로: 시간](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C에서 SQL로: 타임스탬프](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C에서 SQL로: 연-월 간격](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C에서 SQL로: 날짜-시간 간격](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C에서 SQL로 데이터 변환 예제](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
