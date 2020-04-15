---
title: C에서 SQL 데이터 유형으로 데이터 변환 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fb707e77df7d793277d4a23146adc980eede6fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304662"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>데이터를 C에서 SQL 데이터 형식으로 변환
응용 프로그램이 **SQLExecute** 또는 **SQLExecDirect를**호출하면 드라이버는 응용 프로그램의 저장소 위치에서 **SQLBindParameter로** 바인딩된 모든 매개 변수에 대한 데이터를 검색합니다. 응용 프로그램이 **SQLSetPos를**호출하면 드라이버는 업데이트에 대한 데이터를 검색하거나 **SQLBindCol로**바인딩된 열에서 작업을 추가합니다. 실행 시 데이터 매개 변수의 경우 응용 프로그램은 **SQLPutData**를 사용하여 매개 변수 데이터를 보냅니다. 필요한 경우 드라이버는 **SQLBindParameter의** *ValueType* 인수에 의해 지정된 데이터 형식의 데이터를 **SQLBindParameter의** *ParameterType* 인수에 의해 지정된 데이터 유형으로 변환한 다음 데이터를 데이터 원본으로 보냅니다.  
  
 다음 표에서는 ODBC C 데이터 형식에서 ODBC SQL 데이터 유형으로의 지원되는 변환을 보여 주며, 이 에 대한 변환을 보여 주실 수 있습니다. 채워진 원은 SQL 데이터 형식의 기본 변환을 *나타냅니다(ValueType* 값 또는 SQL_DESC_CONCISE_TYPE 설명자 필드가 SQL_C_DEFAULT 때 데이터가 변환되는 C 데이터 형식). 속이 빈 원은 지원되는 변환을 나타냅니다.  
  
 변환된 데이터의 형식은 Windows® 국가 설정의 영향을 받지 않습니다.  
  
 ![변환 지원: ODBC C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 다음 섹션의 표에서는 드라이버 또는 데이터 원본이 데이터 원본으로 전송된 데이터를 변환하는 방법을 설명합니다. 드라이버는 모든 ODBC C 데이터 형식에서 지원하는 ODBC SQL 데이터 유형으로의 변환을 지원해야 합니다. 지정된 ODBC C 데이터 형식의 경우 테이블의 첫 번째 열에는 **SQLBindParameter**에서 *ParameterType* 인수의 법적 입력 값이 나열됩니다. 두 번째 열에는 드라이버가 데이터를 변환할 수 있는지 여부를 결정하기 위해 수행하는 테스트의 결과가 나열됩니다. 세 번째 열에는 **SQLExecDirect,** **SQL실행,** **SQLBulkOperations,** **SQLSetPos**또는 **SQLPutData에**의해 각 결과에 대해 반환된 SQLSTATE가 나열됩니다. 데이터는 SQL_SUCCESS 반환되는 경우에만 데이터 원본으로 전송됩니다.  
  
 **SQLBindParameter의** *ParameterType* 인수에 지정된 C 데이터 형식에 대한 테이블에 표시되지 않는 ODBC SQL 데이터 형식의 식별자가 포함된 경우 **SQLBindParameter는** SQLSTATE 07006(제한된 데이터 형식 특성 위반)을 반환합니다. *ParameterType* 인수에 드라이버 관련 식별자가 포함되어 있고 드라이버가 특정 ODBC C 데이터 형식에서 해당 드라이버 별 SQL 데이터 유형으로의 변환을 지원하지 않는 경우 **SQLBindParameter는** SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환합니다.  
  
 **SQLBindParameter에** 지정된 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 인수가 모두 null 포인터인 경우 해당 함수는 SQLSTATE HY009(null 포인터의 잘못된 사용)를 반환합니다. 테이블에 는 표시되지 않지만 응용 프로그램은 **SQLBindParameter의** *StrLen_or_IndPtr* 인수 또는 NULL SQL 데이터 값을 지정하기 위해 SQL_NULL_DATA **위해 STRLEN_OR_INDPTR** *인수의* 값으로 가리키는 길이/표시기 버퍼의 값을 설정합니다. StrLen_or_IndPtr *인수는* APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당합니다.) 응용 프로그램은 이러한 값을 SQL_NTS **SQLBindParameter** \*또는 **SQLPutData** SQL_DESC_DATA_PTR의 *DataPtr의* 값이 \* *ParameterValuePtr* null 종료 문자열임을 지정합니다.  
  
 다음 용어는 표에 사용됩니다.  
  
-   **데이터 바이트 길이** - 데이터 원본으로 전송되기 전에 데이터가 잘릴지 여부에 관계없이 데이터 원본으로 보낼 수 있는 SQL 데이터의 바이트 수입니다. 문자열 데이터의 경우 null 종료 문자에 대한 공백은 포함되지 않습니다.  
  
-   **열 바이트 길이** - 데이터 원본에 데이터를 저장하는 데 필요한 바이트 수입니다.  
  
-   **문자 바이트 길이** - 문자 형식으로 데이터를 표시하는 데 필요한 최대 바이트 수입니다. 이는 [표시 크기의](../../../odbc/reference/appendixes/display-size.md)각 SQL 데이터 형식에 대해 정의된 대로 이며, 문자 바이트 길이는 바이트, 표시 크기는 문자에 있는 경우를 제외 합니다.  
  
-   **숫자 수** - 빼기 기호, 소수점 및 지수(필요한 경우)를 포함하여 숫자를 나타내는 데 사용되는 문자 수입니다.  
  
-   **단어 에서**   
     ***기울임꼴*** - SQL 문법의 요소입니다. 문법 요소의 구문은 [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조하십시오.  
  
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
