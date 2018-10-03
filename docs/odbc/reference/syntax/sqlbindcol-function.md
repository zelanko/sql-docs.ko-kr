---
title: SQLBindCol 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5092ae588c69c28fcfa243101b57f97da75e8681
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755321"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수 합니다: ISO 92  
  
 **요약**  
 **SQLBindCol** 결과 집합의 열에 응용 프로그램 데이터 버퍼를 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] 결과의 수에 바인딩되도록 열을 설정 합니다. 열은 열 0 인 책갈피 열의 0부터 증가 열 순서 대로 번호가 지정 됩니다. 책갈피 사용 되지 않는 경우-SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 되어,-다음 열 번호는 1부터 시작 합니다.  
  
 *TargetType*  
 [입력] C 데이터 형식 식별자를 \* *TargetValuePtr* 버퍼입니다. 데이터를 검색 하는 사용 하 여 데이터 원본에서 하는 경우 **SQLFetch**를 **SQLFetchScroll**합니다 **SQLBulkOperations**, 또는 **SQLSetPos**, 드라이버를이 형식; 데이터 변환 사용 하 여 데이터 원본에 데이터를 보낼 때 **SQLBulkOperations** 하거나 **SQLSetPos**, 드라이버는이 형식에서 데이터를 변환 합니다. 유효한 C 데이터 형식 및 형식 식별자의 목록을 참조 하세요. 합니다 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에 대 한 섹션입니다.  
  
 경우는 *TargetType* 인수가 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 자릿수가 SQL_DESC_PRECISION 필드에 설정 된 대로 기본 간격 선행 정밀도 (2) 및 기본 간격 초 전체 자릿수 (6) 간격 데이터 형식 각각은 카드가 데이터에 사용 됩니다. 경우는 *TargetType* 인수 SQL_C_NUMERIC, 기본 전체 자릿수 (드라이버 정의 됨) 및 (0), 확장 된 카드가의 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 필드에 설정 된 대로 기본 이면 데이터에 사용 됩니다. 모든 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 적절 한 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
 또한 확장된 C 데이터 유형을 지정할 수 있습니다. 자세한 내용은 [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 *TargetValuePtr*  
 [입력/출력 지연] 열에 바인딩할 데이터 버퍼에 대 한 포인터입니다. **SQLFetch** 하 고 **SQLFetchScroll** 이 버퍼에 데이터를 반환 합니다. **SQLBulkOperations** 이 데이터를 반환 합니다. 때 버퍼 *작업* SQL_FETCH_BY_BOOKMARK;은이 데이터를 검색할 때 버퍼 *작업* SQL_ADD 인지 SQL_UPDATE_BY_BOOKMARK 합니다. **SQLSetPos** 이 데이터를 반환 합니다. 때 버퍼 *작업* SQL_REFRESH;은이 데이터를 검색할 때 버퍼 *작업* SQL_UPDATE는 합니다.  
  
 하는 경우 *TargetValuePtr* 가 null 포인터인 경우 드라이버는 열에 대 한 데이터 버퍼를 바인딩 해제 합니다. 응용 프로그램 수를 호출 하 여 모든 열을 바인딩 해제 **SQLFreeStmt** SQL_UNBIND 옵션과 함께 합니다. 응용 프로그램 데이터 버퍼 열에 대 한 바인딩을 해제할 수 있지만 경우 열에 바인딩된 길이/표시기 버퍼를 아직 합니다 *TargetValuePtr* 호출에서 인수 **SQLBindCol** null 포인터가 있지만 *StrLen_or_IndPtr* 인수가 유효한 값입니다.  
  
 *BufferLength*  
 [입력] 길이 **TargetValuePtr* 바이트 버퍼입니다.  
  
 드라이버를 사용 하 여 *BufferLength* 끝 쓰기를 방지 하려면 합니다 \* *TargetValuePtr* 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 때 버퍼입니다. 문자 데이터를 반환 하는 경우 드라이버는 null 종료 문자를 세는 알 수 있습니다 \* *TargetValuePtr*합니다. **TargetValuePtr* 공간이 있어야 하므로 한 null 종료 문자 또는 드라이버는 데이터는 잘립니다.  
  
 드라이버는 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환 하는 경우 드라이버 무시 *BufferLength* 버퍼 데이터를 저장 하기에 충분히 큰지 가정 합니다. 따라서 고정 길이 데이터에 대해 충분히 큰 버퍼를 할당할 응용 프로그램에 대 한 중요 한 것 또는 드라이버는 버퍼의 끝을 넘어 작성 합니다.  
  
 **SQLBindCol** SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이) 때 *BufferLength* 0 보다 작은 하지만 때가 아니라 *BufferLength* 은 0입니다. 그러나 경우 *TargetType* 문자 형식으로 지정 응용 프로그램을 설정 하지 않아야 *BufferLength* 0으로 ISO CLI 호환 드라이버는 SQLSTATE HY090 반환 하므로 (잘못 된 문자열 또는 버퍼 길이)에 케이스입니다.  
  
 *StrLen_or_IndPtr*  
 [입력/출력 지연] 열에 바인딩할 길이/표시기 버퍼에 대 한 포인터입니다. **SQLFetch** 하 고 **SQLFetchScroll** 이 버퍼의 값을 반환 합니다. **SQLBulkOperations** 값이 검색 될 때 버퍼 *작업* SQL_ADD, SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK 인지 합니다. **SQLBulkOperations** 때이 값을 반환 버퍼 *작업* SQL_FETCH_BY_BOOKMARK 됩니다. **SQLSetPos** 때이 값을 반환 버퍼 *작업* SQL_REFRESH;은 값이 검색 때 버퍼 *작업* SQL_UPDATE 됩니다.  
  
 **SQLFetch**, **SQLFetchScroll**합니다 **SQLBulkOperations**, 및 **SQLSetPos** 길이/표시기 버퍼의 다음 값을 반환할 수 있습니다.  
  
-   반환할 사용 가능한 데이터의 길이  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 응용 프로그램 사용에 대 한 길이/표시기 버퍼의 다음 값을 넣으면 **SQLBulkOperations** 하거나 **SQLSetPos**:  
  
-   전송 중인 데이터의 길이  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 매크로의 결과  
  
-   SQL_COLUMN_IGNORE  
  
 표시기 버퍼 및 길이 버퍼에 별도 버퍼를 표시기 버퍼 길이 버퍼는 다른 모든 값을 반환할 수 있지만 sql_null_data로 반환할 수 있습니다.  
  
 자세한 내용은 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md), [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md), 및 [길이/표시기값사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 하는 경우 *StrLen_or_IndPtr* null 포인터, 길이 또는 표시기 값이 사용 됩니다. 이 null 인 데이터와 데이터를 페치하는 오류입니다.  
  
 참조 [ODBC 64-Bit 정보](../../../odbc/reference/odbc-64-bit-information.md)이면 응용 프로그램을 64 비트 운영 체제에서 실행 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLBindCol** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLBindCol** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|(DM)는 *ColumnNumber* 인수가 0, 및 *TargetType* 인수 SQL_C_BOOKMARK 또는 SQL_C_VARBOOKMARK 없습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 지정 된 값 *ColumnNumber* 결과 집합에 있는 열의 최대 수를 초과 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|잘못 된 응용 프로그램 버퍼 형식|인수 *TargetType* 올바른 데이터 형식을 아니고 SQL_C_DEFAULT 되었습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 계속 실행 될 때 **SQLBindCol** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.<br /><br /> (DM) 드라이버는 ODBC 2 되었습니다. *x* 드라이버를 *ColumnNumber* 인수는 0이 고, 인수에 지정 된 값으로 설정 되었습니다 *BufferLength* 수준이 4 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 조합에 의해 지정 된 변환을 지원 하지 않습니다 합니다 *TargetType* 인수 및 해당 열의 드라이버별 SQL 데이터 형식입니다.<br /><br /> 인수 *ColumnNumber* 되었습니다. 0 및 드라이버 책갈피를 지원 하지 않습니다.<br /><br /> 드라이버는 ODBC 2에만 지원합니다. *x* 고 인수가 *TargetType* 다음 중 하나 였습니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> C 간격 데이터 형식 중 하나에 나열 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에서입니다.<br /><br /> 드라이버 3.50, 및 인수 이전 ODBC 버전 지원 *TargetType* SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLBindCol** 에 연결 하는 데 사용 됩니다 또는 *바인딩* 결과의 열 데이터 버퍼 및 응용 프로그램에서 길이/표시기 버퍼를 설정 합니다. 응용 프로그램을 호출할 때 **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLSetPos** 데이터를 페치 하려면 드라이버 반환 바인딩된 열에 대 한 데이터에 대 한 지정 된 버퍼에 자세한 내용은 참조 하십시오 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다. 응용 프로그램을 호출할 때 **SQLBulkOperations** 를 업데이트 하거나 행을 삽입 하거나 **SQLSetPos** 드라이버가 행을 업데이트 하려면 자세한 정보에 대 한 지정 된 버퍼에서 바인딩된 열에 데이터를 검색 를 참조 하세요 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 하거나 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다. 바인딩에 대 한 자세한 내용은 참조 하세요. [검색 결과 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md)합니다.  
  
 표시 열에서 데이터를 검색할 바인딩될 필요가 없습니다. 응용 프로그램을 호출할 수도 있습니다 **SQLGetData** 열에서 데이터를 검색 합니다. 행 및 호출의 일부 열에 바인딩할 수 있지만 **SQLGetData** ,이 몇 가지 제한 사항이 적용 됩니다. 자세한 내용은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)합니다.  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>열 바인딩, 바인딩 해제 및 다시 바인딩  
 열은 바인딩된, 바인딩되지 않은, 또는 언제 든 지 결과 집합에서 데이터를 가져온 후에 다시 바인딩할 수 있습니다. 새 바인딩에서는 바인딩을 사용 하는 함수 호출 되는 다음에 적용 합니다. 예를 들어, 응용 프로그램 호출 하는 결과 집합의 열을 바인딩합니다 **SQLFetch**합니다. 드라이버는 바인딩된 버퍼에 데이터를 반환합니다. 이제 응용 프로그램 바인딩을 버퍼 집합을 다른 열을 가정 합니다. 드라이버 새로 바인딩된 버퍼에 방금 가져온 행에 대 한 데이터를 배치 하지 않습니다. 될 때까지 대기 하는 대신 **SQLFetch** 다시 호출 되 고 그런 다음 새로 바인딩된 버퍼의 다음 행에 대 한 데이터를 배치 합니다.  
  
> [!NOTE]  
>  SQL_ATTR_USE_BOOKMARKS 문 특성은 항상 열에 0을 바인딩하기 전에 설정 해야 합니다. 이 필요 하지 않습니다 하지만 것이 좋습니다.  
  
## <a name="binding-columns"></a>열 바인딩  
 응용 프로그램이 호출 열을 바인딩하려면 **SQLBindCol** 를 열 수, 유형, 주소 및 데이터 버퍼의 길이 및 길이/표시기 버퍼의 주소를 전달 합니다. 이러한 주소를 사용 하는 방법에 대 한 내용은 "버퍼 주소를"이이 섹션의 뒷부분에 나오는 참조 하세요. 바인딩 열에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)합니다.  
  
 이러한 버퍼를 사용 하 여 지연 됩니다. 응용 프로그램에 바인딩합니다 이므로 **SQLBindCol** 하지만 드라이버에 다른 함수에서 액세스-namely **SQLBulkOperations**를 **SQLFetch**,  **SQLFetchScroll**, 또는 **SQLSetPos**합니다. 포인터에 지정 되어 있는지 확인 해야 하는 응용 프로그램의 것 **SQLBindCol** 바인딩을 적용 동안 유효 합니다. 이러한 포인터를 사용할 수 없게 허용-버퍼를 해제 하는 예를 들어,-및 다음 유효 하도록 예상 하는 함수 호출 결과 정의 되지 않습니다. 자세한 내용은 [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)합니다.  
  
 새 바인딩을 사용 하 여 대체 될, 열 바인딩되지 또는 문을 해제 될 때까지 바인딩이 적용 됩니다.  
  
## <a name="unbinding-columns"></a>열 바인딩 해제  
 단일 열을 바인딩 해제, 응용 프로그램 호출 **SQLBindCol** 사용 하 여 *ColumnNumber* 열의 수로 설정 하 고 *TargetValuePtr* null 포인터로 설정 합니다. 하는 경우 *ColumnNumber* 바인딩되지 않은 열을 가리키는 **SQLBindCol** 여전히 관계 없이 SQL_SUCCESS를 반환 합니다.  
  
 모든 열을 바인딩 해제, 응용 프로그램 호출 **SQLFreeStmt** 사용 하 여 *fOption* SQL_UNBIND로 설정 합니다. 이 0으로 카드가 SQL_DESC_COUNT 필드를 설정 하 여 수행할 수도 있습니다.  
  
## <a name="rebinding-columns"></a>열 다시 바인딩  
 응용 프로그램 바인딩을 변경 하려면 두 가지 작업 중 하나를 수행할 수 있습니다.  
  
-   호출 **SQLBindCol** 이미 바인딩되어 있는 열에 대 한 새 바인딩을 지정 합니다. 드라이버를 새 인덱스로 이전 바인딩을 덮어씁니다.  
  
-   바인딩 호출에 의해 지정 된 버퍼 주소를 추가할 수에 대 한 오프셋을 지정 **SQLBindCol**합니다. 자세한 내용은 다음 섹션에서는 "바인딩 오프셋입니다."을 참조 하세요.  
  
## <a name="binding-offsets"></a>바인딩 오프셋  
 바인딩 오프셋은 데이터 및 길이/표시기 버퍼의 주소에 추가 되는 값 (에 지정 된 대로 합니다 *TargetValuePtr* 및 *StrLen_or_IndPtr* 인수)는 역참조 전에 합니다. 오프셋을 사용 하는 경우 바인딩에 응용 프로그램의 버퍼 레이아웃 하는 방법,의 "템플릿" 하 고 응용 프로그램 메모리의 다른 영역에 오프셋을 변경 하 여에 "템플릿"이를 이동할 수 있습니다. 각 바인딩에 각 주소에 동일한 오프셋을 추가 하기 때문에 다른 열에 대 한 버퍼 간에 상대적 오프셋이 버퍼의 각 집합 내에서 동일 해야 합니다. 이 경우 항상 true 행 단위 바인딩을 사용 됩니다. 해당 버퍼 열 단위 바인딩을 사용 하는 경우 true로 응용 프로그램 레이아웃 신중 하 게 해야 합니다.  
  
 에 대 한 바인딩 오프셋을 사용 하 여 기본적으로 호출 하 여 열을 다시 바인딩해야 하는 것과 같습니다 **SQLBindCol**합니다. 차이점은이 새로 호출 되도록 **SQLBindCol** 의 바인딩 오프셋을 사용 하 여 주소를 변경 되지 않지만 오프셋을 추가 하는 반면 데이터 버퍼 및 길이/표시기 버퍼에 대 한 새 주소를 지정 합니다. 응용 프로그램 브로드캐스트하며,이 오프셋은 항상 원래 바인딩된 주소에 추가 될 때마다 새 오프셋을 지정할 수 있습니다. 특히, 오프셋은 0으로 설정 또는 문 특성 null 포인터로 설정 된 경우 드라이버는 원래 바인딩된 주소를 사용 합니다.  
  
 바인딩 오프셋을 지정 하려면 응용 프로그램을 SQLINTEGER 버퍼의 주소에 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 설정 합니다. 응용 프로그램 바인딩을 사용 하는 함수를 호출 하기 전에이 버퍼의 바이트 오프셋을 배치 합니다. 사용할 버퍼의 주소를 확인 하려면 드라이버 바인딩 주소 오프셋을 추가 합니다. 주소와 오프셋의 합계는 유효한 주소 여야 합니다. 하지만 오프셋 추가 되는 주소를 사용할 필요가 없습니다. 바인딩 오프셋을 사용 하는 방법에 대 한 자세한 내용은 "버퍼 주소를"이이 섹션의 뒷부분에 나오는 참조 하세요.  
  
## <a name="binding-arrays"></a>배열 바인딩  
 행 집합 크기 (SQL_ATTR_ROW_ARRAY_SIZE 문 특성의 값)이 1 보다 크면 응용 프로그램에 단일 버퍼 대신 버퍼 배열을 바인딩합니다. 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)합니다.  
  
 응용 프로그램에는 두 가지 방법으로 배열을 바인딩할 수 있습니다.  
  
-   배열을 각 열에 바인딩하십시오. 이 이라고 *열 단위 바인딩을* 각 데이터 구조 (배열)에 단일 열에 대 한 데이터가 포함 되어 있으므로.  
  
-   하는 전체 행에 대 한 데이터를 저장 하 고 이러한 구조의 배열 바인딩 구조를 정의 합니다. 이 이라고 *행 단위 바인딩은* 단일 행에 대 한 데이터를 포함 하는 각 데이터 구조 때문입니다.  
  
 각 배열 버퍼의 행 집합의 크기로 이상의 요소가 있어야 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 맞춤이 유효한 지 확인 해야 합니다. 맞춤 고려 사항에 대 한 자세한 내용은 참조 하세요. [맞춤](../../../odbc/reference/develop-app/alignment.md)합니다.  
  
## <a name="column-wise-binding"></a>열 단위 바인딩  
 열 단위 바인딩을 응용 프로그램은 별도 데이터 및 길이/표시기 배열을 각 열에 바인딩합니다.  
  
 열 단위 바인딩을 사용 하려면 응용 프로그램을 sql_bind_by_column으로 설정 SQL_ATTR_ROW_BIND_TYPE 문 특성 먼저 설정 합니다. (이것이 기본값입니다.) 응용 프로그램을 바인딩할 각 열에 대해 다음 단계를 수행 합니다.  
  
1.  데이터 버퍼 배열을 할당합니다.  
  
2.  길이/표시기 버퍼 배열을 할당합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 열 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 별도 배열 길이 및 표시기 데이터에 대해 사용할 수 있습니다.  
  
3.  호출 **SQLBindCol** 다음 인수를 사용 합니다.  
  
    -   *TargetType* 유형 데이터 버퍼 배열의 단일 요소입니다.  
  
    -   *TargetValuePtr* 주소 데이터 버퍼 배열입니다.  
  
    -   *BufferLength* 데이터 버퍼 배열의 단일 요소 크기입니다. 합니다 *BufferLength* 데이터는 고정 길이 데이터 인수는 무시 됩니다.  
  
    -   *StrLen_or_IndPtr* 주소 길이/표시기 배열입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은 "버퍼 주소를"이이 섹션의 뒷부분에 나오는 참조 하세요. 열 단위 바인딩에 대 한 자세한 내용은 참조 하세요. [열 단위 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)합니다.  
  
## <a name="row-wise-binding"></a>행 단위 바인딩  
 행 단위 바인딩은 응용 프로그램 바인딩할 각 열에 대 한 데이터 및 길이/표시기 버퍼를 포함 하는 구조체를 정의 합니다.  
  
 행 단위 바인딩을 사용 하려면 응용 프로그램에는 다음 단계를 수행 합니다.  
  
1.  구조 데이터 (데이터 및 길이/표시기 버퍼 등)의 단일 행을 보관할 수를 정의 하 고 이러한 구조 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 행 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 별도 필드 길이 및 표시기 데이터에 대해 사용할 수 있습니다.  
  
2.  데이터의 단일 행을 포함 하는 구조체의 크기 또는 인스턴스는 결과 열 바인딩될 버퍼의 크기를 SQL_ATTR_ROW_BIND_TYPE 문 특성을 설정 합니다. 길이 바인딩된 모든 열 및 구조 또는 바인딩된 열의 주소가 지정된 된 길이 사용 하 여 증가 하는 경우 다음 행에 있는 동일한 열의 시작 부분에 결과 가리키게 됩니다 있도록 버퍼의 패딩에 대 한 공간을 포함 해야 합니다. 사용 하는 경우는 *sizeof* ANSI c에서 연산자를이 동작이 유지 됩니다.  
  
3.  호출 **SQLBindCol** 바인딩할 각 열에 대해 다음 인수를 사용 합니다.  
  
    -   *TargetType* 열에 바인딩될 버퍼 데이터 멤버의 형식입니다.  
  
    -   *TargetValuePtr* 첫 번째 배열 요소에 데이터 버퍼 멤버의 주소입니다.  
  
    -   *BufferLength* 데이터 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은 "버퍼 주소를"이이 섹션의 뒷부분에 나오는 참조 하세요. 열 단위 바인딩에 대 한 자세한 내용은 참조 하세요. [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)합니다.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 합니다 *버퍼 주소* 데이터 또는 길이/표시기 버퍼의 실제 주소입니다. 드라이버 (예: 가져오기 시간 동안) 버퍼에 쓰기 전에 방금 버퍼 주소를 계산 합니다. 에 지정 된 주소를 사용 하는 다음 수식에서 계산 되는 *TargetValuePtr* 및 *StrLen_or_IndPtr* 인수, 바인딩 오프셋 및 행 번호:  
  
 *주소에 바인딩된* + *오프셋 바인딩* + ((*행 번호* – 1) x *요소 크기*)  
  
 여기서는 다음 표에 설명 된 대로 수식의 변수에 정의 됩니다.  
  
|변수|Description|  
|--------------|-----------------|  
|*바인딩된 주소*|데이터 버퍼 주소를 사용 하 여 지정 된 *TargetValuePtr* 에서 인수 **SQLBindCol**합니다.<br /><br /> 길이/표시기 버퍼 주소를 사용 하 여 지정 된 *StrLen_or_IndPtr* 에서 인수 **SQLBindCol**합니다. 자세한 내용은 "추가 주석을" "설명자 및 SQLBindCol" 섹션에서을 참조 하세요.<br /><br /> 바인딩된 주소를이 0 인 경우 데이터 값이 없는 이전 수식에서 계산 된 대로 주소 0이 아닌 경우에 반환 됩니다.|  
|*바인딩 오프셋*|행 단위 바인딩을 사용 하는 경우 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 사용 하 여 주소에서 저장 된 값을 지정 합니다.<br /><br /> 열 단위 바인딩을 사용 하는 경우 또는 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성의 값이 null 포인터인 경우 *바인딩 오프셋* 은 0입니다.|  
|*행 번호*|행 집합의 행 수가 1부터 시작 합니다. 기본값 이므로 단일 행 인출,이 1입니다.|  
|*요소 크기*|바인딩된 배열의 요소 크기입니다.<br /><br /> 열 단위 바인딩을 사용 하는 경우 이것이 **sizeof(SQLINTEGER)** 길이/표시기 버퍼에 대 한 합니다. 값 데이터 버퍼에 대 한 것을 *BufferLength* 인수에 **SQLBindCol** 경우 데이터 형식이 고정 길이 인지 하는 경우 데이터 형식은 가변 길이 및 데이터 형식의 크기입니다.<br /><br /> 행 단위 바인딩을 사용 하는 경우 데이터와 길이/표시기 버퍼에 대 한 SQL_ATTR_ROW_BIND_TYPE 문 특성의 값입니다.|  
  
## <a name="descriptors-and-sqlbindcol"></a>설명자 및 SQLBindCol  
 다음 섹션에서는 설명 하는 방법 **SQLBindCol** 설명자와 상호 작용 합니다.  
  
> [!CAUTION]  
>  호출 **SQLBindCol** 하나의 문으로 다른 문의 영향을 줄 수에 대 한 합니다. 이 발생 된 문과 연결 된 카드가 명시적으로 할당 되 고 있을 때 다른 문과 사용 하 여 연결 합니다. 때문에 **SQLBindCol** 설명자로 수정이 설명자와 연결 된 모든 문이에 수정 내용을 적용 합니다. 이 없는 경우 필요한 동작을 호출 하기 전에 응용 프로그램이 다른 문에서이 설명자를 분리 해야 **SQLBindCol**합니다.  
  
## <a name="argument-mappings"></a>인수 매핑  
 개념상 **SQLBindCol** 시퀀스에서 다음 단계를 수행 합니다.  
  
1.  호출 **SQLGetStmtAttr** 카드가 핸들을 가져올 수 있습니다.  
  
2.  호출 **SQLGetDescField** 이 설명자의 SQL_DESC_COUNT 필드를 가져오려는 경우에 값을 *ColumnNumber* SQL_DESC_COUNT, 호출의 값을 초과 하는 인수 **SQLSetDescField**  SQL_DESC_COUNT에 가치를 높일 *ColumnNumber*합니다.  
  
3.  호출 **SQLSetDescField** 여러 번의 카드가의 다음 필드에 값을 할당 합니다.  
  
    -   SQL_DESC_TYPE과 SQL_DESC_CONCISE_TYPE의 값을 설정 *TargetType*점을 제외 하 고, 경우 *TargetType* 하나인 datetime 또는 간격 하위 형식의 간결한 식별자, SQL_에 SQL_DESC_TYPE 설정 날짜/시간 또는 sql_interval 인, 각각. SQL_DESC_CONCISE_TYPE 간결한 식별자;로 설정합니다. 및 해당 날짜/시간 또는 간격 하위 코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE 집합을 추가 합니다.  
  
    -   적합 한 SQL_DESC_LENGTH, 자릿수가 SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, 및 SQL_DESC_DATETIME_INTERVAL_PRECISION, 중 하나 이상을 설정 *TargetType*합니다.  
  
    -   SQL_DESC_OCTET_LENGTH 필드의 값으로 설정 *BufferLength*합니다.  
  
    -   값에 SQL_DESC_DATA_PTR 필드가 설정 *TargetValue*합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드의 값으로 설정 *StrLen_or_Ind*합니다. (다음 단락 참조).  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드의 값으로 설정 *StrLen_or_Ind*합니다. (다음 단락 참조).  
  
 변수는 합니다 *StrLen_or_Ind* 인수가 참조 하는 표시기 및 길이 정보에 사용 됩니다. 이 변수에; SQL_NULL_DATA 저장 페치 열에 null 값을 발견 하면, 그렇지 않으면 데이터 길이이 변수에 저장 합니다. 로 null 포인터를 전달 *StrLen_or_Ind* 데이터 길이 반환 하는 페치 작업을 유지 하지만 null 값이 있는 경우에 SQL_NULL_DATA를 반환할 수 없으므로 실패 fetch를 사용 하면 됩니다.  
  
 경우에 대 한 호출 **SQLBindCol** 실패에 카드가 설정한 것과 설명자 필드의 내용을 정의 되지 않습니다 하 고는 카드가 SQL_DESC_COUNT 필드의 값이 변경 되지 않습니다.  
  
## <a name="implicit-resetting-of-count-field"></a>COUNT 필드를 암시적으로 재설정  
 **SQLBindCol** SQL_DESC_COUNT 값으로 설정 합니다 *ColumnNumber* 인수 SQL_DESC_COUNT의 값이 증가 하는 경우에 합니다. 경우 값을 *TargetValuePtr* 인수가 null 포인터 및 값을 *ColumnNumber* 인수가 SQL_DESC_COUNT 같음 (즉, 가장 높은 바인딩 해제에 바인딩된 경우 열) 다음 SQL_DESC_ 수는 가장 높은 나머지 바인딩된 열 수가 설정 됩니다.  
  
## <a name="cautions-regarding-sqldefault"></a>SQL_DEFAULT 관련 주의 사항  
 열 데이터를 성공적으로 검색 하려면 응용 프로그램 응용 프로그램 버퍼에 있는 데이터의 시작 지점과 길이가 올바르게 확인 해야 합니다. 응용 프로그램은 명시적인 지정 하면 *TargetType*, 응용 프로그램 오해 쉽게 감지 합니다. 그러나 응용 프로그램을 지정 하면를 *TargetType* SQL_DEFAULT의 **SQLBindCol** 에 적용할 수는 다른 데이터 형식의 열에서 원하는 변경에서 응용 프로그램에 메타 데이터 또는 다른 열에는 코드를 적용 하 여 합니다. 이 경우 응용 프로그램 수 항상 확인할 인출된 열 데이터의 길이 시작 합니다. 이 보고 되지 않은 데이터 오류 또는 메모리 위반이 발생할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 실행을 **선택** 이름별로 정렬 Id, 이름 및 전화 번호, 고객의 결과 집합을 반환할 고객 테이블에 문의 합니다. 그런 다음 호출 **SQLBindCol** 로컬 버퍼에 데이터의 열을 바인딩합니다. 응용 프로그램에서 사용 하 여 데이터의 각 행을 인출 하는 마지막으로, **SQLFetch** 하 고 각 고객의 이름, ID 및 전화 번호를 출력 합니다.  
  
 더 많은 코드 예제를 참조 하세요 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)를 [SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)를 [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md), 및 [SQLSetPos함수](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 참조 하세요 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터를 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|문에서 열 버퍼를 해제합니다.|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|일부 또는 전체 열의 데이터 페치|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
