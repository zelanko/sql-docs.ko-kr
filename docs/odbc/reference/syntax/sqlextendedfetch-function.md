---
title: "SQLExtendedFetch 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6c0336d9f7d3495e7e2ef925b86d47c472ff2ec
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 **SQLExtendedFetch** 결과 집합에서 데이터의 지정 된 행 집합을 인출 하 고 모든 바운드 열에 대 한 데이터를 반환 합니다. 책갈피 또는 절대 또는 상대 위치에서 행 집합을 지정할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3에서*.x*, **SQLExtendedFetch** 로 대체 되었습니다 **SQLFetchScroll**합니다. ODBC 3*.x* 응용 프로그램을 호출 하지 않아야 **SQLExtendedFetch**; 대신 호출 해야 **SQLFetchScroll**합니다. 드라이버 관리자 매핑합니다 **SQLFetchScroll** 를 **SQLExtendedFetch** 는 ODBC 2 작업할 때*.x* 드라이버입니다. ODBC 3*.x* 드라이버를 지원 해야 **SQLExtendedFetch** ODBC 2를 사용 하는 경우*.x* 메서드를 호출 하는 응용 프로그램입니다. 자세한 내용은 "설명"을 참조 하십시오. 및 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *FetchOrientation*  
 [입력] Fetch의 유형입니다. 이와 동일 하 게 *FetchOrientation* 에 **SQLFetchScroll**합니다.  
  
 *FetchOffset*  
 [입력] 인출할 행 수입니다. 이와 동일 하 게 *FetchOffset* 에 **SQLFetchScroll**, 한 가지를 제외 합니다. 때 *FetchOrientation* SQL_FETCH_BOOKMARK은 *FetchOffset* 는 고정 길이 책갈피는 책갈피에서의 오프셋 없습니다. 즉, **SQLExtendedFetch** 은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성이이 인수에서 책갈피를 검색 합니다. 가변 길이 책갈피를 지원 하지 않는 하 고 책갈피에서 오프셋 (0)이 아닌 행 집합을 인출 하는 것을 지원 하지 않습니다.  
  
 *RowCountPtr*  
 [출력] 실제로 가져온 행 수를 반환 하는 버퍼에 대 한 포인터입니다. 이 버퍼는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 지정 된 버퍼와 같은 방식으로 사용 됩니다. 이 버퍼 으로만 사용 되므로 **SQLExtendedFetch**합니다. 사용 되지 않는 **SQLFetch** 또는 **SQLFetchScroll**합니다.  
  
 *RowStatusArray*  
 [출력] 각 행의 상태를 반환 하는 배열에 대 한 포인터입니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 배열과 같은 방식으로 사용 됩니다.  
  
 그러나이 배열의 주소 SQL_DESC_STATUS_ARRAY_PTR IRD 필드에 저장 되지 않습니다. 또한이 배열은 으로만 사용 되므로 **SQLExtendedFetch** 및 **SQLBulkOperations** 와 *작업* SQL_ADD의 또는 **SQLSetPos**후 호출 될 때 **SQLExtendedFetch**합니다. 사용 되지 않는 **SQLFetch** 또는 **SQLFetchScroll**, 여는 사용 하지 않는 **SQLBulkOperations** 또는 **SQLSetPos** 후 호출 될 때 **SQLFetch** 또는 **SQLFetchScroll**합니다. 경우도 많습니다 경우 사용된 **SQLBulkOperations** 와 *작업* SQL_ADD의는 모든 fetch 함수를 호출 하기 전에 호출 됩니다. 즉, S7 문 상태에만 사용 됩니다. S5 또는 S6 문 상태에는 사용 되지 않습니다. 자세한 내용은 참조 [문을 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.  
  
 응용 프로그램에 대 한 유효한 포인터를 제공 해야는 *RowStatusArray* 인수; 그렇지 않은 경우의 동작 **SQLExtendedFetch** 에 대 한 호출의 동작 및 **SQLBulkOperations**또는 **SQLSetPos** 하 여 커서를 배치 된 후 **SQLExtendedFetch** 정의 되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLExtendedFetch** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLError**합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLExtendedFetch** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다. 하나의 열에 오류가 발생 한 경우 **SQLGetDiagField** 호출할 수는 *DiagIdentifier* 의 SQL_DIAG_COLUMN_NUMBER;에서 오류가 발생 하는 열을 확인 하 고  **SQLGetDiagField** 호출할 수는 *DiagIdentifier* 의 해당 열이 포함 된 행을 결정 하는 SQL_DIAG_ROW_NUMBER 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|문자열 또는 열에 대해 반환 된 이진 데이터의 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 했습니다. 문자열 값 경우 오른쪽 잘림 없었습니다. 숫자 값을 숫자의 소수 부분이 잘렸습니다.  (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S01|행 하는 동안 오류가 발생 했습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S06|결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 합니다.|요청 된 행 집합의 현재 위치를 첫 번째 행을 초과 하거나 때 결과 집합의 시작 겹쳐진 *FetchOrientation* SQL_PRIOR 되었습니다 또는 *FetchOrientation* SQL_RELATIVE로가 음수 *FetchOffset* 절대 값이 현재 SQL_ROWSET_SIZE 보다 작습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|일부가 잘렸습니다.|열에 대해 반환 되는 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 interval 데이터 형식을 시간 구성 요소가 포함 된 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|지정한 C 데이터 형식으로 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.|  
|07009|잘못 된 설명자 인덱스입니다.|0 열 바인딩된 **SQLBindCol**, SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지 않았습니다.|NULL 데이터를 가져온 열으로 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** 는 null 포인터입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22003|숫자 값 범위를 벗어났습니다.|하나 이상의 열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환는 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> 자세한 내용은 참조 [간격 및 숫자 데이터 형식에 대 한 지침이](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 부록 d: 데이터 형식에서입니다.|  
|22007|잘못 된 날짜/시간 형식|날짜, 시간 또는 타임 스탬프 C 구조에는 문자는 결과 집합 열에에서 바인딩된 되었으며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 나누기에서 복원 하려고 시도 했습니다 0입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형으로 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> C 간격 유형으로 데이터를 인출할 때 C 간격 유형에서 SQL 형식의 값으로 표시 되지 했습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22018|캐스트 사양의 문자 값|정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 C 유형은 열의 SQL 형식을 문자 데이터 형식. 및 열에 값이 바인딩된 C 형식의 올바른 리터럴.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|24000|잘못된 커서 상태|*StatementHandle* 된 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLError** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*, 함수가 호출 후 및 다시는 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLExtendedFetch** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 호출 하지 않고 호출 된 **SQLExecDirect**, **SQLExecute**, 또는 카탈로그 함수입니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **SQLExtendedFetch** 에 대 한 호출 된는 *StatementHandle* 후 **SQLFetch** 또는 **SQLFetchScroll** 호출한 하기전에 **SQLFreeStmt** SQL_CLOSE 옵션과 함께 호출 되었습니다.<br /><br /> (DM) **SQLBulkOperations** 하기 전에 명령문에 대 한 호출 된 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLExtendedFetch** 를 호출 하 고 그런 다음 **SQLExtendedFetch** 하기 전에 호출 된 **SQLFreeStmt** SQL_CLOSE 옵션과 함께 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY106|인출 유형 범위를 벗어났습니다.|인수에 대해 지정 된 값 (DM) *FetchOrientation* 올바르지 않습니다. ("주석" 참조)<br /><br /> 인수 *FetchOrientation* SQL_FETCH_BOOKMARK, 였으며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> 에서는 SQL_CURSOR_TYPE 문 옵션의 값이 SQL_CURSOR_FORWARD_ONLY, 및 인수 값 *FetchOrientation* SQL_FETCH_NEXT 없습니다.<br /><br /> 인수 *FetchOrientation* SQL_FETCH_RESUME 되었습니다.|  
|HY107|행 값 범위를 벗어났습니다.|에서는 SQL_CURSOR_TYPE 문 옵션으로 지정 된 값 SQL_CURSOR_KEYSET_DRIVEN만 SQL_KEYSET_SIZE 문 특성으로 지정 된 값이 0 보다 크고 SQL_ROWSET_SIZE 문 특성으로 지정 된 값 보다 작음 .|  
|HY111|잘못 된 책갈피 값입니다.|인수 *FetchOrientation* SQL_FETCH_BOOKMARK, 였으며에 지정 된 책갈피는 *FetchOffset* 인수가 잘못 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본에 지정 된 인출 유형을 지원 하지 않습니다.<br /><br /> 드라이버 또는 데이터 원본 변환의 조합으로 지정 하는 지원 하지 않습니다는 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다. 이 오류는 SQL 데이터 형식 열의 드라이버별 SQL 데이터 형식에 매핑된 경우에 적용 됩니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtOption**, SQL_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 동작 **SQLExtendedFetch** 의 동일 **SQLFetchScroll**, 다음을 제외:  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll** 다양 한 방법을 사용 하 여 인출 된 행 수를 반환 합니다. **SQLExtendedFetch** 에 인출 된 행 수를 반환  *\*RowCountPtr*; **SQLFetchScroll** SQL_ATTR_ROWS_FETCHED_PTR 가리키는 버퍼에 직접 가져온 행 수를 반환 합니다. 자세한 내용은 참조는 *RowCountPtr* 인수입니다.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll** 다른 배열에서 각 행의 상태를 반환 합니다. 자세한 내용은 참조는 *RowStatusArray* 인수입니다.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll** 다양 한 방법을 사용 하 여 책갈피를 검색 하는 경우 *FetchOrientation* SQL_FETCH_BOOKMARK는 합니다. **SQLExtendedFetch** 가변 길이 책갈피 또는 책갈피에서 0이 아닌 오프셋에서 가져오는 행 집합을 지원 하지 않습니다. 자세한 내용은 참조는 *FetchOffset* 인수입니다.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll** 다른 행 집합 크기를 사용 합니다. **SQLExtendedFetch** SQL_ROWSET_SIZE 문 특성의 값을 사용 하 고 **SQLFetchScroll** SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값을 사용 합니다.  
  
-   **SQLExtendedFetch** 약간 다른 오류 의미 체계 처리에 **SQLFetchScroll**합니다. 자세한 내용은의 "설명" 섹션에 "오류 처리"를 참조 하십시오 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
-   **SQLExtendedFetch** 바인딩 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성)를 지원 하지 않습니다.  
  
-   에 대 한 호출이 **SQLExtendedFetch** 와 함께 혼합할 수 없고 **SQLFetch** 또는 **SQLFetchScroll**, 쓰고 **SQLBulkOperations** 라고 모든 인출 함수를 호출 하기 전에 **SQLExtendedFetch** 커서를 닫았다가 다시 열 때까지를 호출할 수 없습니다. 즉, **SQLExtendedFetch** S7 문 상태에만 호출할 수 있습니다. 자세한 내용은 참조 [문을 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLFetchScroll** ODBC 2를 사용 하는 동안*.x* 드라이버, 드라이버 관리자 매핑합니다이 호출으로 **SQLExtendedFetch**합니다. 자세한 내용은 참조 하십시오. "SQLFetchScroll 및 ODBC 2*.x* 드라이버"에서 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
 ODBC 2에서*.x*, **SQLExtendedFetch** 여러 행을 인출 하 호출한 및 **SQLFetch** 단일 행을 인출 하기 위해 호출 되었습니다. ODBC 3에서*.x*반면에, **SQLFetch** 여러 행을 인출 하기 위해 호출할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업을 수행합니다.|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침 또는 업데이트 또는 결과 집합의 데이터를 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

