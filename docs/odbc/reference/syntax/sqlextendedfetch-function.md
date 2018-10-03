---
title: SQLExtendedFetch 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1896ec473caf1af8a3fa2bdaa4156ddca3c0a6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697052"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 **SQLExtendedFetch** 결과 집합에서 데이터의 지정 된 행 집합을 인출 하 고 모든 바인딩된 열에 대 한 데이터를 반환 합니다. 절대 또는 상대 위치 또는 책갈피 별로 행 집합을 지정할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3에서 *.x*하십시오 **SQLExtendedFetch** 바뀌었습니다 **SQLFetchScroll**합니다. ODBC 3 *.x* 응용 프로그램을 호출 하지 않아야 **SQLExtendedFetch**; 대신 호출 해야 **SQLFetchScroll**합니다. 드라이버 관리자 매핑합니다 **SQLFetchScroll** 하 **SQLExtendedFetch** 는 ODBC 2를 사용 하 여 작업 하는 경우 *.x* 드라이버입니다. ODBC 3 *.x* 드라이버를 지원 해야 **SQLExtendedFetch** ODBC 2를 사용 하는 경우 *.x* 호출 하는 응용 프로그램입니다. 자세한 내용은 "설명"을 참조 하세요. 및 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침입니다.  
  
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
 [입력] 인출 유형입니다. 이 동일 *FetchOrientation* 에 **SQLFetchScroll**합니다.  
  
 *FetchOffset*  
 [입력] 페치할 행의 수입니다. 이 동일 *FetchOffset* 에서 **SQLFetchScroll**, 한 가지 예외로 합니다. 때 *FetchOrientation* SQL_FETCH_BOOKMARK, 됩니다 *FetchOffset* 는 고정 길이 책갈피에 책갈피에서 오프셋 없습니다. 다시 말해 **SQLExtendedFetch** 은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성이이 인수에서 책갈피를 검색 합니다. 가변 길이 책갈피를 지원 하지 않습니다 하 고 책갈피에서 오프셋 (0)이 아닌 행 집합을 인출 하는 것을 지원 하지 않습니다.  
  
 *RowCountPtr*  
 [출력] 실제로 인출 된 행 수를 반환 하는 버퍼에 대 한 포인터입니다. 이 버퍼는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 지정 된 버퍼와 동일한 방식으로 사용 됩니다. 이 버퍼는 해야만 **SQLExtendedFetch**합니다. 사용 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll**합니다.  
  
 *RowStatusArray*  
 [출력] 각 행의 상태를 반환 하는 배열에 대 한 포인터입니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 배열과 같은 방식으로 사용 됩니다.  
  
 그러나이 배열의 주소 SQL_DESC_STATUS_ARRAY_PTR IRD 필드에 저장 되지 않습니다. 게다가이 배열 에서만 사용 됩니다 **SQLExtendedFetch** 버전과 **SQLBulkOperations** 사용 하 여는 *작업* SQL_ADD의 또는 **SQLSetPos**한 후 호출 되는 경우 **SQLExtendedFetch**합니다. 사용 되지 않습니다 **SQLFetch** 또는 **SQLFetchScroll**, 및에서 사용 되지 않습니다 **SQLBulkOperations** 하거나 **SQLSetPos** 후 호출 될 때 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 것도 하지 사용 되는 경우 **SQLBulkOperations** 사용 하 여는 *작업* SQL_ADD의는 모든 fetch 함수를 호출 하기 전에 호출 됩니다. 즉, S7 문 상태 에서만에서 사용 됩니다. S5 또는 S6 문 상태는 사용 되지 않습니다. 자세한 내용은 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.  
  
 응용 프로그램에 대 한 유효한 포인터를 제공 해야 합니다 *RowStatusArray* 인수입니다; 그렇지 않은 경우의 동작 **SQLExtendedFetch** 에 대 한 호출의 동작 및 **SQLBulkOperations**나 **SQLSetPos** 커서에서 배치 된 후 **SQLExtendedFetch** 정의 되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLExtendedFetch** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLError**합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLExtendedFetch** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다. 단일 열에서 오류가 발생 하는 경우 **SQLGetDiagField** 호출할 수는 *DiagIdentifier* ;에서 오류가 발생 하는 열을 확인 하려면 SQL_DIAG_COLUMN_NUMBER의 및  **SQLGetDiagField** 호출할 수는 *DiagIdentifier* 열이 포함 된 행을 확인 하려면 SQL_DIAG_ROW_NUMBER입니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|공백이 아닌 문자 또는 NULL이 아닌 이진 데이터의 잘림 문자열 또는 이진 데이터 열에 대 한 반환 했습니다. 문자열 값이 오른쪽 잘림 이었습니다. 숫자 값이 숫자의 소수 부분이 잘렸습니다.  (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S06|결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 합니다.|요청 된 행 집합에 첫 번째 행에서 위로 및 하거나 현재 위치를 때 결과 집합의 시작 overlapped *FetchOrientation* SQL_PRIOR 되었습니다 또는 *FetchOrientation* 를 사용 하 여 SQL_RELATIVE는 음수 *FetchOffset* 절대 값 보다 작거나 현재 SQL_ROWSET_SIZE를 되었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 간격 데이터 형식에 대 한 시간의 소수 부분을 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|에 지정 된 C 데이터 형식에는 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.|  
|07009|잘못 된 설명자 인덱스입니다.|열 0이 사용 하 여 바인딩된 **SQLBindCol**, SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지|NULL 데이터가 페치된 열을 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** 가 null 포인터입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22003|숫자 값 범위를 벗어났습니다.|하나 이상의 열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> 자세한 내용은 [간격 및 숫자 데이터 형식에 대 한 지침](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 부록 d: 데이터 형식에서입니다.|  
|22007|잘못 된 날짜/시간 형식|결과 집합의 문자 열 된 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 부서에서 발생 하는 0입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형을 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> 간격 C 형식으로 데이터를 인출할 때 C 간격 유형으로 SQL 형식의 값 표현 방식이 없기 있었습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22018|캐스트 사양의 문자 값|C 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 열의 SQL 형식이 된 문자 데이터 형식입니다. 하는 열에 값을 바인딩된 C 형식의 유효한 리터럴이 없습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|24000|잘못된 커서 상태|합니다 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLError** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle*, 및 함수를 호출한 다음 다시 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLExtendedFetch** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 실행 상태가 없습니다. 이 함수가 먼저 호출 하지 않고 호출 **SQLExecDirect**를 **SQLExecute**, 또는 카탈로그 함수입니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM) **SQLExtendedFetch** 에 대해 호출 된 합니다 *StatementHandle* 후 **SQLFetch** 또는 **SQLFetchScroll** 호출한 전과  **SQLFreeStmt** SQL_CLOSE 옵션과 함께 호출 되었습니다.<br /><br /> (DM) **SQLBulkOperations** 문의 하기 전에 호출 되었습니다 **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLExtendedFetch** 호출 및 그런 다음 **SQLExtendedFetch** 하기 전에 호출 되었습니다 **SQLFreeStmt** SQL_CLOSE 옵션과 함께 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY106|인출 유형 범위를 벗어났습니다.|인수에 지정 된 값 (DM) *FetchOrientation* 올바르지 않습니다. ("주석입니다." 참조)<br /><br /> 인수 *FetchOrientation* SQL_FETCH_BOOKMARK, 되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY, 및 인수 값에서는 SQL_CURSOR_TYPE 문 옵션의 값이 *FetchOrientation* SQL_FETCH_NEXT 없습니다.<br /><br /> 인수 *FetchOrientation* SQL_FETCH_RESUME 되었습니다.|  
|HY107|행 값 범위를 벗어났습니다.|에서는 SQL_CURSOR_TYPE 문 옵션을 사용 하 여 지정 된 값, SQL_CURSOR_KEYSET_DRIVEN 되었지만 SQL_KEYSET_SIZE 문 특성을 사용 하 여 지정한 값이 0 보다 크고 SQL_ROWSET_SIZE 문 특성을 사용 하 여 지정 된 값 보다 작음 .|  
|HY111|잘못 된 책갈피 값입니다.|인수 *FetchOrientation* SQL_FETCH_BOOKMARK, 되었으며에 책갈피를 지정 합니다 *FetchOffset* 인수가 잘못 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본에 지정 된 인출 유형을 지원 하지 않습니다.<br /><br /> 드라이버 또는 데이터 원본 조합에 의해 지정 된 변환을 지원 하지 않습니다 합니다 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다. 이 오류는 SQL 데이터 형식의 열 드라이버별 SQL 데이터 형식에 매핑한 경우에 적용 됩니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtOption**, SQL_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 동작은 **SQLExtendedFetch** 의 동일 **SQLFetchScroll**, 다음과 같은 예외를 사용 하 여:  
  
-   **SQLExtendedFetch** 하 고 **SQLFetchScroll** 다른 방법을 사용 하 여 인출 된 행 수를 반환 합니다. **SQLExtendedFetch** 인출 된 행 수가 반환  *\*RowCountPtr*; **SQLFetchScroll** SQL_ATTR_ROWS_FETCHED_PTR 가리키는 버퍼에 직접 인출 되는 행 수를 반환 합니다. 자세한 내용은 참조는 *RowCountPtr* 인수입니다.  
  
-   **SQLExtendedFetch** 하 고 **SQLFetchScroll** 다른 배열에서 각 행의 상태를 반환 합니다. 자세한 내용은 참조는 *RowStatusArray* 인수입니다.  
  
-   **SQLExtendedFetch** 하 고 **SQLFetchScroll** 다른 방법을 사용 하 여 책갈피를 검색할 때 *FetchOrientation* SQL_FETCH_BOOKMARK는 합니다. **SQLExtendedFetch** 가변 길이 책갈피 또는 책갈피에서 0이 아닌 오프셋에서 가져오는 행 집합을 지원 하지 않습니다. 자세한 내용은 참조는 *FetchOffset* 인수입니다.  
  
-   **SQLExtendedFetch** 하 고 **SQLFetchScroll** 다른 행 집합 크기를 사용 합니다. **SQLExtendedFetch** SQL_ROWSET_SIZE 문 특성의 값을 사용 하 고 **SQLFetchScroll** SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값을 사용 합니다.  
  
-   **SQLExtendedFetch** 약간 다른 오류 보다 의미 체계를 처리 했습니다 **SQLFetchScroll**합니다. 자세한 내용은 "오류 처리"의 "설명" 섹션을 참조 하세요 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
-   **SQLExtendedFetch** 바인딩 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성)를 지원 하지 않습니다.  
  
-   에 대 한 호출 **SQLExtendedFetch** 를 호출 하 여 혼합할 수 없습니다 **SQLFetch** 또는 **SQLFetchScroll**, 경우에 **SQLBulkOperations** 라고 모든 인출 함수를 호출 하기 전에 **SQLExtendedFetch** 커서를 닫았다가 다시 열 때까지 호출할 수 없습니다. 즉, **SQLExtendedFetch** 문 상태 S7 에서만에서 호출할 수 있습니다. 자세한 내용은 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 부록 b: ODBC 상태 전환 표에 합니다.  
  
 응용 프로그램을 호출할 때 **SQLFetchScroll** 는 ODBC 2를 사용 하는 동안 *.x* 드라이버를 드라이버 관리자는이 호출을 매핑합니다 **SQLExtendedFetch**합니다. 자세한 내용은 "SQLFetchScroll 및 ODBC 2 *.x* 드라이버"에서 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
 ODBC 2에서 *.x*를 **SQLExtendedFetch** 여러 행을 인출 호출한 및 **SQLFetch** 단일 행을 인출 하기 위해 호출 되었습니다. ODBC 3에서 *.x*, 다른 한편 **SQLFetch** 여러 행을 인출 하기 위해 호출할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업을 수행합니다.|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침, 업데이트 또는 결과 집합의 데이터 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
