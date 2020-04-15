---
title: SQLBindCol 함수 | 마이크로 소프트 문서
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298743"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLBindCol은** 결과 집합의 열에 응용 프로그램 데이터 버퍼를 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] 바인딩할 결과 집합 열의 수입니다. 열은 0부터 시작하는 열 순서로 번호가 매겨지며 열0은 책갈피 열입니다. 책갈피를 사용하지 않는 경우(즉, SQL_ATTR_USE_BOOKMARKS 문 특성은 SQL_UB_OFF 설정된 다음 열 번호는 1에서 시작합니다.  
  
 *Targettype*  
 [입력] \* *TargetValuePtr* 버퍼의 C 데이터 형식의 식별자입니다. **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**또는 **SQLSetPos를**사용하여 데이터 원본에서 데이터를 검색할 때 드라이버는 데이터를 이 유형으로 변환합니다. **SQLBulkOperations** 또는 **SQLSetPos를**사용 하 고 데이터 원본에 데이터를 보낼 때 드라이버는이 형식에서 데이터를 변환 합니다. 유효한 C 데이터 유형 및 유형 식별자 목록은 부록 D: 데이터 [형식의 C 데이터 유형](../../../odbc/reference/appendixes/c-data-types.md) 섹션을 참조하십시오.  
  
 *TargetType* 인수가 간격 데이터 형식인 경우 ARD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정된 기본 간격 정밀도(2)와 기본 간격 초 정밀도(6)가 각각 데이터에 사용됩니다. *TargetType* 인수가 SQL_C_NUMERIC 경우 ARD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정된 기본 정밀도(드라이버 정의) 및 기본 눈금(0)이 데이터에 사용됩니다. 기본 정밀도 또는 배율이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**을 호출하여 적절한 설명자 필드를 명시적으로 설정해야 합니다.  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 유형을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.  
  
 *대상 밸류프트*  
 [지연된 입력/출력] 열에 바인딩할 데이터 버퍼에 대한 포인터입니다. **SQLFetch** 및 **SQLFetchScroll이** 버퍼에서 데이터를 반환합니다. **SQLBulkOperations는** *작업이* SQL_FETCH_BY_BOOKMARK 때 이 버퍼에서 데이터를 반환합니다. *작업은* SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK 때 이 버퍼에서 데이터를 검색합니다. **SQLSetPos** *는 작업이* SQL_REFRESH 때 이 버퍼에서 데이터를 반환합니다. *는 작업이* SQL_UPDATE 때 이 버퍼에서 데이터를 검색합니다.  
  
 *TargetValuePtr이* null 포인터인 경우 드라이버는 열에 대한 데이터 버퍼를 바인딩 해제합니다. 응용 프로그램은 SQL_UNBIND 옵션으로 **SQLFreeStmt를** 호출하여 모든 열을 바인딩 해제할 수 있습니다. **SQLBindCol** 호출의 *TargetValuePtr* 인수가 null 포인터이지만 *StrLen_or_IndPtr* 인수가 유효한 값인 경우 응용 프로그램은 열에 대한 데이터 버퍼를 바인딩해제할 수 있지만 열에 대한 길이/표시기 버퍼 바인딩이 여전히 있습니다.  
  
 *버퍼 길이*  
 [입력] \* *TargetValuePtr* 버퍼의 바이트 길이입니다.  
  
 드라이버는 *BufferLength를* 사용하여 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 때 \* *TargetValuePtr* 버퍼의 끝을 지나서 작성하지 않도록 합니다. 드라이버는 \* *TargetValuePtr에*문자 데이터를 반환할 때 null-종료 문자를 계산합니다. \*따라서 *TargetValuePtr은* null 종료 문자에 대한 공간을 포함해야 하거나 드라이버가 데이터를 트렁킨다.  
  
 드라이버가 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환하면 드라이버는 *BufferLength를* 무시하고 버퍼가 데이터를 보유할 수 있을 만큼 충분히 크다고 가정합니다. 따라서 응용 프로그램이 고정 길이 데이터에 대해 충분히 큰 버퍼를 할당하거나 드라이버가 버퍼의 끝을 지나 서 작성하는 것이 중요합니다.  
  
 **SQLBindCol은** *버퍼 길이가* 0보다 작지만 *버퍼* 길이가 0인 경우 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환합니다. 그러나 *TargetType이* 문자 형식을 지정하는 경우 ISO CLI 호환 드라이버가 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환하기 때문에 응용 프로그램은 *BufferLength를* 0으로 설정하지 않아야 합니다.  
  
 *StrLen_or_IndPtr*  
 [지연된 입력/출력] 열에 바인딩할 길이/표시기 버퍼에 대한 포인터입니다. **SQLFetch** 및 **SQLFetchScroll이** 버퍼에서 값을 반환합니다. **SQLBulkOperations는** *작업이* SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 때 이 버퍼에서 값을 검색합니다. **SQLBulkOperations는** *작업이* SQL_FETCH_BY_BOOKMARK 때 이 버퍼에서 값을 반환합니다. **SQLSetPos** *는 작업이* SQL_REFRESH 때 이 버퍼에서 값을 반환합니다. *작업이* SQL_UPDATE 때 이 버퍼에서 값을 검색합니다.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**및 **SQLSetPos는** 길이 / 표시기 버퍼에서 다음 값을 반환 할 수 있습니다 .  
  
-   반환할 수 있는 데이터의 길이  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 응용 프로그램은 **SQLBulkOperations** 또는 **SQLSetPos와**함께 사용하기 위해 길이 / 표시기 버퍼에 다음 값을 넣을 수 있습니다.  
  
-   전송되는 데이터의 길이  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 매크로의 결과  
  
-   SQL_COLUMN_IGNORE  
  
 표시기 버퍼와 길이 버퍼가 별도의 버퍼인 경우 표시기 버퍼는 SQL_NULL_DATA 반환할 수 있는 반면 길이 버퍼는 다른 모든 값을 반환할 수 있습니다.  
  
 자세한 내용은 [SQLBulkOperations 함수,](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLFetch 함수,](../../../odbc/reference/syntax/sqlfetch-function.md) [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)및 [길이/표시기 값 사용을](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)참조하십시오.  
  
 *StrLen_or_IndPtr* null 포인터인 경우 길이 또는 표시기 값이 사용되지 않습니다. 데이터를 가져올 때 오류가 발생하며 데이터가 NULL입니다.  
  
 [64비트](../../../odbc/reference/odbc-64-bit-information.md)운영 체제에서 응용 프로그램이 실행되는 경우 ODBC 64비트 정보를 참조하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLBindCol** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **SQLBindCol에서** 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|(DM) *ColumnNumber* 인수가 0이고 *TargetType* 인수가 SQL_C_BOOKMARK SQL_C_VARBOOKMARK 않았습니다.|  
|07009|잘못된 설명자 인덱스|인수 *ColumnNumber에* 대해 지정된 값이 결과 집합의 최대 열 수를 초과했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|잘못된 응용 프로그램 버퍼 유형|TargetType *TargetType* 인수는 유효한 데이터 형식도 아니며 SQL_C_DEFAULT.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLBindCol이** 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 BufferLength에* 대해 지정된 값이 0보다 적습니다.<br /><br /> (DM) 드라이버는 ODBC 2였습니다. *x* 드라이버, *ColumnNumber* 인수가 0으로 설정되었으며 인수 *BufferLength에* 대해 지정된 값이 4와 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 *TargetType* 인수와 해당 열의 드라이버 별 SQL 데이터 형식의 조합으로 지정된 변환을 지원하지 않습니다.<br /><br /> *ColumnNumber* 인수가 0이고 드라이버는 책갈피를 지원하지 않습니다.<br /><br /> 드라이버는 ODBC 2만 지원합니다. *x* 및 인수 *TargetType은* 다음 중 하나입니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 부록 D: 데이터 형식의 [C 데이터 형식에](../../../odbc/reference/appendixes/c-data-types.md) 나열된 간격 C 데이터 형식중 어느 쪽도 해당합니다.<br /><br /> 드라이버는 3.50 이전의 ODBC 버전만 지원하며 *TargetType* 인수가 SQL_C_GUID.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLBindCol은** 결과 집합의 열을 응용 프로그램의 데이터 버퍼 및 길이/표시기 버퍼에 연결하거나 *바인딩하는* 데 사용됩니다. 응용 프로그램에서 **SQLFetch,** **SQLFetchScroll**또는 **SQLSetPos를** 호출하여 데이터를 가져오면 드라이버는 지정된 버퍼에서 바인딩된 열에 대한 데이터를 반환합니다. 자세한 내용은 [SQLFetch 함수를](../../../odbc/reference/syntax/sqlfetch-function.md)참조하십시오. 응용 프로그램이 **SQLBulkOperations를** 호출하여 **행을** 업데이트하거나 삽입하여 행을 업데이트할 때 드라이버는 지정된 버퍼에서 바인딩된 열에 대한 데이터를 검색합니다. 자세한 내용은 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 또는 [SQLSetPos 함수를](../../../odbc/reference/syntax/sqlsetpos-function.md)참조하십시오. 바인딩에 대한 자세한 내용은 [결과 검색(기본)을](../../../odbc/reference/develop-app/retrieving-results-basic.md)참조하십시오.  
  
 열에서 데이터를 검색하기 위해 바인딩할 필요는 없습니다. 응용 프로그램은 **SQLGetData를** 호출하여 열에서 데이터를 검색할 수도 있습니다. 행의 일부 열을 바인딩하고 다른 열에 대해 **SQLGetData를** 호출할 수 있지만 일부 제한 사항이 적용됩니다. 자세한 내용은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)를 참조하십시오.  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>바인딩, 바인딩 해제 및 바인딩 바인딩 다시 바인딩  
 결과 집합에서 데이터를 가져온 후에도 언제든지 열을 바인딩, 언바운드 또는 리바운드할 수 있습니다. 새 바인딩은 다음에 바인딩을 사용하는 함수가 호출될 때 적용됩니다. 예를 들어 응용 프로그램이 결과 집합에서 열을 바인딩하고 **SQLFetch**를 호출한다고 가정합니다. 드라이버는 바인딩된 버퍼에서 데이터를 반환합니다. 이제 응용 프로그램이 다른 버퍼 집합에 열을 바인딩한다고 가정합니다. 드라이버는 새로 바인딩된 버퍼에 방금 가져온 행에 대한 데이터를 넣지 않습니다. 대신 **SQLFetch가** 다시 호출될 때까지 기다린 다음 새로 바인딩된 버퍼에 다음 행에 대한 데이터를 배치합니다.  
  
> [!NOTE]  
>  SQL_ATTR_USE_BOOKMARKS 문 특성은 항상 열0에 열을 바인딩하기 전에 설정해야 합니다. 필수는 아니지만 강력히 권장됩니다.  
  
## <a name="binding-columns"></a>열 바인딩  
 열을 바인딩하기 위해 응용 프로그램은 **SQLBindCol을** 호출하고 데이터 버퍼의 열 번호, 형식, 주소 및 길이 및 길이/표시기 버퍼의 주소를 전달합니다. 이러한 주소를 사용하는 방법에 대한 자세한 내용은 이 섹션의 다음 부분의 "버퍼 주소"를 참조하십시오. 바인딩 열에 대한 자세한 내용은 [SQLBindCol 을 참조하십시오.](../../../odbc/reference/develop-app/using-sqlbindcol.md)  
  
 이러한 버퍼의 사용은 지연됩니다. 즉, 응용 프로그램은 **SQLBindCol에서** 바인딩하지만 드라이버는 **SQLBulkOperations,** **SQLFetch**, **SQLFetchScroll**또는 **SQLSetPos**와 같은 다른 함수에서 액세스합니다. 바인딩이 그대로 유지되는 한 **SQLBindCol에** 지정된 포인터가 유효한지 확인하는 것은 응용 프로그램의 책임입니다. 응용 프로그램에서 이러한 포인터가 유효하지 않게 하는 경우(예: 버퍼를 해제한 다음 유효할 것으로 예상되는 함수를 호출하면 결과는 정의되지 않습니다). 자세한 내용은 [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)를 참조하십시오.  
  
 바인딩은 새 바인딩으로 대체될 때까지 유효하며, 열이 언바운드이거나 문이 해제될 때까지 유지됩니다.  
  
## <a name="unbinding-columns"></a>바인딩 해제 열  
 단일 열을 바인딩해제하기 위해 응용 프로그램은 *ColumnNumber를* 사용하여 **SQLBindCol을** 해당 열의 수로 설정하고 *TargetValuePtr은* null 포인터로 설정합니다. *ColumnNumber가* 언바운드 열을 참조하는 경우 **SQLBindCol은** 여전히 SQL_SUCCESS 반환합니다.  
  
 모든 열을 바인딩 해제하려면 응용 프로그램이 SQL_UNBIND *fOption을* 설정한 **SQLFreeStmt를** 호출합니다. 또한 ARD의 SQL_DESC_COUNT 필드를 0으로 설정하여 수행할 수도 있습니다.  
  
## <a name="rebinding-columns"></a>열 바인딩 다시  
 응용 프로그램은 바인딩을 변경하기 위해 두 작업 중 하나를 수행할 수 있습니다.  
  
-   **SQLBindCol을** 호출하여 이미 바인딩된 열에 대한 새 바인딩을 지정합니다. 드라이버는 이전 바인딩을 새 바인딩으로 덮어씁니다.  
  
-   **SQLBindCol**에 대한 바인딩 호출에 의해 지정된 버퍼 주소에 추가할 오프셋을 지정합니다. 자세한 내용은 다음 섹션인 "바인딩 오프셋"을 참조하십시오.  
  
## <a name="binding-offsets"></a>바인딩 오프셋  
 바인딩 오프셋은 데이터 및 길이/표시기 버퍼의 주소에 추가되는 값입니다(TargetValuePtr 및 *StrLen_or_IndPtr* 인수에 지정된 대로). *TargetValuePtr* 오프셋을 사용할 때 바인딩은 응용 프로그램의 버퍼가 배치되는 방식의 "템플릿"이며 응용 프로그램은 오프셋을 변경하여 이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 각 바인딩의 각 주소에 동일한 오프셋이 추가되므로 서로 다른 열에 대한 버퍼 간의 상대 오프셋은 각 버퍼 집합 내에서 동일해야 합니다. 행 별 바인딩을 사용할 때항상 마찬가지입니다. 응용 프로그램은 열 별 바인딩을 사용할 때 이를 적용하기 위해 해당 버퍼를 신중하게 배치해야 합니다.  
  
 바인딩 오프셋을 사용하면 기본적으로 **SQLBindCol**을 호출하여 열을 다시 바인딩하는 것과 동일한 효과가 있습니다. 차이점은 **SQLBindCol에** 대한 새 호출이 데이터 버퍼 및 길이/표시기 버퍼에 대한 새 주소를 지정하는 반면 바인딩 오프셋을 사용하면 주소가 변경되지 않고 오프셋만 추가된다는 점입니다. 응용 프로그램은 원할 때마다 새 오프셋을 지정할 수 있으며 이 오프셋은 항상 원래 바인딩된 주소에 추가됩니다. 특히 오프셋이 0으로 설정되어 있거나 문 특성이 null 포인터로 설정된 경우 드라이버는 원래 바인딩된 주소를 사용합니다.  
  
 바인딩 오프셋을 지정하기 위해 응용 프로그램은 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 SQLINTEGER 버퍼의 주소로 설정합니다. 응용 프로그램에서 바인딩을 사용하는 함수를 호출하기 전에 이 버퍼에 바이트에 오프셋을 넣습니다. 사용할 버퍼의 주소를 결정하기 위해 드라이버는 바인딩의 주소에 오프셋을 추가합니다. 주소와 오프셋의 합계는 유효한 주소여야 하지만 오프셋이 추가되는 주소는 유효할 필요는 없습니다. 바인딩 오프셋을 사용하는 방법에 대한 자세한 내용은 이 섹션의 후반부 "버퍼 주소"를 참조하십시오.  
  
## <a name="binding-arrays"></a>바인딩 배열  
 행 집합 크기(SQL_ATTR_ROW_ARRAY_SIZE 문 특성값)가 1보다 큰 경우 응용 프로그램은 단일 버퍼 대신 버퍼 배열을 바인딩합니다. 자세한 내용은 [커서 블록](../../../odbc/reference/develop-app/block-cursors.md)을 참조하십시오.  
  
 응용 프로그램은 다음 두 가지 방법으로 배열을 바인딩할 수 있습니다.  
  
-   배열을 각 열에 바인딩합니다. 각 데이터 구조(배열)에는 단일 열에 대한 데이터가 포함되어 있으므로 *열별 바인딩이라고* 합니다.  
  
-   전체 행에 대한 데이터를 보관하고 이러한 구조의 배열을 바인딩할 구조를 정의합니다. 각 데이터 구조에 단일 행에 대한 데이터가 포함되어 있으므로 *행 별 바인딩이라고* 합니다.  
  
 각 버퍼 배열에는 행 집합 크기만큼 많은 요소가 있어야 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 정렬이 유효한지 확인해야 합니다. 정렬 고려 사항에 대한 자세한 내용은 [정렬](../../../odbc/reference/develop-app/alignment.md)을 참조하십시오.  
  
## <a name="column-wise-binding"></a>열 단위 바인딩  
 열 별 바인딩에서 응용 프로그램은 각 열에 별도의 데이터와 길이/표시기 배열을 바인딩합니다.  
  
 열 별 바인딩을 사용 하려면 응용 프로그램은 먼저 SQL_BIND_BY_COLUMN SQL_ATTR_ROW_BIND_TYPE 문 특성을 설정 합니다. 기본값입니다. 바인딩할 각 열을 위해 응용 프로그램은 다음 단계를 수행합니다.  
  
1.  데이터 버퍼 배열을 할당합니다.  
  
2.  길이/표시기 버퍼의 배열을 할당합니다.  
  
    > [!NOTE]  
    >  열 별 바인딩을 사용할 때 응용 프로그램이 설명자에게 직접 쓰는 경우 길이 및 표시기 데이터에 별도의 배열을 사용할 수 있습니다.  
  
3.  다음과 같은 인수를 통해 **SQLBindCol을** 호출합니다.  
  
    -   *TargetType은* 데이터 버퍼 배열의 단일 요소 의 형식입니다.  
  
    -   *TargetValuePtr은* 데이터 버퍼 배열의 주소입니다.  
  
    -   *BufferLength는* 데이터 버퍼 배열의 단일 요소의 크기입니다. 데이터가 고정 길이 데이터인 경우 *BufferLength* 인수는 무시됩니다.  
  
    -   *StrLen_or_IndPtr* 길이/표시기 배열의 주소입니다.  
  
 이 정보가 사용되는 방법에 대한 자세한 내용은 이 섹션의 "버퍼 주소"를 참조하십시오. 열 별 바인딩에 대한 자세한 내용은 [열 별 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)을 참조하십시오.  
  
## <a name="row-wise-binding"></a>행 단위 바인딩  
 행별 바인딩에서 응용 프로그램은 바인딩할 각 열에 대한 데이터 및 길이/표시기 버퍼를 포함하는 구조를 정의합니다.  
  
 행 별 바인딩을 사용 하려면 응용 프로그램은 다음 단계를 수행 합니다.  
  
1.  단일 데이터 행(데이터 및 길이/표시기 버퍼 포함)을 보유하는 구조를 정의하고 이러한 구조의 배열을 할당합니다.  
  
    > [!NOTE]  
    >  행 별 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰는 경우 길이 및 표시기 데이터에 대해 별도의 필드를 사용할 수 있습니다.  
  
2.  SQL_ATTR_ROW_BIND_TYPE 문 특성을 단일 데이터 행을 포함하는 구조의 크기 또는 결과 열이 바인딩되는 버퍼의 인스턴스 크기로 설정합니다. 길이에는 바인딩된 열의 주소가 지정된 길이로 증가될 때 결과가 다음 행의 동일한 열의 시작을 가리키도록 하기 위해 모든 바인딩된 열과 구조 또는 버퍼의 패딩에 대한 공간이 포함되어야 합니다. ANSI C에서 *sizeof* 연산자사용 시 이 동작이 보장됩니다.  
  
3.  바인딩할 각 열에 대 한 다음 인수를 **사용하여 SQLBindCol을** 호출합니다.  
  
    -   *TargetType은* 열에 바인딩할 데이터 버퍼 멤버의 형식입니다.  
  
    -   *TargetValuePtr은* 첫 번째 배열 요소의 데이터 버퍼 멤버의 주소입니다.  
  
    -   *버퍼길이는* 데이터 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보가 사용되는 방법에 대한 자세한 내용은 이 섹션의 "버퍼 주소"를 참조하십시오. 열 별 바인딩에 대한 자세한 내용은 [행 별 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)을 참조하십시오.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 *버퍼 주소는* 데이터 또는 길이/표시기 버퍼의 실제 주소입니다. 드라이버는 버퍼에 기록하기 직전에 버퍼 주소를 계산합니다(예: 가져오기 시간 중). *TargetValuePtr에* 지정된 주소와 *StrLen_or_IndPtr* 인수, 바인딩 오프셋 및 행 번호를 사용하는 다음 수식에서 계산됩니다.  
  
 *바인딩된 주소* + *바인딩 오프셋* +(행*번호* - 1) x *요소 크기)*  
  
 여기서 수식의 변수는 다음 표에 설명된 대로 정의됩니다.  
  
|변수|설명|  
|--------------|-----------------|  
|*바운드 주소*|데이터 버퍼의 경우 **SQLBindCol**에서 *TargetValuePtr* 인수로 지정된 주소입니다.<br /><br /> 길이/표시기 버퍼의 경우 **SQLBindCol**에서 *StrLen_or_IndPtr* 인수로 지정된 주소입니다. 자세한 내용은 "설명자 및 SQLBindCol" 절의 "추가 주석" 섹션을 참조하십시오.<br /><br /> 바인딩된 주소가 0이면 이전 수식에서 계산한 주소가 0이 아니더라도 데이터 값이 반환되지 않습니다.|  
|*바인딩 오프셋*|행 별 바인딩을 사용하는 경우 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성으로 지정된 주소에 저장된 값입니다.<br /><br /> 열 별 바인딩을 사용하거나 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성의 값이 null 포인터인 경우 *바인딩 오프셋은* 0입니다.|  
|*Row Number*|행 집합의 행의 1기반 번호입니다. 기본값인 단일 행 인출의 경우 1입니다.|  
|*요소 크기*|바인딩된 배열의 요소 크기입니다.<br /><br /> 열 별 바인딩을 사용 하는 경우 길이/표시기 버퍼에 대 한 **sizeof (SQLINTEGER)입니다.** 데이터 버퍼의 경우 데이터 형식이 가변 길이인 경우 **SQLBindCol의** *BufferLength* 인수 값과 데이터 형식이 고정 된 경우 데이터 형식의 크기입니다.<br /><br /> 행 별 바인딩을 사용하는 경우 데이터 및 길이/표시기 버퍼 모두에 대한 SQL_ATTR_ROW_BIND_TYPE 문 특성의 값입니다.|  
  
## <a name="descriptors-and-sqlbindcol"></a>설명자 및 SQLBindCol  
 다음 섹션에서는 **SQLBindCol이** 설명자와 상호 작용하는 방법을 설명합니다.  
  
> [!CAUTION]  
>  하나의 문에 **대해 SQLBindCol을** 호출하면 다른 문에 영향을 줄 수 있습니다. 이 문제는 명령문과 연결된 ARD가 명시적으로 할당되고 다른 명령문과도 연결될 때 발생합니다. **SQLBindCol은** 설명자를 수정하기 때문에 수정 사항은 이 설명자가 연결된 모든 문에 적용됩니다. 필수 동작이 아닌 경우 응용 프로그램은 **SQLBindCol**을 호출하기 전에 다른 명령문에서 이 설명자와 분리해야 합니다.  
  
## <a name="argument-mappings"></a>인수 매핑  
 개념적으로 **SQLBindCol은** 다음 단계를 순서대로 수행합니다.  
  
1.  ARD 핸들을 얻으려면 **SQLGetStmtAttr을** 호출합니다.  
  
2.  이 설명자의 SQL_DESC_COUNT 필드를 얻기 위해 **SQLGetDescField를** 호출하고 *ColumnNumber* 인수의 값이 SQL_DESC_COUNT 값을 초과하는 경우 **SQLSetDescField를** 호출하여 SQL_DESC_COUNT 값을 *ColumnNumber*에 증가시다.  
  
3.  **SQLSetDescField를** 여러 번 호출하여 ARD의 다음 필드에 값을 할당합니다.  
  
    -   *targetType이* datetime 또는 interval 하위 유형의 간결한 식별자 중 하나인 경우를 제외하고 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE *targetType*값으로 SQL_INTERVAL SQL_DATETIME SQL_DESC_TYPE 설정합니다. 간결한 식별자로 SQL_DESC_CONCISE_TYPE 설정합니다. SQL_DESC_DATETIME_INTERVAL_CODE 해당 날짜 시간 또는 간격 하위 코드로 설정합니다.  
  
    -   *targetType에*적합한 SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_DATETIME_INTERVAL_PRECISION 중 하나 이상을 설정합니다.  
  
    -   SQL_DESC_OCTET_LENGTH 필드를 *BufferLength*값으로 설정합니다.  
  
    -   SQL_DESC_DATA_PTR 필드를 *TargetValue*값으로 설정합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드를 *StrLen_or_Ind*값으로 설정합니다. (다음 단락을 참조한다.)  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드를 *StrLen_or_Ind*값으로 설정합니다. (다음 단락을 참조한다.)  
  
 *StrLen_or_Ind* 인수가 참조하는 변수는 표시기 및 길이 정보 모두에 사용됩니다. 가져오기가 열에 대한 null 값을 만나는 경우 이 변수에 SQL_NULL_DATA 저장합니다. 그렇지 않으면 이 변수에 데이터 길이를 저장합니다. StrLen_or_Ind null 포인터를 전달하면 가져오기 작업이 데이터 길이를 반환하지 못하게 되지만 null 값이 발생하고 SQL_NULL_DATA 반환할 방법이 없는 경우 fetch가 실패하게 됩니다. *StrLen_or_Ind*  
  
 **SQLBindCol에** 대한 호출이 실패하면 ARD에서 설정한 설명자 필드의 내용은 정의되지 않으며 ARD의 SQL_DESC_COUNT 필드의 값은 변경되지 않습니다.  
  
## <a name="implicit-resetting-of-count-field"></a>COUNT 필드의 암시적 재설정  
 **SQLBindCol은** SQL_DESC_COUNT 값을 늘릴 때만 *columnNumber* 인수의 값으로 SQL_DESC_COUNT 설정합니다. *TargetValuePtr* 인수의 값이 null 포인터이고 *ColumnNumber* 인수의 값이 SQL_DESC_COUNT (즉, 가장 높은 바인딩 열의 바인딩을 해제할 때)과 같으면 SQL_DESC_COUNT 가장 높은 나머지 바인딩 열의 수로 설정됩니다.  
  
## <a name="cautions-regarding-sql_default"></a>SQL_DEFAULT 주의 사항  
 열 데이터를 성공적으로 검색하려면 응용 프로그램이 응용 프로그램 버퍼에서 데이터의 길이와 시작점을 올바르게 결정해야 합니다. 응용 프로그램이 명시적 *TargetType을*지정하면 응용 프로그램 오해가 쉽게 감지됩니다. 그러나 응용 프로그램이 *targetType* SQL_DEFAULT 지정하면 **SQLBindCol은** 메타데이터에 대한 변경또는 코드를 다른 열에 적용하여 응용 프로그램에서 의도한 것과 다른 데이터 형식의 열에 적용할 수 있습니다. 이 경우 응용 프로그램이 가져온 열 데이터의 시작 또는 길이를 항상 결정하지는 않을 수 있습니다. 이로 인해 보고되지 않은 데이터 오류 또는 메모리 위반이 발생할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 Customers 테이블에서 **SELECT** 문을 실행하여 이름으로 정렬된 고객 ID, 이름 및 전화 번호의 결과 집합을 반환합니다. 그런 다음 **SQLBindCol을** 호출하여 데이터 열을 로컬 버퍼에 바인딩합니다. 마지막으로 응용 프로그램은 **SQLFetch를** 사용하여 데이터의 각 행을 가져오고 각 고객의 이름, ID 및 전화 번호를 인쇄합니다.  
  
 자세한 코드 예제는 [SQLBulkOperations 함수,](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLColumns 함수,](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)및 [SQLSetPos 함수를](../../../odbc/reference/syntax/sqlsetpos-function.md)참조하십시오.  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
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
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
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
  
 또한, [샘플 ODBC 프로그램을](../../../odbc/reference/sample-odbc-program.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 대한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|명령문에 열 버퍼 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|데이터 열의 일부 또는 전체 가져오기|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
