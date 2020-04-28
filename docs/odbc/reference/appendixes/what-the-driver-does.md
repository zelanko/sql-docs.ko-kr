---
title: 드라이버의 기능 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301394"
---
# <a name="what-the-driver-does"></a>드라이버가 수행하는 작업
다음 표에는 ODBC *3.x 드라이버가 블록* 및 스크롤 가능 커서에 대해 구현 해야 하는 함수 및 문 특성이 요약 되어 있습니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch** 및 **sqlfetchscroll**으로 채워지는 행 상태 배열의 주소를 설정 합니다. 이 배열은 **sqlsetpos** 가 문 상태 S6에서 호출 되는 경우 **sqlsetpos** 로도 채워집니다. **SQLSetPos** 가 상태 S7에서 호출 되는 경우이 배열은 채워지지 않지만 **sqlextendedfetch** 의 *rowstatusarray* 인수가 가리키는 배열은 채워집니다. 자세한 내용은 부록 B: ODBC 상태 전환 테이블의 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 을 참조 하세요.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch** 및 **sqlfetchscroll** 이 인출 된 행 수를 반환 하는 버퍼의 주소를 설정 합니다. **Sqlextendedfetch** 가 호출 되는 경우이 버퍼는 채워지지 않지만 *rowcountptr* 인수는 인출 된 행 수를 가리킵니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|**Sqlfetch** 및 **sqlfetchscroll**에서 사용 되는 행 집합 크기를 설정 합니다.|  
|SQL_ROWSET_SIZE|**Sqlextendedfetch**에서 사용 되는 행 집합 크기를 설정 합니다. ODBC *3.x 드라이버는* **sqlextendedfetch** 또는 **SQLSETPOS**를 호출 하는 odbc *2.x 응용 프로그램* 을 사용 하려는 경우이를 구현 합니다.|  
|**SQLBulkOperations**|ODBC *2.x 드라이버가 SQL_ADD* *작업과* 함께 **SQLSETPOS** 를 사용 하는 odbc 2.x *응용 프로그램* 에서 작동 해야 하는 경우 드라이버는 SQL_ADD *작업* 으로 **SQLBulkOperations** 외에도 SQL_ADD *작업* 을 사용 하 여 **sqlsetpos** 를 지원 해야 합니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. ODBC *3.x 드라이버는* **sqlextendedfetch** 또는 **SQLSETPOS**를 호출 하는 odbc *2.x 응용 프로그램* 을 사용 하려는 경우이를 구현 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -드라이버는 SQL_ROWSET_SIZE statement 특성의 값에서 행 집합 크기를 검색 합니다.<br />-드라이버는 SQL_ATTR_ROW_STATUS_PTR statement 특성이 아니라 *Rowstatusarray* 인수에서 행 상태 배열의 주소를 검색 합니다. **Sqlextendedfetch** 호출의 *rowstatusarray* 인수는 null 포인터가 아니어야 합니다. ODBC 3.x에서 SQL_ATTR_ROW_STATUS_PTR statement 특성은 null 포인터 일 수 *있습니다.*<br />-드라이버는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성이 아니라 *Rowcountptr* 인수에서 인출 된 행의 주소를 검색 합니다.<br />-드라이버가 **Sqlextendedfetch**를 호출 하 여 행을 인출 하는 동안 오류가 발생 했음을 나타내는 SQLSTATE 01S01 (행 오류)를 반환 합니다. ODBC 3.x 드라이버는 **sqlfetch** 또는 **sqlextendedfetch** 이 호출 될 때가 아니라 **sqlextendedfetch** 가 호출 되는 경우에만 SQLSTATE 01S01 (행 오류)를 반환 해야 *합니다.* 이전 버전과의 호환성을 유지 하기 위해, SQLSTATE 01S01 (행 오류)가 **Sqlextendedfetch**에 의해 반환 되는 경우 드라이버 관리자는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "상태 레코드 시퀀스" 섹션에 명시 된 규칙에 따라 오류 큐의 상태 레코드를 정렬 하지 않습니다.|  
|**SQLFetch**|다음 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -드라이버는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성의 값에서 행 집합 크기를 검색 합니다.<br />-드라이버는 SQL_ATTR_ROW_STATUS_PTR statement 특성에서 행 상태 배열의 주소를 검색 합니다.<br />-드라이버는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에서 인출 된 행의 주소를 검색 합니다.<br />-응용 프로그램은 **Sqlfetchscroll** 및 **sqlfetch**간의 호출을 혼합할 수 있습니다.<br />-   열 0이 바인딩되면 **Sqlfetch** 에서 책갈피를 반환 합니다.<br />-   **Sqlfetch** 를 호출 하 여 둘 이상의 행을 반환할 수 있습니다.<br />-드라이버가 **Sqlfetch**를 호출 하 여 행을 인출 하는 동안 오류가 발생 했음을 나타내는 SQLSTATE 01S01 (행 오류)를 반환 하지 않습니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -드라이버는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성에서 행 집합 크기를 검색 합니다.<br />-드라이버는 SQL_ATTR_ROW_STATUS_PTR statement 특성에서 행 상태 배열의 주소를 검색 합니다.<br />-드라이버는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에서 인출 된 행의 주소를 검색 합니다.<br />-응용 프로그램은 **Sqlfetchscroll** 및 **sqlfetch**간의 호출을 혼합할 수 있습니다.<br />-드라이버가 **Sqlfetchscroll**을 호출 하 여 행을 인출 하는 동안 오류가 발생 했음을 나타내는 SQLSTATE 01S01 (행 오류)를 반환 하지 않습니다.|  
|**SQLSetPos**|다양 한 위치 지정 작업을 수행 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -문 상태 S6 또는 S7에서 호출할 수 있습니다. 자세한 내용은 부록 B: ODBC 상태 전환 테이블의 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 을 참조 하세요.<br />-이를 문 상태 S5 또는 S6에서 호출 하는 경우 드라이버는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에서 행 집합 크기를 검색 하 고 SQL_ATTR_ROW_STATUS_PTR statement 특성에서 행 상태 배열의 주소를 검색 합니다.<br />-이 문이 문 상태 S7에서 호출 되는 경우 드라이버는 **Sqlextendedfetch**의 *rowstatusarray* 인수에서 행 상태 배열의 주소와 SQL_ROWSET_SIZE statement 특성에서 행 집합 크기를 검색 합니다.<br />-드라이버가 상태 S7에서 함수가 호출 될 때 대량 작업을 수행 하기 위해 **SQLSetPos** 를 호출 하 여 행을 인출 하는 동안 오류가 발생 했음을 나타내기 위해 SQLSTATE 01S01 (error in row)만 반환 합니다. 이전 버전과의 호환성을 유지 하기 위해 SQLSTATE 01S01 (행 오류)가 **SQLSetPos**에서 반환 되는 경우 드라이버 관리자는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "상태 레코드 시퀀스" 섹션에 명시 된 규칙에 따라 오류 큐의 상태 레코드를 정렬 하지 않습니다.<br />-드라이버는 SQL_ADD의 *작업* 인수를 사용 하 여 **sqlsetpos** 를 호출 하는 ODBC 2.x 응용 프로그램에서 작동 해야 하는 경우 드라이버는 SQL_ADD의 *작업* 인수를 사용 하 여 **sqlsetpos** 를 지원 해야 *합니다.*|
