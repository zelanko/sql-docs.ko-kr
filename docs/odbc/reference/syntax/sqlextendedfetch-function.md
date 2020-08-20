---
description: SQLExtendedFetch 함수
title: SQLExtendedFetch 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac19d017baf4a3f0e873be64cd2eb812ca1b05e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476113"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 **Sqlextendedfetch** 는 결과 집합에서 지정 된 데이터 행 집합을 인출 하 고 모든 바인딩된 열에 대해 데이터를 반환 합니다. 행 집합은 절대 또는 상대 위치 또는 책갈피로 지정할 수 있습니다.  
  
> [!NOTE]
>  ODBC 3.x에서 **sqlextendedfetch** 는 **sqlextendedfetch***으로 대체*되었습니다. ODBC 3.x*응용 프로그램은* **sqlextendedfetch**를 호출 하면 안 됩니다. 대신 **Sqlfetchscroll**을 호출 해야 합니다. 드라이버 관리자는 ODBC*2.x 드라이버를* 사용 하 여 작업할 때 **Sqlfetchscroll** 를 **sqlfetchscroll** 에 매핑합니다. ODBC 3.x*드라이버는* 이를 호출 하는 odbc*2.x 응용 프로그램* 을 사용 하려는 경우 **sqlextendedfetch** 를 지원 해야 합니다. 자세한 내용은 이전 버전과의 호환성을 위한 부록 G: 드라이버 지침의 "주석" 및 [블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *FetchOrientation*  
 입력 Fetch의 유형입니다. 이는 **Sqlfetchscroll**의 *fetchorientation* 와 동일 합니다.  
  
 *FetchOffset*  
 입력 인출할 행의 번호입니다. 이는 **Sqlfetchscroll**의 *fetchoffset* 과 동일 하지만 한 가지 예외가 있습니다. *Fetchorientation* 가 SQL_FETCH_BOOKMARK 때 *fetchorientation* 은 책갈피의 오프셋이 아니라 고정 길이 책갈피입니다. 즉, **Sqlextendedfetch** 는 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성이 아닌이 인수에서 책갈피를 검색 합니다. 가변 길이 책갈피를 지원 하지 않으며 책갈피에서 0이 아닌 오프셋에 있는 행 집합을 인출 하는 것을 지원 하지 않습니다.  
  
 *함수의 rowcountptr*  
 출력 실제로 인출 된 행 수를 반환할 버퍼에 대 한 포인터입니다. 이 버퍼는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에 지정 된 버퍼와 동일한 방식으로 사용 됩니다. 이 버퍼는 **Sqlextendedfetch**에서만 사용 됩니다. **Sqlfetch** 또는 **sqlfetchscroll**에서 사용 되지 않습니다.  
  
 *RowStatusArray*  
 출력 각 행의 상태를 반환할 배열에 대 한 포인터입니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성에 지정 된 배열과 동일한 방식으로 사용 됩니다.  
  
 그러나이 배열의 주소는 IRD의 SQL_DESC_STATUS_ARRAY_PTR 필드에 저장 되지 않습니다. 또한이 배열은 **sqlextendedfetch에서 사용** 되며 **sqlextendedfetch**이후에 호출 될 때 SQL_ADD 또는 **SQLSetPos** *작업* 을 통해 **SQLBulkOperations** 사용 됩니다. **Sqlfetch** 또는 **sqlfetchscroll**에서 사용 되지 않으며 **sqlfetch** 또는 **Sqlfetchscroll**이후에 호출 될 때 **SQLBulkOperations** 또는 **SQLSetPos** 에서 사용 되지 않습니다. Fetch 함수를 호출 하기 전에 SQL_ADD *작업* 으로 **SQLBulkOperations** 를 호출 하는 경우에도 사용 되지 않습니다. 즉, 문 상태 S7 사용 됩니다. 이는 문 상태 S5 또는 S6에서 사용 되지 않습니다. 자세한 내용은 부록 B: ODBC 상태 전환 테이블의 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 을 참조 하세요.  
  
 응용 프로그램은 *Rowstatusarray* 인수에 올바른 포인터를 제공 해야 합니다. 그렇지 않은 **경우 sqlextendedfetch에 의해 커서가** 배치 **된 후** **sqlextendedfetch** 및 **SQLBulkOperations** 에 대 한 호출의 동작이 정의 되지 않습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlextendedfetch** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 **SQLError**를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlextendedfetch** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다. 단일 열에서 오류가 발생 하는 경우 **SQLGetDiagField** 는 SQL_DIAG_COLUMN_NUMBER *DiagIdentifier* 를 호출 하 여 오류가 발생 한 열을 확인할 수 있습니다. **SQLGetDiagField** 를 SQL_DIAG_ROW_NUMBER *DiagIdentifier* 로 호출 하 여 해당 열이 포함 된 행을 확인할 수 있습니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|열에 대해 반환 된 문자열 또는 이진 데이터로 인해 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터가 잘렸습니다. 문자열 값인 경우 오른쪽이 잘렸습니다. 숫자 값 이면 숫자의 소수 부분이 잘렸습니다.  함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 페치하는 동안 오류가 발생 했습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S06|결과 집합에서 첫 번째 행 집합을 반환 하기 전에 인출 하려고 합니다.|현재 위치가 첫 번째 행을 초과 했을 때 *Fetchorientation* 가 SQL_PRIOR 또는 *fetchorientation* 가 현재 SQL_ROWSET_SIZE와 같거나 작은 *fetchorientation* 을 사용 하 여 SQL_RELATIVE 된 경우 요청 된 행 집합은 결과 집합의 시작 부분을 중첩 합니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함 하는 time, timestamp 및 interval 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|데이터 값을 **SQLBindCol**의 *TargetType* 에 지정 된 C 데이터 형식으로 변환할 수 없습니다.|  
|07009|잘못 된 설명자 인덱스|열 0은 **SQLBindCol**와 바인딩되고 SQL_ATTR_USE_BOOKMARKS statement 특성은 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22002|표시기 변수가 필요한 데 제공 되지 않았습니다.|**SQLBindCol** 로 설정 된 *StrLen_or_IndPtr* NULL 포인터인 열에 null 데이터가 인출 되었습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|하나 이상의 열에 대 한 숫자 값 (숫자 또는 문자열)을 반환 하면 잘릴 수 있는 전체 (소수 자릿수가 아닌) 부분이 발생 합니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> 자세한 내용은 부록 D: 데이터 형식의 [간격 및 숫자 데이터 형식에 대 한 지침](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 을 참조 하세요.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|결과 집합의 문자 열이 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되고 열의 값은 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|22012|0으로 나누었습니다.|산술 식의 값이 반환 되었으며이로 인해 0으로 나누었습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|22015|간격 필드 오버플로입니다.|정확한 숫자 또는 간격 SQL 형식을 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> Interval C 유형에 서 데이터를 인출 하는 경우 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 가 실행 된 상태 이지만 *StatementHandle*과 연결 된 결과 집합이 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLError** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlextendedfetch** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute**또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> Sqlfetch 또는 **Sqlextendedfetch** 이 호출 된 후 *StatementHandle* 옵션 **SQLFetch** 을 SQL_CLOSE 사용 하 여 **SQLFreeStmt** 가 호출 되기 전에 DM () **sqlextendedfetch** 가 호출 되었습니다.<br /><br /> (DM) **SQLBulkOperations** 는 **sqlfetch**, **Sqlfetchscroll**또는 **sqlextendedfetch** 가 호출 되기 전에 문에 대해 호출 된 후 **Sqlextendedfetch** 는 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY106|인출 형식이 범위를 벗어났습니다.|(DM) 인수 *Fetchorientation* 에 지정 된 값이 잘못 되었습니다. "설명"을 참조 하십시오.<br /><br /> *Fetchorientation* 인수가 SQL_FETCH_BOOKMARK 되었고 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF로 설정 되었습니다.<br /><br /> SQL_CURSOR_TYPE 문 옵션의 값이 SQL_CURSOR_FORWARD_ONLY 되었으며 인수 *Fetchorientation* 의 값이 SQL_FETCH_NEXT 되지 않았습니다.<br /><br /> *Fetchorientation* 인수가 SQL_FETCH_RESUME 되었습니다.|  
|HY107|행 값이 범위를 벗어났습니다.|SQL_CURSOR_TYPE statement 옵션과 함께 지정 된 값이 SQL_CURSOR_KEYSET_DRIVEN 되었지만 SQL_KEYSET_SIZE statement 특성으로 지정 된 값이 0 보다 크고 SQL_ROWSET_SIZE statement 특성에 지정 된 값 보다 작아야 합니다.|  
|HY111|책갈피 값이 잘못 되었습니다.|*Fetchorientation* 인수를 SQL_FETCH_BOOKMARK *fetchorientation* 인수에 지정 된 책갈피가 잘못 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본이 지정 된 인출 유형을 지원 하지 않습니다.<br /><br /> 드라이버 또는 데이터 원본은 **SQLBindCol** 의 *TargetType* 조합과 해당 열의 SQL 데이터 형식으로 지정 된 변환을 지원 하지 않습니다. 이 오류는 열의 SQL 데이터 형식이 드라이버별 SQL 데이터 형식에 매핑된 경우에만 적용 됩니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtOption**, SQL_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **Sqlextendedfetch** 의 동작은 **sqlextendedfetch**의 동작과 동일 하지만 다음과 같은 예외가 있습니다.  
  
-   **Sqlextendedfetch** 및 **sqlextendedfetch** 은 다른 메서드를 사용 하 여 인출 된 행 수를 반환 합니다. **Sqlextendedfetch** 는 * \* rowcountptr*에서 인출 된 행 수를 반환 합니다. **Sqlfetchscroll** 은 SQL_ATTR_ROWS_FETCHED_PTR에서 가리키는 버퍼로 직접 인출 된 행 수를 반환 합니다. 자세한 내용은 *Rowcountptr* 인수를 참조 하세요.  
  
-   **Sqlextendedfetch** 및 **sqlextendedfetch** 은 각 행의 상태를 서로 다른 배열로 반환 합니다. 자세한 내용은 *Rowstatusarray* 인수를 참조 하세요.  
  
-   **Sqlextendedfetch** 및 **sqlextendedfetch** 은 *fetchorientation* 가 SQL_FETCH_BOOKMARK 때 다른 방법을 사용 하 여 책갈피를 검색 합니다. **Sqlextendedfetch** 는 가변 길이 책갈피를 지원 하지 않거나 책갈피에서 0이 아닌 오프셋에 있는 행 집합을 인출 합니다. 자세한 내용은 *Fetchoffset* 인수를 참조 하세요.  
  
-   **Sqlextendedfetch** 및 **sqlextendedfetch** 은 다른 행 집합 크기를 사용 합니다. **Sqlextendedfetch** 는 SQL_ROWSET_SIZE statement 특성의 값을 사용 하 고 **sqlextendedfetch** 은 SQL_ATTR_ROW_ARRAY_SIZE statement 특성의 값을 사용 합니다.  
  
-   **Sqlextendedfetch** 의 오류 처리 의미 체계가 **sqlextendedfetch**과 약간 다릅니다. 자세한 내용은 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)의 "Comments" 섹션에서 "오류 처리"를 참조 하십시오.  
  
-   **Sqlextendedfetch** 는 바인딩 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성)을 지원 하지 않습니다.  
  
-   **Sqlextendedfetch** 에 대 한 호출은 **Sqlfetch** 또는 **sqlextendedfetch**에 대 한 호출과 혼합할 수 없습니다. fetch 함수가 호출 되기 전에 **SQLBulkOperations** 가 호출 되 면 커서가 닫혔다가 다시 열릴 때까지 **sqlextendedfetch** 를 호출할 수 없습니다. 즉, **Sqlextendedfetch** 는 문 상태 S7 호출 될 수 있습니다. 자세한 내용은 부록 B: ODBC 상태 전환 테이블의 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md) 을 참조 하세요.  
  
 ODBC*2.x 드라이버를* 사용 하는 동안 응용 프로그램이 **sqlfetchscroll** 을 호출 하면 드라이버 관리자는이 호출을 **sqlfetchscroll**에 매핑합니다. 자세한 내용은 [sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)의 "sqlfetchscroll 및 ODBC*2.x 드라이버"* 를 참조 하십시오.  
  
 ODBC 2.x에서 여러 행을 페치 하기 위해 **sqlextendedfetch** *를 호출*하 고 단일 행을 인출 하기 위해 **sqlfetch** 를 호출 했습니다. 반면 ODBC 3.x*에서는* **sqlfetch** 를 호출 하 여 여러 행을 페치할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서 위치를 지정 하거나, 행 집합의 데이터를 새로 고치거 나, 결과 집합에서 데이터를 업데이트 하거나 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
