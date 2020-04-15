---
title: SQLFetch스크롤 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285883"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 함수(SQLFetchScroll Function)
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLFetchScroll** 결과 집합에서 지정 된 데이터 행 집합을 가져옵니다 및 모든 바인딩된 열에 대 한 데이터를 반환 합니다. 행 집합은 절대 또는 상대 위치 또는 책갈피로 지정할 수 있습니다.  
  
 ODBC 2.x 드라이버로 작업할 때 드라이버 관리자는 이 함수를 **SQLExtendedFetch**에 매핑합니다. 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 대체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *페치 방향*  
 [입력]  
  
 반입 유형:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 자세한 내용은 "주석" 섹션에서 "커서 위치 지정" 섹션을 참조하십시오.  
  
 *가져오기오프셋*  
 [입력]  
  
 가져올 행 의 수입니다. 이 인수의 해석은 *FetchOrientation* 인수의 값에 따라 달라집니다. 자세한 내용은 "주석" 섹션에서 "커서 위치 지정" 섹션을 참조하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLFetchScroll** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 핸들 유형 SQL_HANDLE_STMT 및 문 핸들의 핸들을 호출 하 여 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLFetchScroll에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR. 단일 열에서 오류가 발생하는 경우 **SQLGetDiagField는** SQL_DIAG_COLUMN_NUMBER DiagIdentifier를 사용하여 호출하여 오류가 발생한 열을 확인할 수 있습니다. **및 SQLGetDiagField는** 해당 열이 포함된 행을 결정하기 위해 SQL_DIAG_ROW_NUMBER DiagIdentifier를 사용하여 호출할 수 있습니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환할 수 있는 모든 SQLSTAT(01xxx SQLSTAT)에 대해 하나 이상의 오류가 발생하는 경우 SQL_SUCCESS_WITH_INFO 반환되지만 전부는 아니지만 다중 행 작업의 행이 반환되고 단일 행 작업에서 오류가 발생하면 SQL_ERROR 반환됩니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|열에 대해 반환된 문자열 또는 이진 데이터는 비공백 문자 또는 NULL이 아닌 이진 데이터의 잘림을 초래했습니다. 문자열 값인 경우 오른쪽 잘린 값입니다.|  
|01S01|행의 오류|하나 이상의 행을 가져오는 동안 오류가 발생했습니다.<br /><br /> ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버로 작업할 때 이 SQLSTATE가 반환되는 경우 무시할 수 있습니다.|  
|01S06|결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기를 시도합니다.|요청된 행 집합은 FetchOrientation가 SQL_FETCH_PRIOR 때 결과 집합의 시작과 겹쳤고, 현재 위치는 첫 번째 행을 초과했으며, 현재 행의 수는 행 집합 크기보다 작거나 같습니다.<br /><br /> 요청된 행 집합은 FetchOrientation이 SQL_FETCH_PRIOR 때 결과 집합의 시작과 겹쳤고, 현재 위치는 결과 집합의 끝을 초과했으며, 행 집합 크기는 결과 집합 크기보다 큽했습니다.<br /><br /> 요청된 행집합은 FetchOrientation이 SQL_FETCH_RELATIVE 때 결과 집합의 시작과 겹쳤고, FetchOffset은 음수였으며, FetchOffset의 절대값은 행 집합 크기보다 작거나 같습니다.<br /><br /> 요청된 행집합은 FetchOrientation이 SQL_FETCH_ABSOLUTE 때 결과 집합의 시작을 중첩하고, FetchOffset은 음수였으며, FetchOffset의 절대값은 결과 집합 크기보다 크지만 행 집합 크기에 비해 작거나 작습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S07|분수 잘림|열에 대해 반환된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|결과 집합에서 열의 데이터 값을 **SQLBindCol**에서 *TargetType에* 의해 지정된 데이터 유형으로 변환할 수 없습니다.<br /><br /> 열 0은 SQL_C_BOOKMARK 데이터 유형으로 바인딩되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성은 SQL_UB_VARIABLE 설정되었습니다.<br /><br /> 열 0은 데이터 형식의 SQL_C_VARBOOKMARK 바인딩되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되지 않았습니다.|  
|07009|잘못된 설명자 인덱스|드라이버는 **SQLExtendedFetch를**지원하지 않는 ODBC 2 *.x* 드라이버이고 열바인딩에 지정된 열 번호는 0입니다.<br /><br /> 열 0이 바인딩되었고 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22001|문자열 데이터, 오른쪽 잘린|열에 대해 반환된 가변 길이 책갈피가 잘렸습니다.|  
|22002|표시기 변수가 필요하지만 제공되지 않음|NULL 데이터는 **SQLBindCol(또는** **SQLSetDescField** 또는 **SQLSetDescRec에서**설정한 SQL_DESC_INDICATOR_PTR)에 의해 설정된 *StrLen_or_IndPtr* null 포인터인 열로 가져옵니다.|  
|22003|범위를 벗어난 숫자 값|하나 이상의 바인딩된 열에 대해 숫자 값(숫자 또는 문자열)을 반환하면 숫자의 전체(분수와 반대)가 잘릴 수 있습니다.<br /><br /> 자세한 내용은 [부록 D: 데이터](../../../odbc/reference/appendixes/appendix-d-data-types.md) [형식의 SQL에서 C 데이터 유형으로 데이터 변환을](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 참조하십시오.|  
|22007|잘못된 날짜 시간 형식|결과 집합의 문자 열은 날짜, 시간 또는 타임스탬프 C 구조에 바인딩되었으며 열의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다.|  
|22012|0으로 나누기|산술 식의 값이 반환되어 0으로 분할됩니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 SQL 형식에서 간격 C 유형으로 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> 간격 C 유형으로 데이터를 가져올 때 간격 C 형식에서 SQL 형식의 값에 대한 표현이 없었습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|결과 집합의 문자 열은 문자 C 버퍼에 바인딩되었으며 열에는 버퍼의 문자 집합에 표현이 없는 문자가 포함되어 있습니다.<br /><br /> C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행 된 상태에 있지만 결과 *집합은 StatementHandle*.|  
|40001|직렬화 실패|교착 상태를 방지하기 위해 가져오기가 실행된 트랜잭션이 종료되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLFetchScroll** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect,** **SQLExecute** 또는 카탈로그 함수를 먼저 호출하지 않고 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) **SQLFetch는** **SQLExtendedFetch가** 호출되고 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 전에 *문 핸들에* 대 한 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|SQL_ATTR_USE_BOOKMARK 문 특성은 SQL_UB_VARIABLE 설정되었으며 열 0은 길이가 이 결과 집합의 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩되었습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol,** **SQLColAttribute**또는 **SQLGetDescField를**호출하여 얻을 수 있습니다.|  
|HY106|범위를 벗어난 형식 가져오기|DM) 인수 FetchOrientation에 대해 지정된 값이 잘못되었습니다.<br /><br /> (DM) 인수 FetchOrientationSQL_FETCH_BOOKMARK, SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 문 특성의 값은 SQL_CURSOR_FORWARD_ONLY 인수 FetchOrientation의 값이 SQL_FETCH_NEXT 않았습니다.<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 문 특성의 값은 SQL_NONSCROLLABLE 인수 FetchOrientation의 값이 SQL_FETCH_NEXT 않았습니다.|  
|HY107|범위를 벗어난 행 값|SQL_ATTR_CURSOR_TYPE 문 특성으로 지정된 값은 SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_KEYSET_SIZE 문 특성으로 지정된 값이 0보다 크고 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 지정된 값보다 작습니다.|  
|HY11|책갈피 값이 잘못되었습니다.|인수 FetchOrientation SQL_FETCH_BOOKMARK, 책갈피 는 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성의 값으로 가리키고 유효하지 않거나 null 포인터.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 **SQLBindCol의** *TargetType과* 해당 열의 SQL 데이터 형식의 조합으로 지정된 변환을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 요청된 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 SQL_ATTR_QUERY_TIMEOUT SQLSetStmtAttr을 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLFetchScroll** 결과 집합에서 지정 된 행 집합을 반환 합니다. 행 집합은 절대 또는 상대 위치 또는 책갈피로 지정할 수 있습니다. **SQLFetchScroll는** 결과 집합이 있는 동안에만 호출할 수 있습니다. 바인딩된 열이 있으면 해당 열의 데이터를 반환합니다. 응용 프로그램에서 행 상태 배열에 대한 포인터또는 가져온 행 수를 반환하는 버퍼를 지정한 경우 **SQLFetchScroll도** 이 정보를 반환합니다. **SQLFetchScroll에** 대한 호출은 **SQLFetch에** 대한 호출과 혼합될 수 있지만 **SQLExtendedFetch**에 대한 호출과 혼합할 수 없습니다.  
  
 자세한 내용은 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md) 및 스크롤 가능한 [커서 사용을](../../../odbc/reference/develop-app/using-scrollable-cursors.md)참조하십시오.  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합이 만들어지면 커서는 결과 집합이 시작되기 전에 배치됩니다. **SQLFetchScroll는** 다음 표에 표시된 대로 *FetchOrientation* 및 *FetchOffset* 인수의 값을 기반으로 블록 커서를 배치합니다. 새 행 집합의 시작을 결정하는 정확한 규칙이 다음 섹션에 표시됩니다.  
  
|페치 방향|의미|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|다음 행 집합을 반환합니다. 이는 **SQLFetch**를 호출하는 것과 같습니다.<br /><br /> **SQLFetchScroll는** *FetchOffset*의 값을 무시합니다.|  
|SQL_FETCH_PRIOR|이전 행 집합을 반환합니다.<br /><br /> **SQLFetchScroll는** *FetchOffset*의 값을 무시합니다.|  
|SQL_FETCH_RELATIVE|현재 행 집합의 시작부터 행 집합 *FetchOffset을* 반환합니다.|  
|SQL_FETCH_ABSOLUTE|행 *FetchOffset에서*시작하는 행 집합을 반환합니다.|  
|SQL_FETCH_FIRST|결과 집합에서 첫 번째 행 집합을 반환합니다.<br /><br /> **SQLFetchScroll는** *FetchOffset*의 값을 무시합니다.|  
|SQL_FETCH_LAST|결과 집합에서 마지막 전체 행 집합을 반환합니다.<br /><br /> **SQLFetchScroll는** *FetchOffset*의 값을 무시합니다.|  
|SQL_FETCH_BOOKMARK|SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 의해 지정된 책갈피에서 행 집합 FetchOffset 행을 반환합니다.|  
  
 드라이버가 모든 가져오기 방향을 지원할 필요는 없습니다. 응용 프로그램은 **sqlGetInfo를 호출하는** 정보 유형의 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1(커서의 유형에 따라 다름)를 사용하여 드라이버에서 지원하는 가져오기 방향을 결정합니다. 응용 프로그램은 이러한 정보 유형에서 SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE 및 WQL_CA1_BOOKMARK 비트 마스크를 살펴봐야 합니다. 또한 커서가 정방향 전용이고 FetchOrientation이 SQL_FETCH_NEXT 않은 경우 **SQLFetchScroll는 SQLSTATE** HY106(범위를 벗어난 가져오기 형식)을 반환합니다.  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성은 행 집합의 행 수를 지정합니다. **SQLFetchScroll에서** 가져오는 행 집합이 결과 집합의 끝과 겹치는 경우 **SQLFetchScroll는** 부분 행 집합을 반환합니다. 즉, S + R - 1이 L보다 크고, 여기서 S는 인출되는 행 집합의 시작 행이고, R은 행 집합 크기이고, L은 결과 집합의 마지막 행이며, 행 집합의 첫 번째 L - S + 1 행만 유효합니다. 나머지 행은 비어 있으며 SQL_ROW_NOROW 상태입니다.  
  
 **SQLFetchScroll가** 반환된 후 현재 행은 행 집합의 첫 번째 행입니다.  
  
## <a name="cursor-positioning-rules"></a>커서 위치 지정 규칙  
 다음 섹션에서는 FetchOrientation의 각 값에 대한 정확한 규칙을 설명합니다. 이러한 규칙은 다음 표기법에서 사용합니다.  
  
|Notation|의미|  
|--------------|-------------|  
|*시작하기 전에*|블록 커서는 결과 집합이 시작되기 전에 배치됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 시작 전에 있는 경우 **SQLFetchScroll는** SQL_NO_DATA 반환합니다.|  
|*종료 후*|블록 커서는 결과 집합이 끝난 후에 배치됩니다. 새 행 집합의 첫 번째 행이 결과 집합이 끝난 후인 경우 **SQLFetchScroll는** SQL_NO_DATA 반환합니다.|  
|*커로우셋스타트*|현재 행 집합의 첫 번째 행 수입니다.|  
|*마지막 결과행*|결과 집합의 마지막 행 수입니다.|  
|*행셋크기*|행 집합 크기입니다.|  
|*가져오기오프셋*|*FetchOffset* 인수의 값입니다.|  
|*북마크로우*|SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 의해 지정된 책갈피에 해당하는 행입니다.|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작하기 전에*|1|  
|*커로우셋스타트 + 행셋크기*[1] * \<= 마지막결과행*|*커로우셋스타트 + 로우셋크기*[1]|  
|*커로우셋스타트 + 로우셋크기*[1]*> 마지막결과행*|*종료 후*|  
|*종료 후*|*종료 후*|  
  
 [1] 행을 가져오기 위해 이전 호출 이후 행 집합 크기가 변경된 경우 이전 호출과 함께 사용된 행 집합 크기입니다.  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*시작하기 전에*|*시작하기 전에*|  
|*커로우셋스타트 = 1*|*시작하기 전에*|  
|*1 < 커로우셋스타트 <= 로우셋크기* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*커로우셋스타트 > 로우셋크기* <sup>[2]</sup>|*커로우셋스타트 - 로우셋사이즈* <sup>[2]</sup>|  
|*끝 및 마지막결과행 < RowSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*끝 및 마지막결과 행 >= 행집합 크기* <sup>[2]</sup>|*LastResultRow - 행 크기 + 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll는** SQLSTATE 01S06(결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기 를 시도)을 반환하고 SQL_SUCCESS_WITH_INFO.  
  
 [2] 행을 가져오기 위해 이전 호출 이후 행 집합 크기가 변경된 경우 새 행 집합 크기입니다.  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*(시작하기 전 및 가져오기 > 0) 또는 (종료 후 및 가져오기 오프셋 < 0)*|*--*<sup>[1]</sup>|  
|*시작하기 전 및 가져오기 <= 0*|*시작하기 전에*|  
|*커로우셋스타트 = 1 및 페치오프오프셋 < 0*|*시작하기 전에*|  
|*CurrRowsetstart > 1 및 CurrRowsetStart + 가져오기 < 1 및 &#124; 가져오기 &#124; > RowsetSize* <sup>[3]</sup>|*시작하기 전에*|  
|*CurrRowsetStart > 1 및 CurrRowsetStart + 가져오기 < 1 및 &#124; 가져오기 &#124; <= RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= 커로우셋스타트 \<+ 페치오프셋 = LastResultRow*|*커로우셋스타트 + 페치오프셋*|  
|*커로우셋스타트 + 페치오프> 라스트결과로우*|*종료 후*|  
|*끝 및 가져오기 오프셋 >= 0 이후*|*종료 후*|  
  
 [1] ***SQLFetchScroll는*** SQL_FETCH_ABSOLUTE FetchOrientation 을 사용하여 호출된 것과 동일한 행 집합을 반환합니다. 자세한 내용은 "SQL_FETCH_ABSOLUTE" 섹션을 참조하십시오.  
  
 [2] **SQLFetchScroll는** SQLSTATE 01S06(결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기 를 시도)을 반환하고 SQL_SUCCESS_WITH_INFO.  
  
 [3] 행을 가져오기 위해 이전 호출 이후 행 집합 크기가 변경된 경우 새 행 집합 크기입니다.  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*fetchoffset < 0 및 &#124; 가져오기 &#124; <= LastResultRow*|*마지막 결과행 + 가져오기 오프셋 + 1*|  
|*Fetchoffset < 0 및 &#124; 가져 오기 &#124; > LastResultRow 및 &#124; &#124; > RowsetSize* <sup>[2]</sup>|*시작하기 전에*|  
|*Fetchoffset < 0 및 &#124; 가져 오기 &#124; > 마지막 결과행 및 &#124; 가져오기 &#124; <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*가져오기 오프셋 = 0*|*시작하기 전에*|  
|*1 <= \<가져오기 오프셋 = 마지막 결과행*|*가져오기오프셋*|  
|*가져오기오프셋 > 마지막결과행*|*종료 후*|  
  
 [1] **SQLFetchScroll는** SQLSTATE 01S06(결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기 를 시도)을 반환하고 SQL_SUCCESS_WITH_INFO.  
  
 [2] 행을 가져오기 위해 이전 호출 이후 행 집합 크기가 변경된 경우 새 행 집합 크기입니다.  
  
 동적 커서의 행 위치가 결정되지 않으므로 동적 커서에 대해 수행되는 절대 가져오기는 필요한 결과를 제공할 수 없습니다. 이러한 작업은 먼저 가져오기 다음에 상대 가져오기와 동일합니다. 정적 커서에서 절대 가져오기와 마찬가지로 원자성 연산이 아닙니다.  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*임의*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*행 집합크기* <sup>[1]</sup> <= 마지막결과행|*LastResultRow - 행 크기 + 1* <sup>[1]</sup>|  
|*행셋크기* <sup>[1]</sup> > 마지막결과행|*1*|  
  
 [1] 행을 가져오기 위해 이전 호출 이후 행 집합 크기가 변경된 경우 새 행 집합 크기입니다.  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 다음 규칙이 적용됩니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|*북마크로우 + 가져오기 < 1*|*시작하기 전에*|  
|*1 <= 북마크로우 \<+ 가져오기 = 마지막 결과행*|*책갈피행 + 가져오기오프셋*|  
|*북마크로우 + 페치오프> 라스트결과로우*|*종료 후*|  
  
 책갈피(ODBC)에 대한 자세한 내용은 [북마크(ODBC)를](../../../odbc/reference/develop-app/bookmarks-odbc.md)참조하십시오.  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>커서 이동에 대한 삭제, 추가 및 오류 행의 효과  
 정적 및 키집합 기반 커서는 결과 집합에 추가된 행을 검색하고 결과 집합에서 삭제된 행을 제거합니다. **sqlGetInfo를** SQL_STATIC_CURSOR_ATTRIBUTES2 및 SQL_KEYSET_CURSOR_ATTRIBUTES2 옵션으로 호출하고 SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS 및 SQL_CA2_SENSITIVITY_UPDATES 비트 마스크를 살펴보면 응용 프로그램은 특정 드라이버에서 구현한 커서가 이 작업을 수행하는지 여부를 결정합니다. 삭제된 행을 검색하고 제거할 수 있는 드라이버의 경우 다음 단락에서는 이 동작의 영향을 설명합니다. 삭제된 행을 검색할 수 있지만 제거할 수 없는 드라이버의 경우 삭제는 커서 이동에 영향을 주지 않으며 다음 단락은 적용되지 않습니다.  
  
 커서가 결과 집합에 추가된 행을 검색하거나 결과 집합에서 삭제된 행을 제거하는 경우 데이터를 가져올 때만 이러한 변경 내용을 감지하는 것처럼 나타납니다. 여기에는 **SQLFetchScroll가** FetchOrientation을 SQL_FETCH_RELATIVE 로 설정하고 FetchOffset을 0으로 설정하여 동일한 행 집합을 다시 가져오는 경우를 포함하지만, SQLSetPos가 fOption을 사용하여 호출되는 경우는 SQL_REFRESH. 후자의 경우 행 집합 버퍼의 데이터는 새로 고쳐지지만 다시 가져오지 않으며 삭제된 행은 결과 집합에서 제거되지 않습니다. 따라서 행이 현재 행 집합에서 삭제되거나 현재 행 집합에 삽입되면 커서가 행 집합 버퍼를 수정하지 않습니다. 대신 이전에 삭제된 행을 포함하거나 삽입된 행을 포함하는 행 집합을 가져올 때 변경 사항을 검색합니다.  
  
 다음은 그 예입니다.  
  
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
  
 **SQLFetchScroll** 현재 행 집합에 대 한 위치를 가지고 있는 새 행 집합을 반환 하는 경우-즉, FetchOrientation SQL_FETCH_NEXT, SQL_FETCH_PRIOR 또는 SQL_FETCH_RELATIVE-새 행 집합의 시작 위치를 계산할 때 현재 행 집합에 대 한 변경 내용을 포함 하지 않습니다. 그러나 현재 행 집합을 검색할 수 있는 경우 현재 행 집합 외부의 변경 내용이 포함됩니다. 또한 **SQLFetchScroll현재** 행 집합과 독립적인 위치가 있는 새 행 집합(즉, FetchOrientation이 SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE 또는 SQL_FETCH_BOOKMARK)을 반환하는 경우 현재 행 집합에 있더라도 검색할 수 있는 모든 변경 내용이 포함됩니다.  
  
 새로 추가된 행이 현재 행 집합 내부 또는 외부에 있는지 여부를 결정할 때 부분 행 집합은 마지막 유효한 행에서 끝나는 것으로 간주됩니다. 즉, 행 상태가 SQL_ROW_NOROW 않은 마지막 행입니다. 예를 들어 커서가 새로 추가된 행을 검색할 수 있고 현재 행 집합이 부분 행 집합이고 응용 프로그램이 새 행을 추가하고 커서가 결과 집합의 끝에 이러한 행을 추가한다고 가정합니다. 응용 프로그램에서 FetchOrientation를 SQL_FETCH_NEXT 설정한 **SQLFetchScroll를** 호출하는 경우 **SQLFetchScroll는** 새로 추가된 첫 번째 행부터 행 집합을 반환합니다.  
  
 예를 들어 현재 행 집합이 행 21~30으로 구성되고 행 집합 크기가 10이고 커서가 결과 집합에서 삭제된 행을 제거하고 커서가 결과 집합에 추가된 행을 검색한다고 가정합니다. 다음 표에서는 다양한 상황에서 **SQLFetchScroll가** 반환하는 행을 보여 준다.  
  
|변경|가져오기 유형|가져오기오프셋|새 행 집합[1]|  
|------------|----------------|-----------------|---------------------|  
|행 삭제 21|NEXT|0|31 ~ 40|  
|행 삭제 31|NEXT|0|32 ~ 41|  
|행 21과 22 사이에 행 삽입|NEXT|0|31 ~ 40|  
|행 30과 31 사이에 행 삽입|NEXT|0|삽입된 행, 31 ~ 39|  
|행 삭제 21|PRIOR|0|11 -20|  
|행 삭제 20|PRIOR|0|10 -19|  
|행 21과 22 사이에 행 삽입|PRIOR|0|11 -20|  
|행 20과 21 사이에 행 삽입|PRIOR|0|12 ~ 20, 삽입된 행|  
|행 삭제 21|RELATIVE|0|22 ~ 31<sup>[2]</sup>|  
|행 삭제 21|RELATIVE|1|22 ~ 31|  
|행 21과 22 사이에 행 삽입|RELATIVE|0|21, 삽입된 행, 22 ~ 29|  
|행 21과 22 사이에 행 삽입|RELATIVE|1|22 ~ 31|  
|행 삭제 21|ABSOLUTE|21|22 ~ 31<sup>[2]</sup>|  
|행 삭제 22|ABSOLUTE|21|21, 23 ~ 31|  
|행 21과 22 사이에 행 삽입|ABSOLUTE|22|삽입된 행, 22 ~ 29|  
  
 [1] 이 열은 행이 삽입되거나 삭제되기 전에 행 번호를 사용합니다.  
  
 [2] 이 경우 커서는 행 21부터 시작하는 행을 반환하려고 시도합니다. 행 21이 삭제되었기 때문에 반환되는 첫 번째 행은 행 22입니다.  
  
 오류 행(즉, SQL_ROW_ERROR 상태가 있는 행)은 커서 이동에 영향을 주지 않습니다. 예를 들어 현재 행 집합이 행 11로 시작하고 행 11의 상태가 SQL_ROW_ERROR 경우 FetchOrientation을 사용하여 **SQLFetchScroll를** SQL_FETCH_RELATIVE 설정하고 FetchOffset을 5로 설정하면 행 11의 상태가 SQL_SUCCESS 것처럼 행 집합이 16으로 시작됩니다.  
  
## <a name="returning-data-in-bound-columns"></a>바운드 열의 데이터 반환  
 **SQLFetchScroll는** **SQLFetch**와 동일한 방식으로 바인딩된 열의 데이터를 반환합니다. 자세한 내용은 [SQLFetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"바인딩된 열의 데이터 반환"을 참조하십시오.  
  
 바인딩된 열이 없는 경우 **SQLFetchScroll는** 데이터를 반환하지 않지만 블록 커서를 지정된 위치로 이동합니다. **SQLGetData를** 사용하여 블록 커서의 언바운드 열에서 데이터를 검색할 수 있는지 여부는 드라이버에 따라 다릅니다. **SQLGetInfo에** 대 한 호출 SQL_GETDATA_EXTENSIONS 정보 형식에 대 한 SQL_GD_BLOCK 비트를 반환 하는 경우이 기능을 지원 됩니다.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 **SQLFetchScroll는** 동일한 수식을 사용하여 **SQLFetch**. 자세한 내용은 [SQLBindCol 함수의](../../../odbc/reference/syntax/sqlbindcol-function.md)"버퍼 주소"를 참조하십시오.  
  
## <a name="row-status-array"></a>행 상태 배열  
 **SQLFetchScroll는 SQLFetch와** 동일한 방식으로 행 상태 배열의 값을 설정합니다. 자세한 내용은 [SQLFetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"행 상태 배열"을 참조하십시오.  
  
## <a name="rows-fetched-buffer"></a>행 가져온 버퍼  
 **SQLFetchScroll는** **SQLFetch와**동일한 방식으로 가져온 행에서 가져온 행 수를 반환합니다. 자세한 내용은 [SQLFetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"행 가져온 버퍼"를 참조하십시오.  
  
## <a name="error-handling"></a>오류 처리  
 응용 프로그램이 ODBC 3.x 드라이버에서 **SQLFetchScroll를** 호출하면 드라이버 관리자는 드라이버에서 **SQLFetchScroll을** 호출합니다. 응용 프로그램이 ODBC 2.x 드라이버에서 **SQLFetchScroll를** 호출하면 드라이버 관리자는 드라이버에서 SQLExtendedFetch를 호출합니다. **SQLFetchScroll** 및 SQLExtendedFetch 약간 다른 방식으로 오류를 처리 하기 때문에 응용 프로그램은 ODBC 2.x 및 ODBC 3.x 드라이버에서 **SQLFetchScroll를** 호출할 때 약간 다른 오류 동작을 보습니다.  
  
 **SQLFetchScroll는 SQLFetch와** 동일한 방식으로 **SQLFetch**오류 및 경고를 반환합니다. 자세한 내용은 **SQLFetch의**"오류 처리"를 참조하십시오. **SQLExtendedFetch는** 다음과 같은 예외를 제외하고 **SQLFetch와**동일한 방식으로 오류를 반환합니다.  
  
 행 집합의 특정 행에 적용되는 경고가 발생하면 SQLExtendedFetch는 행 상태 배열의 해당 항목을 SQL_ROW_SUCCESS_WITH_INFO 아닌 SQL_ROW_SUCCESS 설정합니다.  
  
 행 집합의 모든 행에서 오류가 발생하는 경우 SQLExtendedFetch는 SQL_ERROR 아닌 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 개별 행에 적용되는 각 상태 레코드 그룹에서 SQLExtendedFetch에서 반환되는 첫 번째 상태 레코드에는 SQLSTATE 01S01(행의 오류)이 포함되어야 합니다. **SQLFetchScroll이** SQLSTATE를 반환 하지 않습니다. SQLExtendedFetch 추가 SQLSTATE를 반환할 수 없는 경우 이 SQLSTATE를 반환해야 합니다.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetch스크롤 및 낙관적 동시성  
 커서가 낙관적 동시성(즉, SQL_ATTR_CONCURRENCY 문 특성의 값을 SQL_CONCUR_VALUES 또는 SQL_CONCUR_ROWVER 경우 **SQLFetchScroll는** 데이터 원본에서 사용되는 낙관적 동시성 값을 업데이트하여 행이 변경되었는지 여부를 검색합니다. 이 문제는 **SQLFetchScroll가** 현재 행 집합을 다시 가져오는 경우를 포함하여 새 행 집합을 가져올 때마다 발생합니다. (FetchOrientation SQL_FETCH_RELATIVE 설정 하 고 FetchOffset 0으로 설정 하 고 호출 됩니다.  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetch스크롤 및 ODBC 2.x 드라이버  
 응용 프로그램이 ODBC 2.x 드라이버에서 **SQLFetchScroll를** 호출하면 드라이버 관리자는 이 호출을 **SQLExtendedFetch**에 매핑합니다. **SQLExtendedFetch의**인수에 대해 다음 값을 전달합니다.  
  
|SQLExtendedFetch 인수|값|  
|-------------------------------|-----------|  
|명령문 핸들|**SQLFetch스크롤에서**문 핸들 처리 .|  
|페치 방향|**SQLFetch스크롤의**방향 가져오기 .|  
|가져오기오프셋|FetchOrientation SQL_FETCH_BOOKMARK 않은 경우 **SQLFetchScroll에서** FetchOffset 인수의 값이 사용 됩니다.<br /><br /> FetchOrientation가 SQL_FETCH_BOOKMARK 경우 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 의해 지정된 주소에 저장된 값이 사용됩니다.|  
|행카운트Ptr|SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 의해 지정된 주소입니다.|  
|행 상태 배열|SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정된 주소입니다.|  
  
 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [커서 블록, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 참조하십시오.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>설명자 및 SQLFetch스크롤  
 **SQLFetchScroll** 는 **SQLFetch**와 동일한 방식으로 설명자와 상호 작용합니다. 자세한 내용은 [SQLFetch 함수의](../../../odbc/reference/syntax/sqlfetch-function.md)"설명자 및 SQLFetchScroll" 섹션을 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 [열 별 바인딩,](../../../odbc/reference/develop-app/column-wise-binding.md) [행 별 바인딩,](../../../odbc/reference/develop-app/row-wise-binding.md) [위치 업데이트 및 삭제 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)및 [SQLSetPos를 통해 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|대량 삽입, 업데이트 또는 삭제 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|명령문에서 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 결과 집합의 데이터 업데이트 또는 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
