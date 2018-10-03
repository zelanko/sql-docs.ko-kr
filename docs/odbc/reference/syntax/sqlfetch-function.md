---
title: SQLFetch 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d1e4c4462aa10a2d99e50e71d7b2e86fa4d8555
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825941"
---
# <a name="sqlfetch-function"></a>SQLFetch 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수 합니다: ISO 92  
  
 **요약**  
 **SQLFetch** 결과 집합에서 데이터의 다음 행 집합을 인출 하 고 모든 바인딩된 열에 대 한 데이터를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFetch** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 [SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 사용 하 여를 *HandleType*호출의와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLFetch** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다. 단일 열에서 오류가 발생 하는 경우 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 호출할 수는 *DiagIdentifier* ;에서 오류가 발생 하는 열을 확인 하려면 SQL_DIAG_COLUMN_NUMBER의 및  **SQLGetDiagField** 호출할 수는 *DiagIdentifier* 열을 포함 하는 행을 확인 하려면 SQL_DIAG_ROW_NUMBER입니다.  
  
 다중 행 작업의 하나 또는 더 많은 전부는 아니지만, 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 하는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|공백이 아닌 문자 또는 NULL이 아닌 이진 데이터의 잘림 문자열 또는 이진 데이터 열에 대 한 반환 했습니다. 문자열 값이 오른쪽 잘림 이었습니다.|  
|01S01|행에 오류가 있습니다.|하나 이상의 행을 인출 하는 동안 오류가 발생 했습니다.<br /><br /> (이 SQLSTATE는 ODBC 3 때 반환 되 면 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 무시할 수 있습니다.)|  
|01S07|소수 잘림|열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 간격 데이터 형식에 대 한 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다 *TargetType* 에 **SQLBindCol**합니다.<br /><br /> 0 열 데이터 형식의 SQL_C_BOOKMARK, 바인딩된 및 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_VARIABLE로 설정 되었습니다.<br /><br /> 0 열 데이터 형식의 SQL_C_VARBOOKMARK, 바인딩 및 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_VARIABLE에 설정 되지 않았습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|드라이버는 ODBC 2 되었습니다 *.x* 드라이버를 지원 하지 않는 **SQLExtendedFetch**, 열에 대 한 바인딩에 지정 된 열 번호 되었습니다. 0 및 합니다.<br /><br /> 열 0, 바인딩되고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터 오른쪽 잘림|열에 대해 반환 된 가변 길이 책갈피가 잘렸습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지|NULL 데이터가 페치된 열을 갖는 *StrLen_or_IndPtr* 설정한 **SQLBindCol** (또는 설정한 SQL_DESC_INDICATOR_PTR **SQLSetDescField** 또는  **SQLSetDescRec**)가 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|하나 이상의 바인딩된 열에 대 한 문자열을 숫자로 숫자 값을 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.<br /><br /> 자세한 내용은 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식에서입니다.|  
|22007|잘못 된 날짜/시간 형식|결과 집합의 문자 열 된 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되며 열에 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다.|  
|22012|0으로 나누기|산술 식에서 값을 반환한, 부서에서 발생 하는 0입니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형을 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> 간격 C 형식으로 데이터를 인출할 때 C 간격 유형으로 SQL 형식의 값 표현 방식이 없기 있었습니다.|  
|22018|캐스트 사양의 문자 값|결과 집합의 문자 열 C 문자 버퍼에 바인딩된 열 버퍼의 문자 집합에 표현이 없는 된 문자를 포함 하며<br /><br /> C 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 열의 SQL 형식이 된 문자 데이터 형식입니다. 하는 열에 값을 바인딩된 C 형식의 유효한 리터럴이 없습니다.|  
|24000|잘못된 커서 상태|합니다 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.|  
|40001|Serialization 오류|실행 된 fetch는 트랜잭션이 교착 상태를 방지 하기 위해 종료 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. **SQLFetch** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*. 그런 다음 **SQLFetch** 에서 다시 호출 된 함수는 *StatementHandle*합니다.<br /><br /> 또는 **SQLFetch** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*  다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLFetch** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 실행 상태가 없습니다. 첫 번째 호출 하지 않고 함수를 호출한 **SQLExecDirect**를 **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM) **SQLFetch** 에 대해 호출 되었습니다 합니다 *StatementHandle* 후 **SQLExtendedFetch** 호출한 전과 **SQLFreeStmt** 는 SQL_를 사용 하 여 닫기 옵션 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE로 설정 된 및 0 열이 결과 집합에 대 한 책갈피에 대 한 최대 길이 같은 길이가 없습니다. 버퍼에 바인딩 되었습니다. (이 길이 IRD의 SQL_DESC_OCTET_LENGTH 필드 수 및 호출 하 여 가져올 수 있습니다 **SQLDescribeCol**하십시오 **SQLColAttribute**, 또는 **SQLGetDescField**.)|  
|HY107|행 값 범위를 벗어났습니다.|SQL_ATTR_CURSOR_TYPE 문 특성을 사용 하 여 지정 된 값, SQL_CURSOR_KEYSET_DRIVEN 되었지만 SQL_ATTR_KEYSET_SIZE 문 특성을 사용 하 여 지정한 값이 0 보다 크고는 SQL_ATTR_ROW_ARRAY_를 사용 하 여 지정 된 값 보다 작음 크기 문 특성입니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 조합에 의해 지정 된 변환을 지원 하지 않습니다 합니다 *TargetType* 에 **SQLBindCol** 및 해당 열의 SQL 데이터 형식입니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 시간 제한 기간 SQLSetStmtAttr에서 SQL_ATTR_QUERY_TIMEOUT 통해 설정 됩니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLFetch** 결과 집합의 다음 행 집합을 반환 합니다. 결과 집합이 존재 하는 동안에 호출할 수 있습니다: 즉,을 호출한 후에 결과 집합을 만들고 커서 하기 전에 결과 집합을 통해 닫혀 있습니다. 모든 열에 바인딩되어 있는 경우 해당 열에 데이터를 반환 합니다. 응용 프로그램에서 행 상태 배열이 나 인출 하는 행의 수를 반환 하는 버퍼에 대 한 포인터를 지정한 경우 **SQLFetch** 도이 정보를 반환 합니다. 에 대 한 호출 **SQLFetch** 를 호출 하 여 함께 사용할 수 있습니다 **SQLFetchScroll** 호출 하 여 혼합할 수 없습니다 하지만 **SQLExtendedFetch**합니다. 자세한 내용은 [행의 데이터를 인출](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)합니다.  
  
 경우는 ODBC 3 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 드라이버 관리자 매핑합니다 **SQLFetch** 호출 **SQLExtendedFetch** 에 대 한는 ODBC 2 *.x* 드라이버를 지 원하는 **SQLExtendedFetch**합니다. 경우 ODBC 2 *.x* 드라이버를 지원 하지 않습니다 **SQLExtendedFetch**, 드라이버 관리자 매핑합니다 **SQLFetch** 호출 **SQLFetch** ODBC 2 *.x* 드라이버 단일 행만 인출할 수 있습니다.  
  
 자세한 내용은 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침입니다.  
  
## <a name="positioning-the-cursor"></a>커서를 놓고  
 결과 집합을 만든 경우 커서는 결과 집합을 시작 하기 전에 배치 됩니다. **SQLFetch** 다음 행 집합을 인출 합니다. 호출 하는 것과 같습니다 **SQLFetchScroll** 사용 하 여 *FetchOrientation* SQL_FETCH_NEXT로 설정 합니다. 커서에 대 한 자세한 내용은 참조 하세요. [커서](../../../odbc/reference/develop-app/cursors.md) 하 고 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)합니다.  
  
 SQL_ATTR_ROW_ARRAY_SIZE 문 특성 행 집합의 행 수를 지정합니다. 행 집합으로 인출 되는 경우 **SQLFetch** 결과 집합의 끝을 겹치는 **SQLFetch** 부분 행 집합을 반환 합니다. 즉, S + R-1은 L 보다 큼, 여기서 S는 행 집합의 반입 되 고 R 시작 행을 행 집합 크기 이며 L 마지막 행 결과 집합에서 다음만 첫 번째 L-S + 행 집합의 1 행 경우 유효 합니다. 나머지 행 비어 있으며 SQL_ROW_NOROW의 상태.  
  
 이후에 **SQLFetch** 현재 행이 행 집합의 첫 번째 행을 반환 합니다.  
  
 다음 표에 나열 된 규칙을 호출한 후 커서 위치 지정 설명 **SQLFetch**이 섹션의 두 번째 표에 나열 된 조건에 따라 합니다.  
  
|조건|새 행 집합의 첫 번째 행|  
|---------------|-----------------------------|  
|시작 하기 전에|1|  
|*CurrRowsetStart* \< =  *LastResultRow – RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow – RowsetSize*[1]|종료 후|  
|종료 후|종료 후|  
  
 [1] 행 집합 크기 인출 간에 변경 되 면 이전 인출에 사용 된 행 집합 크기입니다.  
  
 [2] 행 집합 크기 인출 간에 변경 되 면 새 인출에 사용 된 행 집합 크기입니다.  
  
|표기법|의미|  
|--------------|-------------|  
|시작 하기 전에|블록 커서 결과 집합을 시작 하기 전에 배치 됩니다. 결과 집합을 시작 하기 전에 새 행 집합의 첫 번째 행 이면 **SQLFetch** SQL_NO_DATA를 반환 합니다.|  
|종료 후|블록 커서는 결과의 끝을 설정한 후에 배치 됩니다. 결과 집합의 끝 뒤에 새 행 집합의 첫 번째 행 이면 **SQLFetch** SQL_NO_DATA를 반환 합니다.|  
|*CurrRowsetStart*|현재 행 집합에서 첫 번째 행의 수입니다.|  
|*LastResultRow*|결과 집합의 마지막 행의 수입니다.|  
|*RowsetSize*|행 집합 크기입니다.|  
  
 예를 들어 결과 집합에 100 개 행 및 행 집합 크기는 5입니다. 다음 표에서 반환한 행 집합 및 반환 코드를 보여 줍니다 **SQLFetch** 다른 시작 위치에 대 한 합니다.  
  
|현재 행 집합|반환 코드|새 행 집합|행 인출 횟수|  
|--------------------|-----------------|----------------|------------------------|  
|시작 하기 전에|SQL_SUCCESS|1 ~ 5|5|  
|1 ~ 5|SQL_SUCCESS|6 ~ 10|5|  
|52에 56|SQL_SUCCESS|57-61|5|  
|91 ~ 95|SQL_SUCCESS|96 ~ 100|5|  
|93에 97|SQL_SUCCESS|98에서 100까지. 행 상태 배열이의 4 및 5 행 SQL_ROW_NOROW로 설정 됩니다.|3|  
|96 ~ 100|SQL_NO_DATA|없음|0|  
|99 ~ 100|SQL_NO_DATA|없음|0|  
|종료 후|SQL_NO_DATA|없음|0|  
  
## <a name="returning-data-in-bound-columns"></a>바인딩된 열에서 데이터를 반환합니다.  
 로 **SQLFetch** 반환 각 행에서 해당 열에 바인딩된 버퍼에 바인딩된 각 열에 대 한 데이터를 넣습니다. 열에 바인딩되어 있는 경우 **SQLFetch** 데이터를 반환 하지 않지만 블록 커서를 앞으로 이동 합니다. 데이터를 사용 하 여 계속 검색할 수 있습니다 **SQLGetData**합니다. 다중 커서는 커서가 있는 경우 (즉, SQL_ATTR_ROW_ARRAY_SIZE가 1 보다 큰), **SQLGetData** SQL_GD_BLOCK이 반환 하는 경우에 호출할 수 있습니다 **SQLGetInfo** 사용 하 여 호출 되는  *정보 항목* SQL_GETDATA_EXTENSIONS입니다. (자세한 내용은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 행에 바인딩된 각 열에 대 한 **SQLFetch** 다음을 수행 합니다.  
  
1.  모두 SQL_NULL_DATA로 길이/표시기 버퍼를 설정 하 고 데이터에 NULL 인 경우 다음 열으로 진행 됩니다. 데이터가 NULL이 고 길이/표시기 버퍼 없음, 바인딩된 경우 **SQLFetch** 행에 대 한 SQLSTATE 22002 (지표 변수가 필요 하지만 제공 되지)를 반환 하 고 다음 행으로 진행 됩니다. 길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소"를 참조 하세요 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
     열에 대 한 데이터를 NULL이 아닌 경우 **SQLFetch** 2 단계로 진행 됩니다.  
  
2.  SQL_ATTR_MAX_LENGTH 문 특성을 0이 아닌 값으로 설정 됩니다. 열에 문자 또는 이진 데이터를 데이터 SQL_ATTR_MAX_LENGTH 바이트로 잘립니다.  
  
    > [!NOTE]  
    >  네트워크 트래픽을 줄이기 위해 SQL_ATTR_MAX_LENGTH 문 특성을 것입니다. 일반적으로 네트워크를 통해 반환 하기 전에 데이터를 자릅니다 되는 데이터 원본에 의해 구현 됩니다. 드라이버 및 데이터 원본 지원 하도록 않아도 됩니다. 따라서 특정 크기로 데이터가 잘리고 있는지을 보장 하기 위해 응용 프로그램은 해당 크기의 버퍼를 할당 및 크기를 지정 합니다 *cbValueMax* 에서 인수 **SQLBindCol**합니다.  
  
3.  지정 된 형식으로 데이터를 변환할 *TargetType* 에 **SQLBindCol**합니다.  
  
4.  데이터는 문자 또는 이진 같은 가변 길이 데이터 형식으로 변환 된 경우 **SQLFetch** 데이터의 길이 데이터 버퍼의 길이 초과 하는지 여부를 확인 합니다. (Null 종결 문자 포함)는 문자 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLFetch** null 종결 문자 길이의 덜 데이터 버퍼의 길이 데이터를 자릅니다. 그런 다음 null-종료 될 데이터입니다. 이진 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLFetch** 데이터 버퍼의 길이를 자동으로 잘립니다. 사용 하 여 데이터 버퍼의 길이가 지정 되어 *BufferLength* 에 **SQLBindCol**합니다.  
  
     **SQLFetch** 되지 자릅니다 데이터 형식이 고정 길이 데이터를 변환, 데이터 버퍼의 길이 데이터 형식의 크기는 항상 가정 합니다.  
  
5.  데이터 버퍼를 변환 (및 가능한 경우) 데이터를 넣습니다. 데이터 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소"를 참조 하세요 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
6.  길이/표시기 버퍼에 데이터의 길이 저장합니다. 표시기 포인터와 길이 포인터가 모두 동일한 버퍼에 설정 된 경우 (호출으로 **SQLBindCol** 않습니다), 길이 유효한 데이터에 대 한 버퍼에 기록 되 고 SQL_NULL_DATA NULL 데이터에 대 한 버퍼에 기록 됩니다. 길이/표시기 버퍼 없음, 바인딩된 경우 **SQLFetch** 길이 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터에 대 한이 고 데이터의 길이 변환 후 자르기 전에 데이터 버퍼가 너무 작아 때문입니다. 드라이버는 경우에 따라 긴 데이터의 경우 변환 후 데이터의 길이 확인할 수 없습니다, 경우 SQL_NO_TOTAL 길이 설정 합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘렸습니다, 하는 경우이 특성의 값 대신 실제 길이 길이/표시기 버퍼에 저장 됩니다. 이 특성은 변환 하기 전에 서버에서 데이터가 잘릴 드라이버의 실제 길이 파악 하지 못함을 있도록 때문입니다.  
  
    -   다른 모든 데이터 형식에 대 한이 값은 길이 데이터의 변환 후 즉, 해당 데이터를 변환 하는 형식의 크기입니다.  
  
     길이/표시기 버퍼의 주소를 확인 하는 방법에 대 한 내용은의 "버퍼 주소"를 참조 하세요 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
7.  유효 자릿수의 손실 없이 변환 하는 동안 데이터가 잘리고 경우 (예를 들어 실수 1.234 잘리면 정수로 변환 하는 경우 1) **SQLFetch** SQLSTATE 01S07 반환 (소수 잘림) 및 SQL_ SUCCESS_WITH_INFO 합니다. 데이터 버퍼의 길이가 너무 작아서 때문에 데이터가 잘린 경우 (예를 들어, "abcdef" 문자열은 버퍼에 저장 4 바이트)를 **SQLFetch** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘리면 **SQLFetch** 관계 없이 SQL_SUCCESS를 반환 하 고 SQLSTATE 01S07 반환 하지 않습니다 (소수 잘림) 또는 SQLSTATE 01004 (데이터 잘림). 데이터 (예를 들어는 SQL_C_TINYINT 100,000 보다 큰 SQL_INTEGER 값을 변환 된 경우), 유효 자릿수의 손실을 사용 하 여 변환 하는 동안 잘리면 **SQLFetch** SQLSTATE 22003 (범위를 벗어났습니다. 숫자 값)를 반환 합니다. (행 집합 크기가 1) 하는 경우 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO (행 집합 크기가 1 보다 큰 경우).  
  
 경우에 바인딩된 데이터 버퍼 및 길이/표시기 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 행 집합의 각 행의 상태를 반환 하는 행 상태 배열이 사용 됩니다. 이 배열의 주소 SQL_ATTR_ROW_STATUS_PTR 문 특성을 사용 하 여 지정 됩니다. 응용 프로그램에 의해 할당 되었습니다 배열과 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정 된 만큼의 요소가 있어야 합니다. 해당 값 설정 됩니다 **SQLFetch**를 **SQLFetchScroll**, 및 **SQLBulkOperations** 하거나 **SQLSetPos** (호출 된 경우 제외 커서에서 배치 된 후 **SQLExtendedFetch**). SQL_ATTR_ROW_STATUS_PTR 문 특성의 값이 null 포인터 이면 이러한 함수는 행 상태를 반환 하지 않습니다.  
  
 경우에 행 상태 배열 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
 다음 값을 행 상태 배열이 반환 됩니다.  
  
|행 상태 배열 값입니다.|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행을 성공적으로 가져온 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않은 합니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행을 성공적으로 가져온 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되지 않은 합니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED [1], [2] 및 [3]|행을 성공적으로 가져온 및이 결과 집합에서 마지막으로 인출 된 이후 변경 되었습니다. 행이 결과 집합에서 다시 인출 됩니다 아니면으로 새로 고쳐집니다 **SQLSetPos**, 행의 새 상태에는 상태가 변경 됩니다.|  
|SQL_ROW_DELETED가 [3]|행이 결과 집합에서 마지막으로 페치된 이후로 삭제 되었습니다.|  
|SQL_ROW_ADDED [4]|행으로 삽입 된 **SQLBulkOperations**합니다. 행이 결과 집합에서 다시 인출 됩니다 아니면으로 새로 고쳐집니다 **SQLSetPos**, 상태가 SQL_ROW_SUCCESS입니다.|  
|SQL_ROW_NOROW|행 집합 결과 집합의 끝을 중첩 하 고 행이 행 상태 배열이 요소에 해당 하는 반환 된 키를 누릅니다.|  
  
 [1] keyset, 혼합 및 동적 커서에 대 한 키 값을 업데이트 하는 경우 데이터의 행을 삭제 된 것으로 간주 됩니다 하 고 새 행을 추가 합니다.  
  
 [2] 일부 드라이버는 데이터에 대 한 업데이트를 검색할 수 없습니다 및이 값을 반환할 수 없습니다. 응용 프로그램이 호출 드라이버에 따라 다시 인출 된 행에 업데이트를 검색할 수 있는지 여부를 결정할 **SQLGetInfo** SQL_ROW_UPDATES 옵션을 사용 합니다.  
  
 [3] **SQLFetch** 호출와 혼합 하는 경우에이 값을 반환할 수 있습니다 **SQLFetchScroll**합니다. 왜냐하면 **SQLFetch** 결과 집합을 통해 앞으로 이동 하 고 단독으로 사용 될 때 모든 행을 다시 인출 하지 않습니다. 행에 따라 다시 인출, 하므로 **SQLFetch** 이전에 인출된 된 행에 대 한 변경 내용을 검색 하지 않습니다. 그러나 경우 **SQLFetchScroll** 행을 이전에 가져온 모든 전에 커서를 배치 하 고 **SQLFetch** 해당 행을 인출 하는 데 사용 됩니다 **SQLFetch** 변경 내용을 감지할 수 있습니다 이러한 행입니다.  
  
 [4] 반환한 SQLBulkOperations만입니다. 설정 되지 **SQLFetch** 하거나 **SQLFetchScroll**합니다.  
  
### <a name="rows-fetched-buffer"></a>행 인출된 버퍼  
 인출 버퍼 행 인출 되 고 된 하는 동안 오류가 발생 하기 때문에 데이터가 없는 반환 하는 행을 포함 하 여, 가져온 행 수를 반환 됩니다. 즉, 행을 행 상태 배열에 올바르지 않은 SQL_ROW_NOROW 수 것입니다. 이 버퍼의 주소는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 사용 하 여 지정 됩니다. 버퍼는 응용 프로그램에 의해 할당 됩니다. 에 의해 설정 된 **SQLFetch** 하 고 **SQLFetchScroll**합니다. SQL_ATTR_ROWS_FETCHED_PTR 문 특성의 값이 null 포인터 이면 이러한 함수는 인출 된 행 수를 반환 하지 않습니다. 결과 집합의 현재 행의 수를 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 특성을 사용 합니다.  
  
 경우에 행이 인출 버퍼의 내용을 정의 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO, sql_no_data가 반환 될 때,이 경우를 제외 하 고 반환 하지 않습니다는 인출 버퍼 행의 값은 0으로 설정 됩니다.  
  
### <a name="error-handling"></a>오류 처리  
 오류 및 경고는 전체 함수 또는 개별 행에 적용할 수 있습니다. 진단 레코드에 대 한 자세한 내용은 참조 하세요. [진단을](../../../odbc/reference/develop-app/diagnostics.md) 하 고 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>전체 함수에서 오류 및 경고  
 오류가 SQLSTATE HYT00 등 전체 함수를 적용할 경우 (제한 시간 만료 됨) 또는 24000 (잘못 된 커서 상태), SQLSTATE **SQLFetch** 해당 SQLSTATE 및 SQL_ERROR를 반환 합니다. 행 집합 버퍼의 내용을 정의 하지 않으며 커서 위치는 변경 되지 않습니다.  
  
 경고 함수 전체에 적용 되 면 **SQLFetch** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 적용할 수를 반환 합니다. 함수 전체에 적용 되는 경고에 대 한 상태 레코드를 개별 행에 적용 되는 상태 레코드 전에 반환 됩니다.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>개별 행의 오류 및 경고  
 (예: SQLSTATE 22012 (0으로 나누기))는 오류 또는 경고 (예: SQLSTATE 01004 (데이터 잘림))는 단일 행에 적용 되 면 **SQLFetch**다음을 수행 합니다.  
  
-   경고에 대 한 오류 또는 SQL_ROW_SUCCESS_WITH_INFO SQL_ROW_ERROR을 행 상태 배열의 해당 요소를 설정합니다.  
  
-   오류 또는 경고에 대 한 Sqlstate를 포함 하는 0 개 이상의 상태 레코드를 추가 합니다.  
  
-   상태 레코드에 있는 행 및 열 번호 필드를 설정합니다. 하는 경우 **SQLFetch** 행 또는 열 번호를 확인할 수 없습니다이 숫자 SQL_ROW_NUMBER_UNKNOWN 또는 SQL_COLUMN_NUMBER_UNKNOWN를 각각 설정 합니다. 상태 레코드를 특정 열에 적용 되지 않는 경우 **SQLFetch** SQL_NO_COLUMN_NUMBER를 열 수를 설정 합니다.  
  
 **SQLFetch** 계속 행 집합의 모든 행이 인출 될 때까지 행을 인출 합니다. SQL_ERROR를 반환 하는 경우 (상태 SQL_ROW_NOROW 행 제외) 행 집합의 모든 행에 오류가 발생 하지 않으면 SQL_SUCCESS_WITH_INFO를 반환 합니다. 행 집합 크기가 1이 고 해당 행에서 오류가 발생 하는 경우 특히에서 **SQLFetch** SQL_ERROR를 반환 합니다.  
  
 **SQLFetch** 행 번호 순서 대로 상태 레코드를 반환 합니다. 즉, 알 수 없는 행 (있는 경우)에 대 한 모든 상태 레코드를 반환 첫 번째 행 (있는 경우)에 대 한 모든 상태 레코드가 반환 된 다음 및 다음 두 번째 행 (있는 경우) 등에 대 한 모든 상태 레코드를 반환 합니다. 각 행에 대 한 상태 레코드 상태 레코드; 순서에 대 한 일반 규칙에 따라 정렬 됩니다. 자세한 내용은 "상태 레코드의 시퀀스"를 참조 하세요 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
### <a name="descriptors-and-sqlfetch"></a>설명자 및 SQLFetch  
 다음 섹션에서는 설명 하는 방법 **SQLFetch** 설명자와 상호 작용 합니다.  
  
#### <a name="argument-mappings"></a>인수 매핑  
 드라이버의 인수를 기준으로 모든 설명자 필드를 설정 하지 않습니다 **SQLFetch**합니다.  
  
#### <a name="other-descriptor-fields"></a>다른 설명자 필드  
 다음 설명자 필드를 사용 **SQLFetch**합니다.  
  
|설명자 필드|Desc입니다.|필드에|통해 설정|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|카드가|헤더|SQL_ATTR_ROW_ARRAY_SIZE 문 특성|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|헤더|SQL_ATTR_ROW_STATUS_PTR 문 특성|  
|SQL_DESC_BIND_OFFSET_PTR|카드가|헤더|SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성|  
|SQL_DESC_BIND_TYPE|카드가|헤더|SQL_ATTR_ROW_BIND_TYPE 문 특성|  
|SQL_DESC_COUNT|카드가|헤더|*ColumnNumber* 인수의 **SQLBindCol**|  
|SQL_DESC_DATA_PTR|카드가|레코드|*TargetValuePtr* 인수의 **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|카드가|레코드|*StrLen_or_IndPtr* 인수에 **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|카드가|레코드|*BufferLength* 인수에 **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|카드가|레코드|*StrLen_or_IndPtr* 인수에 **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|헤더|SQL_ATTR_ROWS_FETCHED_PTR 문 특성|  
|SQL_DESC_TYPE|카드가|레코드|*TargetType* 인수에 **SQLBindCol**|  
  
 모든 설명자 필드를 통해 설정할 수도 있습니다 **SQLSetDescField**합니다.  
  
#### <a name="separate-length-and-indicator-buffers"></a>별도 길이 표시기 버퍼  
 응용 프로그램은 단일 버퍼 또는 길이 및 표시기 값을 보유할 수 있는 두 개의 별도 버퍼 바인딩할 수 있습니다. 응용 프로그램을 호출할 때 **SQLBindCol**, 전달 되는 동일한 주소에 카드가 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드를 설정 하는 드라이버를 *StrLen_or_IndPtr* 인수입니다. 응용 프로그램을 호출할 때 **SQLSetDescField** 하거나 **SQLSetDescRec**,이 두 필드를 다른 주소로 설정할 수 있습니다.  
  
 **SQLFetch** 응용 프로그램에 별도 길이 표시기 버퍼를 지정 하는지 여부를 결정 합니다. 이 경우 데이터가 없는 경우 NULL **SQLFetch** 표시기 버퍼를 0으로 설정 하 고 길이가 버퍼 길이 반환 합니다. 데이터가 NULL 인 경우 **SQLFetch** 표시기 버퍼를 sql_null_data로 설정 하 고 길이 버퍼를 수정 하지는 않습니다.  
  
### <a name="code-example"></a>코드 예  
 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)를 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)합니다 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 및 [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)합니다.  
  
### <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|문의 커서 닫기|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|일부 또는 전체 열의 데이터 페치|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
