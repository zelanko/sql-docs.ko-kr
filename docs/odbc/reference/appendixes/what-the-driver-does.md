---
title: "드라이버에서 수행 하는 작업 | Microsoft Docs"
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e94046370f8140fdacec2cf708de0a62311a27
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-does"></a>드라이버에서 수행 하는 작업
다음 표에서 요약 함수 및 문 특성 ODBC 3*.x* 드라이버 블록 및 스크롤 가능 커서에 대해 구현 해야 합니다.  
  
|함수 또는<br /><br /> 문 특성|설명|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR을|행 상태 배열이의 주소에 의해 채워짐 설정 **SQLFetch** 및 **SQLFetchScroll**합니다. 이 배열에도 여 채워집니다 **SQLSetPos** 경우 **SQLSetPos** S6 문 상태에서 호출 됩니다. 경우 **SQLSetPos** 라고 S7 상태에서이 배열은 비어 있지만 배열에서 가리키는 *RowStatusArray* 의 인수 **SQLExtendedFetch** 채워집니다. 자세한 내용은 참조 [문을 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|버퍼의 주소를 설정 하는 **SQLFetch** 및 **SQLFetchScroll** 인출 된 행 수를 반환 합니다. 경우 **SQLExtendedFetch** 은 호출,이 버퍼 비어 있지만 *RowCountPtr* 인수 인출 된 행 수를 가리킵니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|사용 하는 행 집합 크기 설정 **SQLFetch** 및 **SQLFetchScroll**합니다.|  
|SQL_ROWSET_SIZE|사용 하는 행 집합 크기 설정 **SQLExtendedFetch**합니다. ODBC 3*.x* ODBC 2를 사용 하는 경우이 드라이버 구현.* x* 를 호출 하는 응용 프로그램 **SQLExtendedFetch** 또는 **SQLSetPos**합니다.|  
|**SQLBulkOperations**|ODBC 3 경우*.x* 드라이버는 ODBC 2와 작동 해야 합니다.* x* 를 사용 하는 응용 프로그램 **SQLSetPos** 와 *작업* SQL_ADD의 드라이버를 지원 해야 **SQLSetPos** 와 * 작업* 외에 SQL_ADD의 **SQLBulkOperations** 와 *작업* SQL_ADD의 합니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. ODBC 3*.x* ODBC 2를 사용 하는 경우이 드라이버 구현.* x* 를 호출 하는 응용 프로그램 **SQLExtendedFetch** 또는 **SQLSetPos**합니다. 다음은 구현 세부 정보:<br /><br /> -드라이버 SQL_ROWSET_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />-에서 행 상태 배열이의 주소를 검색 하는 드라이버는 *RowStatusArray* 인수, SQL_ATTR_ROW_STATUS_PTR 문 특성입니다. *RowStatusArray* 인수에 대 한 호출에 **SQLExtendedFetch** null 포인터가 아니어야 합니다. (ODBC 3에서*.x*, SQL_ATTR_ROW_STATUS_PTR 문 특성은 null 포인터 일 수 있습니다.)<br />-검색 하 여 행이 인출 버퍼의 주소는 *RowCountPtr* 인수, SQL_ATTR_ROWS_FETCHED_PTR 문 특성입니다.<br />-하면 드라이버는 SQLSTATE 01S01 반환 (행에서 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했습니다 나타내는 **SQLExtendedFetch**합니다. ODBC 3*.x* 드라이버는 SQLSTATE 01S01 반환할지 (행에서 오류) 경우에만 **SQLExtendedFetch** 를 호출 하지 때 **SQLFetch** 또는 **SQLFetchScroll** 라고 합니다. 이전 버전과 호환성을 유지 하는 경우 SQLSTATE 01S01 (행에서 오류)가 반환한 **SQLExtendedFetch**, 드라이버 관리자 상태 레코드의 시퀀스의 상태를 "에서 설명한 규칙에 따라 오류 큐에 정렬 되지 않은 기록"섹션의 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보:<br /><br /> -드라이버 SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />-드라이버 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열이의 주소를 검색합니다.<br />-드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 버퍼를 인출 된 행의 주소를 검색 합니다.<br />-응용 프로그램 간의 호출을 혼합할 수 **SQLFetchScroll** 및 **SQLFetch**합니다.<br />-   **SQLFetch** 0 열이 바인딩된 경우 책갈피를 반환 합니다.<br />-   **SQLFetch** 둘 이상의 행을 반환 하기 위해 호출할 수 있습니다.<br />-드라이버는 SQLSTATE 01S01를 반환 하지 않습니다 (행에서 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했습니다 나타내는 **SQLFetch**합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보:<br /><br /> -드라이버 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에서 행 집합 크기를 검색합니다.<br />-드라이버 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열이의 주소를 검색합니다.<br />-드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 버퍼를 인출 된 행의 주소를 검색 합니다.<br />-응용 프로그램 간의 호출을 혼합할 수 **SQLFetchScroll** 및 **SQLFetch**합니다.<br />-드라이버는 SQLSTATE 01S01를 반환 하지 않습니다 (행에서 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했습니다 나타내는 **SQLFetchScroll**합니다.|  
|**SQLSetPos**|다양 한 위치 지정된 작업을 수행합니다. 다음은 구현 세부 정보:<br /><br /> -이 S6 또는 S7 문 상태에서 호출할 수 있습니다. 자세한 내용은 참조 하십시오. [문을 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.<br />-이 메서드가 S5 또는 S6 문 상태에서 호출 되는 경우 드라이버 SQL_ATTR_ROWS_FETCHED_PTR 문 특성 및 행 상태 배열이 SQL_ATTR_ROW_STATUS_PTR 문 특성에서의 주소에서 행 집합 크기를 검색 합니다.<br />-이 메서드가 S7 문 상태에서 호출 되는 경우에서 검색 하 여 행 집합 크기 SQL_ROWSET_SIZE 문 특성 및 행 상태 배열이에서 주소는 *RowStatusArray* 인수의 ** SQLExtendedFetch**합니다.<br />-하면 드라이버는 SQLSTATE 01S01 반환 (행에서 오류)를 호출 하 여 인출 된 행 하는 동안 오류가 발생 했음을 알리는 에게만 **SQLSetPos** S7 상태에는 함수가 호출 될 때 대량 작업을 수행 하 합니다. 하는 경우 이전 버전과 호환성을 유지 하기 위해 SQLSTATE 01S01 (행에서 오류)가 반환한 **SQLSetPos**, 드라이버 관리자 상태 레코드 시퀀스의 상태 "레코드"에 명시 된 규칙에 따라 오류 큐에 정렬 되지 않은 섹션의 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.<br />-경우 드라이버는 ODBC 2와 작동 해야 합니다. *x* 를 호출 하는 응용 프로그램 **SQLSetPos** 와 *작업* SQL_ADD의 인수, 드라이버를 지원 해야 **SQLSetPos** 는 와* 작업* SQL_ADD의 인수입니다.|
