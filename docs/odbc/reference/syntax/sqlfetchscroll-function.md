---
title: SQLFetchScroll 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb75ebceb1f70ddc8b517a3dc94af97a18965939
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345185"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 함수(SQLFetchScroll Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlfetchscroll** 은 결과 집합에서 지정 된 데이터 행 집합을 인출 하 고 모든 바인딩된 열에 대해 데이터를 반환 합니다. 행 집합은 절대 또는 상대 위치 또는 책갈피로 지정할 수 있습니다.  
  
 ODBC 2.x 드라이버를 사용 하는 경우 드라이버 관리자는이 함수를 **Sqlextendedfetch**에 매핑합니다. 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *FetchOrientation*  
 입력  
  
 Fetch의 유형입니다.  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 자세한 내용은 "주석" 섹션의 "커서 위치 지정"을 참조 하세요.  
  
 *FetchOffset*  
 입력  
  
 인출할 행의 번호입니다. 이 인수의 해석은 *Fetchorientation* 인수의 값에 따라 달라 집니다. 자세한 내용은 "주석" 섹션의 "커서 위치 지정"을 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlfetchscroll** 이 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 HandleType SQL_HANDLE_STMT 및 StatementHandle 핸들을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqlfetchscroll** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다. 단일 열에서 오류가 발생 하는 경우 DiagIdentifier의 SQL_DIAG_COLUMN_NUMBER를 사용 하 여 **SQLGetDiagField** 를 호출 하 여 오류가 발생 한 열을 확인할 수 있습니다. and **SQLGetDiagField** 는 DIAGIDENTIFIER of SQL_DIAG_ROW_NUMBER를 호출 하 여 해당 열이 포함 된 행을 확인할 수 있습니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (01xxx SQLSTATEs 제외)를 반환할 수 있는 모든 SQLSTATEs의 경우에는 한 개 이상의 행 작업에 오류가 발생 하는 경우 SQL_SUCCESS_WITH_INFO가 반환 되 고, 다음에 오류가 발생 하면 SQL_ERROR가 반환 됩니다. 단일 행 작업  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|열에 대해 반환 된 문자열 또는 이진 데이터로 인해 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터가 잘렸습니다. 문자열 값인 경우 오른쪽이 잘렸습니다.|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 페치하는 동안 오류가 발생 했습니다.<br /><br /> ODBC*3.x 응용 프로그램* 에서 odbc*2.x 드라이버를* 사용할 때이 SQLSTATE가 반환 되는 경우 무시 해도 됩니다.|  
|01S06|결과 집합에서 첫 번째 행 집합을 반환 하기 전에 인출 하려고 합니다.|FetchOrientation가 SQL_FETCH_PRIOR 때 현재 위치가 첫 번째 행을 벗어나 요청 된 행 집합이 결과 집합의 시작 부분을 겹쳐져 현재 행 수가 행 집합 크기 보다 작거나 같습니다.<br /><br /> FetchOrientation가 SQL_FETCH_PRIOR 때 현재 위치가 결과 집합의 끝을 넘어 행 집합 크기가 결과 집합 크기 보다 큰 경우 요청 된 행 집합은 결과 집합의 시작 부분을 중첩 합니다.<br /><br /> FetchOrientation가 SQL_FETCH_RELATIVE이 고, Fetchorientation이 음수이 고, Fetchorientation의 절대값이 행 집합 크기 보다 작거나 같은 경우 요청 된 행 집합은 결과 집합의 시작 부분을 중첩 합니다.<br /><br /> FetchOrientation가 SQL_FETCH_ABSOLUTE이 고 Fetchorientation이 음수이 고 Fetchorientation의 절대값이 결과 집합 크기 보다 크지만 행 집합 크기 보다 작거나 같은 경우 요청 된 행 집합은 결과 집합의 시작 부분을 중첩 합니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함 하는 time, timestamp 및 interval 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 **SQLBindCol**의 *TargetType* 에 지정 된 데이터 형식으로 변환할 수 없습니다.<br /><br /> 열 0은 SQL_C_BOOKMARK의 데이터 형식으로 바인딩되며 SQL_ATTR_USE_BOOKMARKS statement 특성은 SQL_UB_VARIABLE로 설정 되었습니다.<br /><br /> 열 0이 SQL_C_VARBOOKMARK 데이터 형식으로 바인딩 되었으며 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스|드라이버가 **Sqlextendedfetch**를 지원 하지 않고 열에 대해 바인딩에 지정 된 열 번호가 0 인 ODBC*2.x 드라이버 였습니다* .<br /><br /> 열 0이 바인딩되고 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|열에 대해 반환 된 가변 길이 책갈피가 잘렸습니다.|  
|22002|표시기 변수가 필요한 데 제공 되지 않았습니다.|**SQLBindCol** 에 의해 설정 된 *StrLen_or_IndPtr* 또는 **SQLSetDescField** 또는 **SQLSetDescRec**에 의해 설정 된 SQL_DESC_INDICATOR_PTR가 null 포인터인 열로 null 데이터가 인출 되었습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|하나 이상의 바인딩된 열에 대해 숫자 값 (숫자 또는 문자열)을 반환 하면 잘릴 수 있는 전체 (소수 자릿수가 아닌) 부분이 발생 합니다.<br /><br /> 자세한 내용은 부록 D [의 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 을 참조 하세요. 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|날짜/시간 형식이 잘못 되었습니다.|결과 집합의 문자 열이 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되고 열의 값은 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다.|  
|22012|0으로 나누었습니다.|산술 식의 값이 반환 되었으며이로 인해 0으로 나누었습니다.|  
|22015|간격 필드 오버플로입니다.|정확한 숫자 또는 간격 SQL 형식을 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> Interval C 유형에 서 데이터를 인출 하는 경우 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|결과 집합의 문자 열이 문자 C 버퍼에 바인딩되고 버퍼의 문자 집합에 표시 되지 않은 문자가 열에 포함 되어 있습니다.<br /><br /> C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 가 실행 된 상태 이지만 결과 집합이 *StatementHandle*와 연결 되지 않았습니다.|  
|40001|Serialization 오류|반입이 실행 된 트랜잭션이 교착 상태를 방지 하기 위해 종료 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소 됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlfetchscroll** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE이 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute** 또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA이 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlextendedfetch** 를 호출한 후 SQL_CLOSE 옵션을 사용 하는 **SQLFreeStmt** 가 호출 되기 전에 *StatementHandle* 에 대해 **sqlfetch** 가 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|SQL_ATTR_USE_BOOKMARK statement 특성이 SQL_UB_VARIABLE로 설정 되 고, 열 0이이 결과 집합에 대 한 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩 되었습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol**, **sqlcolattribute**또는 **SQLGetDescField**를 호출 하 여 가져올 수 있습니다.|  
|HY106|인출 형식이 범위를 벗어났습니다.|DM) 인수 FetchOrientation에 지정 된 값이 잘못 되었습니다.<br /><br /> (DM) 인수 FetchOrientation는 SQL_FETCH_BOOKMARK이 고 SQL_ATTR_USE_BOOKMARKS statement 특성은 SQL_UB_OFF로 설정 되었습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE statement 특성의 값이 SQL_CURSOR_FORWARD_ONLY이 고 인수 FetchOrientation의 값이 SQL_FETCH_NEXT 되지 않았습니다.<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE statement 특성의 값이 SQL_NONSCROLLABLE이 고 인수 FetchOrientation의 값이 SQL_FETCH_NEXT 되지 않았습니다.|  
|HY107|행 값이 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE statement 특성에 지정 된 값이 SQL_CURSOR_KEYSET_DRIVEN 이지만 SQL_ATTR_KEYSET_SIZE statement 특성으로 지정 된 값이 0 보다 크고 SQL_ATTR_ROW_ARRAY_에 지정 된 값 보다 작아야 합니다. SIZE 문 특성입니다.|  
|HY111|책갈피 값이 잘못 되었습니다.|FetchOrientation 인수는 SQL_FETCH_BOOKMARK이 고 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성의 값이 가리키는 책갈피는 유효 하지 않거나 null 포인터입니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본은 **SQLBindCol** 의 *TargetType* 조합과 해당 열의 SQL 데이터 형식으로 지정 된 변환을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출에서 SQL_STILL_EXECUTING를 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **Sqlfetchscroll** 은 결과 집합에서 지정 된 행 집합을 반환 합니다. 행 집합은 절대 또는 상대 위치나 책갈피를 기준으로 지정할 수 있습니다. **Sqlfetchscroll** 은 결과 집합이 있는 동안 (즉, 결과 집합을 생성 하는 호출 후, 결과 집합 위에 커서가 닫 혔 음)에만 호출 될 수 있습니다. 바인딩된 열이 있으면 해당 열에 있는 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열 또는 인출 된 행 수를 반환 하는 버퍼에 대 한 포인터를 지정한 경우 **Sqlfetchscroll** 은이 정보를 반환 합니다. **Sqlfetchscroll** 에 대 한 호출은 **sqlfetch** 호출을 혼합할 수 있지만 **sqlfetchscroll**에 대 한 호출과 혼합할 수 없습니다.  
  
 자세한 내용은 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md) 및 [스크롤 가능 커서 사용](../../../odbc/reference/develop-app/using-scrollable-cursors.md)을 참조 하세요.  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합을 만들 때 커서는 결과 집합의 시작 부분 앞에 배치 됩니다. **Sqlfetchscroll** 은 다음 표에 나와 있는 것 처럼 *Fetchorientation* 및 *fetchoffset* 인수 값을 기준으로 블록 커서를 배치 합니다. 새 행 집합의 시작을 확인 하는 정확한 규칙은 다음 섹션에 나와 있습니다.  
  
|FetchOrientation|의미|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|다음 행 집합을 반환 합니다. 이는 **Sqlfetch**를 호출 하는 것과 같습니다.<br /><br /> **Sqlfetchscroll** 은 *fetchoffset*값을 무시 합니다.|  
|SQL_FETCH_PRIOR|이전 행 집합을 반환 합니다.<br /><br /> **Sqlfetchscroll** 은 *fetchoffset*값을 무시 합니다.|  
|SQL_FETCH_RELATIVE|현재 행 집합의 시작 부분에서 행 집합 *Fetchoffset* 을 반환 합니다.|  
|SQL_FETCH_ABSOLUTE|*Fetchoffset*행에서 시작 하는 행 집합을 반환 합니다.|  
|SQL_FETCH_FIRST|결과 집합에서 첫 번째 행 집합을 반환 합니다.<br /><br /> **Sqlfetchscroll** 은 *fetchoffset*값을 무시 합니다.|  
|SQL_FETCH_LAST|결과 집합에서 마지막 전체 행 집합을 반환 합니다.<br /><br /> **Sqlfetchscroll** 은 *fetchoffset*값을 무시 합니다.|  
|SQL_FETCH_BOOKMARK|SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성에 지정 된 책갈피에서 행 집합 FetchOffset 행을 반환 합니다.|  
  
 모든 인출 방향을 지원 하기 위해 드라이버는 필요 하지 않습니다. 응용 프로그램은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 (커서의 형식에 따라 다름)의 정보 형식으로 **SQLGetInfo** 를 호출 하 여 인출 방향을 결정 합니다. 드라이버에서 지원 됩니다. 응용 프로그램은 이러한 정보 형식에서 SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE 및 WQL_CA1_BOOKMARK 비트 마스크를 확인 해야 합니다. 또한 커서가 전진 전용이 고 FetchOrientation가 SQL_FETCH_NEXT 않은 경우 **Sqlfetchscroll** 은 SQLSTATE HY106 (인출 유형 범위를 벗어남)를 반환 합니다.  
  
 SQL_ATTR_ROW_ARRAY_SIZE statement 특성은 행 집합의 행 수를 지정 합니다. **Sqlfetchscroll** 에서 인출 되는 행 집합이 결과 집합의 끝과 겹치면 **sqlfetchscroll** 이 부분 행 집합을 반환 합니다. 즉, S + R-1이를 초과 하는 경우. 여기서 S는 인출 되는 행 집합의 시작 행이 고, R은 행 집합 크기 이며, L은 결과 집합의 마지막 행입니다. 그러면 행 집합의 첫 번째 L-value + 1 행만 유효 합니다. 나머지 행은 비어 있고 상태는 SQL_ROW_NOROW입니다.  
  
 **Sqlfetchscroll** 이 반환 된 후 현재 행은 행 집합의 첫 번째 행입니다.  
  
## <a name="cursor-positioning-rules"></a>커서 위치 지정 규칙  
 다음 섹션에서는 FetchOrientation의 각 값에 대 한 정확한 규칙을 설명 합니다. 이러한 규칙은 다음 표기법을 사용 합니다.  
  
|Notation|의미|  
|--------------|-------------|  
|*시작 하기 전*|블록 커서는 결과 집합의 시작 부분 앞에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 시작 앞에 있으면 **Sqlfetchscroll** 은 SQL_NO_DATA를 반환 합니다.|  
|*종료 후*|블록 커서는 결과 집합의 끝 뒤에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 끝 뒤에 있는 경우 **Sqlfetchscroll** 은 SQL_NO_DATA를 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합에 있는 첫 번째 행의 번호입니다.|  
|*LastResultRow*|결과 집합에서 마지막 행의 번호입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
|*FetchOffset*|*Fetchoffset* 인수의 값입니다.|  
|*BookmarkRow*|SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성에 지정 된 책갈피에 해당 하는 행입니다.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전*|1|  
|*CurrRowsetStart + RowsetSize*[1] *\<= LastResultRow*|*CurrRowsetStart + RowsetSize* 비슷합니다|  
|*CurrRowsetStart + RowsetSize* 비슷합니다 *> LastResultRow*|*종료 후*|  
|*종료 후*|*종료 후*|  
  
 [1] 인출 행에 대 한 이전 호출 이후 행 집합 크기가 변경 된 경우 이전 호출에 사용 된 행 집합 크기입니다.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전*|*시작 하기 전*|  
|*CurrRowsetStart = 1*|*시작 하기 전*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart-RowsetSize* <sup>[2]</sup>|  
|*END 및 LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*END 및 LastResultRow > = RowsetSize* <sup>[2]</sup>|*Lastresultrow-RowsetSize + 1* <sup>[2]</sup>|  
  
 [1] **Sqlfetchscroll** 은 SQLSTATE 01S06 (결과 집합에서 첫 번째 행 집합을 반환 하기 전에 인출 시도) 및 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 [2] 인출 행에 대 한 이전 호출 이후 행 집합 크기가 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*(Start 및 FetchOffset > 0) 또는 (end 및 FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 및 FetchOffset < = 0*|*시작 하기 전*|  
|*CurrRowsetStart = 1 및 FetchOffset < 0*|*시작 하기 전*|  
|*CurrRowsetStart > 1 및 CurrRowsetStart + fetchoffset < 1 및 &#124; Fetchoffset &#124; > RowsetSize* <sup>[3]</sup>|*시작 하기 전*|  
|*CurrRowsetStart > 1 및 CurrRowsetStart + fetchoffset < 1 및 &#124; fetchoffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + fetchoffset \<= lastresultrow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*종료 후*|  
|*End 및 FetchOffset > = 0*|*종료 후*|  
  
 [1] ***Sqlfetchscroll*** 은 SQL_FETCH_ABSOLUTE로 설정 된 fetchorientation로 호출 된 것과 동일한 행 집합을 반환 합니다. 자세한 내용은 "SQL_FETCH_ABSOLUTE" 섹션을 참조 하세요.  
  
 [2] **Sqlfetchscroll** 은 SQLSTATE 01S06 (결과 집합에서 첫 번째 행 집합을 반환 하기 전에 인출 시도) 및 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 [3] 인출 행에 대 한 이전 호출 이후 행 집합 크기가 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*FetchOffset < 0 및 &#124; fetchoffset &#124; < = lastresultrow*|*LastResultRow + FetchOffset + 1*|  
|*Fetchoffset < 0 및 &#124; Fetchoffset &#124; > lastresultrow 및 &#124; fetchoffset &#124; > RowsetSize* <sup>[2]</sup>|*시작 하기 전*|  
|*Fetchoffset < 0 및 &#124; Fetchoffset &#124; > lastresultrow 및 &#124; fetchoffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*시작 하기 전*|  
|*1 <= FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*종료 후*|  
  
 [1] **Sqlfetchscroll** 은 SQLSTATE 01S06 (결과 집합에서 첫 번째 행 집합을 반환 하기 전에 인출 시도) 및 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 [2] 인출 행에 대 한 이전 호출 이후 행 집합 크기가 변경 된 경우 새 행 집합 크기입니다.  
  
 동적 커서에 대해 수행 되는 절대 페치는 동적 커서의 행 위치가 결정 되지 않으므로 필요한 결과를 제공할 수 없습니다. 이러한 작업은 fetch를 먼저 수행한 다음 fetch를 기준으로 하는 것과 같습니다. 정적 커서의 절대 인출 처럼 원자성 연산이 아닙니다.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*일부*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> <= LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 인출 행에 대 한 이전 호출 이후 행 집합 크기가 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*책갈피 행 + FetchOffset < 1*|*시작 하기 전*|  
|*1 < = 책갈피 행 + fetchoffset \<= lastresultrow*|*책갈피 행 + FetchOffset*|  
|*책갈피 행 + FetchOffset > LastResultRow*|*종료 후*|  
  
 책갈피에 대 한 자세한 내용은 [책갈피 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)를 참조 하세요.  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>커서 이동 시 삭제, 추가 및 오류 행의 영향  
 정적 및 키 집합 커서는 때때로 결과 집합에 추가 된 행을 검색 하 고 결과 집합에서 삭제 된 행을 제거 합니다. SQL_STATIC_CURSOR_ATTRIBUTES2 및 SQL_KEYSET_CURSOR_ATTRIBUTES2 옵션을 사용 하 여 **SQLGetInfo** 를 호출 하 고 SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS 및 SQL_CA2_SENSITIVITY_UPDATES 비트 마스크를 살펴보면 응용 프로그램은 특정 드라이버에서 구현 하는 커서를 통해이 작업을 수행 하는지 여부를 결정 합니다. 삭제 된 행을 검색 하 고 제거할 수 있는 드라이버의 경우 다음 단락에서이 동작의 영향을 설명 합니다. 삭제 된 행은 검색할 수 있지만 제거할 수는 없는 드라이버의 경우 커서 이동에 영향을 주지 않으며 다음 단락은 적용 되지 않습니다.  
  
 커서에서 결과 집합에 추가 된 행을 검색 하거나 결과 집합에서 삭제 된 행을 제거 하는 경우 데이터를 인출할 때만 이러한 변경 내용을 검색 하는 것 처럼 나타납니다. 여기에는 FetchOrientation가 SQL_FETCH_RELATIVE로 설정 되 고 FetchOffset이 0으로 설정 되 고 다시 페치가 0으로 설정 된 **Sqlfetchscroll** 이 호출 되 고, FOPTION을 SQL_REFRESH로 설정 하 여 SQLSetPos가 호출 되는 경우는 포함 되지 않습니다. 후자의 경우 행 집합 버퍼의 데이터는 새로 고쳐지지만 반환 되 고, 삭제 된 행은 결과 집합에서 제거 되지 않습니다. 따라서 행을 삭제 하거나 현재 행 집합에 삽입 하면 커서는 행 집합 버퍼를 수정 하지 않습니다. 대신 이전에 삭제 된 행을 포함 한 행 집합을 인출 하거나 삽입 된 행을 포함 하는 행 집합을 가져오는 경우 변경 내용을 검색 합니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 **Sqlfetchscroll** 이 현재 행 집합을 기준으로 위치가 있는 새 행 집합을 반환 하는 경우 (즉, FETCHORIENTATION는 SQL_FETCH_NEXT, SQL_FETCH_PRIOR 또는 SQL_FETCH_RELATIVE-)을 계산할 때 현재 행 집합에 대 한 변경 내용을 포함 하지 않습니다. 새 행 집합의 시작 위치입니다. 그러나이를 검색할 수 있는 경우에는 현재 행 집합 외부의 변경 내용이 포함 됩니다. 또한 **Sqlfetchscroll** 이 현재 행 집합에 독립적으로 위치가 있는 새 행 집합을 반환 하는 경우 FETCHORIENTATION은 SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE 또는 SQL_FETCH_BOOKMARK입니다. 여기에는 모든 변경 내용이 포함 됩니다. 현재 행 집합에 있는 경우에도 검색할 수 있습니다.  
  
 새로 추가 된 행이 현재 행 집합 내부 또는 외부에 있는지 확인 하는 경우 부분 행 집합은 마지막으로 유효한 행에서 끝으로 간주 됩니다. 즉, 행 상태가 SQL_ROW_NOROW이 아닌 마지막 행을 말합니다. 예를 들어 커서가 새로 추가 된 행을 검색할 수 있고, 현재 행 집합이 부분 행 집합 이며, 응용 프로그램에서 새 행을 추가 하 고, 커서는 결과 집합의 끝에 이러한 행을 추가 한다고 가정 합니다. 응용 프로그램이 FetchOrientation가 SQL_FETCH_NEXT로 설정 된 **Sqlfetchscroll** 을 호출 하는 경우 **sqlfetchscroll** 은 새로 추가 된 첫 번째 행부터 행 집합을 반환 합니다.  
  
 예를 들어 현재 행 집합이 21 ~ 30 행으로 구성 되 고 행 집합 크기가 10 이면 커서는 결과 집합에서 삭제 된 행을 제거 하 고 결과 집합에 추가 된 행을 검색 합니다. 다음 표에서는 다양 한 상황에서 **Sqlfetchscroll** 이 반환 하는 행을 보여 줍니다.  
  
|변경|인출 유형|FetchOffset|새 행 집합 [1]|  
|------------|----------------|-----------------|---------------------|  
|행 삭제 21|NEXT|0|31 ~ 40|  
|행 31 삭제|NEXT|0|32 ~ 41|  
|열 21과 22 사이에 행 삽입|NEXT|0|31 ~ 40|  
|30에서 31 사이의 행 삽입|NEXT|0|삽입 된 행, 31-39|  
|행 삭제 21|PRIOR|0|11 ~ 20|  
|행 삭제 20|PRIOR|0|10 ~ 19|  
|열 21과 22 사이에 행 삽입|PRIOR|0|11 ~ 20|  
|행 20과 21 사이에 행 삽입|PRIOR|0|12-20, 삽입 된 행|  
|행 삭제 21|RELATIVE|0|22 ~ 31<sup>[2]</sup>|  
|행 삭제 21|RELATIVE|1|22 ~ 31|  
|열 21과 22 사이에 행 삽입|RELATIVE|0|21, 삽입 된 행, 22-29|  
|열 21과 22 사이에 행 삽입|RELATIVE|1|22 ~ 31|  
|행 삭제 21|ABSOLUTE|21|22 ~ 31<sup>[2]</sup>|  
|22 행 삭제|ABSOLUTE|21|21, 23 ~ 31|  
|열 21과 22 사이에 행 삽입|ABSOLUTE|22|삽입 된 행, 22-29|  
  
 [1]이 열은 행 번호를 사용 하 여 행을 삽입 하거나 삭제 합니다.  
  
 [2]이 경우 커서는 21 행부터 행을 반환 하려고 시도 합니다. 행 21이 삭제 되었으므로 반환 되는 첫 번째 행은 22 번째 행입니다.  
  
 오류 행 (즉, 상태가 SQL_ROW_ERROR 인 행)은 커서 이동에 영향을 주지 않습니다. 예를 들어 현재 행 집합이 행 11로 시작 하 고 행 11의 상태가 SQL_ROW_ERROR 인 경우 FetchOrientation를 SQL_FETCH_RELATIVE로 설정 하 고 FetchOffset을 5로 설정 하 여 **Sqlfetchscroll** 을 호출 하면 행 집합을 반환 합니다. 행 11의 상태가 SQL_SUCCESS입니다.  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에서 데이터 반환  
 **Sqlfetchscroll** 은 **sqlfetch**와 동일한 방식으로 바인딩된 열의 데이터를 반환 합니다. 자세한 내용은 [Sqlfetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)에서 "바인딩된 열의 데이터 반환"을 참조 하세요.  
  
 바인딩된 열이 없는 경우 **Sqlfetchscroll** 은 데이터를 반환 하지 않지만 블록 커서를 지정 된 위치로 이동 합니다. **SQLGetData** 를 사용 하는 블록 커서의 바인딩되지 않은 열에서 데이터를 검색할 수 있는지 여부는 드라이버에 따라 달라 집니다. 이 기능은 **SQLGetInfo** 에 대 한 호출이 SQL_GETDATA_EXTENSIONS 정보 형식에 대 한 SQL_GD_BLOCK 비트를 반환 하는 경우에 지원 됩니다.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 **Sqlfetchscroll** 은 동일한 수식을 사용 하 여 데이터 주소 및 길이/표시기 버퍼를 **sqlfetch**로 결정 합니다. 자세한 내용은 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)에서 "Buffer Addresses"를 참조 하십시오.  
  
## <a name="row-status-array"></a>행 상태 배열  
 **Sqlfetchscroll** 은 sqlfetch와 동일한 방식으로 행 상태 배열의 값을 설정 합니다. 자세한 내용은 [Sqlfetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"행 상태 배열"을 참조 하세요.  
  
## <a name="rows-fetched-buffer"></a>인출 되는 행 버퍼  
 **Sqlfetchscroll** 은 **sqlfetch**와 동일한 방식으로 인출 된 행에서 인출 된 행 수를 반환 합니다. 자세한 내용은 [Sqlfetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"인출 되는 행"을 참조 하세요.  
  
## <a name="error-handling"></a>오류 처리  
 응용 프로그램이 ODBC 3.x 드라이버에서 **sqlfetchscroll** 을 호출 하면 드라이버 관리자는 드라이버에서 **sqlfetchscroll** 을 호출 합니다. 응용 프로그램이 ODBC 2.x 드라이버에서 **Sqlfetchscroll** 을 호출 하면 드라이버 관리자는 드라이버에서 Sqlfetchscroll를 호출 합니다. **Sqlfetchscroll** 및 Sqlfetchscroll는 약간 다른 방식으로 오류를 처리 하므로 odbc 2.X 및 odbc 2.x 드라이버에서 **sqlfetchscroll** 을 호출 하면 응용 프로그램에서 약간 다른 오류 동작을 볼 수 있습니다.  
  
 **Sqlfetchscroll** 은 **sqlfetch**와 동일한 방식으로 오류 및 경고를 반환 합니다. 자세한 내용은 **Sqlfetch**의 "오류 처리"를 참조 하십시오. **Sqlextendedfetch** 는 다음과 같은 경우를 제외 하 고 **sqlfetch**와 동일한 방식으로 오류를 반환 합니다.  
  
 행 집합의 특정 행에 적용 되는 경고가 발생 하면 SQLExtendedFetch는 행 상태 배열의 해당 항목을 SQL_ROW_SUCCESS_WITH_INFO가 아닌 SQL_ROW_SUCCESS로 설정 합니다.  
  
 행 집합의 모든 행에서 오류가 발생 하는 경우 SQLExtendedFetch는 SQL_ERROR가 아닌 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 개별 행에 적용 되는 각 상태 레코드 그룹에서 SQLExtendedFetch에 의해 반환 되는 첫 번째 상태 레코드는 SQLSTATE 01S01 (행에 오류)를 포함 해야 합니다. **Sqlfetchscroll** 은이 SQLSTATE를 반환 하지 않습니다. SQLExtendedFetch가 추가 SQLSTATEs를 반환할 수 없는 경우에도이 SQLSTATE를 반환 해야 합니다.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 및 낙관적 동시성  
 커서에서 낙관적 동시성을 사용 하는 경우 (즉, SQL_ATTR_CONCURRENCY statement 특성의 값은 SQL_CONCUR_VALUES 또는 SQL_CONCUR_ROWVER- **Sqlfetchscroll** 은 데이터 원본에서 사용 하는 낙관적 동시성 값을 업데이트 하 여 행이 변경 되었습니다. 이는 **Sqlfetchscroll** 이 현재 행 집합을 refetches 때를 포함 하 여 새 행 집합을 인출할 때마다 발생 합니다. (FetchOrientation이 SQL_FETCH_RELATIVE로 설정 되 고 Fetchorientation이 0으로 설정 되어 호출 됩니다.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 및 ODBC 2.x 드라이버  
 응용 프로그램이 ODBC 2.x 드라이버에서 **Sqlfetchscroll** 을 호출 하면 드라이버 관리자는이 호출을 **sqlfetchscroll**에 매핑합니다. **Sqlextendedfetch**의 인수에 대해 다음 값을 전달 합니다.  
  
|SQLExtendedFetch 인수|값|  
|-------------------------------|-----------|  
|StatementHandle|**Sqlfetchscroll**의 StatementHandle입니다.|  
|FetchOrientation|**Sqlfetchscroll**의 fetchorientation입니다.|  
|FetchOffset|FetchOrientation가 SQL_FETCH_BOOKMARK가 아닌 경우 **Sqlfetchscroll** 의 fetchorientation 인수 값이 사용 됩니다.<br /><br /> FetchOrientation가 SQL_FETCH_BOOKMARK 인 경우 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성에 지정 된 주소에 저장 된 값이 사용 됩니다.|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR statement 특성에 지정 된 주소입니다.|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR statement 특성에 지정 된 주소입니다.|  
  
 자세한 내용은 [블록 커서, 스크롤 가능 커서 및](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 부록 G의 이전 버전과의 호환성을 참조 하세요. 이전 버전과의 호환성을 위한 드라이버 지침  
  
## <a name="descriptors-and-sqlfetchscroll"></a>설명자 및 SQLFetchScroll  
 **Sqlfetchscroll** 은 **sqlfetch**와 동일한 방식으로 설명자와 상호 작용 합니다. 자세한 내용은 [Sqlfetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)에서 "설명자 및 SQLFetchScroll" 섹션을 참조 하세요.  
  
## <a name="code-example"></a>코드 예  
 [열 단위](../../../odbc/reference/develop-app/column-wise-binding.md)바인딩, [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md), [위치 지정 Update 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), SQLSetPos를 [사용 하 여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|문에서 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서 위치를 지정 하거나, 행 집합의 데이터를 새로 고치거 나, 결과 집합에서 데이터를 업데이트 하거나 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
