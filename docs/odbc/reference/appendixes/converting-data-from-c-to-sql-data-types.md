---
title: 데이터를 C에서 SQL 데이터 형식으로 변환 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aca333a6f3006b1f12cf44d1670e38556027e476
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019123"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>데이터를 C에서 SQL 데이터 형식으로 변환
응용 프로그램에서 **Sqlexecute** 또는 **sqlexecdirect**를 호출 하면 드라이버는 응용 프로그램의 저장소 위치에서 **SQLBindParameter** 로 바인딩된 모든 매개 변수에 대 한 데이터를 검색 합니다. 응용 프로그램이 **SQLSetPos**를 호출 하면 드라이버는 **SQLBindCol**에 바인딩된 열에서 업데이트 또는 추가 작업에 대 한 데이터를 검색 합니다. 실행 시 데이터 매개 변수의 경우 응용 프로그램은 **Sqlputdata**를 사용 하 여 매개 변수 데이터를 보냅니다. 필요한 경우 드라이버는 **SQLBindParameter** 의 *ValueType* 인수에 지정 된 데이터를 **SQLBindParameter**의 *ParameterType* 인수에 지정 된 데이터 형식으로 변환한 다음 데이터를 데이터 원본으로 보냅니다.  
  
 다음 표에서는 ODBC C 데이터 형식에서 ODBC SQL 데이터 형식으로의 지원 되는 변환을 보여 줍니다. 채워진 원은 SQL 데이터 형식에 대 한 기본 변환을 나타냅니다. *ValueType* 값 또는 SQL_DESC_CONCISE_TYPE 설명자 필드를 SQL_C_DEFAULT 하는 경우 데이터가 변환 되는 C 데이터 형식입니다. 빈 원은 지원 되는 변환을 나타냅니다.  
  
 변환 된 데이터의 형식은 Windows® country 설정의 영향을 받지 않습니다.  
  
 ![변환 지원: ODBC C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 다음 섹션의 표에서는 드라이버 또는 데이터 원본에서 데이터 원본으로 전송 되는 데이터를 변환 하는 방법을 설명 합니다. 모든 ODBC C 데이터 형식에서 지원 되는 ODBC SQL 데이터 형식으로의 변환을 지원 하려면 드라이버가 필요 합니다. 지정 된 ODBC C 데이터 형식에 대해 테이블의 첫 번째 열에는 **SQLBindParameter**에 있는 *ParameterType* 인수의 올바른 입력 값이 나열 됩니다. 두 번째 열은 드라이버에서 데이터를 변환할 수 있는지 확인 하기 위해 수행 하는 테스트 결과를 나열 합니다. 세 번째 열에는 **Sqlexecdirect**, **sqlexecute**, **SQLBulkOperations**, **SQLSetPos**또는 **sqlexecdirect**에서 각 결과에 대해 반환 되는 SQLSTATE가 나열 됩니다. SQL_SUCCESS 반환 되는 경우에만 데이터를 데이터 원본으로 보냅니다.  
  
 **SQLBindParameter** 의 *ParameterType* 인수에 지정 된 C 데이터 형식에 대 한 테이블에 표시 되지 않는 ODBC SQL 데이터 형식의 식별자가 포함 된 경우 **SQLBindParameter** 는 SQLSTATE 07006 (제한 된 데이터 형식 특성 위반)을 반환 합니다. *ParameterType* 인수에 드라이버별 식별자가 포함 되어 있고 드라이버가 특정 ODBC C 데이터 형식에서 해당 드라이버별 SQL 데이터 형식으로의 변환을 지원 하지 않는 경우 **SQLBINDPARAMETER** 는 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 합니다.  
  
 **SQLBindParameter** 에 지정 된 *Parametervalueptr* 및 *StrLen_or_IndPtr* 인수가 모두 NULL 포인터인 경우이 함수는 SQLSTATE HY009 (null 포인터 사용이 잘못 되었습니다)를 반환 합니다. 테이블에는 표시 되지 않지만 응용 프로그램은 **SQLBindParameter** 의 *StrLen_or_IndPtr* 인수가 가리키는 길이/표시 버퍼의 값을 설정 하거나 **sqlputdata** 의 *STRLEN_OR_INDPTR* 인수 값을 SQL_NULL_DATA 하 여 NULL SQL 데이터 값을 지정 합니다. *StrLen_or_IndPtr* 인수는 apd의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다. 응용 프로그램은 이러한 값을 SQL_NTS 설정 하 여 \* **sqlputdata** 에서 **SQLBindParameter** 또는 \* *dataptr* 의 *parametervalueptr* 에 있는 값 (apd의 SQL_DESC_DATA_PTR 필드가 가리키는)이 null로 끝나는 문자열 임을 지정 합니다.  
  
 테이블에 사용 되는 용어는 다음과 같습니다.  
  
-   데이터 **의 바이트 길이** -데이터 원본에 전송 하기 전에 데이터를 잘라낼 지 여부에 관계 없이 데이터 원본으로 보낼 수 있는 SQL 데이터의 바이트 수입니다. 문자열 데이터의 경우 null 종료 문자를 위한 공간이 포함 되지 않습니다.  
  
-   **열 바이트 길이** -데이터 원본에 데이터를 저장 하는 데 필요한 바이트 수입니다.  
  
-   **문자 바이트 길이** -문자 형식으로 데이터를 표시 하는 데 필요한 최대 바이트 수입니다. 이는 [표시 크기](../../../odbc/reference/appendixes/display-size.md)의 각 SQL 데이터 형식에 대해 정의 된 것과 같습니다. 단, 문자 바이트 길이는 바이트 단위 이지만 표시 크기는 문자 수입니다.  
  
-   **자릿수** -빼기 기호, 소수점 및 지수가 포함 된 숫자를 나타내는 데 사용 되는 문자 수입니다 (필요한 경우).  
  
-   **단어**   
     ***기울임꼴*** -SQL 문법의 요소입니다. 문법 요소의 구문은 [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조 하세요.  
  
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
