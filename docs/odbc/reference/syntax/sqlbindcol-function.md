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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1c89ff79ee0fcac37f7b6e231e957e051c9db2e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289288"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLBindCol** 는 응용 프로그램 데이터 버퍼를 결과 집합의 열에 바인딩합니다.  
  
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
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *ColumnNumber*  
 입력 바인딩할 결과 집합 열의 수입니다. 열은 0부터 시작 하 여 열 순서를 기준으로 번호가 매겨집니다. 여기서 열 0은 책갈피 열입니다. 책갈피를 사용 하지 않는 경우, 즉 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF로 설정 된 경우 열 번호는 1부터 시작 합니다.  
  
 *TargetType*  
 입력 *Targetvalueptr* 버퍼 \*C 데이터 형식의 식별자입니다. **Sqlfetch**, **sqlfetchscroll**, **SQLBulkOperations**또는 **SQLSetPos**를 사용 하 여 데이터 원본에서 데이터를 검색 하는 경우 드라이버는 데이터를이 형식으로 변환 합니다. **SQLBulkOperations** 또는 **SQLSetPos**를 사용 하 여 데이터 원본에 데이터를 보낼 때 드라이버는이 유형의 데이터를 변환 합니다. 유효한 C 데이터 형식 및 형식 식별자 목록은 부록 D: 데이터 형식의 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션을 참조 하세요.  
  
 *TargetType* 인수가 interval 데이터 형식인 경우에는 데이터에 대 한 기본 간격 선행 전체 자릿수 (2)와 기본 간격 초 전체 자릿수 (6)가 각각의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정 됩니다. *TargetType* 인수가 SQL_C_NUMERIC 이면 데이터에 사용 되는 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 기본 전체 자릿수 (드라이버 정의) 및 기본 소수 자릿수 (0)가 사용 됩니다. 기본 전체 자릿수 또는 소수 자릿수가 적절 하지 않은 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 적절 한 설명자 필드를 명시적으로 설정 해야 합니다.  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)을 참조 하세요.  
  
 *TargetValuePtr*  
 [지연 된 입/출력] 열에 바인딩할 데이터 버퍼에 대 한 포인터입니다. **Sqlfetch** 및 **sqlfetchscroll** 은이 버퍼의 데이터를 반환 합니다. **SQLBulkOperations** 는 *작업이* SQL_FETCH_BY_BOOKMARK 경우이 버퍼에 데이터를 반환 합니다. *작업이* SQL_ADD 되거나 SQL_UPDATE_BY_BOOKMARK 되는 경우이 버퍼에서 데이터를 검색 합니다. *작업이* SQL_REFRESH 되 면 **SQLSetPos** 는이 버퍼의 데이터를 반환 합니다. *작업이* SQL_UPDATE 될 때이 버퍼에서 데이터를 검색 합니다.  
  
 *Targetvalueptr* 이 null 포인터인 경우 드라이버는 열에 대 한 데이터 버퍼의 바인딩을 해제 합니다. 응용 프로그램은 SQL_UNBIND 옵션으로 **SQLFreeStmt** 를 호출 하 여 모든 열의 바인딩을 해제할 수 있습니다. 응용 프로그램은 열에 대 한 데이터 버퍼의 바인딩을 해제할 수 있지만 **SQLBindCol** 에 대 한 호출의 *Targetvalueptr* 인수가 null 포인터이 고 *StrLen_or_IndPtr* 인수가 유효한 값인 경우에는 열에 대 한 길이/표시기 버퍼가 계속 바인딩됩니다.  
  
 *BufferLength*  
 입력 \**Targetvalueptr* 버퍼의 길이 (바이트)입니다.  
  
 드라이버는 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 때 \**Targetvalueptr* 버퍼의 끝을 지나서 쓰기를 방지 하기 위해 *bufferlength* 를 사용 합니다. 드라이버는 \**Targetvalueptr*에 문자 데이터를 반환 하는 경우 null 종료 문자를 계산 합니다. 따라서 *Targetvalueptr* \*null 종료 문자에 대 한 공간을 포함 해야 합니다. 그렇지 않으면 드라이버에서 데이터를 자릅니다.  
  
 드라이버가 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환 하는 경우 드라이버는 *Bufferlength* 를 무시 하 고 버퍼가 데이터를 저장할 수 있을 만큼 충분히 큰지 가정 합니다. 따라서 응용 프로그램이 고정 길이 데이터에 대해 충분 한 크기의 버퍼를 할당 하는 것이 중요 합니다. 그렇지 않으면 드라이버가 버퍼의 끝을 넘어 기록 됩니다.  
  
 **SQLBindCol** 은 *bufferlength* 가 0 보다 *작은 경우 SQLSTATE* HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 합니다. 그러나 *TargetType* 에서 문자 형식을 지정 하는 경우에는 ISO CLI 규격 드라이버가이 경우 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 하기 때문에 응용 프로그램은 *bufferlength* 를 0으로 설정 하면 안 됩니다.  
  
 *StrLen_or_IndPtr*  
 [지연 된 입/출력] 열에 바인딩할 길이/표시기 버퍼에 대 한 포인터입니다. **Sqlfetch** 및 **sqlfetchscroll** 은이 버퍼에서 값을 반환 합니다. **SQLBulkOperations** 는 *작업이* SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 경우이 버퍼에서 값을 검색 합니다. **SQLBulkOperations** 는 *작업이* SQL_FETCH_BY_BOOKMARK 경우이 버퍼에 값을 반환 합니다. *작업이* SQL_REFRESH 되 면 **SQLSetPos** 는이 버퍼의 값을 반환 합니다. *작업이* SQL_UPDATE 될 때이 버퍼에서 값을 검색 합니다.  
  
 **Sqlfetch**, **sqlfetchscroll**, **SQLBulkOperations**및 **SQLSetPos** 는 길이/표시기 버퍼에서 다음 값을 반환할 수 있습니다.  
  
-   반환할 수 있는 데이터의 길이입니다.  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 응용 프로그램은 **SQLBulkOperations** 또는 **SQLSetPos**에서 사용할 길이/지표 버퍼에 다음 값을 입력할 수 있습니다.  
  
-   전송 되는 데이터의 길이입니다.  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다.  
  
-   SQL_COLUMN_IGNORE  
  
 표시기 버퍼와 길이 버퍼가 별도 버퍼 이면 표시기 버퍼는 SQL_NULL_DATA만 반환할 수 있지만 길이 버퍼는 다른 모든 값을 반환할 수 있습니다.  
  
 자세한 내용은 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [sqlfetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md), [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)및 [길이/지표 값 사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)을 참조 하세요.  
  
 *StrLen_or_IndPtr* null 포인터인 경우 길이 또는 표시기 값을 사용 하지 않습니다. 데이터를 인출 하는 동안 오류가 발생 하 여 데이터가 NULL입니다.  
  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLBindCol** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLBindCol** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|(DM) *Columnnumber* 인수가 0이 고 *TargetType* 인수가 SQL_C_BOOKMARK 되지 않았거나 SQL_C_VARBOOKMARK.|  
|07009|잘못 된 설명자 인덱스|인수 *Columnnumber* 에 지정 된 값이 결과 집합의 최대 열 개수를 초과 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. *\*MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|응용 프로그램 버퍼 유형이 잘못 되었습니다.|인수 *TargetType* 이 올바른 데이터 형식 또는 SQL_C_DEFAULT 아닙니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLBindCol** 가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우<br /><br /> (DM) 드라이버가 ODBC 2 였습니다. *x* 드라이버, *columnnumber* 인수가 0으로 설정 되었고, 인수 *bufferlength* 에 지정 된 값이 4와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본은 해당 열에 대 한 *TargetType* 인수와 드라이버별 SQL 데이터 형식의 조합으로 지정 된 변환을 지원 하지 않습니다.<br /><br /> 인수 *Columnnumber* 가 0이 고 드라이버가 책갈피를 지원 하지 않습니다.<br /><br /> 드라이버는 ODBC 2만 지원 합니다. *x* 및 인수 *TargetType* 은 다음 중 하나입니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 및 부록 D의 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) : 데이터 형식에 나열 된 간격 c 데이터 형식입니다.<br /><br /> 드라이버는 3.50 이전 버전의 ODBC 버전만 지원 하 고 인수 *TargetType* 은 SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLBindCol** 는 결과 집합의 열을 데이터 버퍼에 연결 하거나 *바인딩하* 는 데 사용 되며 응용 프로그램에서 길이/표시기 버퍼에 연결 합니다. 응용 프로그램이 **Sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos** 를 호출 하 여 데이터를 인출 하는 경우 드라이버는 지정 된 버퍼의 바인딩된 열에 대 한 데이터를 반환 합니다. 자세한 내용은 [Sqlfetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조 하세요. 응용 프로그램에서 **SQLBulkOperations** 를 호출 하 여 행 또는 **SQLSetPos** 를 업데이트 하거나 삽입 하 여 행을 업데이트 하는 경우 드라이버는 지정 된 버퍼에서 바인딩된 열의 데이터를 검색 합니다. 자세한 내용은 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 또는 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요. 바인딩에 대 한 자세한 내용은 [결과 검색 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md)을 참조 하세요.  
  
 열은 데이터를 검색 하기 위해 바인딩할 필요가 없습니다. 응용 프로그램은 또한 **SQLGetData** 를 호출 하 여 열에서 데이터를 검색할 수 있습니다. 행의 일부 열을 바인딩하고 다른 열에 대해 **SQLGetData** 를 호출할 수도 있지만이 경우 몇 가지 제한 사항이 적용 됩니다. 자세한 내용은 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)를 참조 하세요.  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>열 바인딩, 바인딩 해제 및 리바인딩  
 열은 결과 집합에서 데이터를 가져온 후에도 언제 든 지 바인딩, 바인딩 해제 또는 다시 바인딩할 수 있습니다. 새 바인딩은 다음에 바인딩을 사용 하는 함수를 호출할 때 적용 됩니다. 예를 들어 응용 프로그램이 결과 집합의 열을 바인딩하고 **Sqlfetch**를 호출 한다고 가정 합니다. 드라이버는 바인딩된 버퍼의 데이터를 반환 합니다. 이제 응용 프로그램이 열을 다른 버퍼 집합에 바인딩하는 것으로 가정 합니다. 드라이버는 새로 바인딩된 버퍼에 인출 된 행의 데이터를 넣지 않습니다. 대신 **Sqlfetch** 가 다시 호출 될 때까지 대기한 다음 새로 바인딩된 버퍼에 다음 행에 대 한 데이터를 배치 합니다.  
  
> [!NOTE]  
>  열 0에 열을 바인딩하기 전에 statement 특성 SQL_ATTR_USE_BOOKMARKS 항상 설정 해야 합니다. 이는 필수는 아니지만 적극 권장 됩니다.  
  
## <a name="binding-columns"></a>열 바인딩  
 열을 바인딩하려면 응용 프로그램은 **SQLBindCol** 를 호출 하 고 데이터 버퍼의 열 번호, 형식, 주소 및 길이와 길이/지표 버퍼의 주소를 전달 합니다. 이러한 주소를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "Buffer Addresses"를 참조 하십시오. 바인딩 열에 대 한 자세한 내용은 [SQLBindCol 사용](../../../odbc/reference/develop-app/using-sqlbindcol.md)을 참조 하세요.  
  
 이러한 버퍼의 사용은 지연 됩니다. 즉, 응용 프로그램은 **SQLBindCol** 에 바인딩하며, 드라이버는 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos**와 같은 다른 함수에서 액세스 합니다. **SQLBindCol** 에 지정 된 포인터가 적용 되는 동안에도 유효한 상태로 유지 되도록 하는 것은 응용 프로그램의 책임입니다. 응용 프로그램에서 이러한 포인터가 무효화 될 수 있는 경우 (예: 버퍼를 해제 한 다음 유효한 것으로 예상 하는 함수 호출) 결과가 정의 되지 않습니다. 자세한 내용은 [지연 된 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)를 참조 하세요.  
  
 바인딩은 새 바인딩으로 대체 되거나, 열이 바인딩되지 않거나, 문이 해제 될 때까지 계속 적용 됩니다.  
  
## <a name="unbinding-columns"></a>열 바인딩 해제  
 단일 열을 바인딩 해제 하기 위해 응용 프로그램은 *Columnnumber* 가 해당 열 수로 설정 되 고 *Targetvalueptr* 이 Null 포인터로 설정 된 **SQLBindCol** 를 호출 합니다. *Columnnumber* 가 바인딩되지 않은 열을 참조 하는 경우 **SQLBindCol** 는 계속 SQL_SUCCESS 반환 합니다.  
  
 모든 열을 바인딩 해제 하기 위해 응용 프로그램은 *Foption* 을 SQL_UNBIND로 설정 하 여 **SQLFreeStmt** 를 호출 합니다. 이는 SQL_DESC_COUNT 필드를 0으로 설정 하 여 수행할 수도 있습니다.  
  
## <a name="rebinding-columns"></a>열 다시 바인딩  
 응용 프로그램은 다음 두 작업 중 하나를 수행 하 여 바인딩을 변경할 수 있습니다.  
  
-   이미 바인딩된 열에 대해 새 바인딩을 지정 하려면 **SQLBindCol** 를 호출 합니다. 드라이버가 기존 바인딩을 새 바인딩으로 덮어씁니다.  
  
-   **SQLBindCol**에 대 한 바인딩 호출로 지정 된 버퍼 주소에 추가할 오프셋을 지정 합니다. 자세한 내용은 다음 섹션인 "바인딩 오프셋"을 참조 하세요.  
  
## <a name="binding-offsets"></a>바인딩 오프셋  
 바인딩 오프셋은 역참조 되기 전에 데이터 및 길이/표시기 버퍼 ( *Targetvalueptr* 및 *StrLen_or_IndPtr* 인수에 지정 된)의 주소에 추가 되는 값입니다. 오프셋을 사용할 때 바인딩은 응용 프로그램의 버퍼 레이아웃 방법의 "템플릿" 이며, 응용 프로그램은 오프셋을 변경 하 여이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 각 바인딩의 각 주소에 동일한 오프셋이 추가 되기 때문에 각 버퍼 집합 내에서 서로 다른 열의 버퍼 간 상대 오프셋은 동일 해야 합니다. 행 단위 바인딩을 사용 하는 경우이는 항상 true입니다. 응용 프로그램은 열 단위 바인딩이 사용 될 때이를 true로 설정 하기 위해 버퍼를 신중 하 게 배치 해야 합니다.  
  
 바인딩 오프셋을 사용 하면 기본적으로 **SQLBindCol**를 호출 하 여 열을 다시 바인딩하는 것과 동일한 효과가 있습니다. 차이점은 **SQLBindCol** 에 대 한 새 호출에서 데이터 버퍼 및 길이/표시기 버퍼에 대 한 새 주소를 지정 하는 반면, 바인딩 오프셋을 사용 하면 주소가 변경 되지는 않지만 오프셋을 추가 한다는 것입니다. 응용 프로그램은 원할 때마다 새 오프셋을 지정할 수 있으며이 오프셋은 항상 원래 바인딩된 주소에 추가 됩니다. 특히 offset이 0으로 설정 되거나 statement 특성이 null 포인터로 설정 된 경우 드라이버는 원래 바인딩된 주소를 사용 합니다.  
  
 바인딩 오프셋을 지정 하기 위해 응용 프로그램은 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성을 SQLINTEGER 버퍼의 주소로 설정 합니다. 응용 프로그램은 바인딩을 사용 하는 함수를 호출 하기 전에이 버퍼에 오프셋 (바이트)을 배치 합니다. 사용할 버퍼의 주소를 확인 하기 위해 드라이버는 바인딩의 주소에 오프셋을 추가 합니다. 주소와 오프셋의 합계는 유효한 주소 여야 하지만 오프셋이 추가 된 주소는 유효 하지 않아도 됩니다. 바인딩 오프셋을 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "Buffer Addresses"를 참조 하십시오.  
  
## <a name="binding-arrays"></a>바인딩 배열  
 행 집합 크기 (SQL_ATTR_ROW_ARRAY_SIZE statement 특성의 값)가 1 보다 크면 응용 프로그램은 단일 버퍼 대신 버퍼 배열을 바인딩합니다. 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)를 참조 하세요.  
  
 응용 프로그램은 다음 두 가지 방법으로 배열을 바인딩할 수 있습니다.  
  
-   각 열에 배열을 바인딩합니다. 각 데이터 구조 (배열)는 단일 열에 대 한 데이터를 포함 하기 때문에이를 *열 단위 바인딩* 이라고 합니다.  
  
-   전체 행의 데이터를 포함 하는 구조체를 정의 하 고 이러한 구조체의 배열을 바인딩합니다. 각 데이터 구조는 단일 행에 대 한 데이터를 포함 하기 때문에이를 *행 단위 바인딩* 이라고 합니다.  
  
 버퍼의 각 배열에는 적어도 행 집합의 크기와 같은 수의 요소가 있어야 합니다.  
  
> [!NOTE]  
>  응용 프로그램에서 정렬이 올바른지 확인 해야 합니다. 맞춤 고려 사항에 대 한 자세한 내용은 [맞춤](../../../odbc/reference/develop-app/alignment.md)을 참조 하십시오.  
  
## <a name="column-wise-binding"></a>열 단위 바인딩  
 열 단위 바인딩에서 응용 프로그램은 각 열에 개별 데이터 및 길이/표시기 배열을 바인딩합니다.  
  
 열 단위 바인딩을 사용 하기 위해 응용 프로그램은 먼저 SQL_ATTR_ROW_BIND_TYPE statement 특성을 SQL_BIND_BY_COLUMN로 설정 합니다. 이것이 기본값입니다. 바인딩할 각 열에 대해 응용 프로그램은 다음 단계를 수행 합니다.  
  
1.  데이터 버퍼 배열을 할당 합니다.  
  
2.  길이/표시기 버퍼의 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  열 단위 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰면 길이 및 표시기 데이터에 대해 별도의 배열을 사용할 수 있습니다.  
  
3.  다음 인수를 사용 하 여 **SQLBindCol** 를 호출 합니다.  
  
    -   *TargetType* 은 데이터 버퍼 배열에서 단일 요소의 형식입니다.  
  
    -   *Targetvalueptr* 은 데이터 버퍼 배열의 주소입니다.  
  
    -   *Bufferlength* 는 데이터 버퍼 배열에서 단일 요소의 크기입니다. 데이터가 고정 길이 데이터 이면 *Bufferlength* 인수가 무시 됩니다.  
  
    -   *StrLen_or_IndPtr* 는 길이/지표 배열의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "Buffer Addresses"를 참조 하십시오. 열 단위 바인딩에 대 한 자세한 내용은 [열 단위 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)을 참조 하세요.  
  
## <a name="row-wise-binding"></a>행 단위 바인딩  
 행 단위 바인딩에서 응용 프로그램은 바인딩할 각 열에 대 한 데이터 및 길이/표시기 버퍼를 포함 하는 구조체를 정의 합니다.  
  
 행 단위 바인딩을 사용 하기 위해 응용 프로그램에서는 다음 단계를 수행 합니다.  
  
1.  데이터 및 길이/표시기 버퍼를 모두 포함 하 여 데이터의 단일 행을 보유 하는 구조체를 정의 하 고 이러한 구조체의 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  행 단위 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰면 길이 및 표시기 데이터에 대해 별도의 필드를 사용할 수 있습니다.  
  
2.  SQL_ATTR_ROW_BIND_TYPE statement 특성을 단일 데이터 행을 포함 하는 구조 크기나 결과 열이 바인딩될 버퍼의 크기에 맞게 설정 합니다. 길이에는 바인딩된 열의 주소가 지정 된 길이 만큼 증가 하는 경우 결과는 다음 행의 같은 열 시작을 가리키도록 하기 위해 모든 바인딩된 열의 공간 및 구조 또는 버퍼의 안쪽 여백을 포함 해야 합니다. ANSI C에서 *sizeof* 연산자를 사용 하는 경우이 동작이 보장 됩니다.  
  
3.  바인딩할 각 열에 대해 다음 인수를 사용 하 여 **SQLBindCol** 를 호출 합니다.  
  
    -   *TargetType* 은 열에 바인딩할 데이터 버퍼 멤버의 형식입니다.  
  
    -   *Targetvalueptr* 은 첫 번째 배열 요소에 있는 데이터 버퍼 멤버의 주소입니다.  
  
    -   *Bufferlength* 는 데이터 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 은 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "Buffer Addresses"를 참조 하십시오. 열 단위 바인딩에 대 한 자세한 내용은 [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)을 참조 하세요.  
  
## <a name="buffer-addresses"></a>버퍼 주소  
 *버퍼 주소* 는 데이터 또는 길이/표시기 버퍼의 실제 주소입니다. 드라이버는 버퍼에 쓰기 직전에 버퍼 주소를 계산 합니다 (예: 인출 시간 동안). *Targetvalueptr* 에 지정 된 주소와 *StrLen_or_IndPtr* 인수, 바인딩 오프셋 및 행 번호를 사용 하는 다음 수식에서 계산 됩니다.  
  
 *바인딩된 주소* + *바인딩 오프셋* + ((*행 번호* -1) x *요소 크기*)  
  
 여기서 수식의 변수는 다음 표에 설명 된 대로 정의 됩니다.  
  
|변수|설명|  
|--------------|-----------------|  
|*바인딩된 주소*|데이터 버퍼의 경우 **SQLBindCol**의 *Targetvalueptr* 인수를 사용 하 여 지정 된 주소입니다.<br /><br /> 길이/표시기 버퍼의 경우 **SQLBindCol**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 주소입니다. 자세한 내용은 "설명자 and SQLBindCol" 섹션의 "추가 주석"을 참조 하세요.<br /><br /> 바인딩된 주소가 0 이면 이전 수식에서 계산 된 주소가 0이 아닌 경우에도 데이터 값이 반환 되지 않습니다.|  
|*바인딩 오프셋*|행 단위 바인딩을 사용 하는 경우 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성으로 지정 된 주소에 저장 된 값입니다.<br /><br /> 열 단위 바인딩을 사용 하거나 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성의 값이 null 포인터인 경우 *바인딩 오프셋* 은 0입니다.|  
|*행 번호*|행 집합의 행 번호 (1부터 수)입니다. 단일 행 페치의 경우 기본값은 1입니다.|  
|*요소 크기*|바인딩된 배열의 요소 크기입니다.<br /><br /> 열 단위 바인딩을 사용 하는 경우 길이/표시기 버퍼에 대 한 **sizeof (SQLINTEGER)** 입니다. 데이터 버퍼의 경우 데이터 형식이 가변 길이인 경우 **SQLBindCol** 에서 *bufferlength* 인수의 값이 고 데이터 형식이 고정 길이인 경우 데이터 형식의 크기입니다.<br /><br /> 행 단위 바인딩을 사용 하는 경우이 값은 데이터 및 길이/표시 버퍼에 대 한 SQL_ATTR_ROW_BIND_TYPE statement 특성의 값입니다.|  
  
## <a name="descriptors-and-sqlbindcol"></a>설명자 및 SQLBindCol  
 다음 섹션에서는 **SQLBindCol** 가 설명자와 상호 작용 하는 방법을 설명 합니다.  
  
> [!CAUTION]  
>  한 문에 대해 **SQLBindCol** 를 호출 하면 다른 문에 영향을 줄 수 있습니다. 이는 문과 연결 된가 명시적으로 할당 되 고 다른 문과도 연결 된 경우에 발생 합니다. **SQLBindCol** 은 설명자를 수정 하기 때문에이 설명자가 연결 된 모든 문에 수정 내용이 적용 됩니다. 이 동작이 필요한 동작이 아닌 경우 응용 프로그램은 **SQLBindCol**를 호출 하기 전에 다른 문에서이 설명자를 분리 해야 합니다.  
  
## <a name="argument-mappings"></a>인수 매핑  
 개념적으로 **SQLBindCol** 는 다음 단계를 순서 대로 수행 합니다.  
  
1.  **SQLGetStmtAttr** 를 호출 하 여 핸들을 가져옵니다.  
  
2.  **SQLGetDescField** 를 호출 하 여이 설명자의 SQL_DESC_COUNT 필드를 가져오고 *columnnumber* 인수의 값이 SQL_DESC_COUNT 값을 초과 하는 경우 **SQLSetDescField** 를 호출 하 여 SQL_DESC_COUNT 값을 *columnnumber*로 늘립니다.  
  
3.  **SQLSetDescField** 을 여러 번 호출 하 여 다음 필드에 값을 할당 합니다.  
  
    -   Targettype이 datetime 또는 interval 하위 형식의 간결한 식별자 중 *하나인 경우 SQL_DESC_TYPE* 를 각각 SQL_DATETIME 또는 SQL_INTERVAL로 설정 한다는 점을 제외 하 SQL_DESC_CONCISE_TYPE 고 SQL_DESC_TYPE를 *targettype*값으로 설정 합니다. SQL_DESC_CONCISE_TYPE를 간결한 식별자로 설정 합니다. 및는 SQL_DESC_DATETIME_INTERVAL_CODE를 해당 하는 DATETIME 또는 INTERVAL 하위 코드에 설정 합니다.  
  
    -   *TargetType*에 적절 한 SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_DATETIME_INTERVAL_PRECISION를 하나 이상 설정 합니다.  
  
    -   SQL_DESC_OCTET_LENGTH 필드를 *Bufferlength*의 값으로 설정 합니다.  
  
    -   SQL_DESC_DATA_PTR 필드를 *Targetvalue*값으로 설정 합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드를 *StrLen_or_Ind*값으로 설정 합니다. 다음 단락을 참조 하세요.  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드를 *StrLen_or_Ind*값으로 설정 합니다. 다음 단락을 참조 하세요.  
  
 *StrLen_or_Ind* 인수가 참조 하는 변수는 표시기 및 길이 정보 모두에 사용 됩니다. 인출에서 열에 대해 null 값이 발견 되 면이 변수에 SQL_NULL_DATA를 저장 합니다. 그렇지 않으면이 변수에 데이터 길이를 저장 합니다. Null 포인터를 *StrLen_or_Ind* 로 전달 하면 fetch 작업에서 데이터 길이가 반환 되지 않지만, null 값을 발견 하 여 SQL_NULL_DATA를 반환할 방법이 없는 경우 반입이 실패 합니다.  
  
 **SQLBindCol** 에 대 한 호출이 실패 하는 경우 해당 값에 설정 된 설명자 필드의 내용이 정의 되지 않으며 해당 값의 SQL_DESC_COUNT 필드 값이 변경 되지 않습니다.  
  
## <a name="implicit-resetting-of-count-field"></a>개수 필드의 암시적 다시 설정  
 **SQLBindCol** 는 SQL_DESC_COUNT 값이 증가 하는 경우에만 *columnnumber* 인수 값으로 SQL_DESC_COUNT를 설정 합니다. *Targetvalueptr* 인수의 값이 null 포인터이 고 *columnnumber* 인수의 값이 SQL_DESC_COUNT와 같으면 (즉, 가장 높은 바인딩 열을 바인딩 해제 하는 경우) SQL_DESC_COUNT은 가장 높은 나머지 바인딩된 열의 숫자로 설정 됩니다.  
  
## <a name="cautions-regarding-sql_default"></a>SQL_DEFAULT에 대 한 주의 사항  
 열 데이터를 성공적으로 검색 하려면 응용 프로그램에서 응용 프로그램 버퍼에 있는 데이터의 길이와 시작 지점을 올바르게 결정 해야 합니다. 응용 프로그램에서 명시적 *TargetType*을 지정 하면 응용 프로그램 오해 쉽게 검색 됩니다. 그러나 응용 프로그램에서 SQL_DEFAULT의 *TargetType* 을 지정 하면 메타 데이터에 대 한 변경 또는 다른 열에 코드를 적용 하 여 응용 프로그램에서 의도 한 것과 다른 데이터 형식의 열에 **SQLBindCol** 를 적용할 수 있습니다. 이 경우 응용 프로그램은 인출 된 열 데이터의 시작 또는 길이를 항상 확인 하지 않을 수 있습니다. 보고 되지 않은 데이터 오류 또는 메모리 위반이 발생할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 Customers 테이블에서 **SELECT** 문을 실행 하 여 이름별로 정렬 된 고객 id, 이름 및 전화 번호의 결과 집합을 반환 합니다. 그런 다음 **SQLBindCol** 를 호출 하 여 데이터 열을 로컬 버퍼에 바인딩합니다. 마지막으로, 응용 프로그램은 **Sqlfetch** 를 사용 하 여 데이터의 각 행을 페치하고 각 고객의 이름, ID 및 전화 번호를 인쇄 합니다.  
  
 더 많은 코드 예제는 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [sqlcolumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md), [Sqlfetchscroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)및 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
```cpp  
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
  
 또한 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|문에서 열 버퍼 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|데이터 열의 일부 또는 전체를 가져오는 중|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
