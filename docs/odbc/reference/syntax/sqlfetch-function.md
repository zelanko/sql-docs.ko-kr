---
title: SQLFetch 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c5d2d14786080f665e488acf2bfa888f09a5df4
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345204"
---
# <a name="sqlfetch-function"></a>SQLFetch 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlfetch** 는 결과 집합에서 데이터의 다음 행 집합을 인출 하 고 모든 바운드 열에 대 한 데이터를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlfetch** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 *HandleType* SQL_HANDLE_STMT 및 StatementHandle *핸들* 을 사용 하 여 [SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqlfetch** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다. 단일 열에서 오류가 발생 하는 경우 *DiagIdentifier* 의 SQL_DIAG_COLUMN_NUMBER를 사용 하 여 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 를 호출 하 여 오류가 발생 한 열을 확인할 수 있습니다. and **SQLGetDiagField** 는 *DiagIdentifier* of SQL_DIAG_ROW_NUMBER를 호출 하 여 해당 열이 포함 된 행을 확인할 수 있습니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (01xxx SQLSTATEs 제외)를 반환할 수 있는 모든 SQLSTATEs의 경우에는 한 개 이상의 행 작업에 오류가 발생 하는 경우 SQL_SUCCESS_WITH_INFO가 반환 되 고, 다음에 오류가 발생 하면 SQL_ERROR가 반환 됩니다. 단일 행 작업  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|열에 대해 반환 된 문자열 또는 이진 데이터로 인해 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터가 잘렸습니다. 문자열 값인 경우 오른쪽이 잘렸습니다.|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 페치하는 동안 오류가 발생 했습니다.<br /><br /> ODBC*3.x 응용 프로그램* 에서 odbc*2.x 드라이버를* 사용할 때이 SQLSTATE가 반환 되는 경우 무시 해도 됩니다.|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소가 포함 된 시간, 타임 스탬프 및 interval 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 **SQLBindCol**의 *TargetType* 에 지정 된 데이터 형식으로 변환할 수 없습니다.<br /><br /> 열 0은 SQL_C_BOOKMARK의 데이터 형식으로 바인딩되며 SQL_ATTR_USE_BOOKMARKS statement 특성은 SQL_UB_VARIABLE로 설정 되었습니다.<br /><br /> 열 0이 SQL_C_VARBOOKMARK 데이터 형식으로 바인딩 되었으며 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스|드라이버가 **Sqlextendedfetch**를 지원 하지 않고 열에 대해 바인딩에 지정 된 열 번호가 0 인 ODBC*2.x 드라이버 였습니다* .<br /><br /> 열 0이 바인딩되고 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|열에 대해 반환 된 가변 길이 책갈피가 잘렸습니다.|  
|22002|표시기 변수가 필요한 데 제공 되지 않았습니다.|**SQLBindCol** 에 의해 설정 된 *StrLen_or_IndPtr* 또는 **SQLSetDescField** 또는 **SQLSetDescRec**에 의해 설정 된 SQL_DESC_INDICATOR_PTR가 null 포인터인 열로 null 데이터가 인출 되었습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|하나 이상의 바인딩된 열에 대해 숫자 값을 숫자 또는 문자열로 반환 하면 잘린 숫자의 전체 부분이 소수 부분으로 표시 되지 않습니다.<br /><br /> 자세한 내용은 부록 D의 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 을 참조 하세요. 데이터 형식.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|결과 집합의 문자 열이 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되고 열의 값은 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다.|  
|22012|0으로 나누었습니다.|산술 식의 값이 반환 되었으며이로 인해 0으로 나누었습니다.|  
|22015|간격 필드 오버플로입니다.|정확한 숫자 또는 간격 SQL 형식을 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> Interval C 유형에 서 데이터를 인출 하는 경우 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|결과 집합의 문자 열이 문자 C 버퍼에 바인딩되고 버퍼의 문자 집합에 표시 되지 않은 문자가 열에 포함 되어 있습니다.<br /><br /> C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 가 실행 된 상태 이지만 결과 집합이 *StatementHandle*와 연결 되지 않았습니다.|  
|40001|Serialization 오류|반입이 실행 된 트랜잭션이 교착 상태를 방지 하기 위해 종료 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소 됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. **Sqlfetch** 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlfetch** 또는 **sqlcancelhandle** 이 호출 되었습니다. 그런 다음 *StatementHandle*에서 **sqlfetch** 함수를 다시 호출 했습니다.<br /><br /> 또는 **Sqlfetch** 함수를 호출 하 고 실행을 완료 하기 전에 다중 스레드 응용 프로그램의 다른 스레드에서 **Sqlfetch** 또는 **sqlcancelhandle** 이 *StatementHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlfetch** 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE이 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute** 또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA이 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlextendedfetch** 를 호출한 후 SQL_CLOSE 옵션을 사용 하는 **SQLFreeStmt** 가 호출 되기 전에 *StatementHandle* 에 대해 **sqlfetch** 가 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|SQL_ATTR_USE_BOOKMARK statement 특성이 SQL_UB_VARIABLE로 설정 되 고, 열 0이이 결과 집합에 대 한 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩 되었습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol**, **sqlcolattribute**또는 **SQLGetDescField**를 호출 하 여 가져올 수 있습니다.|  
|HY107|행 값이 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE statement 특성에 지정 된 값이 SQL_CURSOR_KEYSET_DRIVEN 이지만 SQL_ATTR_KEYSET_SIZE statement 특성으로 지정 된 값이 0 보다 크고 SQL_ATTR_ROW_ARRAY_에 지정 된 값 보다 작아야 합니다. SIZE 문 특성입니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본은 **SQLBindCol** 의 *TargetType* 조합과 해당 열의 SQL 데이터 형식으로 지정 된 변환을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출에서 SQL_STILL_EXECUTING를 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **Sqlfetch** 는 결과 집합에서 다음 행 집합을 반환 합니다. 결과 집합이 있는 동안에만 호출할 수 있습니다. 즉, 결과 집합을 생성 하는 호출 후와 해당 결과 집합 위에 커서가 닫히도록 합니다. 바인딩된 열이 있으면 해당 열에 있는 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열 또는 인출 된 행 수를 반환할 버퍼에 대 한 포인터를 지정한 경우 **Sqlfetch** 도이 정보를 반환 합니다. Sqlfetch 에 대 한 호출은 **sqlfetchscroll** 에 대 한 호출과 혼합할 수 있지만 **sqlextendedfetch**호출로 혼합할 수 없습니다. 자세한 내용은 [데이터 행 페치](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)를 참조 하세요.  
  
 Odbc*2.x 응용 프로그램이* odbc*2.x 드라이버를* 사용 하 여 작동 하는 경우, 드라이버 관리자는 sqlextendedfetch **를 지 원하는**odbc*2.X 드라이버에* 대 한 **sqlextendedfetch** 에 sqlfetch 호출을 매핑합니다. ODBC*2.x 드라이버가* **sqlextendedfetch**를 지원 하지 않는 경우 드라이버 관리자는 단일 행만 인출할 수 있도록 odbc 2.x 드라이버에서 Sqlfetch **호출을** **sqlfetch** 에 매핑합니다 *.*  
  
 자세한 내용은 [블록 커서, 스크롤 가능 커서 및](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 부록 G의 이전 버전과의 호환성을 참조 하세요. 이전 버전과의 호환성을 위한 드라이버 지침  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합을 만들 때 커서는 결과 집합의 시작 부분 앞에 배치 됩니다. **Sqlfetch** 는 다음 행 집합을 인출 합니다. SQL_FETCH_NEXT로 설정 된 *Fetchorientation* 로 **sqlfetchscroll** 을 호출 하는 것과 같습니다. 커서에 대 한 자세한 내용은 [커서](../../../odbc/reference/develop-app/cursors.md) 및 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)를 참조 하세요.  
  
 SQL_ATTR_ROW_ARRAY_SIZE statement 특성은 행 집합의 행 수를 지정 합니다. **Sqlfetch** 에서 인출 되는 행 집합이 결과 집합의 끝과 겹치면 **sqlfetch** 에서 부분 행 집합을 반환 합니다. 즉, S + R-1이를 초과 하는 경우. 여기서 S는 인출 되는 행 집합의 시작 행이 고, R은 행 집합 크기 이며, L은 결과 집합의 마지막 행입니다. 그러면 행 집합의 첫 번째 L-value + 1 행만 유효 합니다. 나머지 행은 비어 있고 상태는 SQL_ROW_NOROW입니다.  
  
 **Sqlfetch** 가 반환 된 후 현재 행은 행 집합의 첫 번째 행입니다.  
  
 다음 표에 나열 된 규칙에서는이 섹션의 두 번째 테이블에 나열 된 조건에 따라 **Sqlfetch**를 호출한 후의 커서 위치 지정에 대해 설명 합니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|시작 하기 전|1|  
|*CurrRowsetStart* Lastresultrow-RowsetSize [1] \< = |*CurrRowsetStart* + *RowsetSize*[2]|  
|CurrRowsetStart > *lastresultrow-RowsetSize*[1]|종료 후|  
|종료 후|종료 후|  
  
 [1] 인출 사이에 행 집합 크기가 변경 되는 경우 이전 인출에 사용 된 행 집합 크기입니다.  
  
 [2] 인출 사이에 행 집합 크기가 변경 되는 경우 새 인출에 사용 된 행 집합 크기입니다.  
  
|Notation|의미|  
|--------------|-------------|  
|시작 하기 전|블록 커서는 결과 집합의 시작 부분 앞에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 시작 앞에 있으면 **Sqlfetch** 는 SQL_NO_DATA을 반환 합니다.|  
|종료 후|블록 커서는 결과 집합의 끝 뒤에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 끝 뒤에 있는 경우 **Sqlfetch** 는 SQL_NO_DATA을 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합에 있는 첫 번째 행의 번호입니다.|  
|*LastResultRow*|결과 집합에서 마지막 행의 번호입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
  
 예를 들어 결과 집합의 행이 100이 고 행 집합 크기가 5 인 경우 다음 표에서는 다른 시작 위치에 대해 **Sqlfetch** 에서 반환 된 행 집합 및 반환 코드를 보여 줍니다.  
  
|현재 행 집합|반환 코드|새 행 집합|인출 된 행 개수|  
|--------------------|-----------------|----------------|------------------------|  
|시작 하기 전|SQL_SUCCESS|1 ~ 5|5|  
|1 ~ 5|SQL_SUCCESS|6 ~ 10|5|  
|52 ~ 56|SQL_SUCCESS|57 ~ 61|5|  
|91 ~ 95|SQL_SUCCESS|96 ~ 100|5|  
|93 ~ 97|SQL_SUCCESS|98 ~ 100 행 상태 배열의 행 4와 5가 SQL_ROW_NOROW로 설정 됩니다.|3|  
|96 ~ 100|SQL_NO_DATA|없음|0|  
|99 ~ 100|SQL_NO_DATA|없음|0|  
|종료 후|SQL_NO_DATA|없음|0|  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에서 데이터 반환  
 **Sqlfetch** 는 각 행을 반환 하므로 해당 열에 바인딩된 버퍼에 바인딩된 각 열에 대 한 데이터를 저장 합니다. 바인딩되지 않은 열이 있으면 **Sqlfetch** 는 데이터를 반환 하지 않지만 블록 커서를 앞으로 이동 합니다. **SQLGetData**를 사용 하 여 데이터를 계속 검색할 수 있습니다. 커서가 다중 행 커서 인 경우 (즉, SQL_ATTR_ROW_ARRAY_SIZE가 1 보다 큰 경우) *INFOTYPE* SQL_GETDATA_EXTENSIONS를 사용 하 여 **SQLGetInfo** 를 호출 하면 SQL_GD_BLOCK가 반환 되는 경우에만 **SQLGetData** 를 호출할 수 있습니다. (자세한 내용은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)를 참조 하세요.)  
  
 **Sqlfetch** 는 행의 각 바인딩된 열에 대해 다음을 수행 합니다.  
  
1.  길이가/표시기 버퍼를 SQL_NULL_DATA로 설정 하 고 데이터가 NULL 인 경우 다음 열로 진행 합니다. 데이터가 NULL이 고 길이/표시기 버퍼가 바인딩되지 않은 경우 **Sqlfetch** 는 행에 대해 SQLSTATE 22002 (필요한 표시기 변수를 제공 하지 않음)을 반환 하 고 다음 행으로 진행 합니다. 길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "buffer Addresses"를 참조 하십시오.  
  
     열에 대 한 데이터가 NULL이 아닌 경우 **Sqlfetch** 는 2 단계로 진행 됩니다.  
  
2.  SQL_ATTR_MAX_LENGTH statement 특성을 0이 아닌 값으로 설정 하 고 열에 문자 또는 이진 데이터를 포함 하는 경우 데이터가 SQL_ATTR_MAX_LENGTH bytes로 잘립니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH statement 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 일반적으로 데이터 원본에 의해 구현 되며, 네트워크를 통해 반환 하기 전에 데이터를 자릅니다. 드라이버 및 데이터 원본은이를 지 원하는 데 필요 하지 않습니다. 따라서 데이터가 특정 크기로 잘리지 않도록 하기 위해 응용 프로그램은 해당 크기의 버퍼를 할당 하 고 **SQLBindCol**의 *cbValueMax* 인수에 크기를 지정 해야 합니다.  
  
3.  데이터를 **SQLBindCol**의 *TargetType* 에 지정 된 형식으로 변환 합니다.  
  
4.  데이터가 문자 또는 이진 등의 가변 길이 데이터 형식으로 변환 된 경우 **Sqlfetch** 는 데이터 길이가 데이터 버퍼의 길이를 초과 하는지 여부를 확인 합니다. 문자 데이터의 길이 (null 종결 문자 포함)가 데이터 버퍼의 길이를 초과 하는 경우 **Sqlfetch** 는 데이터 버퍼의 길이에서 null 종료 문자의 길이를 뺀 값으로 데이터를 자릅니다. 그런 다음 데이터를 null로 종료 합니다. 이진 데이터의 길이가 데이터 버퍼의 길이를 초과 하는 경우 **Sqlfetch** 는 데이터 버퍼의 길이로 자릅니다. 데이터 버퍼의 길이는 **SQLBindCol**에서 *bufferlength* 로 지정 됩니다.  
  
     **Sqlfetch** 는 고정 길이 데이터 형식으로 변환 된 데이터를 잘리지 않습니다. 데이터 버퍼의 길이는 항상 데이터 형식의 크기 라고 가정 합니다.  
  
5.  변환 되 고 잘린 데이터를 데이터 버퍼에 배치 합니다. 데이터 버퍼의 주소를 확인 하는 방법에 대 한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "buffer Addresses"를 참조 하십시오.  
  
6.  길이/표시기 버퍼에 데이터의 길이를 넣습니다. **SQLBindCol** 에 대 한 호출로 표시기 포인터와 길이 포인터가 모두 동일한 버퍼로 설정 된 경우에는 유효한 데이터에 대 한 길이가 버퍼에 기록 되 고 SQL_NULL_DATA가 NULL 데이터의 버퍼에 기록 됩니다. 길이/표시기 버퍼가 바인딩되지 않은 경우 **Sqlfetch** 는 길이를 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터의 경우 데이터 버퍼가 너무 작기 때문에 변환 후와 잘림 이전의 데이터 길이입니다. 변환 후 드라이버에서 데이터 길이를 확인할 수 없는 경우, 경우에 따라 긴 데이터를 사용 하는 경우 처럼 길이를 SQL_NO_TOTAL로 설정 합니다. SQL_ATTR_MAX_LENGTH statement 특성으로 인해 데이터가 잘린 경우이 특성의 값은 실제 길이 대신 길이/표시기 버퍼에 배치 됩니다. 이 특성은 변환 전에 서버에서 데이터를 잘라내는 것 이므로 드라이버에서 실제 길이를 확인할 수 있는 방법이 없기 때문입니다.  
  
    -   다른 모든 데이터 형식의 경우 변환 후의 데이터 길이입니다. 즉, 데이터가 변환 된 형식의 크기입니다.  
  
     길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "buffer Addresses"를 참조 하십시오.  
  
7.  유효 자릿수가 손실 되지 않은 상태에서 (예를 들어 실수 번호 1.234가 변환 될 때 정수 1로 잘린다) **Sqlfetch** 는 SQLSTATE 01S07 (소수 잘림) 및 SQL_SUCCESS_WITH_INFO를 반환 합니다. 데이터 버퍼 길이가 너무 작기 때문에 데이터가 잘린 경우 (예: "abcdef" 문자열이 4 바이트 버퍼에 배치 되는 경우) **Sqlfetch** 는 SQLSTATE 01004 (데이터 잘림) 및 SQL_SUCCESS_WITH_INFO를 반환 합니다. SQL_ATTR_MAX_LENGTH statement 특성으로 인해 데이터가 잘린 경우 **Sqlfetch** 는 SQL_SUCCESS를 반환 하 고 sqlstate 01S07 (소수 잘림) 또는 sqlstate 01004 (데이터가 잘렸습니다)를 반환 하지 않습니다. 유효 자릿수가 손실 된 경우 (예: 10만 보다 큰 SQL_INTEGER 값이 SQL_C_TINYINT로 변환 된 경우) **Sqlfetch** 는 SQLSTATE 22003 (범위를 벗어난 숫자 값) 및 SQL_ERROR를 반환 합니다 (예: 행 집합 크기가 1) 또는 SQL_SUCCESS_WITH_INFO (행 집합 크기가 1 보다 큰 경우)  
  
 **Sqlfetch** 또는 **SQLFETCHSCROLL** 이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는 경우에는 바인딩된 데이터 버퍼 및 길이/표시기 버퍼의 내용이 정의 되지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 행 상태 배열은 행 집합에 있는 각 행의 상태를 반환 하는 데 사용 됩니다. 이 배열의 주소는 SQL_ATTR_ROW_STATUS_PTR statement 특성으로 지정 됩니다. 배열은 응용 프로그램에 의해 할당 되며 SQL_ATTR_ROW_ARRAY_SIZE statement 특성에 지정 된 것과 같은 수의 요소를 포함 해야 합니다. 해당 값은 Sqlfetch, **Sqlfetchscroll**및 **SQLBulkOperations** 또는 **SQLSetPos** 로 설정 됩니다 (커서가 **sqlextendedfetch**로 배치 된 후에 호출 된 경우 제외). SQL_ATTR_ROW_STATUS_PTR statement 특성의 값이 null 포인터인 경우 이러한 함수는 행 상태를 반환 하지 않습니다.  
  
 **Sqlfetch** 또는 **SQLFETCHSCROLL** 이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 하지 않는 경우 행 상태 배열 버퍼의 내용이 정의 되지 않습니다.  
  
 행 상태 배열에서 반환 되는 값은 다음과 같습니다.  
  
|행 상태 배열 값|설명|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 인출 되었으며이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않았습니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 인출 되었으며이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않았습니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED [1], [2] 및 [3]|행이 인출 되 고이 결과 집합에서 마지막으로 인출 된 후 변경 되었습니다. 이 결과 집합에서 행을 다시 페치 하거나 **SQLSetPos**로 새로 고치면 상태가 행의 새 상태로 변경 됩니다.|  
|SQL_ROW_DELETED[3]|이 결과 집합에서 행이 마지막으로 인출 된 후 행이 삭제 되었습니다.|  
|SQL_ROW_ADDED[4]|**SQLBulkOperations**에 의해 행이 삽입 되었습니다. 이 결과 집합에서 행을 다시 인출 하거나 **SQLSetPos**로 새로 고치면 상태는 SQL_ROW_SUCCESS입니다.|  
|SQL_ROW_NOROW|행 집합은 결과 집합의 끝 부분을 속하는지를 행 상태 배열의이 요소에 해당 하는 행이 반환 되지 않았습니다.|  
  
 [1] 키 집합, 혼합 및 동적 커서의 경우 키 값이 업데이트 되 면 데이터 행이 삭제 된 것으로 간주 되 고 새 행이 추가 된 것으로 간주 됩니다.  
  
 [2] 일부 드라이버는 데이터에 대 한 업데이트를 검색할 수 없으므로이 값을 반환할 수 없습니다. 드라이버가 refetched 형 행의 업데이트를 검색할 수 있는지 여부를 확인 하기 위해 응용 프로그램은 SQL_ROW_UPDATES 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다.  
  
 [3] **Sqlfetch** 는 **sqlfetchscroll**에 대 한 호출과 혼합 되어 있는 경우에만이 값을 반환할 수 있습니다. 이는 **Sqlfetch** 가 결과 집합을 통해 앞으로 이동 하 고 독점적으로 사용 되는 경우는 행을 다시 페치 않기 때문입니다. Refetched 행이 없으므로 **Sqlfetch** 는 이전에 인출 된 행의 변경 내용을 검색 하지 않습니다. 그러나 **Sqlfetchscroll** 이 이전에 인출 된 행 및 **sqlfetch** 를 사용 하 여 해당 행을 인출 하기 전에 커서를 배치 하면 **sqlfetch** 에서 해당 행에 대 한 변경 내용을 검색할 수 있습니다.  
  
 [4]은 (는) SQLBulkOperations에 의해서만 반환 됩니다. **Sqlfetch** 또는 **sqlfetchscroll**에 의해 설정 되지 않았습니다.  
  
### <a name="rows-fetched-buffer"></a>인출 되는 행 버퍼  
 인출 된 버퍼는 인출 하는 동안 오류가 발생 하 여 데이터가 반환 되지 않은 행을 포함 하 여 인출 된 행 수를 반환 하는 데 사용 됩니다. 즉, 행 상태 배열의 값이 SQL_ROW_NOROW 되지 않은 행의 수입니다. 이 버퍼의 주소는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성으로 지정 됩니다. 응용 프로그램에서 버퍼를 할당 합니다. **Sqlfetch** 및 **sqlfetchscroll**에 의해 설정 됩니다. SQL_ATTR_ROWS_FETCHED_PTR statement 특성의 값이 null 포인터인 경우 이러한 함수는 인출 된 행 수를 반환 하지 않습니다. 응용 프로그램은 결과 집합의 현재 행 번호를 확인 하기 위해 SQL_ATTR_ROW_NUMBER 특성으로 **SQLGetStmtAttr** 을 호출할 수 있습니다.  
  
 인출 된 행 버퍼의 내용은 **Sqlfetch** 또는 **SQLFETCHSCROLL** 이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는 경우 정의 되지 않습니다. 단, SQL_NO_DATA가 반환 되는 경우를 제외 하 고 인출 된 행의 값이 0으로 설정 됩니다.  
  
### <a name="error-handling"></a>오류 처리  
 오류 및 경고는 개별 행 또는 전체 함수에 적용 될 수 있습니다. 진단 레코드에 대 한 자세한 내용은 [Diagnostics](../../../odbc/reference/develop-app/diagnostics.md) and [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)을 참조 하세요.  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>전체 함수에 대 한 오류 및 경고  
 SQLSTATE HYT00 (Timeout 만료 됨) 또는 SQLSTATE 24000 (잘못 된 커서 상태)와 같은 전체 함수에 오류가 적용 되는 경우 **Sqlfetch** 는 SQL_ERROR 및 해당 sqlstate를 반환 합니다. 행 집합 버퍼의 내용은 정의 되지 않으며 커서 위치는 변경 되지 않습니다.  
  
 경고가 전체 함수에 적용 되는 경우 **Sqlfetch** 는 SQL_SUCCESS_WITH_INFO 및 해당 SQLSTATE를 반환 합니다. 전체 함수에 적용 되는 경고에 대 한 상태 레코드는 개별 행에 적용 되는 상태 레코드 보다 먼저 반환 됩니다.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>개별 행의 오류 및 경고  
 오류 (예: SQLSTATE 22012 (0으로 나누기)) 또는 경고 (예: SQLSTATE 01004 (데이터 잘림))가 단일 행에 적용 되는 경우 **Sqlfetch**는 다음을 수행 합니다.  
  
-   오류 또는 SQL_ROW_SUCCESS_WITH_INFO에 대 한 SQL_ROW_ERROR 행 상태 배열의 해당 요소를 설정 합니다.  
  
-   오류 또는 경고에 대 한 SQLSTATEs를 포함 하는 상태 레코드를 0 개 이상 추가 합니다.  
  
-   상태 레코드의 행 및 열 번호 필드를 설정 합니다. **Sqlfetch** 에서 행 또는 열 번호를 확인할 수 없는 경우에는 각각 해당 숫자를 SQL_ROW_NUMBER_UNKNOWN 또는 SQL_COLUMN_NUMBER_UNKNOWN로 설정 합니다. 상태 레코드가 특정 열에 적용 되지 않는 경우 **Sqlfetch** 는 열 번호를 SQL_NO_COLUMN_NUMBER로 설정 합니다.  
  
 **Sqlfetch** 는 행 집합의 모든 행을 반입할 때까지 행을 계속 인출 합니다. 행 집합의 모든 행에서 오류가 발생 하지 않는 한 SQL_SUCCESS_WITH_INFO를 반환 합니다 (상태 SQL_ROW_NOROW 행 포함 안 함) .이 경우 SQL_ERROR를 반환 합니다. 특히 행 집합 크기가 1이 고 해당 행에서 오류가 발생 하는 경우 **Sqlfetch** 는 SQL_ERROR을 반환 합니다.  
  
 **Sqlfetch** 는 상태 레코드를 행 번호 순서로 반환 합니다. 즉, 알 수 없는 행 (있는 경우)에 대 한 모든 상태 레코드를 반환 합니다. 그런 다음 첫 번째 행 (있는 경우)에 대 한 모든 상태 레코드를 반환 하 고 두 번째 행 (있는 경우)에 대 한 모든 상태 레코드를 반환 합니다. 각 행에 대 한 상태 레코드는 상태 레코드를 정렬 하는 일반적인 규칙에 따라 정렬 됩니다. 자세한 내용은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "상태 레코드 시퀀스"를 참조 하십시오.  
  
### <a name="descriptors-and-sqlfetch"></a>설명자 및 SQLFetch  
 다음 섹션에서는 **Sqlfetch** 가 설명자와 상호 작용 하는 방법에 대해 설명 합니다.  
  
#### <a name="argument-mappings"></a>인수 매핑  
 이 드라이버는 **Sqlfetch**의 인수를 기반으로 설명자 필드를 설정 하지 않습니다.  
  
#### <a name="other-descriptor-fields"></a>기타 설명자 필드  
 다음 설명자 필드는 **Sqlfetch**에서 사용 됩니다.  
  
|설명자 필드|설명.|필드의|설정|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|카드|헤더|SQL_ATTR_ROW_ARRAY_SIZE statement 특성|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|헤더|SQL_ATTR_ROW_STATUS_PTR statement 특성|  
|SQL_DESC_BIND_OFFSET_PTR|카드|헤더|SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성|  
|SQL_DESC_BIND_TYPE|카드|헤더|SQL_ATTR_ROW_BIND_TYPE statement 특성|  
|SQL_DESC_COUNT|카드|헤더|**SQLBindCol** 의 *columnnumber* 인수|  
|SQL_DESC_DATA_PTR|카드|레코드|**SQLBindCol** 의 *Targetvalueptr* 인수|  
|SQL_DESC_INDICATOR_PTR|카드|레코드|**SQLBindCol** 의 *StrLen_or_IndPtr* 인수|  
|SQL_DESC_OCTET_LENGTH|카드|레코드|**SQLBindCol** 의 *bufferlength* 인수|  
|SQL_DESC_OCTET_LENGTH_PTR|카드|레코드|**SQLBindCol** 의 *StrLen_or_IndPtr* 인수|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|헤더|SQL_ATTR_ROWS_FETCHED_PTR statement 특성|  
|SQL_DESC_TYPE|카드|레코드|**SQLBindCol** 의 *TargetType* 인수|  
  
 **SQLSetDescField**를 통해 모든 설명자 필드를 설정할 수도 있습니다.  
  
#### <a name="separate-length-and-indicator-buffers"></a>별도의 길이 및 표시기 버퍼  
 응용 프로그램은 길이 및 표시기 값을 저장 하는 데 사용할 수 있는 단일 버퍼 또는 두 개의 개별 버퍼를 바인딩할 수 있습니다. 응용 프로그램에서 **SQLBindCol**를 호출 하면 드라이버는 SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_INDICATOR_PTR 필드를 *StrLen_or_IndPtr* 인수에 전달 되는 동일한 주소로 설정 합니다. 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하는 경우이 두 필드를 서로 다른 주소로 설정할 수 있습니다.  
  
 **Sqlfetch** 는 응용 프로그램에서 별도의 길이와 표시기 버퍼를 지정 했는지 여부를 확인 합니다. 이 경우 데이터가 NULL이 아닌 경우 **Sqlfetch** 는 표시기 버퍼를 0으로 설정 하 고 길이 버퍼의 길이를 반환 합니다. 데이터가 NULL 이면 **Sqlfetch** 는 표시기 버퍼를 SQL_NULL_DATA로 설정 하 고 길이 버퍼를 수정 하지 않습니다.  
  
### <a name="code-example"></a>코드 예  
 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)및 [sqlcolumns](../../../odbc/reference/syntax/sqlprocedures-function.md)를 참조 하세요.  
  
### <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|문에서 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|데이터 열의 일부 또는 전체를 가져오는 중|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행을 위한 문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
