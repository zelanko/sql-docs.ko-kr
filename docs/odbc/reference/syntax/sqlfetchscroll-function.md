---
title: SQLFetchScroll 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b7e5141a465249c818b50466b34a8155adc1d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982177"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 함수(SQLFetchScroll Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLFetchScroll** 결과 집합에서 데이터의 지정 된 행 집합을 인출 하 고 모든 바인딩된 열에 대 한 데이터를 반환 합니다. 절대 또는 상대 위치 또는 책갈피 별로 행 집합을 지정할 수 있습니다.  
  
 드라이버 관리자는이 함수를 매핑하는 odbc 2.x에서 작업할 때 **SQLExtendedFetch**합니다. 자세한 내용은 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
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
  
 자세한 내용은 "설명" 섹션에서 "커서 위치 지정"을 참조 하세요.  
  
 *FetchOffset*  
 [입력]  
  
 페치할 행의 수입니다. 값에 따라이 인수의 해석을 합니다 *FetchOrientation* 인수입니다. 자세한 내용은 "설명" 섹션에서 "커서 위치 지정"을 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFetchScroll** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 호출 HandleType 및 핸들을 사용 하 여 StatementHandle 합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLFetchScroll** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다. 단일 열에서 오류가 발생 하는 경우 **SQLGetDiagField** ;에서 오류가 발생 하는 열을 확인 하려면 SQL_DIAG_COLUMN_NUMBER DiagIdentifier를 사용 하 여 호출할 수 있습니다 하 고 **SQLGetDiagField** 호출할 수 있습니다 행을 확인 하려면 SQL_DIAG_ROW_NUMBER DiagIdentifier를 사용 하 여 열이 포함 된 합니다.  
  
 다중 행 작업의 하나 또는 더 많은 전부는 아니지만, 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 하는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|공백이 아닌 문자 또는 NULL이 아닌 이진 데이터의 잘림 문자열 또는 이진 데이터 열에 대 한 반환 했습니다. 문자열 값이 오른쪽 잘림 이었습니다.|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다.<br /><br /> (이 SQLSTATE는 ODBC 3 때 반환 되 면 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 무시할 수 있습니다.)|  
|01S06|결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 합니다.|요청 된 행 집합 overlapped FetchOrientation SQL_FETCH_PRIOR, 현재 위치가 첫 번째 행을 초과 했습니다 였으며 현재 행의 수는 행 집합 크기 보다 작거나 때 결과 집합을 시작 합니다.<br /><br /> 요청 된 행 집합 overlapped FetchOrientation SQL_FETCH_PRIOR, 현재 위치를 결과 집합의 끝을 넘어 이며 행 집합 크기는 결과 집합 크기 보다 큰 경우의 결과 집합의 시작 합니다.<br /><br /> 요청 된 행 집합 overlapped FetchOrientation SQL_FETCH_RELATIVE, FetchOffset이 음수, 이며 FetchOffset의 절대 값을 행 집합 크기 보다 작거나 때 결과 집합을 시작 합니다.<br /><br /> 요청 된 행 집합 overlapped FetchOrientation SQL_FETCH_ABSOLUTE, FetchOffset이 음수, 이며 FetchOffset의 절대 값을 결과 집합 크기 보다 큰 경우의 결과 집합의 시작 되지만 행 집합 크기 보다 작거나 합니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 간격 데이터 형식에 대 한 시간의 소수 부분을 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.<br /><br /> 0 열 데이터 형식의 SQL_C_BOOKMARK, 바인딩된 및 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_VARIABLE로 설정 되었습니다.<br /><br /> 0 열 데이터 형식의 SQL_C_VARBOOKMARK, 바인딩 및 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_VARIABLE에 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|드라이버는 ODBC 2 되었습니다 *.x* 드라이버를 지원 하지 않는 **SQLExtendedFetch**, 열에 대 한 바인딩에 지정 된 열 번호 되었습니다. 0 및 합니다.<br /><br /> 열 0, 바인딩되고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터 오른쪽 잘림|열에 대해 반환 된 가변 길이 책갈피가 잘렸습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지|NULL 데이터가 페치된 열을 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** (또는 설정한 SQL_DESC_INDICATOR_PTR **SQLSetDescField** 또는  **SQLSetDescRec**)가 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|하나 이상의 바인딩된 열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.<br /><br /> 자세한 내용은 [SQL에서 C 데이터 형식 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 에서 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22007|잘못 된 날짜/시간 형식|결과 집합의 문자 열 된 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다.|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 부서에서 발생 하는 0입니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형을 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> 간격 C 형식으로 데이터를 인출할 때 C 간격 유형으로 SQL 형식의 값 표현 방식이 없기 있었습니다.|  
|22018|캐스트 사양의 문자 값|결과 집합의 문자 열 C 문자 버퍼에 바인딩된 열 버퍼의 문자 집합에 표현이 없는 된 문자를 포함 하며<br /><br /> C 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 열의 SQL 형식이 된 문자 데이터 형식입니다. 하는 열에 값을 바인딩된 C 형식의 유효한 리터럴이 없습니다.|  
|24000|잘못된 커서 상태|합니다 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.|  
|40001|Serialization 오류|실행 된 fetch는 트랜잭션이 교착 상태를 방지 하기 위해 종료 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLFetchScroll** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 실행 상태가 없습니다. 첫 번째 호출 하지 않고 함수를 호출한 **SQLExecDirect**를 **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM) **SQLFetch** 에 대해 호출 되었습니다 합니다 *StatementHandle* 후 **SQLExtendedFetch** 호출한 전과 **SQLFreeStmt** 는 SQL_를 사용 하 여 닫기 옵션 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE로 설정 된 및 0 열이 결과 집합에 대 한 책갈피에 대 한 최대 길이 같은 길이가 없습니다. 버퍼에 바인딩 되었습니다. (이 길이 IRD의 SQL_DESC_OCTET_LENGTH 필드 수 및 호출 하 여 가져올 수 있습니다 **SQLDescribeCol**하십시오 **SQLColAttribute**, 또는 **SQLGetDescField**.)|  
|HY106|인출 유형 범위를 벗어났습니다.|DM) FetchOrientation 인수로 지정한 값을 잘못 되었습니다.<br /><br /> (DM) FetchOrientation 인수가 SQL_FETCH_BOOKMARK, 및 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 문 특성의 값에 SQL_CURSOR_FORWARD_ONLY, 되었고 FetchOrientation SQL_FETCH_NEXT 없습니다. 인수 값입니다.<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 문 특성의 값을 SQL_NONSCROLLABLE 및 FetchOrientation SQL_FETCH_NEXT 없습니다. 인수 값을 했습니다.|  
|HY107|행 값 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE 문 특성을 사용 하 여 지정 된 값, SQL_CURSOR_KEYSET_DRIVEN 되었지만 SQL_ATTR_KEYSET_SIZE 문 특성을 사용 하 여 지정한 값이 0 보다 크고는 SQL_ATTR_ROW_ARRAY_를 사용 하 여 지정 된 값 보다 작음 크기 문 특성입니다.|  
|HY111|잘못 된 책갈피 값입니다.|FetchOrientation 인수가 SQL_FETCH_BOOKMARK, 및 값은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성을 가리키는 책갈피 잘못 되었거나이 null 포인터입니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 조합에 의해 지정 된 변환을 지원 하지 않습니다 합니다 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 시간 제한 기간 SQLSetStmtAttr에서 SQL_ATTR_QUERY_TIMEOUT 통해 설정 됩니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLFetchScroll** 결과 집합에서 지정 된 행 집합을 반환 합니다. 절대 또는 상대 위치 또는 책갈피 별로 행 집합을 지정할 수 있습니다. **SQLFetchScroll** 결과 집합을 있기는-즉, 호출 결과 집합을 만든 후 커서 앞 결과 집합을 통해 닫혀만 호출할 수 있습니다. 모든 열에 바인딩되어 있는 경우 해당 열에 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열이 나 인출 하는 행의 수를 반환 하는 버퍼에 대 한 포인터를 지정한 경우 **SQLFetchScroll** 뿐만 아니라이 정보를 반환 합니다. 에 대 한 호출 **SQLFetchScroll** 를 호출 하 여 함께 사용할 수 있습니다 **SQLFetch** 호출 하 여 혼합할 수 없습니다 하지만 **SQLExtendedFetch**합니다.  
  
 자세한 내용은 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md) 하 고 [스크롤 가능 커서를 사용 하 여](../../../odbc/reference/develop-app/using-scrollable-cursors.md)입니다.  
  
## <a name="positioning-the-cursor"></a>커서를 놓고  
 결과 집합을 만든 경우 커서는 결과 집합을 시작 하기 전에 배치 됩니다. **SQLFetchScroll** 의 값을 기반으로 블록 커서를 배치 합니다 *FetchOrientation* 하 고 *FetchOffset* 인수는 다음 표에 나와 있는 것 처럼 합니다. 새 행 집합의 시작을 확인 하는 것에 대 한 정확한 규칙은 다음 섹션에 표시 됩니다.  
  
|FetchOrientation|의미|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|다음 행 집합을 반환 합니다. 이 호출할 때와 동일한 **SQLFetch**합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_PRIOR|이전 행 집합을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_RELATIVE|행 집합 반환 *FetchOffset* 현재 행 집합의 시작 부분에서.|  
|SQL_FETCH_ABSOLUTE|행부터 행 집합 반환 *FetchOffset*합니다.|  
|SQL_FETCH_FIRST|결과 집합의 첫 번째 행을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_LAST|결과 집합의 마지막 전체 행 집합을 반환 합니다.<br /><br /> **SQLFetchScroll** 의 값을 무시 *FetchOffset*합니다.|  
|SQL_FETCH_BOOKMARK|행 집합은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 지정한 책갈피에서 FetchOffset 행을 반환 합니다.|  
  
 드라이버 모든 인출 방향;를 지 원하는 데 필요 하지 않습니다. 응용 프로그램 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 유형으로는 fetch를 확인 하려면 방향은 드라이버에서 지원 됩니다. 응용 프로그램에서 이러한 정보 유형 SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE, 및 WQL_CA1_BOOKMARK 비트 마스크에 표시 됩니다. 또한 커서는 정방향 전용 및 FetchOrientation SQL_FETCH_NEXT에 없는 경우 **SQLFetchScroll** SQLSTATE HY106 반환 (반입 형식이 범위를 벗어났습니다.).  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성 행 집합의 행 수를 지정합니다. 행 집합으로 인출 되는 경우 **SQLFetchScroll** 결과 집합의 끝을 겹치는 **SQLFetchScroll** 부분 행 집합을 반환 합니다. 즉, S + R-1은 L 보다 큼, 여기서 S는 행 집합의 반입 되 고 R 시작 행을 행 집합 크기 이며 L 마지막 행 결과 집합에서 다음만 첫 번째 L-S + 행 집합의 1 행 경우 유효 합니다. 나머지 행 비어 있으며 SQL_ROW_NOROW의 상태.  
  
 이후에 **SQLFetchScroll** 현재 행이 행 집합의 첫 번째 행을 반환 합니다.  
  
## <a name="cursor-positioning-rules"></a>커서 위치 지정을 규칙  
 다음 섹션에서는 FetchOrientation의 각 값에 대 한 정확한 규칙을 설명합니다. 이러한 규칙 다음 표기법을 사용합니다.  
  
|Notation|의미|  
|--------------|-------------|  
|*시작 하기 전에*|블록 커서 결과 집합을 시작 하기 전에 배치 됩니다. 결과 집합을 시작 하기 전에 새 행 집합의 첫 번째 행 이면 **SQLFetchScroll** SQL_NO_DATA를 반환 합니다.|  
|*종료 후*|블록 커서는 결과의 끝을 설정한 후에 배치 됩니다. 결과 집합의 끝 뒤에 새 행 집합의 첫 번째 행 이면 **SQLFetchScroll** SQL_NO_DATA를 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합에서 첫 번째 행의 수입니다.|  
|*LastResultRow*|결과 집합의 마지막 행의 수입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
|*FetchOffset*|값을 *FetchOffset* 인수입니다.|  
|*BookmarkRow*|SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 지정한 책갈피에 해당 하는 행입니다.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전에*|1|  
|*CurrRowsetStart + RowsetSize*[1] *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*종료 후*|  
|*종료 후*|*종료 후*|  
  
 [1] 행 집합 크기 행을 인출 이전 호출 이후 변경 된 경우 이전 호출에 사용 된 행 집합 크기입니다.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작 하기 전에*|*시작 하기 전에*|  
|*CurrRowsetStart = 1*|*시작 하기 전에*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*종료 및 LastResultRow 후 < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*종료 및 LastResultRow 후 > = RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize + 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06를 반환 합니다 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [2] 행 집합 크기 행을 인출 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*(및 FetchOffset 시작 전에 > 0) 또는 (종료 및 FetchOffset 후 < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart AND FetchOffset <= 0*|*시작 하기 전에*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*시작 하기 전에*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*시작 하기 전에*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; <= RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*종료 후*|  
|*종료 및 FetchOffset 후 > = 0*|*종료 후*|  
  
 [1] ***SQLFetchScroll*** FetchOrientation SQL_FETCH_ABSOLUTE로를 사용 하 여 호출 된 것 처럼 동일한 행 집합을 반환 합니다. 자세한 내용은 "SQL_FETCH_ABSOLUTE" 섹션을 참조 하세요.  
  
 [2] **SQLFetchScroll** SQLSTATE 01S06를 반환 합니다 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [3] 행 집합 크기 행을 인출 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; <= LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 및 &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*시작 하기 전에*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*시작 하기 전에*|  
|*1 <= FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*종료 후*|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06를 반환 합니다 (결과 집합은 첫 번째 행을 반환 하기 전에 반입 하려고 함) 및 SQL_SUCCESS_WITH_INFO 합니다.  
  
 [2] 행 집합 크기 행을 인출 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
 동적 커서에 대해 수행 하는 절대 인출 동적 커서의 행 위치를 결정 되지 않으므로 필요한 결과 제공할 수 없습니다. 이러한 작업은 먼저 입력 한 다음 인출 상대; 페치 정적 커서에 대해 절대 인출 그대로 원자성 작업이 아닙니다.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*Any*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> <= LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 행 집합 크기 행을 인출 이전 호출 이후 변경 된 경우 새 행 집합 크기입니다.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 다음 규칙이 적용 됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*시작 하기 전에*|  
|*1 <= BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*종료 후*|  
  
 책갈피에 대 한 정보를 참조 하세요 [책갈피 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)합니다.  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>삭제, 추가 효과 커서 이동에 오류 행  
 정적 및 키 집합 커서는 경우에 따라 결과에 추가 된 행 집합과 결과 집합에서 삭제 된 행 제거를 검색 합니다. 호출 하 여 **SQLGetInfo** SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS, 및 SQL_CA2_SENSITIVITY_ 찾고 SQL_STATIC_CURSOR_ATTRIBUTES2와 SQL_KEYSET_CURSOR_ATTRIBUTES2 옵션 업데이트 마스크를 응용 프로그램 특정 드라이버에서 구현 된 커서 초기화할이 있는지 여부를 확인 합니다. 삭제 된 행을 검색 하 고 제거할 수 있는 드라이버의 경우 다음 단락에서는이 동작의 영향을 설명 합니다. 삭제 된 행을 검색할 수 있지만 제거할 수 없으므로 드라이버에 대 한 삭제 커서 움직임에 영향을 주지 있고 다음 단락에서는 적용 되지 않습니다.  
  
 커서 결과 집합에 추가 하는 행을 검색, 결과 집합에서 삭제 된 행을 제거 하는 경우 데이터를 인출 하는 경우에 이러한 변경 내용을 감지 처럼 표시 됩니다. 경우를 포함 하면 **SQLFetchScroll** FetchOrientation SQL_FETCH_RELATIVE FetchOffset 동일한 행 집합을 다시 인출 하도록 0으로 설정으로 설정 된 라고 하지만 SQLSetPos fOption SQL_로 호출 될 때 대/소문자를 포함 하지 않습니다 새로 고칩니다. 후자의 경우, 행 집합 버퍼에 데이터가 새로 고쳐질, 하지만 하지 따라 다시 인출 되거나 삭제 된 행 결과 집합에서 제거 되지 않습니다. 따라서 행에서 삭제 되었거나 현재 행 집합에 삽입할 경우 때 커서 행 집합 버퍼를 수정 하지 않습니다. 대신 변경 하는 모든 행 집합 인출 하는 경우 이전에 삭제 된 행을 포함 또는 삽입 된 행은 이제 검색 합니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
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
  
 때 **SQLFetchScroll** 현재 행 집합-상대적인 위치에 있는 새 행 집합을 반환 합니다. 즉, FetchOrientation는 SQL_FETCH_NEXT, SQL_FETCH_PRIOR를 또는 SQL_FETCH_RELATIVE-현재 행 집합에 변경 내용을 포함 하지 않습니다 새 행 집합의 시작 위치를 계산 합니다. 그러나를 감지 하 고 수 하는 경우 현재 행 집합 외부 변경 내용을 포함지 않습니다. 또한 때 **SQLFetchScroll** 현재 행 집합-의 독립 된 위치에 있는 새 행 집합을 반환 FetchOrientation 즉 SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE, 또는 SQL_FETCH_BOOKMARK-것 현재 행 집합에 있을 경우에, 검색은 모든 변경 내용이 포함 되어 있습니다.  
  
 마지막으로 된 유효한 행의 끝에 부분 행 집합 것으로 간주 됩니다을 내부 또는 외부 현재 행 집합의 새로 추가 된 행이 있는지 여부를 결정 하는 경우 즉, 마지막 행에는 행 상태가 SQL_ROW_NOROW입니다. 예를 들어, 커서를 새로 추가 된 행을 검색할 수 있으므로, 현재 행 집합에 부분 행 집합은, 응용 프로그램에 새 행 추가 및 커서 결과 집합의 끝에 이러한 행을 추가 합니다. 응용 프로그램을 호출 하는 경우 **SQLFetchScroll** FetchOrientation SQL_FETCH_NEXT로 설정 된 **SQLFetchScroll** 새로 추가 된 첫 번째 행부터 행 집합을 반환 합니다.  
  
 예를 들어 현재 행 집합 행 21 ~ 30 구성, 행 집합 크기는 10, 결과 집합에서 삭제 된 행을 제거 하는 커서 및 커서 결과 집합에 추가 하는 행을 검색 합니다. 다음 표에서 행 **SQLFetchScroll** 다양 한 상황에서 반환 합니다.  
  
|변경|인출 유형|FetchOffset|새 행 집합 [1]|  
|------------|----------------|-----------------|---------------------|  
|21 행 삭제|NEXT|0|31 ~ 40|  
|31 행 삭제|NEXT|0|32-41|  
|행 21 22 사이 행 삽입|NEXT|0|31 ~ 40|  
|행 30에서 31 사이 행 삽입|NEXT|0|삽입 된 행을 31-39|  
|21 행 삭제|PRIOR|0|11 ~ 20|  
|20 행 삭제|PRIOR|0|10 ~ 19|  
|행 21 22 사이 행 삽입|PRIOR|0|11 ~ 20|  
|행 20 및 21 사이 행 삽입|PRIOR|0|12 ~ 20, 삽입 된 행|  
|21 행 삭제|RELATIVE|0|22 일에서 31<sup>[2]</sup>|  
|21 행 삭제|RELATIVE|1|22 일에서 31 일|  
|행 21 22 사이 행 삽입|RELATIVE|0|삽입 된 행 21, 22 29 일|  
|행 21 22 사이 행 삽입|RELATIVE|1|22 일에서 31 일|  
|21 행 삭제|ABSOLUTE|21|22 일에서 31<sup>[2]</sup>|  
|22 행 삭제|ABSOLUTE|21|21, 23 일에서 31 일|  
|행 21 22 사이 행 삽입|ABSOLUTE|22|삽입 된 행, 29 일 22|  
  
 [1]이이 열 전에 모든 행 삽입 또는 삭제 된 행 번호를 사용 합니다.  
  
 [2]이 경우 커서 행 21 사용 하 여 시작 하는 행을 반환 하려고 합니다. 21 행 삭제 되었으므로 반환 하는 첫 번째 행은 행 22입니다.  
  
 오류 행 (즉, 행 상태와 함께 SQL_ROW_ERROR) 커서 이동 영향을 주지 않습니다. 예를 들어 현재 행 집합 행 11 및 상태를 사용 하 여 시작 하는 경우 행 11이 SQL_ROW_ERROR 호출 **SQLFetchScroll** SQL_FETCH_RELATIVE 및 FetchOffset로 FetchOrientation 5로 설정 16 행부터 행 집합 반환 마찬가지로 11 행에 대 한 상태에 관계 없이 SQL_SUCCESS 되었으면 합니다.  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에서 데이터를 반환합니다.  
 **SQLFetchScroll** 바인딩된 열에서 동일한 방식으로 데이터를 반환 **SQLFetch**합니다. 자세한 내용은 "반환 데이터에 바인딩된 열"를 참조 하세요 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
 열에 바인딩되어 있는 경우 **SQLFetchScroll** 데이터를 반환 하지 않습니다 하지만 지정된 된 위치에 블록 커서를 이동지 않습니다. 블록 커서의 바인딩되지 않은 열에서 데이터를 검색할 수 있는지 여부 **SQLGetData** 드라이버에 따라 달라 집니다. 이 기능을 호출 하는 경우 지원 됩니다 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 정보 유형에 대 한 비트 SQL_GD_BLOCK를 반환 합니다.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 **SQLFetchScroll** 동일한 공식을 사용 하 여으로 데이터 및 길이/표시기 버퍼의 주소를 확인할 **SQLFetch**합니다. 자세한 내용은 "버퍼 주소"를 참조 하세요 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 **SQLFetchScroll** SQLFetch로 동일한 방식으로 행 상태 배열에 값을 설정 합니다. 자세한 내용은 "행 상태 배열"를 참조 하세요 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="rows-fetched-buffer"></a>행 인출된 버퍼  
 **SQLFetchScroll** 동일한 방식으로 행이 인출 버퍼에서 가져올 행의 수를 반환 **SQLFetch**합니다. 자세한 내용은 "행 인출 버퍼"의 참조 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="error-handling"></a>오류 처리  
 응용 프로그램을 호출할 때 **SQLFetchScroll** ODBC 3.x 드라이버를 드라이버 관리자 호출 **SQLFetchScroll** 드라이버에서. 응용 프로그램을 호출할 때 **SQLFetchScroll** SQLExtendedFetch 드라이버에서 드라이버 관리자는 ODBC 2.x 드라이버에서 호출 합니다. 때문에 **SQLFetchScroll** SQLExtendedFetch 약간 다른 방식으로 오류를 처리, 응용 프로그램이 약간 다른 오류 동작 보입니다 호출할 때 **SQLFetchScroll** odbc에서 2.x 및 ODBC 3.x 드라이버입니다.  
  
 **SQLFetchScroll** 동일한 방식으로 오류 및 경고를 반환 **SQLFetch**; 자세한 내용은 "오류 처리"를 참조 하십시오 **SQLFetch**합니다. **SQLExtendedFetch** 동일한 방식으로 오류를 반환 합니다. **SQLFetch**, 다음과 같은 예외를 사용 하 여:  
  
 행 집합의 특정 행에 적용 되는 경고가 발생 하면 SQLExtendedFetch SQL_ROW_SUCCESS, 없습니다 SQL_ROW_SUCCESS_WITH_INFO 행 상태 배열에서 해당 항목을 설정 합니다.  
  
 행 집합의 모든 행에 오류가 발생 하면 SQLExtendedFetch 없습니다 SQL_ERROR, SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 각 그룹의 상태 레코드의 개별 행에 적용 되는 첫 번째 상태 레코드 SQLExtendedFetch 반환한 SQLSTATE 01S01 포함 해야 합니다 (행의 오류). **SQLFetchScroll** 이 SQLSTATE를 반환 하지 않습니다. SQLExtendedFetch 추가 Sqlstate를 반환할 수 없는 경우이 SQLSTATE 여전히 반환 해야 합니다.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 및 낙관적 동시성  
 낙관적 동시성을 사용 하 여 커서-즉, SQL_ATTR_CONCURRENCY 문 특성에 값이 SQL_CONCUR_VALUES 또는 SQL_CONCUR_ROWVER-하는 경우 **SQLFetchScroll** 데이터가 사용 하는 낙관적 동시성 값 업데이트 행 변경 되었는지 여부를 검색할 원본입니다. 때마다 이런 **SQLFetchScroll** 현재 행 집합을 다시 해당 하는 경우를 포함 하 여 새 행 집합을 인출 합니다. (으로 호출 될 FetchOrientation SQL_FETCH_RELATIVE FetchOffset 0으로 설정으로 설정 합니다.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 및 ODBC 2.x 드라이버  
 응용 프로그램을 호출할 때 **SQLFetchScroll** 드라이버 관리자는 ODBC 2.x 드라이버에서이 호출을 매핑합니다 **SQLExtendedFetch**합니다. 다음의 인수 값 전달 **SQLExtendedFetch**합니다.  
  
|SQLExtendedFetch 인수|값|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle **SQLFetchScroll**합니다.|  
|FetchOrientation|FetchOrientation **SQLFetchScroll**합니다.|  
|FetchOffset|FetchOrientation SQL_FETCH_BOOKMARK에 FetchOffset 인수 값 없으면 **SQLFetchScroll** 사용 됩니다.<br /><br /> FetchOrientation SQL_FETCH_BOOKMARK 이면은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 의해 지정 된 주소에 저장 된 값이 사용 됩니다.|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 지정 된 주소입니다.|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 주소입니다.|  
  
 자세한 내용은 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>설명자 및 SQLFetchScroll  
 **SQLFetchScroll** 설명자를 사용 하 여 동일한 방식으로 상호 작용 **SQLFetch**합니다. 자세한 내용은의 "설명자 및 SQLFetchScroll" 섹션을 참조 하세요 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [열 단위 바인딩을](../../../odbc/reference/develop-app/column-wise-binding.md), [행 단위 바인딩은](../../../odbc/reference/develop-app/row-wise-binding.md)를 [Update 및 Delete 문을 배치](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), 및 [SQLSetPos를사용하여행집합의행을업데이트하는중입니다.](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업을 수행합니다.|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|문의 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침, 업데이트 또는 결과 집합의 데이터 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
