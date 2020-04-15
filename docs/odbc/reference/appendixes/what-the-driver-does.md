---
title: 운전자가 하는 일 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301394"
---
# <a name="what-the-driver-does"></a>드라이버가 수행하는 작업
다음 표에는 ODBC *3.x* 드라이버가 블록 및 스크롤 가능한 커서에 대해 구현해야 하는 함수 및 명령문 특성이 요약되어 있습니다.  
  
|기능 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|**SQLFetch** 및 **SQLFetchScroll로**채워진 행 상태 배열의 주소를 설정합니다. 이 배열은 **SQLSetPos가** 명령문 상태 S6에서 호출되는 경우에도 **SQLSetPos로** 채워져 있습니다. **SQLSetPos** 상태 S7에서 호출 되는 경우이 배열은 채워지지 않습니다 하지만 **SQLExtendedFetch의** *RowStatusArray* 인수에 의해 가리키는 배열이 채워지지 않습니다. 자세한 내용은 부록 B: ODBC 상태 전환 표의 [문 전환을](../../../odbc/reference/appendixes/statement-transitions.md) 참조하십시오.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**SQLFetch** 및 **SQLFetchScroll** 가져온 행 수를 반환 하는 버퍼의 주소를 설정 합니다. **SQLExtendedFetch가** 호출되면 이 버퍼는 채워지지 않지만 *RowCountPtr* 인수는 가져온 행 수를 가리킵니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQLFetch 및 **SQLFetchScroll에서**사용하는 행 집합 크기를 설정합니다. **SQLFetch**|  
|SQL_ROWSET_SIZE|**SQLExtendedFetch에서**사용하는 행 집합 크기를 설정합니다. ODBC *3.x* 드라이버는 **SQLExtendedFetch** 또는 **SQLSetPos를**호출하는 ODBC *2.x* 응용 프로그램과 함께 작업하려는 경우 이를 구현합니다.|  
|**SQLBulk운영**|ODBC *3.x* 드라이버가 SQL_ADD *작업과* 함께 **SQLSetPos를** 사용하는 ODBC *2.x* 응용 프로그램과 함께 작동해야 하는 경우 드라이버는 SQL_ADD *작업과* **SQLBulkOperations** 외에 SQL_ADD *작업으로* **SQLSetPos를** 지원해야 합니다.|  
|**SQLExtendedFetch**|지정된 행 집합을 반환합니다. ODBC *3.x* 드라이버는 **SQLExtendedFetch** 또는 **SQLSetPos를**호출하는 ODBC *2.x* 응용 프로그램과 함께 작업하려는 경우 이를 구현합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 드라이버는 SQL_ROWSET_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />- 드라이버는 SQL_ATTR_ROW_STATUS_PTR 문 특성이 아닌 *RowStatusArray* 인수에서 행 상태 배열의 주소를 검색합니다. **SQLExtendedFetch에** 대한 호출의 *RowStatusArray* 인수는 null 포인터가 아니어야 합니다. ODBC *3.x에서*SQL_ATTR_ROW_STATUS_PTR 문 특성은 null 포인터일 수 있습니다.<br />- 드라이버는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성이 아닌 *RowCountPtr* 인수에서 가져온 행의 주소를 검색합니다.<br />- 드라이버는 SQLSTATE 01S01 (행의 오류)를 반환하여 **SQLExtendedFetch**에 대한 호출로 행을 가져오는 동안 오류가 발생했음을 나타냅니다. ODBC *3.x* 드라이버는 SQLFetch 또는 **SQLFetchScroll가** 호출될 때가 아니라 **SQLExtendedFetch가** 호출될 때만 **SQLSTATE** 01S01(행의 오류)을 반환해야 합니다. 이전 버전과의 호환성을 유지하기 위해 SQLState 01S01(행의 오류)이 **SQLExtendedFetch에서**반환될 때 드라이버 관리자는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "상태 레코드 시퀀스" 섹션에 명시된 규칙에 따라 오류 큐에서 상태 레코드를 정렬하지 않습니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 드라이버는 SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값에서 행 집합 크기를 검색합니다.<br />- 드라이버는 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열의 주소를 검색합니다.<br />- 드라이버는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 가져온 행의 버퍼의 주소를 검색합니다.<br />- 응용 프로그램은 **SQLFetchScroll와** **SQLFetch**사이의 호출을 혼합 할 수 있습니다.<br />-   **SQLFetch는** 열 0이 바인딩된 경우 책갈피를 반환합니다.<br />-   **SQLFetch는** 두 개 이상의 행을 반환하기 위해 호출할 수 있습니다.<br />- 드라이버는 **SQLState**01S01 (행의 오류)를 반환하지 않습니다.|  
|**SQLFetchScroll**|지정된 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 드라이버는 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에서 행 집합 크기를 검색합니다.<br />- 드라이버는 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열의 주소를 검색합니다.<br />- 드라이버는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 가져온 행의 버퍼의 주소를 검색합니다.<br />- 응용 프로그램은 **SQLFetchScroll와** **SQLFetch**사이의 호출을 혼합 할 수 있습니다.<br />- 드라이버는 **SQLState**01S01 (행의 오류)를 반환하지 않습니다.|  
|**SQLSetPos**|다양한 위치 가있는 작업을 수행합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 이것은 문 상태 S6 또는 S7에서 호출 할 수 있습니다. 자세한 내용은 부록 B: ODBC 상태 전환 표의 [문 전환을](../../../odbc/reference/appendixes/statement-transitions.md) 참조하십시오.<br />- 이 문 상태 S5 또는 S6에서 호출 되는 경우 드라이버는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성및 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 행 상태 배열의 주소에서 행 집합 크기를 검색 합니다.<br />- 이 문 상태 S7에서 호출 되는 경우 드라이버는 SQL_ROWSET_SIZE 문 특성및 행 상태 배열의 주소에서 행 집합 크기를 검색 **합니다./** *ROWStatusArray* 의 ROWStatus 인수에서 .<br />- 드라이버는 SQLSTATE 01S01 (행의 오류)을 반환만 함수가 상태 S7에서 호출 될 때 대량 작업을 수행하기 위해 **SQLSetPos에** 대한 호출에 의해 행을 가져 온 동안 오류가 발생했음을 나타냅니다. 이전 버전과의 호환성을 유지하기 위해 SQLSTATE 01S01(행의 오류)이 **SQLSetPos에서**반환되는 경우 드라이버 관리자는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "상태 레코드 시퀀스" 섹션에 명시된 규칙에 따라 오류 큐에서 상태 레코드를 정렬하지 않습니다.<br />- 드라이버가 SQL_ADD *작업* 인수와 **SQLSetPos를** 호출 하는 ODBC *2.x* 응용 프로그램으로 작동 해야 하는 경우 드라이버는 SQL_ADD *작업* 인수와 **SQLSetPos를** 지원 해야 합니다.|
