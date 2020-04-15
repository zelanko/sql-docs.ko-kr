---
title: SQLExtended페치페치 함수 | 마이크로 소프트 문서
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
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285983"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 함수
**규칙**  
 버전 도입: ODBC 1.0 표준 규정 준수: 더 이상 사용되지 않는  
  
 **요약**  
 **SQLExtendedFetch결과** 집합에서 지정된 데이터 행 집합을 가져오고 바인딩된 모든 열에 대 한 데이터를 반환 합니다. 행 집합은 절대 또는 상대 위치 또는 책갈피로 지정할 수 있습니다.  
  
> [!NOTE]
>  ODBC 3 *.x에서* **SQLExtendedFetch는** **SQLFetch스크롤로**대체되었습니다. ODBC 3 *.x* 응용 프로그램은 **SQLExtendedFetch를**호출해서는 안됩니다. 대신 **SQLFetchScroll**을 호출해야 합니다. 드라이버 관리자는 ODBC 2 *.x* 드라이버로 작업할 때 **SQLFetchScroll을** **SQLExtendedFetch에** 매핑합니다. ODBC 3 *.x* 드라이버는 **SQLExtendedFetch를** 지원해야 합니다.*.x* 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 "주석" 및 [차단 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 참조하십시오.  
  
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
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *페치 방향*  
 [입력] 가져오기 유형입니다. 이는 **SQLFetchScroll**의 *FetchOrientation* 와 동일합니다.  
  
 *가져오기오프셋*  
 [입력] 가져올 행 의 수입니다. 이는 한 가지 예외를 제외하고 **SQLFetchScroll에서** *FetchOffset과* 동일합니다. *FetchOrientation가* SQL_FETCH_BOOKMARK *경우 FetchOffset은* 책갈피에서 오프셋이 아닌 고정 길이 책갈피입니다. 즉, **SQLExtendedFetch는** SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성이 아니라 이 인수에서 책갈피를 검색합니다. 길이가 가변책마크는 지원하지 않으며 책갈피에서 오프셋(0이 아닌)에서 행 집합 가져오기를 지원하지 않습니다.  
  
 *행카운트Ptr*  
 [출력] 실제로 가져온 행 수를 반환할 버퍼에 대한 포인터입니다. 이 버퍼는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 지정한 버퍼와 동일한 방식으로 사용됩니다. 이 버퍼는 **SQLExtendedFetch**에서만 사용됩니다. SQLFetch 또는 **SQLFetchScroll** 에서 사용되지 않습니다. **SQLFetchScroll**  
  
 *행 상태 배열*  
 [출력] 각 행의 상태를 반환할 배열에 대한 포인터입니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정된 배열과 동일한 방식으로 사용됩니다.  
  
 그러나 이 배열의 주소는 IRD의 SQL_DESC_STATUS_ARRAY_PTR 필드에 저장되지 않습니다. 또한 이 배열은 **SQLExtendedFetch** 및 **SQLBulkOperations에서만** 사용되며 **SQLExtendedFetch**다음으로 호출될 때 SQL_ADD 또는 **SQLSetPos** *작업이* 사용됩니다. **SQLFetch** 또는 **SQLFetchScroll에서**사용되지 않으며 **SQLFetch** 또는 **SQLFetchScroll**다음으로 호출될 때 **SQLBulkOperations** 또는 **SQLSetPos에서** 사용되지 않습니다. 또한 가져오기 함수가 호출되기 전에 SQL_ADD *작업이* 있는 **SQLBulkOperations가** 호출될 때도 사용되지 않습니다. 즉, 명령문 상태 S7에서만 사용됩니다. S5 또는 S6 상태에서는 사용되지 않습니다. 자세한 내용은 부록 B: ODBC 상태 전환 표의 [문 전환을](../../../odbc/reference/appendixes/statement-transitions.md) 참조하십시오.  
  
 응용 프로그램은 *RowStatusArray* 인수에서 유효한 포인터를 제공해야 합니다. 그렇지 않은 경우 **SQLExtendedFetch의** 동작과 **SQLExtendedFetch에** 의해 커서가 배치된 후 **SQLBulkOperations** 또는 **SQLSetPos에** 대한 호출 동작은 정의되지 않습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLExtendedFetch** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 **SQLError를**호출 하 여 관련 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLExtendedFetch에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR. 단일 열에서 오류가 발생하는 경우 **SQLGetDiagField는** SQL_DIAG_COLUMN_NUMBER *DiagIdentifier를* 사용하여 호출하여 오류가 발생한 열을 확인할 수 있습니다. **및 SQLGetDiagField는** 해당 열이 포함된 행을 결정하기 위해 SQL_DIAG_ROW_NUMBER *DiagIdentifier를* 사용하여 호출할 수 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|열에 대해 반환된 문자열 또는 이진 데이터는 비공백 문자 또는 NULL이 아닌 이진 데이터의 잘림을 초래했습니다. 문자열 값인 경우 오른쪽 잘린 값입니다. 숫자 값인 경우 숫자의 소수 부분이 잘렸습니다.  (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S01|행의 오류|하나 이상의 행을 가져오는 동안 오류가 발생했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S06|결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기를 시도합니다.|요청된 행 집합은 현재 위치가 첫 번째 행을 초과할 때 결과 집합의 시작과 겹쳤으며, *FetchOrientation이* SQL_PRIOR 또는 *FetchOrientation이* SQL_RELATIVE 절대값이 현재 SQL_ROWSET_SIZE 같거나 같을 수 있는 음수 *FetchOffset으로* SQL_RELATIVE. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S07|분수 잘림|열에 대해 반환된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|데이터 값을 **SQLBindCol**에서 *TargetType에* 의해 지정된 C 데이터 유형으로 변환할 수 없습니다.|  
|07009|잘못된 설명자 인덱스|열 0은 **SQLBindCol과**바인딩되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성은 SQL_UB_OFF 설정되었습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22002|표시기 변수가 필요하지만 제공되지 않음|NULL 데이터는 **SQLBindCol에서** 설정한 *StrLen_or_IndPtr* null 포인터인 열로 가져왔습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22003|범위를 벗어난 숫자 값|하나 이상의 열에 대해 숫자 값(숫자 또는 문자열)을 반환하면 숫자의 전체(소수와 반대)가 잘릴 수 있습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> 자세한 내용은 부록 D: 데이터 [형식의 간격 및 숫자 데이터 형식에 대한 지침을](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 참조하십시오.|  
|22007|잘못된 날짜 시간 형식|결과 집합의 문자 열은 날짜, 시간 또는 타임스탬프 C 구조에 바인딩되었으며 열의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22012|0으로 나누기|산술 식의 값이 반환되어 0으로 분할됩니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 SQL 형식에서 간격 C 유형으로 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> 간격 C 유형으로 데이터를 가져올 때 간격 C 형식에서 SQL 형식의 값에 대한 표현이 없었습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22018|캐스트 사양에 대해 잘못된 문자 값|C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|24000|잘못된 커서 상태|*StatementHandle* 실행 된 상태에 있었지만 결과 *집합은 StatementHandle*.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLError에서** 반환된 오류 메시지는 오류와 그 원인을 설명합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle에서*호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLExtendedFetch** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect**, **SQLExecute**또는 카탈로그 함수를 호출하지 않고 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) **SQLExtendedFetch는** **SQLFetch** 또는 **SQLFetchScroll가** 호출되고 **SQLFreeStmt가** SQL_CLOSE 옵션으로 호출되기 전에 *문 핸들에* 대해 호출되었습니다.<br /><br /> (DM) **SQLBulkOperations는** **SQLFetch**, **SQLFetchScroll**또는 **SQLExtendedFetch가** 호출되기 전에 문을 호출한 다음 **SQLFreeStmt가** SQL_CLOSE 옵션으로 호출되기 전에 **SQLExtendedFetch가** 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY106|범위를 벗어난 형식 가져오기|(DM) *인수 FetchOrientation에* 대해 지정된 값이 잘못되었습니다. ("댓글"참조))<br /><br /> 인수 *FetchOrientation* SQL_FETCH_BOOKMARK, SQL_ATTR_USE_BOOKMARKS 문 특성SQL_UB_OFF 설정 되었습니다.<br /><br /> SQL_CURSOR_TYPE 문 옵션의 값은 SQL_CURSOR_FORWARD_ONLY 인수 *FetchOrientation의* 값이 SQL_FETCH_NEXT 않았습니다.<br /><br /> 인수 *FetchOrientation* SQL_FETCH_RESUME.|  
|HY107|범위를 벗어난 행 값|SQL_CURSOR_TYPE 문 옵션으로 지정된 값은 SQL_CURSOR_KEYSET_DRIVEN SQL_KEYSET_SIZE 문 특성으로 지정된 값이 0보다 크고 SQL_ROWSET_SIZE 문 특성에 지정된 값보다 작습니다.|  
|HY11|책갈피 값이 잘못되었습니다.|인수 *FetchOrientation* SQL_FETCH_BOOKMARK 및 *FetchOffset* 인수에 지정 된 책갈피 유효 하지 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 지정된 가져오기 유형을 지원하지 않습니다.<br /><br /> 드라이버 또는 데이터 원본은 **SQLBindCol의** *TargetType과* 해당 열의 SQL 데이터 형식의 조합으로 지정된 변환을 지원하지 않습니다. 이 오류는 열의 SQL 데이터 형식이 드라이버 별 SQL 데이터 형식에 매핑된 경우에만 적용됩니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 시간 설정 기간은 **SQLSetStmtOption**, SQL_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLExtendedFetch의** 동작은 다음과 같은 예외를 제외하고 **SQLFetchScroll의**동작과 동일합니다.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll는** 다른 메서드를 사용하여 가져온 행 수를 반환합니다. **SQLExtendedFetch는** * \*RowCountPtr에서*가져온 행 수를 반환합니다. **SQLFetchScroll는** SQL_ATTR_ROWS_FETCHED_PTR 가리키는 버퍼에 직접 가져온 행 수를 반환합니다. 자세한 내용은 *RowCountPtr* 인수를 참조하십시오.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll는** 서로 다른 배열에서 각 행의 상태를 반환합니다. 자세한 내용은 *RowStatusArray* 인수를 참조하십시오.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll** 는 다른 메서드를 사용하여 *FetchOrientation이* SQL_FETCH_BOOKMARK 때 책갈피를 검색합니다. **SQLExtendedFetch는** 책갈피에서 0이 아닌 오프셋에서 가변 길이 책갈피 또는 페지 행 집합을 지원하지 않습니다. 자세한 내용은 *FetchOffset* 인수를 참조하십시오.  
  
-   **SQLExtendedFetch** 및 **SQLFetchScroll는** 서로 다른 행 집합 크기를 사용합니다. **SQLExtendedFetch는** SQL_ROWSET_SIZE 문 특성의 값을 사용하고 **SQLFetchScroll는** SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값을 사용합니다.  
  
-   **SQLExtendedFetch** **SQLFetch**. 자세한 내용은 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)의 "주석" 섹션에서 "오류 처리" 를 참조하십시오.  
  
-   **SQLExtendedFetch** 바인딩 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성)을 지원 하지 않습니다.  
  
-   **SQLExtendedFetch에** 대한 호출은 **SQLFetch** 또는 **SQLFetchScroll에**대한 호출과 혼합할 수 없으며, 가져오기 함수를 호출하기 전에 **SQLBulkOperations가** 호출되는 경우 커서가 닫혀 다시 열릴 때까지 **SQLExtendedFetch를** 호출할 수 없습니다. 즉, **SQLExtendedFetch는** 명령문 상태 S7에서만 호출할 수 있습니다. 자세한 내용은 부록 B: ODBC 상태 전환 표의 [문 전환을](../../../odbc/reference/appendixes/statement-transitions.md) 참조하십시오.  
  
 응용 프로그램이 ODBC 2 *.x* 드라이버를 사용하는 동안 **SQLFetchScroll을** 호출하면 드라이버 관리자는 이 호출을 **SQLExtendedFetch**에 매핑합니다. 자세한 내용은 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)및 ODBC 2 *.x* 드라이버"를 참조하십시오.  
  
 ODBC 2 *.x에서* **SQLExtendedFetch는** 여러 행을 가져오기 위해 호출되었으며 **SQLFetch는** 단일 행을 가져오기 위해 호출되었습니다. 반면 ODBC 3 *.x에서는* **SQLFetch를** 호출하여 여러 행을 가져올 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 결과 집합의 데이터 업데이트 또는 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
