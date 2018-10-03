---
title: 드라이버가 수행 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 685f67c9f24593a5c50097de426b76fef068d6e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628181"
---
# <a name="what-the-driver-does"></a>드라이버가 수행하는 작업
다음 표에서 기능 및 문 특성을 ODBC 3 *.x* 드라이버 블록 및 스크롤 가능 커서에 대해 구현 해야 합니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|행 상태 배열 주소를 입력 하 여 집합 **SQLFetch** 하 고 **SQLFetchScroll**합니다. 이 배열도 채워져 **SQLSetPos** 하는 경우 **SQLSetPos** S6 문 상태의 라고 합니다. 하는 경우 **SQLSetPos** 라고 S7 상태에서이 배열은 비어 있지만 가리키는 배열 합니다 *RowStatusArray* 인수의 **SQLExtendedFetch** 채워집니다. 자세한 내용은 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR을 설정|버퍼의 주소를 설정 **SQLFetch** 하 고 **SQLFetchScroll** 인출 된 행 수를 반환 합니다. 경우 **SQLExtendedFetch** 가 호출 하 고,이 버퍼 채워지지 않습니다 하지만 *RowCountPtr* 인수 인출 된 행 수를 가리킵니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|사용 되는 행 집합 크기 설정 **SQLFetch** 하 고 **SQLFetchScroll**합니다.|  
|SQL_ROWSET_SIZE|사용 되는 행 집합 크기 설정 **SQLExtendedFetch**합니다. ODBC 3 *.x* ODBC 2를 사용 하는 경우이 드라이버 구현. *x* 를 호출 하는 응용 프로그램 **SQLExtendedFetch** 하거나 **SQLSetPos**합니다.|  
|**SQLBulkOperations**|경우는 ODBC 3 *.x* 드라이버는 ODBC 2를 사용 하 여 작동 해야 합니다. *x* 를 사용 하는 응용 프로그램 **SQLSetPos** 와 *작업* SQL_ADD의 드라이버를 지원 해야 **SQLSetPos** 사용 하 여는  *작업* 외에 SQL_ADD의 **SQLBulkOperations** 와 *작업* SQL_ADD입니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. ODBC 3 *.x* ODBC 2를 사용 하는 경우이 드라이버 구현. *x* 를 호출 하는 응용 프로그램 **SQLExtendedFetch** 하거나 **SQLSetPos**합니다. 다음은 구현 세부 정보입니다.<br /><br /> -드라이버 SQL_ROWSET_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />-드라이버에서 행 상태 배열 주소를 검색 합니다 *RowStatusArray* 인수, SQL_ATTR_ROW_STATUS_PTR 문 특성에 없습니다. 합니다 *RowStatusArray* 호출에서 인수 **SQLExtendedFetch** null 포인터가 아니어야 합니다. (ODBC 3에서 유의 *.x*, SQL_ATTR_ROW_STATUS_PTR 문 특성은 null 포인터 일 수 있습니다.)<br />-드라이버에서 행 인출 버퍼의 주소를 검색 합니다 *RowCountPtr* 인수, SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 없습니다.<br />-드라이버는 SQLSTATE 01S01 반환 (행의 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했음을 알리는 **SQLExtendedFetch**합니다. ODBC 3 *.x* 드라이버는 SQLSTATE 01S01 반환할지 (행의 오류) 경우에만 **SQLExtendedFetch** 가 호출 되지 경우 **SQLFetch** 또는 **SQLFetchScroll** 라고 합니다. 이전 버전과 호환성을 유지 하는 경우 SQLSTATE 01S01 (행의 오류)가 반환한 **SQLExtendedFetch**, 드라이버 관리자는 시퀀스의 상태를 "에서 설명한 규칙에 따라 오류 큐의 상태 레코드를 정렬 되지 않은 레코드"섹션 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> -드라이버 SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />-드라이버 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열 주소를 검색합니다.<br />-드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 버퍼를 인출 하는 행의 주소를 검색 합니다.<br />-응용 프로그램 간의 호출을 혼합할 수 있습니다 **SQLFetchScroll** 하 고 **SQLFetch**합니다.<br />-   **SQLFetch** 0 열에 바인딩되는 경우에 책갈피를 반환 합니다.<br />-   **SQLFetch** 둘 이상의 행을 반환할 호출할 수 있습니다.<br />-드라이버는 SQLSTATE 01S01를 반환 하지 않습니다 (행의 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했음을 알리는 **SQLFetch**합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보입니다.<br /><br /> -드라이버 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에서 행 집합 크기를 검색합니다.<br />-드라이버 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열 주소를 검색합니다.<br />-드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 버퍼를 인출 하는 행의 주소를 검색 합니다.<br />-응용 프로그램 간의 호출을 혼합할 수 있습니다 **SQLFetchScroll** 하 고 **SQLFetch**합니다.<br />-드라이버는 SQLSTATE 01S01를 반환 하지 않습니다 (행의 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했음을 알리는 **SQLFetchScroll**합니다.|  
|**SQLSetPos**|다양 한 배치 작업을 수행합니다. 다음은 구현 세부 정보입니다.<br /><br /> -S6 또는 S7 문 상태의이 호출할 수 있습니다. 자세한 내용은 참조 하세요. [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.<br />-이 호출 하면 S5 또는 S6 문 상태의 드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성 및 행 상태 배열 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 주소에서 행 집합 크기를 검색 합니다.<br />-이 호출 하면 S7 문 상태의 검색 하 여 행 집합 크기 SQL_ROWSET_SIZE 문 특성 및 행 상태 배열에서 주소를 *RowStatusArray* 인수의  **SQLExtendedFetch**합니다.<br />-드라이버는 SQLSTATE 01S01 반환 (행의 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했음을 알리는 에게만 **SQLSetPos** S7 상태의 함수를 호출 하는 경우 대량 작업을 수행 하 합니다. 하는 경우 이전 버전과 호환성을 유지 하기 위해 SQLSTATE 01S01 (행의 오류)가 반환한 **SQLSetPos**, 드라이버 관리자는 시퀀스의 상태 "레코드"에 명시 된 규칙에 따라 오류 큐의 상태 레코드를 정렬 되지 않은 부분 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.<br />-경우 드라이버는 ODBC 2를 사용 하 여 작동 해야 합니다. *x* 를 호출 하는 응용 프로그램 **SQLSetPos** 사용 하 여는 *작업이* SQL_ADD의 인수, 드라이버를 지원 해야 **SQLSetPos** 는를사용하여 *작업* SQL_ADD의 인수입니다.|
