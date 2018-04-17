---
title: SQLFetch 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f1d87bc952852df3301d095203f6c94794de795d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfetch-function"></a>SQLFetch 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLFetch** 결과 집합에서 데이터의 다음 행 집합을 인출 하 고 모든 바운드 열에 대 한 데이터를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFetch** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 [SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 와 *HandleType*여의 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLFetch** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다. 하나의 열에 오류가 발생 한 경우 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 호출할 수는 *DiagIdentifier* 의 SQL_DIAG_COLUMN_NUMBER;에서 오류가 발생 하는 열을 확인 하 고  **SQLGetDiagField** 호출할 수는 *DiagIdentifier* 의 해당 열이 포함 된 행을 결정 하는 SQL_DIAG_ROW_NUMBER 합니다.  
  
 다중 행 작업의 하나 또는 더 전부가 아닌 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 되는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|문자열 또는 열에 대해 반환 된 이진 데이터의 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 했습니다. 문자열 값 경우 오른쪽 잘림 없었습니다.|  
|01S01|행 하는 동안 오류가 발생 했습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다.<br /><br /> (이 SQLSTATE 때 ODBC 3에 반환 되 면*.x* 응용 프로그램이 ODBC 2와 작동*.x* 드라이버를 무시할 수 있습니다.)|  
|01S07|일부가 잘렸습니다.|열에 대해 반환 되는 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 interval 데이터 형식에 대 한 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.<br /><br /> 0 열 SQL_C_BOOKMARK의 데이터 형식과 바인딩되며 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 되었습니다.<br /><br /> SQL_C_VARBOOKMARK의 데이터 형식으로 열 0 바인딩 되었습니다 및 SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARKS 문 특성 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|드라이버는 ODBC 2는*.x* 지원 하지 않는 드라이버 **SQLExtendedFetch**, 열에 대 한 바인딩에 지정 된 열 번호는 및입니다.<br /><br /> 열 0, 바인딩되며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터 오른쪽 잘림|열에 대해 반환 되는 다양 한 길이의 책갈피가 잘렸습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지 않았습니다.|NULL 데이터를 가져온 열으로 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** (또는 설정한 SQL_DESC_INDICATOR_PTR **SQLSetDescField** 또는  **SQLSetDescRec**)이 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|숫자 값을 숫자로 또는 하나 이상의 바인딩된 열에 대 한 문자열을 반환 것 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.<br /><br /> 자세한 내용은 참조 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식에서입니다.|  
|22007|잘못 된 날짜/시간 형식|날짜, 시간 또는 타임 스탬프 C 구조에는 문자는 결과 집합 열에에서 바인딩된 되었으며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프.|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 나누기에서 복원 하려고 시도 했습니다 0입니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형으로 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> C 간격 유형으로 데이터를 인출할 때 C 간격 유형에서 SQL 형식의 값으로 표시 되지 했습니다.|  
|22018|캐스트 사양의 문자 값|결과 집합의 문자 열 C 문자 버퍼에 바인딩되며 열 버퍼의 문자 집합에 없는 표현 된 문자를 포함 되었습니다.<br /><br /> 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 C 유형은 열의 SQL 형식을 문자 데이터 형식. 및 열에 값이 바인딩된 C 형식의 올바른 리터럴.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.|  
|40001|Serialization 오류|교착 상태를 방지 하는 페치 실행 된 트랜잭션이 종료 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. **SQLFetch** 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*. 그런 다음 **SQLFetch** 에서 다시 호출 된 함수는 *StatementHandle*합니다.<br /><br /> 또는 **SQLFetch** 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*  다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLFetch** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 호출 하지 않고 호출 된 **SQLExecDirect**, **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **SQLFetch** 에 대해 호출 되었습니다는 *StatementHandle* 후 **SQLExtendedFetch** 호출 하기 전에 **SQLFreeStmt** 는 SQL_와 CLOSE 옵션이 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE로 설정 된 및 0 열이 결과 집합에 대 한 책갈피에 대 한 최대 길이 길이가 없습니다. 버퍼에 바인딩 되었습니다. (이 길이 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수를 호출 하 여 얻을 수 있습니다 **SQLDescribeCol**, **SQLColAttribute**, 또는 **SQLGetDescField**.)|  
|HY107|행 값 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE 문 특성으로 지정 된 값 SQL_CURSOR_KEYSET_DRIVEN만 SQL_ATTR_KEYSET_SIZE 문 특성으로 지정 된 값이 0 보다 크고는 SQL_ATTR_ROW_ARRAY_로 지정 된 값 보다 작음 크기 문 특성입니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 변환의 조합으로 지정 하는 지원 하지 않습니다는 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 제한 시간 SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 **SQLFetch** 결과 집합의 다음 행 집합을 반환 합니다. 결과 집합이 존재 하는 동안에 호출할 수 있습니다: 즉, 결과 집합을 호출한 후에 만들어지는 하 고 결과 집합 위에 커서 앞 닫힙니다. 열에 바인딩된 경우 해당 열에 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열이 또는, 가져온 행 수를 반환 하는 버퍼에 대 한 포인터를 지정 하는 경우 **SQLFetch** 도이 정보를 반환 합니다. 에 대 한 호출이 **SQLFetch** 호출을 혼합할 수 **SQLFetchScroll** 와 함께 혼합할 수 없고 있지만 **SQLExtendedFetch**합니다. 자세한 내용은 참조 [행의 데이터를 인출](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)합니다.  
  
 ODBC 3 경우*.x* 는 ODBC 2와 작동 하는 응용 프로그램*.x* 드라이버, 드라이버 관리자 매핑합니다 **SQLFetch** 에 대 한 호출이 **SQLExtendedFetch** 에 대 한는 ODBC 2*.x* 를 지 원하는 드라이버 **SQLExtendedFetch**합니다. 경우 ODBC 2*.x* 드라이버가 지원 하지 않으면 **SQLExtendedFetch**, 드라이버 관리자 매핑합니다 **SQLFetch** 에 대 한 호출이 **SQLFetch** ODBC 2 *.x* 단일 행만 가져올 수 있는 드라이버입니다.  
  
 자세한 내용은 참조 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
## <a name="positioning-the-cursor"></a>커서 위치 지정  
 결과 집합을 만든 커서 결과 집합을 시작 하기 전에 배치 됩니다. **SQLFetch** 다음 행 집합을 인출 합니다. 호출 하는 것과 같습니다 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_NEXT로 설정 합니다. 커서에 대 한 자세한 내용은 참조 [커서](../../../odbc/reference/develop-app/cursors.md) 및 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)합니다.  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성은 행 집합의 행 수를 지정합니다. 행 집합으로 인출 되는 경우 **SQLFetch** 결과 집합의 끝 겹치는 **SQLFetch** 부분 행 집합을 반환 합니다. 즉, S + R-1 L 보다 큼, 여기서 S는 행 집합의 반입 되 고 R 시작 행 행 집합 크기 이며 L은 마지막 행 결과 집합의 다음 첫 번째 L만 – S + 행 집합의 1 행 경우 유효 합니다. 나머지 행은 빈 이며 SQL_ROW_NOROW의 상태입니다.  
  
 후 **SQLFetch** 현재 행이 행 집합의 첫 번째 행을 반환 합니다.  
  
 다음 표에 나열 된 규칙에 대 한 호출 후 커서 위치를 설명 **SQLFetch**이 섹션의 두 번째 테이블에 나열 된 조건에 따라 합니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|시작 하기 전에|1.|  
|*CurrRowsetStart* \< =  *LastResultRow – RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow – RowsetSize*[1]|종료 후|  
|종료 후|종료 후|  
  
 [1] 행 집합 크기 인출 간에 변경 하는 경우 이전 인출에 사용 된 행 집합 크기입니다.  
  
 [2] 행 집합 크기 인출 간에 변경 하는 경우 새 인출에 사용 된 행 집합 크기입니다.  
  
|표기법|의미|  
|--------------|-------------|  
|시작 하기 전에|블록 커서 결과 집합을 시작 하기 전에 배치 됩니다. 새 행 집합의 첫 번째 행이 결과 집합을 시작 하기 전에 **SQLFetch** SQL_NO_DATA를 반환 합니다.|  
|종료 후|블록 커서 후 집합 결과의 끝에 배치 됩니다. 새 행 집합의 첫 번째 행은 결과 집합의 끝 이후에 경우 **SQLFetch** SQL_NO_DATA를 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합의 첫 번째 행의 수입니다.|  
|*LastResultRow*|결과 집합의 마지막 행의 수입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
  
 예를 들어 결과 집합에 100 개의 행 및 행 집합 크기는 5입니다. 다음 표에서에서 반환 된 행 집합 및 반환 코드를 보여 줍니다. **SQLFetch** 다른 시작 위치에 대 한 합니다.  
  
|현재 행 집합|반환 코드|새 행 집합|행 인출|  
|--------------------|-----------------|----------------|------------------------|  
|시작 하기 전에|SQL_SUCCESS|1 ~ 5|5|  
|1 ~ 5|SQL_SUCCESS|6-10|5|  
|52에 56|SQL_SUCCESS|57-61|5|  
|91 ~ 95|SQL_SUCCESS|96 ~ 100|5|  
|93를 97|SQL_SUCCESS|98에서 100까지. 행의 행 상태 배열이 4 및 5 SQL_ROW_NOROW로 설정 됩니다.|3|  
|96 ~ 100|SQL_NO_DATA|없음|0|  
|99를 100|SQL_NO_DATA|없음|0|  
|종료 후|SQL_NO_DATA|없음|0|  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에 데이터를 반환합니다.  
 으로 **SQLFetch** 반환 각 행에서 해당 열에 바인딩된 버퍼에 바인딩된 각 열에 대 한 데이터를 저장 합니다. 열에 바인딩된 경우 **SQLFetch** 데이터를 반환 하지 않지만 앞으로 블록 커서 이동 합니다. 사용 하 여 데이터를 검색할 수 있습니다 **SQLGetData**합니다. 다중 행 커서는 커서가 있는 경우 (즉, SQL_ATTR_ROW_ARRAY_SIZE가 1 보다 큰) 경우 **SQLGetData** SQL_GD_BLOCK이 반환 하는 경우에 호출할 수 **SQLGetInfo** 로 호출 되는  *정보 항목* SQL_GETDATA_EXTENSIONS입니다. (자세한 내용은 참조 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 행에 바인딩된 각 열에 대 한 **SQLFetch** 다음 작업을 수행 합니다.  
  
1.  길이/표시기 버퍼를 sql_null_data로 설정 하 고 데이터가 NULL 인 경우 다음 열으로 진행 됩니다. 데이터가 NULL이 고 길이/표시기 버퍼 없음, 바인딩된 경우 **SQLFetch** 행에 대 한 SQLSTATE 22002 (지표 변수가 필요 하지만 제공 되지 않은)을 반환 하 고 다음 행으로 진행 됩니다. 길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소" 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
     열에 대 한 데이터 매개 변수가 NULL 이면 **SQLFetch** 2 단계로 진행 됩니다.  
  
2.  SQL_ATTR_MAX_LENGTH 문 특성은 0이 아닌 값으로 설정 하 고 문자 또는 이진 데이터 열을 포함 하는 경우 데이터 SQL_ATTR_MAX_LENGTH 바이트로 잘립니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 문 특성은 네트워크 트래픽이 감소 하는 데 사용 됩니다. 일반적으로 네트워크를 통해 반환 하기 전에 데이터를 자릅니다 하는 데이터 원본에 의해 구현 됩니다. 드라이버 및 데이터 원본 지원 하기 위한 필요 하지 않습니다. 따라서 데이터가 특정 크기로 잘리고을 보장 하기 위해 응용 프로그램 해야 해당 크기의 버퍼를 할당 하 고 크기를 지정 된 *cbValueMax* 인수 **SQLBindCol**합니다.  
  
3.  데이터를 지정 하는 형식의 변환 *TargetType* 에 **SQLBindCol**합니다.  
  
4.  데이터를 문자 또는 이진, 같은 가변 길이 데이터 형식으로 변환 된 경우 **SQLFetch** 데이터의 길이 데이터 버퍼의 길이 초과 하는지 여부를 확인 합니다. (Null 종결 문자 포함)는 문자 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLFetch** null 종결 문자 길이 보다 데이터 버퍼의 길이에 데이터를 자릅니다. 그 다음 null-데이터를 종료 합니다. 이진 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLFetch** 데이터 버퍼의 길이를 자동으로 잘립니다. 데이터 버퍼의 길이와 지정 된 *BufferLength* 에 **SQLBindCol**합니다.  
  
     **SQLFetch** 되지 자릅니다 데이터를 변환할 고정 길이 데이터 형식; 항상 데이터 버퍼의 길이 데이터 형식의 크기 이라고 가정 합니다.  
  
5.  데이터 버퍼에 변환 된 (및 가능한 잘린) 데이터를 저장합니다. 데이터 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소" 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
6.  길이/표시기 버퍼에 데이터의 길이 저장합니다. 표시기 포인터와 길이 포인터 둘 다 동일한 버퍼에 설정 된 경우 (호출으로 **SQLBindCol** 않습니다), 올바른 데이터에 대 한 버퍼 길이 작성 및 SQL_NULL_DATA NULL 데이터에 대 한 버퍼에 기록 됩니다. 길이/표시기 버퍼 없음, 바인딩된 경우 **SQLFetch** 길이 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터에 대 한이 고 데이터의 길이 변환 후 잘림 하기 전에 데이터 버퍼가 너무 작아 때문입니다. 드라이버 때 긴 데이터의 경우 변환 후 데이터의 길이 확인할 수 없으면, 길이 SQL_NO_TOTAL를 설정 합니다. 데이터가 SQL_ATTR_MAX_LENGTH 문 특성으로 인해 잘렸습니다,이 특성의 값 실제 길이 대신 길이/표시기 버퍼에 저장 됩니다. 즉,이 특성은 드라이버의 실제 길이 어떤 파악 하지 못함을 있도록 변환 하기 전에 서버에서 데이터를 자를 설계 되었습니다.  
  
    -   다른 모든 데이터 형식 변환; 후 데이터의 길이입니다. 즉, 데이터가 변환 된 형식의 크기를입니다.  
  
     길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소" 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
7.  유효 자릿수의 손실 없이 변환 하는 동안 데이터가 잘리고 경우 (예를 들어 실수 1.234 잘립니다 정수 변환 될 때 1), **SQLFetch** SQLSTATE 01S07 반환 (잘렸습니다.) 및 SQL_ SUCCESS_WITH_INFO 합니다. 데이터 버퍼의 길이가 너무 작아 때문에 데이터가 잘린 경우 (예를 들어 문자열 "abcdef"가 버퍼에 저장 4 바이트), **SQLFetch** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘리는 경우 **SQLFetch** 관계 없이 SQL_SUCCESS를 반환 하 고 SQLSTATE 01S07 반환 하지 않습니다 (소수 자릿수 잘림) 또는 SQLSTATE 01004 (데이터 잘림). 데이터 (예를 들어 SQL_INTEGER 값은 100, 000 보다 큰 프로그램 SQL_C_TINYINT로 변환 되었습니다), 유효 자릿수의 손실 변환 하는 동안 잘리는 경우 **SQLFetch** SQLSTATE 22003 (범위를 벗어났습니다. 숫자 값)를 반환 합니다. (행 집합 크기는 1) 하는 경우 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO (행 집합 크기가 1 보다 큰 경우).  
  
 경우에 바인딩된 데이터 버퍼 및 길이/표시기 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 또는 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열이  
 행 집합의 각 행의 상태를 반환 하는 행 상태 배열이 사용 됩니다. 이 배열의 주소 SQL_ATTR_ROW_STATUS_PTR 문 특성으로 지정 됩니다. 배열 응용 프로그램에 의해 할당 되 고 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정 된 만큼의 요소에 있어야 합니다. 해당 값에 의해 설정 된 **SQLFetch**, **SQLFetchScroll**, 및 **SQLBulkOperations** 또는 **SQLSetPos** (제외 하 고 호출 된 경우 커서에서 배치 된 후 **SQLExtendedFetch**). SQL_ATTR_ROW_STATUS_PTR 문 특성의 값이 null 포인터 이면 이러한 함수는 행 상태를 반환 하지 않습니다.  
  
 경우에 행 상태 배열 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 또는 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
 다음 값은 행 상태 배열이 반환 됩니다.  
  
|행 상태 배열 값입니다.|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 인출 된 성공적으로 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않은 합니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 인출 된 성공적으로 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않은 합니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED [1], [2] 및 [3]|행이 인출 된 성공적으로 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되었습니다. 행이 결과 집합에서 다시 인출 됩니다 하거나 새로 고쳐질 **SQLSetPos**, 상태가 행의 새 상태를 변경 합니다.|  
|SQL_ROW_DELETED가 [3]|이 결과 집합에서 마지막으로 인출 된 이후 해당 행이 삭제 되었습니다.|  
|SQL_ROW_ADDED [4]|의해 삽입 된 행 **SQLBulkOperations**합니다. 행이 결과 집합에서 다시 인출 됩니다 하거나 새로 고쳐질 **SQLSetPos**, 상태 SQL_ROW_SUCCESS입니다.|  
|SQL_ROW_NOROW|행 집합 결과 집합의 끝 겹쳐진 및 행 상태 배열이의이 요소에 상응 하는 행이 반환 되었습니다.|  
  
 [1] 키 집합, 혼합 및 동적 커서에 대 한 키 값을 업데이트 하는 경우 데이터의 행 삭제 된 것으로 간주 됩니다 하 고 새 행 추가.  
  
 [2] 일부 드라이버는 데이터에 대 한 업데이트를 검색할 수 없습니다 및이 값을 반환할 수 없습니다. 드라이버에 따라 다시 인출 된 행에 업데이트를 검색할 수 있는지를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_ROW_UPDATES 옵션을 사용 합니다.  
  
 [3] **SQLFetch** 에 대 한 호출이와 혼합 하는 경우에이 값을 반환할 수 **SQLFetchScroll**합니다. 때문에 이것이 **SQLFetch** 결과 집합 앞으로 이동 하 고 단독으로 사용 될 때 모든 행에 다시 인출 하지 않습니다. 행에 따라 다시 인출, 때문에 **SQLFetch** 이전에 인출 된 행에 대 한 변경 내용을 검색 하지 않습니다. 그러나 경우 **SQLFetchScroll** 이전에 행을 인출 된 전에 커서가 놓입니다 및 **SQLFetch** 해당 행을 인출 하는 데 사용 **SQLFetch** 변경 내용을 검색할 수 있습니다 이러한 행 수입니다.  
  
 [4]에서 반환 된 SQLBulkOperations만 합니다. 으로 설정 하지 않은 **SQLFetch** 또는 **SQLFetchScroll**합니다.  
  
### <a name="rows-fetched-buffer"></a>버퍼를 인출 하는 행  
 버퍼를 인출 된 행을 인출 되 고 된 하는 동안 오류가 발생 하기 때문에 데이터가 없는 반환 된 행을 포함 하 여, 가져온 행 수를 반환 하는 데 사용 됩니다. 즉, 이기을 행 상태 배열이의 값이 없습니다 SQL_ROW_NOROW 행의 수입니다. 이 버퍼의 주소 SQL_ATTR_ROWS_FETCHED_PTR 문 특성으로 지정 됩니다. 응용 프로그램에서의 버퍼를 할당 합니다. 에 의해 설정 된 **SQLFetch** 및 **SQLFetchScroll**합니다. SQL_ATTR_ROWS_FETCHED_PTR 문 특성의 값이 null 포인터 이면 이러한 함수는 인출 된 행 수를 반환 하지 않습니다. 결과 집합의 현재 행의 번호를 확인 하려면 응용 프로그램이 호출할 수 **SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 특성을 사용 합니다.  
  
 경우에 행이 인출 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 또는 **SQLFetchScroll** 경우 SQL_NO_DATA가 반환 되는 경우를 제외 하 고 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다는 인출 버퍼 행에 값을 0으로 설정 됩니다.  
  
### <a name="error-handling"></a>오류 처리  
 오류 및 경고 전체 함수 또는 개별 행을 적용할 수 있습니다. 진단 레코드에 대 한 자세한 내용은 참조 [진단](../../../odbc/reference/develop-app/diagnostics.md) 및 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>전체 함수에서 오류 및 경고  
 오류가 SQLSTATE HYT00 같은 함수는 전체에 적용 됩니다 (제한 시간 만료 됨) 또는 24000 (잘못 된 커서 상태), SQLSTATE **SQLFetch** 해당 SQLSTATE 및 SQL_ERROR를 반환 합니다. 행 집합 버퍼의 내용을 정의 되지 않으며 커서 위치는 변경 되지 않습니다.  
  
 경고 함수 전체에 적용 되 면 **SQLFetch** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 해당 반환 합니다. 상태 레코드 함수 전체에 적용 되는 경고에 대 한 개별 행에 적용 되는 상태 레코드 보다 먼저 반환 됩니다.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>개별 행의 오류 및 경고  
 단일 행에 적용 됩니다 (예: SQLSTATE 22012 (0으로 나누기))는 오류 또는 경고 (예: SQLSTATE 01004 (데이터 잘림)) 하는 경우 **SQLFetch**다음 작업을 수행 합니다.  
  
-   경고에 대 한 오류 또는 SQL_ROW_SUCCESS_WITH_INFO SQL_ROW_ERROR를 행 상태 배열이의 해당 요소를 설정합니다.  
  
-   오류 또는 경고에 대 한 Sqlstate를 포함 하는 0 개 이상의 상태 레코드를 추가 합니다.  
  
-   상태 레코드에서 행 및 열 번호 필드를 설정합니다. 경우 **SQLFetch** 행 또는 열 번호를 확인할 수 없습니다 것 숫자 SQL_ROW_NUMBER_UNKNOWN 또는 SQL_COLUMN_NUMBER_UNKNOWN를 각각 설정 합니다. 상태 레코드 특정 열에 적용 되지 않는 경우 **SQLFetch** SQL_NO_COLUMN_NUMBER를 열 수를 설정 합니다.  
  
 **SQLFetch** 행 집합의 모든 행 인출 될 때까지 행을 인출 하는 계속 됩니다. 이 경우 SQL_ERROR를 반환 (SQL_ROW_NOROW 상태와 함께 행을 포함 하지 않음) 행 집합의 모든 행에 오류가 발생 하지 않는 한 SQL_SUCCESS_WITH_INFO를 반환 합니다. 특히, 행 집합 크기가 1이 고 해당 행에서 오류가 발생 하는 경우 **SQLFetch** SQL_ERROR를 반환 합니다.  
  
 **SQLFetch** 행 번호 순서로 상태 레코드를 반환 합니다. 즉, 알 수 없는 행 (있는 경우)에 대 한 모든 상태 레코드를 반환 다음 (있는 경우)는 첫 번째 행에 대 한 모든 상태 레코드를 반환 하 고 두 번째 행 (있는 경우), 등에 대 한 모든 상태 레코드를 반환 합니다. 각 행에 대 한 상태 레코드 상태 레코드; 순서에 대 한 일반 규칙에 따라 정렬 됩니다. 자세한 내용은에서 "상태 레코드의 시퀀스" 참조 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
### <a name="descriptors-and-sqlfetch"></a>설명자 및 SQLFetch  
 다음 섹션에서는 설명 방법을 **SQLFetch** 설명자와 상호 작용 합니다.  
  
#### <a name="argument-mappings"></a>인수 매핑  
 드라이버의 인수에 따라 모든 설명자 필드를 설정 하지 않으면 **SQLFetch**합니다.  
  
#### <a name="other-descriptor-fields"></a>다른 설명자 필드  
 사용 되는 다음 설명자 필드가 **SQLFetch**합니다.  
  
|설명자 필드|Desc입니다.|필드에|통해 설정|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|카드가|헤더|SQL_ATTR_ROW_ARRAY_SIZE 문 특성|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|헤더|SQL_ATTR_ROW_STATUS_PTR 문 특성|  
|SQL_DESC_BIND_OFFSET_PTR|카드가|헤더|SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성|  
|SQL_DESC_BIND_TYPE|카드가|헤더|SQL_ATTR_ROW_BIND_TYPE 문 특성|  
|SQL_DESC_COUNT|카드가|헤더|*ColumnNumber* 의 인수 **SQLBindCol**|  
|SQL_DESC_DATA_PTR|카드가|레코드|*TargetValuePtr* 의 인수 **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|카드가|레코드|*StrLen_or_IndPtr* 인수 **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|카드가|레코드|*BufferLength* 인수 **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|카드가|레코드|*StrLen_or_IndPtr* 인수 **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|헤더|SQL_ATTR_ROWS_FETCHED_PTR 문 특성|  
|SQL_DESC_TYPE|카드가|레코드|*TargetType* 인수 **SQLBindCol**|  
  
 통해 모든 설명자 필드를 설정할 수도 있습니다 **SQLSetDescField**합니다.  
  
#### <a name="separate-length-and-indicator-buffers"></a>별도 길이 표시기 버퍼  
 응용 프로그램 단일 버퍼 또는 길이 표시기 값을 포함 하도록 사용할 수 있는 두 개의 별도 버퍼에 바인딩할 수 있습니다. 응용 프로그램 호출 하는 경우 **SQLBindCol**, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드는 카드가의 전달 되는 동일한 주소를 설정 하는 드라이버는 *StrLen_or_IndPtr* 인수입니다. 응용 프로그램 호출 하는 경우 **SQLSetDescField** 또는 **SQLSetDescRec**, 서로 다른 주소에이 두 필드를 설정할 수 있습니다.  
  
 **SQLFetch** 는 응용 프로그램에서 별도 길이 표시기 버퍼를 지정 하는지 여부를 결정 합니다. 이 경우 데이터가 없는 경우 NULL, **SQLFetch** 표시기 버퍼를 0으로 설정 하 고 길이 버퍼 길이 반환 합니다. NULL 인 경우 해당 데이터 **SQLFetch** 표시기 버퍼 sql_null_data로 설정 되 고 길이 버퍼를 수정 하지는 않습니다.  
  
### <a name="code-example"></a>코드 예  
 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 및 [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)합니다.  
  
### <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|문의 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|일부 또는 전체 데이터 열을 인출합니다.|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
