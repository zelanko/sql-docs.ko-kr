---
title: SQLFetch 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285973"
---
# <a name="sqlfetch-function"></a>SQLFetch 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLFetch는** 결과 집합에서 다음 데이터 행 집합을 가져오고 바인딩된 모든 열에 대한 데이터를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLFetchSQL_ERROR** 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *SQL_HANDLE_STMT 핸들 유형* 및 *문 핸들*핸들을 사용하는 *Handle* [SQLGetDiagRec 함수를](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLFetch에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR. 단일 열에서 오류가 발생하는 경우 [SQLGetDiagField는](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) SQL_DIAG_COLUMN_NUMBER *DiagIdentifier를* 사용하여 호출하여 오류가 발생한 열을 확인할 수 있습니다. **및 SQLGetDiagField는** 해당 열이 포함된 행을 결정하기 위해 SQL_DIAG_ROW_NUMBER *DiagIdentifier를* 사용하여 호출할 수 있습니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환할 수 있는 모든 SQLSTAT(01xxx SQLSTAT)에 대해 하나 이상의 오류가 발생하는 경우 SQL_SUCCESS_WITH_INFO 반환되지만 전부는 아니지만 다중 행 작업의 행이 반환되고 단일 행 작업에서 오류가 발생하면 SQL_ERROR 반환됩니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|열에 대해 반환된 문자열 또는 이진 데이터는 비공백 문자 또는 NULL이 아닌 이진 데이터의 잘림을 초래했습니다. 문자열 값인 경우 오른쪽 잘린 값입니다.|  
|01S01|행의 오류|하나 이상의 행을 가져오는 동안 오류가 발생했습니다.<br /><br /> ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버로 작업할 때 이 SQLSTATE가 반환되는 경우 무시할 수 있습니다.|  
|01S07|분수 잘림|열에 대해 반환된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|결과 집합에서 열의 데이터 값을 **SQLBindCol**에서 *TargetType에* 의해 지정된 데이터 유형으로 변환할 수 없습니다.<br /><br /> 열 0은 SQL_C_BOOKMARK 데이터 유형으로 바인딩되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성은 SQL_UB_VARIABLE 설정되었습니다.<br /><br /> 열 0은 데이터 형식의 SQL_C_VARBOOKMARK 바인딩되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되지 않았습니다.|  
|07009|잘못된 설명자 인덱스|드라이버는 **SQLExtendedFetch를**지원하지 않는 ODBC 2 *.x* 드라이버이고 열바인딩에 지정된 열 번호는 0입니다.<br /><br /> 열 0이 바인딩되었고 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22001|문자열 데이터, 오른쪽 잘린|열에 대해 반환된 가변 길이 책갈피가 잘렸습니다.|  
|22002|표시기 변수가 필요하지만 제공되지 않음|NULL 데이터는 **SQLBindCol(또는** **SQLSetDescField** 또는 **SQLSetDescRec에서**설정한 SQL_DESC_INDICATOR_PTR)에 의해 설정된 *StrLen_or_IndPtr* null 포인터인 열로 가져옵니다.|  
|22003|범위를 벗어난 숫자 값|숫자 값을 하나 이상의 바인딩된 열에 대해 숫자 또는 문자열로 반환하면 숫자의 전체(분수와 반대)가 잘리게 됩니다.<br /><br /> 자세한 내용은 부록 D: 데이터 [형식의 SQL에서 C 데이터 유형으로 데이터 변환을](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 참조하십시오.|  
|22007|잘못된 날짜 시간 형식|결과 집합의 문자 열은 날짜, 시간 또는 타임스탬프 C 구조에 바인딩되었으며 열의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다.|  
|22012|0으로 나누기|산술 식의 값이 반환되어 0으로 분할됩니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 SQL 형식에서 간격 C 유형으로 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> 간격 C 유형으로 데이터를 가져올 때 간격 C 형식에서 SQL 형식의 값에 대한 표현이 없었습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|결과 집합의 문자 열은 문자 C 버퍼에 바인딩되었으며 열에는 버퍼의 문자 집합에 표현이 없는 문자가 포함되어 있습니다.<br /><br /> C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행 된 상태에 있지만 결과 *집합은 StatementHandle*.|  
|40001|직렬화 실패|교착 상태를 방지하기 위해 가져오기가 실행된 트랜잭션이 종료되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. **SQLFetch** 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *문 핸들*에서 호출되었습니다. 그런 다음 **SQLFetch** 함수는 *문 핸들에서*다시 호출되었습니다.<br /><br /> 또는 **SQLFetch** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLFetch** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect,** **SQLExecute** 또는 카탈로그 함수를 먼저 호출하지 않고 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) **SQLFetch는** **SQLExtendedFetch가** 호출되고 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 전에 *문 핸들에* 대 한 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|SQL_ATTR_USE_BOOKMARK 문 특성은 SQL_UB_VARIABLE 설정되었으며 열 0은 길이가 이 결과 집합의 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩되었습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol,** **SQLColAttribute**또는 **SQLGetDescField를**호출하여 얻을 수 있습니다.|  
|HY107|범위를 벗어난 행 값|SQL_ATTR_CURSOR_TYPE 문 특성으로 지정된 값은 SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_KEYSET_SIZE 문 특성으로 지정된 값이 0보다 크고 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 지정된 값보다 작습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 **SQLBindCol의** *TargetType과* 해당 열의 SQL 데이터 형식의 조합으로 지정된 변환을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 요청된 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 SQL_ATTR_QUERY_TIMEOUT SQLSetStmtAttr을 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLFetch는** 결과 집합에서 다음 행 집합을 반환합니다. 결과 집합이 있는 동안에만 호출할 수 있습니다. 바인딩된 열이 있으면 해당 열의 데이터를 반환합니다. 응용 프로그램에서 행 상태 배열에 대한 포인터또는 가져온 행 수를 반환하는 버퍼를 지정한 경우 **SQLFetch도** 이 정보를 반환합니다. **SQLFetch에** 대한 호출은 **SQLFetchScroll** 호출과 혼합할 수 있지만 **SQLExtendedFetch**에 대한 호출과 혼합할 수 없습니다. 자세한 내용은 [데이터 행 가져오기](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)를 참조하십시오.  
  
 ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버와 함께 작동하는 경우 드라이버 관리자는 **SQLExtendedFetch를** 지원하는 ODBC 2 *.x* 드라이버에 대해 **SQLExtendedFetch** 호출을 매핑합니다. **SQLExtendedFetch** ODBC*2.x* 드라이버가 **SQLExtendedFetch를**지원하지 않는 경우 드라이버 관리자는 ODBC 2 *.x* 드라이버에서 **SQLFetch** 호출을 매핑하여 단일 행만 가져올 수 있습니다. **SQLFetch**  
  
 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [커서 블록, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 참조하십시오.  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합이 만들어지면 커서는 결과 집합이 시작되기 전에 배치됩니다. **SQLFetch는** 다음 행 집합을 가져옵니다. *이는 fetchOrientation이* SQL_FETCH_NEXT 설정된 **SQLFetchScroll를** 호출하는 것과 같습니다. 커서에 대한 자세한 내용은 [커서](../../../odbc/reference/develop-app/cursors.md) 및 [블록 커서를](../../../odbc/reference/develop-app/block-cursors.md)참조하십시오.  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성은 행 집합의 행 수를 지정합니다. **SQLFetch에서** 가져오는 행 집합이 결과 집합의 끝과 겹치는 경우 **SQLFetch는** 부분 행 집합을 반환합니다. 즉, S + R - 1이 L보다 크고, 여기서 S는 인출되는 행 집합의 시작 행이고, R은 행 집합 크기이고, L은 결과 집합의 마지막 행이며, 행 집합의 첫 번째 L - S + 1 행만 유효합니다. 나머지 행은 비어 있으며 SQL_ROW_NOROW 상태입니다.  
  
 **SQLFetch가** 반환된 후 현재 행은 행 집합의 첫 번째 행입니다.  
  
 다음 표에 나열된 규칙은 이 섹션의 두 번째 테이블에 나열된 조건을 기반으로 **SQLFetch를**호출한 후 커서 위치를 설명합니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|시작하기 전에|1|  
|*커로우셋스타트* \< =  *마지막결과행 - 행셋크기*[1]|*커로우셋스타트* + *로우셋크기*[2]|  
|*커로우셋스타트* > *마지막결과행 - 행셋크기*[1]|종료 후|  
|종료 후|종료 후|  
  
 [1] 가져오기 간에 행 집합 크기가 변경된 경우 이전 가져오기와 함께 사용된 행 집합 크기입니다.  
  
 [2] 가져오기 간에 행 집합 크기가 변경된 경우 새 가져오기와 함께 사용된 행 집합 크기입니다.  
  
|Notation|의미|  
|--------------|-------------|  
|시작하기 전에|블록 커서는 결과 집합이 시작되기 전에 배치됩니다. 새 행 집합의 첫 번째 행이 결과 집합의 시작 전에 있는 경우 **SQLFetch는** SQL_NO_DATA 반환합니다.|  
|종료 후|블록 커서는 결과 집합이 끝난 후에 배치됩니다. 새 행 집합의 첫 번째 행이 결과 집합이 끝난 후인 경우 **SQLFetch는** SQL_NO_DATA 반환합니다.|  
|*커로우셋스타트*|현재 행 집합의 첫 번째 행 수입니다.|  
|*마지막 결과행*|결과 집합의 마지막 행 수입니다.|  
|*행셋크기*|행 집합 크기입니다.|  
  
 예를 들어 결과 집합에 100개의 행이 있고 행 집합 크기가 5라고 가정합니다. 다음 표에서는 다른 시작 위치에 대해 **SQLFetch에서** 반환하는 행 집합 및 반환 코드를 보여 옵니다.  
  
|현재 행 집합|반환 코드|새 행 집합|가져온 행의 #|  
|--------------------|-----------------|----------------|------------------------|  
|시작하기 전에|SQL_SUCCESS|1에서 5까지|5|  
|1에서 5까지|SQL_SUCCESS|6 ~ 10|5|  
|52 - 56|SQL_SUCCESS|57 - 61|5|  
|91 - 95|SQL_SUCCESS|96 ~ 100|5|  
|93 - 97|SQL_SUCCESS|98 ~ 100. 행 상태 배열의 행 4와 5는 SQL_ROW_NOROW 설정됩니다.|3|  
|96 ~ 100|SQL_NO_DATA|없음|0|  
|99 ~ 100|SQL_NO_DATA|없음|0|  
|종료 후|SQL_NO_DATA|없음|0|  
  
## <a name="returning-data-in-bound-columns"></a>바운드 열의 데이터 반환  
 **SQLFetch각** 행을 반환 할 때 해당 열에 바인딩 된 버퍼의 각 바인딩된 열에 대 한 데이터를 넣습니다. 바인딩된 열이 없는 경우 **SQLFetch는** 데이터를 반환하지 않지만 블록 커서를 앞으로 이동합니다. **SQLGetData**를 사용하여 데이터를 계속 검색할 수 있습니다. 커서가 다중 행 커서(즉, SQL_ATTR_ROW_ARRAY_SIZE 1보다 큰 경우)는 **SQLGetInfo가** *SQL_GETDATA_EXTENSIONS InfoType을* 사용하여 호출될 때 SQL_GD_BLOCK 반환되는 경우에만 **SQLGetData를** 호출할 수 있습니다. (자세한 내용은 [SQLGetData를](../../../odbc/reference/syntax/sqlgetdata-function.md)참조하십시오.)  
  
 행의 각 바인딩된 열에 대해 **SQLFetch는** 다음을 수행합니다.  
  
1.  길이/표시기 버퍼를 SQL_NULL_DATA 설정하고 데이터가 NULL인 경우 다음 열로 진행합니다. 데이터가 NULL이고 길이/표시기 버퍼가 바인딩되지 않은 경우 **SQLFetch는** 행에 대해 SQLSTATE 22002(필요한 표시기 변수는 제공되지 않음)를 반환하고 다음 행으로 진행합니다. 길이/표시기 버퍼의 주소를 확인하는 방법에 대한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "버퍼 주소"를 참조하십시오.  
  
     열의 데이터가 NULL이 아닌 경우 **SQLFetch는** 2단계로 진행됩니다.  
  
2.  SQL_ATTR_MAX_LENGTH 문 특성이 영하지 않은 값으로 설정되고 열에 문자 또는 이진 데이터가 포함되어 있으면 데이터가 바이트SQL_ATTR_MAX_LENGTH 로 잘립니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 명령문 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 일반적으로 네트워크를 통해 데이터를 반환하기 전에 데이터를 트렁크로 하는 데이터 원본에 의해 구현됩니다. 드라이버와 데이터 원본을 지원하기 위해 필요하지 않습니다. 따라서 데이터가 특정 크기로 잘리도록 하려면 응용 프로그램은 해당 크기의 버퍼를 할당하고 **SQLBindCol**에서 *cbValueMax* 인수의 크기를 지정해야 합니다.  
  
3.  **SQLBindCol에서** *TargetType에* 의해 지정된 유형으로 데이터를 변환합니다.  
  
4.  데이터가 문자 또는 이진과 같은 가변 길이 데이터 유형으로 변환된 경우 **SQLFetch는** 데이터 길이가 데이터 버퍼의 길이를 초과하는지 여부를 확인합니다. 문자 데이터의 길이(null-termination 문자 포함)가 데이터 버퍼의 길이를 초과하는 경우 **SQLFetch는** 데이터를 데이터 버퍼의 길이로 축소하여 null-termination 문자의 길이를 줄입니다. 그런 다음 데이터를 null-종료합니다. 이진 데이터의 길이가 데이터 버퍼의 길이를 초과하는 경우 **SQLFetch는** 이를 데이터 버퍼의 길이로 연결합니다. 데이터 버퍼의 길이는 **SQLBindCol**에서 *BufferLength로* 지정됩니다.  
  
     **SQLFetch는** 고정 길이 데이터 유형으로 변환된 데이터를 트렁킨다음을 사용하지 않습니다. 항상 데이터 버퍼의 길이가 데이터 형식의 크기라고 가정합니다.  
  
5.  변환된(및 잘린) 데이터를 데이터 버퍼에 넣습니다. 데이터 버퍼의 주소를 확인하는 방법에 대한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "버퍼 주소"를 참조하십시오.  
  
6.  데이터의 길이를 길이/표시기 버퍼에 넣습니다. 표시기 포인터와 길이 포인터가 모두 동일한 버퍼로 설정된 **경우(SQLBindCol** 호출과 마찬가지로) 길이가 유효한 데이터에 대한 버퍼에 기록되고 SQL_NULL_DATA NULL 데이터에 대한 버퍼에 기록됩니다. 길이/표시기 버퍼가 바인딩되지 않은 경우 **SQLFetch는** 길이를 반환하지 않습니다.  
  
    -   문자 또는 이진 데이터의 경우 데이터 버퍼가 너무 작기 때문에 변환 후 및 잘림 전 의 데이터 길이입니다. 드라이버가 변환 후 데이터의 길이를 확인할 수 없는 경우(예: 긴 데이터의 경우)는 길이를 SQL_NO_TOTAL 설정합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘린 경우 이 특성의 값은 실제 길이 대신 길이/표시기 버퍼에 배치됩니다. 이 특성은 변환 하기 전에 서버에서 데이터를 트러닝 하도록 설계 되었습니다., 그래서 드라이버는 실제 길이 알아낼 수 있는 방법이 없습니다.  
  
    -   다른 모든 데이터 형식의 경우 변환 후 데이터의 길이입니다. 즉, 데이터가 변환된 형식의 크기입니다.  
  
     길이/표시기 버퍼의 주소를 확인하는 방법에 대한 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)의 "버퍼 주소"를 참조하십시오.  
  
7.  상당한 자릿수의 손실 없이 변환 하는 동안 데이터가 잘린 경우 (예를 들어, 실제 숫자 1.234 변환 될 때 정수 1에 잘리다), **SQLFetch** 반환 SQLSTATE 01S07 (분수 잘림) 및 SQL_SUCCESS_WITH_INFO. 데이터 버퍼의 길이가 너무 작기 때문에 데이터가 잘린 경우(예: 문자열 "abcdef"가 4바이트 버퍼에 배치됨) **SQLFetch는** SQLSTATE 01004(데이터 잘린 데이터)를 반환하고 SQL_SUCCESS_WITH_INFO. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘린 경우 **SQLFetch는** SQL_SUCCESS 반환하고 SQLSTATE 01S07(분수 잘림) 또는 SQLSTATE 01004(데이터가 잘린 데이터)를 반환하지 않습니다. 상당한 자릿수의 손실로 변환 하는 동안 데이터가 잘린 경우 (예를 들어, 100,000 보다 큰 SQL_INTEGER 값이 SQL_C_TINYINT 변환 된 경우), **SQLFetch** 반환 SQLSTATE 22003 (숫자 값 범위를 벗어났습니다) 및 SQL_ERROR (행 집합 크기가 1) 또는 SQL_SUCCESS_WITH_INFO (행 집합 크기가 1 보다 큰 경우).  
  
 **SQLFetch** 또는 **SQLFetchScroll가** SQL_SUCCESS 반환하거나 SQL_SUCCESS_WITH_INFO 않는 경우 바인딩된 데이터 버퍼와 길이/표시기 버퍼의 내용은 정의되지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 행 상태 배열은 행 집합의 각 행의 상태를 반환하는 데 사용됩니다. 이 배열의 주소는 SQL_ATTR_ROW_STATUS_PTR 문 특성으로 지정됩니다. 배열은 응용 프로그램에서 할당되며 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정된 만큼의 요소가 있어야 합니다. 해당 값은 **SQLFetch,** **SQLFetchScroll**및 **SQLBulkOperations** 또는 **SQLSetPos에** 의해 설정됩니다(SQLExtendedFetch에 의해 **SQLExtendedFetch**커서가 배치된 후 호출된 경우 제외). SQL_ATTR_ROW_STATUS_PTR 문 특성의 값이 null 포인터인 경우 이러한 함수는 행 상태를 반환하지 않습니다.  
  
 **SQLFetch** 또는 **SQLFetchScroll** SQL_SUCCESS 반환 하지 않는 경우 행 상태 배열 버퍼의 내용은 정의 되지 SQL_SUCCESS SQL_SUCCESS_WITH_INFO.  
  
 다음 값은 행 상태 배열에서 반환됩니다.  
  
|행 상태 배열 값|설명|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 성공적으로 인출되었으며 이 결과 집합에서 마지막으로 가져온 이후 변경되지 않았습니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 성공적으로 인출되었으며 이 결과 집합에서 마지막으로 가져온 이후 변경되지 않았습니다. 그러나 행에 대한 경고가 반환되었습니다.|  
|SQL_ROW_ERROR|행을 가져오는 동안 오류가 발생했습니다.|  
|SQL_ROW_UPDATED[1],[2], [3]|행이 성공적으로 인출되었으며 이 결과 집합에서 마지막으로 가져온 이후 변경되었습니다. 이 결과 집합에서 행을 다시 가져오거나 **SQLSetPos에**의해 새로 고쳐지면 상태가 행의 새 상태로 변경됩니다.|  
|SQL_ROW_DELETED[3]|이 결과 집합에서 마지막으로 가져온 이후 행이 삭제되었습니다.|  
|SQL_ROW_ADDED[4]|행은 **SQLBulkOperations**. 이 결과 집합에서 행을 다시 가져오거나 **SQLSetPos에**의해 새로 고쳐지면 해당 상태가 SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|행 집합은 결과 집합의 끝을 겹치고 행 상태 배열의 이 요소에 해당하는 행이 반환되지 않았습니다.|  
  
 [1] 키집합, 혼합 및 동적 커서의 경우 키 값이 업데이트되면 데이터 행이 삭제되고 새 행이 추가된 것으로 간주됩니다.  
  
 [2] 일부 드라이버는 데이터에 대한 업데이트를 검색할 수 없으므로 이 값을 반환할 수 없습니다. 드라이버가 다시 가져온 행에 대한 업데이트를 검색할 수 있는지 여부를 확인하기 위해 응용 프로그램은 SQL_ROW_UPDATES 옵션을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 [3] **SQLFetch는** **SQLFetchScroll**에 대한 호출과 혼합된 경우에만 이 값을 반환할 수 있습니다. **이는 SQLFetch가** 결과 집합을 통해 앞으로 이동하고 단독으로 사용되는 경우 행을 다시 가져오지 않기 때문입니다. 행이 다시 인출되지 않으므로 **SQLFetch는** 이전에 가져온 행에 대한 변경 내용을 검색하지 않습니다. 그러나 **SQLFetchScroll이전에** 가져온 행에 커서를 배치하고 **SQLFetch가** 해당 행을 가져오는 데 사용되는 경우 **SQLFetch는** 해당 행에 대한 변경 내용을 검색할 수 있습니다.  
  
 [4] SQLBulkOperations에서만 반환됩니다. **SQLFetch** 또는 **SQLFetchScroll에**의해 설정되지 않았습니다.  
  
### <a name="rows-fetched-buffer"></a>행 가져온 버퍼  
 인출된 행 버퍼는 가져오는 동안 오류가 발생했기 때문에 데이터가 반환되지 않은 행을 포함하여 가져온 행 수를 반환하는 데 사용됩니다. 즉, 행 상태 배열의 값이 SQL_ROW_NOROW 않은 행 수입니다. 이 버퍼의 주소는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성으로 지정됩니다. 버퍼는 응용 프로그램에 의해 할당됩니다. **SQLFetch** 및 **SQLFetchScroll에**의해 설정됩니다. SQL_ATTR_ROWS_FETCHED_PTR 문 특성의 값이 null 포인터인 경우 이러한 함수는 가져온 행 수를 반환하지 않습니다. 결과 집합에서 현재 행의 수를 확인 하려면 응용 프로그램에서 SQL_ATTR_ROW_NUMBER 특성으로 **SQLGetStmtAttr을** 호출할 수 있습니다.  
  
 SQL_NO_DATA 반환되는 경우를 **제외하고, SQLFetch** 또는 **SQLFetchScroll가** SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 반환하지 않는 경우 가져온 행 버퍼의 내용은 정의되지 SQL_NO_DATA.  
  
### <a name="error-handling"></a>오류 처리  
 오류 및 경고는 개별 행 또는 전체 함수에 적용할 수 있습니다. 진단 레코드에 대한 자세한 내용은 [진단](../../../odbc/reference/develop-app/diagnostics.md) 및 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)을 참조하십시오.  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>전체 함수의 오류 및 경고  
 SQLSTATE HYT00(시간 제한 만료) 또는 SQLSTATE 24000(잘못된 커서 상태)과 같은 전체 함수에 오류가 있는 경우 **SQLFetch는** SQL_ERROR 및 해당 SQLSTATE를 반환합니다. 행 집합 버퍼의 내용은 정의되지 않으며 커서 위치는 변경되지 않습니다.  
  
 전체 함수에 경고가 적용되는 경우 **SQLFetch는** SQL_SUCCESS_WITH_INFO 및 해당 SQLSTATE를 반환합니다. 전체 함수에 적용되는 경고에 대한 상태 레코드는 개별 행에 적용되는 상태 레코드 앞에 반환됩니다.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>개별 행의 오류 및 경고  
 오류(예: SQLSTATE 22012(0으로 나누기)) 또는 경고(예: SQLSTATE 01004(데이터 잘린 데이터 잘린))가 단일 행에 적용되는 경우 **SQLFetch는**다음을 수행합니다.  
  
-   행 상태 배열의 해당 요소를 오류에 대한 SQL_ROW_ERROR 경고에 대한 SQL_ROW_SUCCESS_WITH_INFO 설정합니다.  
  
-   오류 또는 경고에 대한 SQLSTATEs를 포함하는 0개 이상의 상태 레코드를 추가합니다.  
  
-   상태 레코드에서 행 및 열 번호 필드를 설정합니다. **SQLFetch행** 또는 열 번호를 확인할 수 없는 경우 해당 숫자를 각각 SQL_ROW_NUMBER_UNKNOWN 또는 SQL_COLUMN_NUMBER_UNKNOWN 설정합니다. 상태 레코드가 특정 열에 적용되지 않는 경우 **SQLFetch는** 열 번호를 SQL_NO_COLUMN_NUMBER 설정합니다.  
  
 **SQLFetch는** 행 집합의 모든 행을 가져올 때까지 행을 계속 가져옵니다. 행 집합의 모든 행에서 오류가 발생하지 않는 한 SQL_SUCCESS_WITH_INFO 반환합니다(상태 SQL_ROW_NOROW 있는 행 포함 제외)SQL_ERROR 반환합니다. 특히 행 집합 크기가 1이고 해당 행에서 오류가 발생하면 **SQLFetch가** SQL_ERROR 반환합니다.  
  
 **SQLFetch는** 행 번호 순서로 상태 레코드를 반환합니다. 즉, 알 수 없는 행에 대한 모든 상태 레코드를 반환합니다(있는 경우). 그런 다음 첫 번째 행(있는 경우)에 대한 모든 상태 레코드를 반환한 다음 두 번째 행(있는 경우)에 대한 모든 상태 레코드를 반환합니다. 각 행의 상태 레코드는 상태 레코드 순서를 지정하기 위한 일반 규칙에 따라 정렬됩니다. 자세한 내용은 [SQLGetDiagField의](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)"상태 레코드 시퀀스"를 참조하십시오.  
  
### <a name="descriptors-and-sqlfetch"></a>설명자 및 SQLFetch  
 다음 섹션에서는 **SQLFetch가** 설명자와 상호 작용하는 방법을 설명합니다.  
  
#### <a name="argument-mappings"></a>인수 매핑  
 드라이버는 **SQLFetch**의 인수를 기반으로 설명자 필드를 설정하지 않습니다.  
  
#### <a name="other-descriptor-fields"></a>기타 설명자 필드  
 다음 설명자 필드는 **SQLFetch**에서 사용됩니다.  
  
|설명자 필드|Desc.|필드 인|를 통해 설정|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|Ard|머리글|SQL_ATTR_ROW_ARRAY_SIZE 문 특성|  
|SQL_DESC_ARRAY_STATUS_PTR|Ird|머리글|SQL_ATTR_ROW_STATUS_PTR 문 특성|  
|SQL_DESC_BIND_OFFSET_PTR|Ard|머리글|SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성|  
|SQL_DESC_BIND_TYPE|Ard|머리글|SQL_ATTR_ROW_BIND_TYPE 문 특성|  
|SQL_DESC_COUNT|Ard|머리글|*열수* **SQLBindCol의** 인수|  
|SQL_DESC_DATA_PTR|Ard|레코드|**SQLBindCol의** *대상 값 Ptr* 인수|  
|SQL_DESC_INDICATOR_PTR|Ard|레코드|**SQLBindCol에서** *StrLen_or_IndPtr* 인수|  
|SQL_DESC_OCTET_LENGTH|Ard|레코드|**SQLBindCol의** *버퍼길이* 인수|  
|SQL_DESC_OCTET_LENGTH_PTR|Ard|레코드|**SQLBindCol에서** *StrLen_or_IndPtr* 인수|  
|SQL_DESC_ROWS_PROCESSED_PTR|Ird|머리글|SQL_ATTR_ROWS_FETCHED_PTR 문 특성|  
|SQL_DESC_TYPE|Ard|레코드|**SQLBindCol의** *대상 형식* 인수|  
  
 모든 설명자 필드는 **SQLSetDescField**를 통해 설정할 수도 있습니다.  
  
#### <a name="separate-length-and-indicator-buffers"></a>길이 및 표시기 버퍼 분리  
 응용 프로그램은 길이 및 표시기 값을 유지하는 데 사용할 수 있는 단일 버퍼 또는 두 개의 개별 버퍼를 바인딩할 수 있습니다. 응용 프로그램이 **SQLBindCol을**호출하면 드라이버는 ard의 SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_INDICATOR_PTR 필드를 *StrLen_or_IndPtr* 인수에서 전달되는 동일한 주소로 설정합니다. 응용 프로그램이 **SQLSetDescField** 또는 **SQLSetDescRec를**호출할 때 이 두 필드를 다른 주소로 설정할 수 있습니다.  
  
 **SQLFetch는** 응용 프로그램에 별도의 길이 및 표시기 버퍼를 지정했는지 여부를 결정합니다. 이 경우 데이터가 NULL이 아닌 경우 **SQLFetch는** 표시기 버퍼를 0으로 설정하고 길이 버퍼의 길이를 반환합니다. 데이터가 NULL이면 **SQLFetch는** 표시기 버퍼를 SQL_NULL_DATA 설정하며 길이 버퍼를 수정하지 않습니다.  
  
### <a name="code-example"></a>코드 예  
 [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQL열,](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)및 [SQL프로시저를](../../../odbc/reference/syntax/sqlprocedures-function.md)참조하십시오.  
  
### <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|명령문에서 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|데이터 열의 일부 또는 전체 가져오기|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
