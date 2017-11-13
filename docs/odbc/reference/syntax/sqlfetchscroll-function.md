---
title: "SQLFetchScroll 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79224469fe1e6e4f0840eceb394b30cec63fcd2a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 함수(SQLFetchScroll Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLFetchScroll** 결과 집합에서 데이터의 지정 된 행 집합을 인출 하 고 모든 바운드 열에 대 한 데이터를 반환 합니다. 책갈피 또는 절대 또는 상대 위치에서 행 집합을 지정할 수 있습니다.  
  
 드라이버 관리자는이 함수를 매핑합니다 ODBC 2.x 드라이버를 사용할 때는 **SQLExtendedFetch**합니다. 자세한 내용은 참조 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *FetchOrientation*  
 [입력]  
  
 인출 유형:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 자세한 내용은 "설명" 섹션의 "커서 위치 지정"을 참조 하세요.  
  
 *FetchOffset*  
 [입력]  
  
 인출할 행 수입니다. 값에 따라이 인수에 대 한 해석은 *FetchOrientation* 인수입니다. 자세한 내용은 "설명" 섹션의 "커서 위치 지정"을 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFetchScroll** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 여 HandleType 및 핸들을 사용 하 여 StatementHandle 합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLFetchScroll** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다. 하나의 열에 오류가 발생 한 경우 **SQLGetDiagField** ;에서 오류가 발생 하는 열을 확인 하려면 SQL_DIAG_COLUMN_NUMBER DiagIdentifier 호출할 수 및 **SQLGetDiagField** 호출할 수 있습니다 행을 확인 하려면 SQL_DIAG_ROW_NUMBER DiagIdentifier와 해당 열이 포함 된 합니다.  
  
 다중 행 작업의 하나 또는 더 전부가 아닌 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 되는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|문자열 또는 열에 대해 반환 된 이진 데이터의 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 했습니다. 문자열 값 경우 오른쪽 잘림 없었습니다.|  
|01S01|행 하는 동안 오류가 발생 했습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다.<br /><br /> (이 SQLSTATE 때 ODBC 3에 반환 되 면*.x* 응용 프로그램이 ODBC 2와 작동*.x* 드라이버를 무시할 수 있습니다.)|  
|01S06|결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 합니다.|요청 된 행 집합 겹쳐진 FetchOrientation SQL_FETCH_PRIOR, 현재 위치는 첫 번째 행을 초과 했습니다 였으며 현재 행의 수는 행 집합 크기 보다 작거나 때 결과 집합의 시작 합니다.<br /><br /> 요청 된 행 집합 겹쳐진 FetchOrientation SQL_FETCH_PRIOR, 현재 위치를 결과 집합의 끝을 넘어 이며 행 집합 크기는 결과 집합 크기 보다 큰 경우 결과 집합의 시작 합니다.<br /><br /> 요청 된 행 집합 겹쳐진 FetchOrientation SQL_FETCH_RELATIVE, FetchOffset 졌습니다 이며 FetchOffset의 절대 값 보다 작거나 행 집합 크기와 같은 경우 결과 집합의 시작 합니다.<br /><br /> 요청 된 행 집합 겹쳐진 FetchOrientation SQL_FETCH_ABSOLUTE, FetchOffset 졌습니다 이며 FetchOffset의 절대 값의 결과 집합 크기 보다 큰 경우 결과 집합의 시작 되지만 행 집합 크기입니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|일부가 잘렸습니다.|열에 대해 반환 되는 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 interval 데이터 형식을 시간 구성 요소가 포함 된 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.<br /><br /> 0 열 SQL_C_BOOKMARK의 데이터 형식과 바인딩되며 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 되었습니다.<br /><br /> SQL_C_VARBOOKMARK의 데이터 형식으로 열 0 바인딩 되었습니다 및 SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARKS 문 특성 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|드라이버는 ODBC 2는*.x* 지원 하지 않는 드라이버 **SQLExtendedFetch**, 열에 대 한 바인딩에 지정 된 열 번호는 및입니다.<br /><br /> 열 0, 바인딩되며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터 오른쪽 잘림|열에 대해 반환 되는 다양 한 길이의 책갈피가 잘렸습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지 않았습니다.|NULL 데이터를 가져온 열으로 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** (또는 설정한 SQL_DESC_INDICATOR_PTR **SQLSetDescField** 또는  **SQLSetDescRec**)이 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|하나 이상의 바인딩된 열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환는 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.<br /><br /> 자세한 내용은 참조 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 에 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22007|잘못 된 날짜/시간 형식|날짜, 시간 또는 타임 스탬프 C 구조에는 문자는 결과 집합 열에에서 바인딩된 되었으며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프.|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 나누기에서 복원 하려고 시도 했습니다 0입니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형으로 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> C 간격 유형으로 데이터를 인출할 때 C 간격 유형에서 SQL 형식의 값으로 표시 되지 했습니다.|  
|22018|캐스트 사양의 문자 값|결과 집합의 문자 열 C 문자 버퍼에 바인딩되며 열 버퍼의 문자 집합에 없는 표현 된 문자를 포함 되었습니다.<br /><br /> 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 C 유형은 열의 SQL 형식을 문자 데이터 형식. 및 열에 값이 바인딩된 C 형식의 올바른 리터럴.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.|  
|40001|Serialization 오류|교착 상태를 방지 하는 페치 실행 된 트랜잭션이 종료 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLFetchScroll** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 호출 하지 않고 호출 된 **SQLExecDirect**, **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **SQLFetch** 에 대해 호출 되었습니다는 *StatementHandle* 후 **SQLExtendedFetch** 호출 하기 전에 **SQLFreeStmt** 는 SQL_와 CLOSE 옵션이 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE로 설정 된 및 0 열이 결과 집합에 대 한 책갈피에 대 한 최대 길이 길이가 없습니다. 버퍼에 바인딩 되었습니다. (이 길이 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수를 호출 하 여 얻을 수 있습니다 **SQLDescribeCol**, **SQLColAttribute**, 또는 **SQLGetDescField**.)|  
|HY106|인출 유형 범위를 벗어났습니다.|DM) FetchOrientation 인수에 대해 지정 된 값 올바르지 않습니다.<br /><br /> (DM) 인수 FetchOrientation가 SQL_FETCH_BOOKMARK, 고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 문 특성의 값은 SQL_CURSOR_FORWARD_ONLY, FetchOrientation SQL_FETCH_NEXT 없습니다. 인수 값.<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 문 특성의 값은 SQL_NONSCROLLABLE, FetchOrientation SQL_FETCH_NEXT 없습니다. 인수 값.|  
|HY107|행 값 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE 문 특성으로 지정 된 값 SQL_CURSOR_KEYSET_DRIVEN만 SQL_ATTR_KEYSET_SIZE 문 특성으로 지정 된 값이 0 보다 크고는 SQL_ATTR_ROW_ARRAY_로 지정 된 값 보다 작음 크기 문 특성입니다.|  
|HY111|잘못 된 책갈피 값입니다.|인수 FetchOrientation SQL_FETCH_BOOKMARK, 였으며 값은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성을 가리키는 책갈피가 잘못 되었거나이 null 포인터입니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 변환의 조합으로 지정 하는 지원 하지 않습니다는 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 제한 시간 SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 **SQLFetchScroll** 결과 집합에서 지정 된 행 집합을 반환 합니다. 절대 또는 상대 위치 또는 책갈피 행 집합을 지정할 수 있습니다. **SQLFetchScroll** 결과 집합이 존재 하는 동안에 호출할 수 있습니다-즉, 결과 집합을 호출한 후에 만들어지는 하 고 결과 집합 위에 커서 앞 닫힙니다. 열에 바인딩된 경우 해당 열에 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열이 또는, 가져온 행 수를 반환 하는 버퍼에 대 한 포인터를 지정 하는 경우 **SQLFetchScroll** 뿐만 아니라이 정보를 반환 합니다. 에 대 한 호출이 **SQLFetchScroll** 호출을 혼합할 수 **SQLFetch** 와 함께 혼합할 수 없고 있지만 **SQLExtendedFetch**합니다.  
  
 자세한 내용은 참조 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md) 및 [스크롤 가능 커서를 사용 하 여](../../../odbc/reference/develop-app/using-scrollable-cursors.md)합니다.  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합을 만든 커서 결과 집합을 시작 하기 전에 배치 됩니다. **SQLFetchScroll** 의 값을 기반으로 블록 커서를 배치는 *FetchOrientation* 및 *FetchOffset* 인수는 다음 표에 나와 있는 것 처럼 합니다. 새 행 집합의 시작 부분을 결정 하는 규칙은 다음 섹션에 표시 됩니다.  
  
|FetchOrientation|의미|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|다음 행 집합을 반환 합니다. 이 호출에 해당 하는 **SQLFetch**합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_PRIOR|이전 행 집합을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_RELATIVE|행 집합 반환 *FetchOffset* 현재 행 집합의 시작 부분부터 합니다.|  
|SQL_FETCH_ABSOLUTE|행부터 행 집합을 반환 *FetchOffset*합니다.|  
|SQL_FETCH_FIRST|결과 집합의 첫 번째 행 집합을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_LAST|결과 집합의 마지막 전체 행 집합을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_BOOKMARK|행 집합은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 지정 된 책갈피에서 FetchOffset 행을 반환 합니다.|  
  
 드라이버 모든 인출 방향; 지 원하는 데 필요 하지 않습니다. 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 유형으로는 fetch를 확인 하려면 방향은 드라이버에서 사용할 수 있습니다. 응용 프로그램에서 이러한 정보 유형이 SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE, 및 WQL_CA1_BOOKMARK 비트 마스크에 표시 됩니다. 또한 커서는 정방향 전용 FetchOrientation SQL_FETCH_NEXT, 되지 않은 경우, **SQLFetchScroll** SQLSTATE HY106 반환 (인출 유형 범위를 벗어났습니다.).  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성은 행 집합의 행 수를 지정합니다. 행 집합으로 인출 되는 경우 **SQLFetchScroll** 결과 집합의 끝 겹치는 **SQLFetchScroll** 부분 행 집합을 반환 합니다. 즉, S + R-1 L 보다 큼, 여기서 S는 행 집합의 반입 되 고 R 시작 행 행 집합 크기 이며 L은 마지막 행 결과 집합의 다음 첫 번째 L만 – S + 행 집합의 1 행 경우 유효 합니다. 나머지 행은 빈 이며 SQL_ROW_NOROW의 상태입니다.  
  
 후 **SQLFetchScroll** 현재 행이 행 집합의 첫 번째 행을 반환 합니다.  
  
## <a name="cursor-positioning-rules"></a>커서 규칙 위치 지정  
 다음 섹션에서는 FetchOrientation의 각 값에 대 한 정확한 규칙을 설명 합니다. 이러한 규칙은 다음 표기법을 사용 합니다.  
  
|표기법|의미|  
|--------------|-------------|  
|*시작 하기 전에*|블록 커서 결과 집합을 시작 하기 전에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합을 시작 하기 전에 **SQLFetchScroll** SQL_NO_DATA를 반환 합니다.|  
|*종료 후*|블록 커서 후 집합 결과의 끝에 배치 됩니다. 새 행 집합의 첫 번째 행은 결과 집합의 끝 이후에 경우 **SQLFetchScroll** SQL_NO_DATA를 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합의 첫 번째 행의 수입니다.|  
|*LastResultRow*|결과 집합의 마지막 행의 수입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
|*FetchOffset*|값은 *FetchOffset* 인수입니다.|  
|*BookmarkRow*|SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 지정한 책갈피에 해당 하는 행입니다.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전에*|1.|  
|*CurrRowsetStart + RowsetSize*[1]  *\<LastResultRow =*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*종료 후*|  
|*종료 후*|*종료 후*|  
  
 [1] 행 집합 크기 행을 인출 하기 이전 호출 이후 변경 된 경우 이전 호출에 사용 된 행 집합 크기입니다.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전에*|*시작 하기 전에*|  
|*CurrRowsetStart = 1*|*시작 하기 전에*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2].</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*종료 및 LastResultRow 후 < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*종료 및 LastResultRow 후 > RowsetSize =* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2].</sup>|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06 반환 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [2] 행 집합 크기 행을 인출 하기 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*(및 FetchOffset 시작 전에 > 0) 또는 (및 FetchOffset 뒤 < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 및 FetchOffset < = 0*|*시작 하기 전에*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*시작 하기 전에*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*시작 하기 전에*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<LastResultRow =*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*종료 후*|  
|*종료 및 FetchOffset 후 > = 0*|*종료 후*|  
  
 [1] ***SQLFetchScroll*** FetchOrientation SQL_FETCH_ABSOLUTE로 설정 된 호출 하는 경우 동일한 행 집합을 반환 합니다. 자세한 내용은 "SQL_FETCH_ABSOLUTE" 섹션을 참조 합니다.  
  
 [2] **SQLFetchScroll** SQLSTATE 01S06 반환 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [3] 행 집합 크기 행을 인출 하기 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*시작 하기 전에*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*시작 하기 전에*|  
|*1 < = FetchOffset \<LastResultRow =*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*종료 후*|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06 반환 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [2] 행 집합 크기 행을 인출 하기 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
 동적 커서에서 행 위치로 정의 되지 않은 상태 절대 인출 동적 커서에 대해 수행 하 여 필요한 결과 제공할 수 없습니다. 이러한 작업이 인출 상대; 먼저 옵니다 fetch와 같습니다. 정적 커서에 대해 절대 인출 그대로 원자 단위 연산 않습니다.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*모든*|*1.*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < LastResultRow =|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1.*|  
  
 [1] 행 집합 크기 행을 인출 하기 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*시작 하기 전에*|  
|*1 < = BookmarkRow + FetchOffset \<LastResultRow =*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*종료 후*|  
  
 책갈피에 대 한 정보를 참조 하십시오. [책갈피 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)합니다.  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>커서 이동에 오류 행 및 삭제, 추가 된을의 효과  
 정적 및 키 집합 구동 커서 경우가 감지 결과에 추가 된 행 집합 결과 집합에서 삭제 된 행을 제거 합니다. 호출 하 여 **SQLGetInfo** SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS, 및 SQL_CA2_SENSITIVITY_에서 찾아 SQL_STATIC_CURSOR_ATTRIBUTES2 및 SQL_KEYSET_CURSOR_ATTRIBUTES2 옵션 업데이트를 나타내는 비트 마스크, 응용 프로그램에서는 특정 드라이버에서 구현 된 커서가를 수행 하는지 여부를 확인 합니다. 삭제 된 행을 검색 하 고 제거할 수 있는 드라이버에 대 한 다음 단락에서는이 동작의 효과 설명 합니다. 삭제 된 행을 검색할 수 있지만 제거할 수 없는 드라이버에 대 한 삭제는 커서 움직임에 영향을 미치지 하 고 다음 단락에서는 적용 되지 않습니다.  
  
 커서 결과 집합에 추가 하는 행을 검색 또는 결과 집합에서 삭제 된 행을 제거 하는 경우 데이터를 인출 하는 경우에 이러한 변경 내용을 감지 처럼 나타납니다. 경우를 포함 하면 **SQLFetchScroll** FetchOrientation SQL_FETCH_RELATIVE 및 FetchOffset을 동일한 행 집합을 다시 인출할 0으로 설정으로 설정 된 라고 하지만 SQLSetPos fOption SQL_로 설정 된 호출 될 때 대/소문자를 포함 하지 않습니다 새로 고칩니다. 후자의 경우에는 버퍼의에서 데이터는 행 집합을 새로 고칠 있지만 따라 다시 인출 하지 및 삭제 된 행은 결과 집합에서 제거 되지 않습니다. 따라서 행에서 삭제 되었거나 현재 행 집합에 삽입 된 경우 커서 행 집합 버퍼를 수정 하지 않습니다. 대신, 변경 하는 모든 행 집합 인출 하는 경우 이전에 삭제 된 행을 포함 하거나 이제에 삽입 된 행이 포함를 검색 합니다.  
  
 예를 들어  
  
```  
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
  
 때 **SQLFetchScroll** 현재 행 집합에 상대적인 위치에 있는 새 행 집합을 반환-FetchOrientation 즉, SQL_FETCH_NEXT, SQL_FETCH_PRIOR, 또는 SQL_FETCH_RELATIVE-변경 내용이 현재 행 집합에 포함 되지 않습니다 새 행 집합의 시작 위치를 계산 합니다. 그러나이 감지 수 있는 경우 현재 행 집합 외부 변경 내용 포함지 않습니다. 또한, **SQLFetchScroll** 는 위치가 현재 행 집합의 독립적인 새 행 집합을 반환-FetchOrientation 즉, SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE, 또는 SQL_FETCH_BOOKMARK-것 현재 행 집합에 있는 경우에 검색 하 고, 수는 모든 변경 내용이 포함 되어 있습니다.  
  
 새로 추가 된 행의 내부 또는 외부 현재 행 집합을 확인 하, 마지막 유효한 행; 끝에 부분 행 집합 간주 됩니다. 즉, 마지막 행을 행 상태 하지 SQL_ROW_NOROW 합니다. 예를 들어, 커서를 새로 추가 된 행을 검색할 수, 현재 행 집합은 부분 행 집합, 새 행을 추가 하는 응용 프로그램 및 커서 결과 집합의 끝에 이러한 행을 추가 합니다. 응용 프로그램을 호출 하는 경우 **SQLFetchScroll** FetchOrientation SQL_FETCH_NEXT로 설정 된 **SQLFetchScroll** 새로 추가 된 첫 번째 행부터 행 집합을 반환 합니다.  
  
 예를 들어 행 21-30을 구성 하는 현재 행 집합, 행 집합 크기는 10, 결과 집합에서 삭제 된 행을 제거 하는 커서 및 커서 결과 집합에 추가 하는 행을 검색 합니다. 다음 표에서 행을 표시 **SQLFetchScroll** 다양 한 상황에서 반환 합니다.  
  
|변경|인출 유형|FetchOffset|새 행 집합 [1]|  
|------------|----------------|-----------------|---------------------|  
|21 행 삭제|NEXT|0|31 ~ 40|  
|31 행 삭제|NEXT|0|32-41|  
|행 21-22 사이 행 삽입|NEXT|0|31 ~ 40|  
|행 30, 31 사이 행 삽입|NEXT|0|삽입된 한 행을 31-39|  
|21 행 삭제|PRIOR|0|11 ~ 20|  
|20 행 삭제|PRIOR|0|10-19|  
|행 21-22 사이 행 삽입|PRIOR|0|11 ~ 20|  
|행 20 및 21 사이 행 삽입|PRIOR|0|12 ~ 20, 삽입 된 행|  
|21 행 삭제|RELATIVE|0|22 ~ 31<sup>[2]</sup>|  
|21 행 삭제|RELATIVE|1.|22에서 31|  
|행 21-22 사이 행 삽입|RELATIVE|0|삽입 된 행 21, 22-29|  
|행 21-22 사이 행 삽입|RELATIVE|1.|22에서 31|  
|21 행 삭제|ABSOLUTE|21|22 ~ 31<sup>[2]</sup>|  
|22 행 삭제|ABSOLUTE|21|21, 23 ~ 31|  
|행 21-22 사이 행 삽입|ABSOLUTE|22|삽입된 한 행을 22-29|  
  
 [모든 행 삽입 또는 삭제 된 전에 1]이이 열은 행 번호를 사용 합니다.  
  
 [2]이 경우 커서 21 행부터 시작 하는 행을 반환 하려고 합니다. 21 행 삭제 되었으므로 첫 번째 반환 행을 22.  
  
 오류 행 (즉, 행 상태와 함께 SQL_ROW_ERROR의) 커서 움직임 영향을 주지 않습니다. 예를 들어 현재 행 집합 행 11과 상태를 시작 행 11은 SQL_ROW_ERROR 호출 **SQLFetchScroll** FetchOrientation SQL_FETCH_RELATIVE 및 FetchOffset로 설정는 5로 설정 16, 행부터 행 집합 반환 와 마찬가지로 11 행에 대 한 상태에 관계 없이 SQL_SUCCESS가 있습니다.  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에 데이터를 반환합니다.  
 **SQLFetchScroll** 바인딩된 열에 동일한 방식으로 데이터를 반환 **SQLFetch**합니다. 자세한 내용은 "반환 데이터에 바인딩된 열 참조"에 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
 열에 바인딩된 경우 **SQLFetchScroll** 데이터를 반환 하지 않지만 지정된 된 위치를 블록 커서를 이동 합니다. 블록 커서의 바인딩되지 않은 열에서 데이터를 검색할 수 있는지 여부 **SQLGetData** 드라이버에 따라 달라 집니다. 호출 하는 경우이 기능은 사용할 수 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 정보 종류에 대 한 비트가 SQL_GD_BLOCK를 반환 합니다.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 **SQLFetchScroll** 으로 데이터 및 길이/표시기 버퍼의 주소를 확인 하는 동일한 수식을 사용 **SQLFetch**합니다. 자세한 내용은의 "버퍼 주소" 참조 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
## <a name="row-status-array"></a>행 상태 배열이  
 **SQLFetchScroll** 동일한 방식으로 SQLFetch 행 상태 배열이의 값을 설정 합니다. 자세한 내용은의 "행 상태 배열이" 참조 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="rows-fetched-buffer"></a>버퍼를 인출 하는 행  
 **SQLFetchScroll** 같은 방식으로 행이 인출 버퍼에서 가져온 행 수를 반환 **SQLFetch**합니다. 자세한 내용은 "행 인출 버퍼"의 참조 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="error-handling"></a>오류 처리  
 응용 프로그램 호출 하는 경우 **SQLFetchScroll** ODBC 3.x 드라이버를 드라이버 관리자 호출 **SQLFetchScroll** 드라이버에서입니다. 응용 프로그램 호출 하는 경우 **SQLFetchScroll** SQLExtendedFetch 드라이버에서 드라이버 관리자는 ODBC 2.x 드라이버에서 호출 합니다. 때문에 **SQLFetchScroll** 되 고 SQLExtendedFetch 약간 다른 방식으로 오류를 처리, 응용 프로그램이 약간 다른 오류 동작 표시를 호출할 때 **SQLFetchScroll** odbc에서 2.x 및 ODBC 3.x 드라이버입니다.  
  
 **SQLFetchScroll** 오류 및 경고와 같은 방식으로 반환 **SQLFetch**; 자세한 내용은의 "오류 처리"를 참조 **SQLFetch**합니다. **SQLExtendedFetch** 같은 방식으로 오류를 반환 **SQLFetch**, 다음을 제외 합니다.  
  
 경고는 행 집합의 특정 행에 적용 되는 경우 SQLExtendedFetch SQL_ROW_SUCCESS, 하지 SQL_ROW_SUCCESS_WITH_INFO 행 상태 배열이에서 해당 항목을 설정 합니다.  
  
 행 집합의 모든 행에 오류가 발생 한 경우 SQLExtendedFetch 하지 SQL_ERROR, SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 각 그룹의 상태 레코드의 개별 행에 적용 되는 첫 번째 상태 레코드 SQLExtendedFetch에서 반환 된 SQLSTATE 01S01 포함 해야 합니다 (행에 오류가 있습니다); **SQLFetchScroll** 이 SQLSTATE를 반환 하지 않습니다. SQLExtendedFetch 추가 Sqlstate를 반환할 수 없는 경우이 SQLSTATE 여전히 반환 해야 합니다.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 및 낙관적 동시성  
 커서가 낙관적 동시성을 사용 하는 경우-즉, SQL_ATTR_CONCURRENCY 문 특성에 값이 SQL_CONCUR_VALUES 또는 SQL_CONCUR_ROWVER- **SQLFetchScroll** 데이터에서 사용 하는 낙관적 동시성 값 업데이트 행 변경 되었는지 여부를 확인 하기 소스입니다. 이런 경우가 발생 때마다 **SQLFetchScroll** 현재 행 집합을 다시 경우를 포함 하는 새 행 집합을 인출 합니다. (으로 호출 될 FetchOrientation SQL_FETCH_RELATIVE 및 0으로 설정 하는 FetchOffset로 설정 합니다.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 및 ODBC 2.x 드라이버  
 응용 프로그램 호출 하는 경우 **SQLFetchScroll** ODBC 2.x 드라이버를 드라이버 관리자는이 호출으로 매핑되는 **SQLExtendedFetch**합니다. 인수에 대해 다음 값을 전달 하기 **SQLExtendedFetch**합니다.  
  
|SQLExtendedFetch 인수|값|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle **SQLFetchScroll**합니다.|  
|FetchOrientation|FetchOrientation **SQLFetchScroll**합니다.|  
|FetchOffset|FetchOrientation SQL_FETCH_BOOKMARK에 FetchOffset 인수 값 없으면 **SQLFetchScroll** 사용 됩니다.<br /><br /> FetchOrientation SQL_FETCH_BOOKMARK 이면은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성으로 지정 된 주소에 저장 된 값이 사용 됩니다.|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 지정 된 주소입니다.|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 주소입니다.|  
  
 자세한 내용은 참조 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>설명자 및 SQLFetchScroll  
 **SQLFetchScroll** 설명자와 동일한 방식으로 상호 작용 하 **SQLFetch**합니다. 자세한 내용은의 "설명자 및 SQLFetchScroll" 섹션을 참조 하십시오. [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [열 단위 바인딩을](../../../odbc/reference/develop-app/column-wise-binding.md), [행 단위 바인딩을](../../../odbc/reference/develop-app/row-wise-binding.md), [Update 및 Delete 문을 배치](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), 및 [SQLSetPos와행집합의행업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업을 수행합니다.|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|문의 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침 또는 업데이트 또는 결과 집합의 데이터를 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

