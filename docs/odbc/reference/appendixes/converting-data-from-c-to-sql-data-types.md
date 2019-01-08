---
title: C에서 SQL 데이터 형식으로 데이터를 변환 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 168fa55d89488277cd17f4bdca3105f7d879c8f8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509404"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>데이터를 C에서 SQL 데이터 형식으로 변환
응용 프로그램을 호출할 때 **SQLExecute** 하거나 **SQLExecDirect**, 드라이버를 사용 하 여 바인딩된 매개 변수 데이터를 검색 합니다 **SQLBindParameter** 의 저장소 위치에서 응용 프로그램입니다. 응용 프로그램을 호출할 때 **SQLSetPos**, 드라이버 업데이트에 대 한 데이터를 검색 하거나 추가 작업을 사용 하 여 바인딩된 열에서 **SQLBindCol**합니다. 응용 프로그램 실행 시 데이터 매개 변수를 사용 하 여 매개 변수 데이터를 보냅니다 **SQLPutData**합니다. 필요한 드라이버 변환 데이터에 지정 된 데이터 형식에서 합니다 *ValueType* 에서 인수 **SQLBindParameter** 에서 지정한 데이터 형식으로는 *ParameterType*에 인수 **SQLBindParameter**, 한 다음 데이터 원본에 데이터를 보냅니다.  
  
 다음 표에서 ODBC C에서 지원 되는 변환 데이터 형식을 ODBC SQL 데이터 형식을 보여 줍니다. 속이 찬된 원에는 SQL 데이터 형식에 대 한 기본 변환을 나타냅니다 (C 데이터 형식 있는 데이터를 변환할 경우 값 *ValueType* SQL_DESC_CONCISE_TYPE 설명자 필드는 SQL_C_DEFAULT 또는). 속이 빈 원에 지원 되는 변환을 나타냅니다.  
  
 변환 된 데이터의 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.  
  
 ![지원 되는 변환: ODBC C에서 SQL 데이터 형식](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 다음 섹션의 표에서 드라이버나 데이터 원본; 데이터 원본에 전송 되는 데이터 변환 하는 방법 설명 드라이버는 모든 ODBC C 데이터 형식에서 지원 되는 ODBC SQL 데이터 형식으로의 변환을 지원 해야 합니다. 테이블의 첫 번째 열을 지정된 된 ODBC C 데이터 형식에 대 한 유효한 입력된 값을 나열 합니다는 *ParameterType* 에서 인수 **SQLBindParameter**합니다. 두 번째 열의 데이터를 변환할 수 있는 경우 확인을 수행 하는 드라이버는 테스트의 결과 나열 합니다. 세 번째 열을 나열 하 여 각 결과 대 한 반환 된 SQLSTATE **SQLExecDirect**, **SQLExecute**하십시오 **SQLBulkOperations**, **SQLSetPos**, 또는 **SQLPutData**합니다. 데이터는 SQL_SUCCESS가 반환 하는 경우에 데이터 원본에 전송 됩니다.  
  
 경우는 *ParameterType* 에서 인수 **SQLBindParameter** 지정된 된 C 데이터 형식에 대 한 테이블에 표시 되지 않는 ODBC SQL 데이터 형식 식별자가 포함 된 **SQLBindParameter**SQLSTATE 07006를 반환 합니다 (제한 된 데이터 형식 특성 위반). 경우는 *ParameterType* 인수는 드라이버 관련 식별자를 포함 하며 드라이버는 드라이버별 SQL 데이터 형식으로 특정 ODBC C 데이터 형식에서 변환을 지원 하지 않습니다 **SQLBindParameter** SQLSTATE HYC00를 반환 합니다 (선택적 기능이 구현 되지 않음).  
  
 경우는 *ParameterValuePtr* 하 고 *StrLen_or_IndPtr* 인수에 지정 된 **SQLBindParameter** 가 모두 null 포인터인 함수는 SQLSTATE HY009 반환 (잘못 된 null 포인터 사용)입니다. 테이블에는 표시 되지 않습니다, 하지만 응용 프로그램에서 가리키는 길이/표시기 버퍼의 값을 설정 합니다 *StrLen_or_IndPtr* 인수의 **SQLBindParameter** 의 값를  *StrLen_or_IndPtr* 인수의 **SQLPutData** 를 sql_null_data로 NULL SQL 데이터 값을 지정 합니다. (합니다 *StrLen_or_IndPtr* 인수 APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 해당 합니다.) 응용 프로그램 값을 설정 이러한 값을 지정 하는 SQL_NTS \* *ParameterValuePtr* 에서 **SQLBindParameter** 하거나 \* *DataPtr*에 **SQLPutData** 은 null로 끝나는 문자열로 (APD의 SQL_DESC_DATA_PTR 필드가 가리키는 함).  
  
 다음 용어는 테이블에 사용 됩니다.  
  
-   **데이터의 바이트 길이** 번호-데이터 원본에 보낼 수 있는 SQL 데이터의 바이트를 여부는 데이터가 잘릴 수 데이터 원본에 전송 되기 전에 합니다. 문자열 데이터에 대 한이 null 종료 문자에 대 한 공간이 포함 되지 않습니다.  
  
-   **열의 바이트 길이** -데이터 소스에서 데이터를 저장 하는 데 필요한 바이트 수입니다.  
  
-   **문자 바이트 길이** 최대-문자 형식에서 데이터를 표시 하는 데 필요한 바이트 수입니다. 이 각 SQL 데이터 형식에 대해 정의 된 대로 [표시 크기](../../../odbc/reference/appendixes/display-size.md)표시 크기 문자에서는 문자 바이트 길이 (바이트)는 제외 하 고 있습니다.  
  
-   **자릿수** -번호 문자의 수를 나타내는 데 등 빼기 기호, 소수점 지 수 (필요한 경우).  
  
-   **단어**   
     ***기울임꼴*** -SQL 문법 요소입니다. 문법 요소의 구문에 대 한 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C에서 SQL로: 문자](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C에서 SQL로: 숫자](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C에서 SQL로: 비트](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C에서 SQL로: 이진 파일](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C에서 SQL로: 날짜](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C에서 SQL로: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C에서 SQL로: 시간](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C에서 SQL로: 타임 스탬프](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C에서 SQL로: 연도-월 간격](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C에서 SQL로: 날짜-시간 간격](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C에서 SQL로 데이터 변환 예제](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
