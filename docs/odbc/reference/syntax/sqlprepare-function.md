---
title: SQLPrepare 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 292b1c4d9cd0281de610af4e53f25aa3d0ab6f90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005760"
---
# <a name="sqlprepare-function"></a>SQLPrepare 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLPrepare** SQL 문자열 실행을 준비 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *StatementText*  
 [입력] SQL 텍스트 문자열입니다.  
  
 *TextLength*  
 [입력] 길이 **StatementText* 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLPrepare** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLPrepare** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|지정 된 문 특성을 일시적으로 유사한 값에 대체 되므로 구현 작업 조건으로 인해 잘못 되었습니다. (**SQLGetStmtAttr** 일시적으로 대체 값 결정 호출할 수 있습니다.) 대체 값이 적합 합니다 *StatementHandle* 커서를 닫을 때까지 합니다. 변경할 수 있는 문 특성은 다음과 같습니다. SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 된 **삽입** 문과 값을 삽입할 수는 파생된 테이블의 정도 일치 하지 않습니다.|  
|21S02|파생된 테이블의 단계가 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 된 **CREATE VIEW** 문과 수가 지정 된 이름은 쿼리 사양에 정의 된 파생 테이블을 같은 정도로 아닙니다.|  
|22018|캐스트 사양의 문자 값|**StatementText* 리터럴 또는 매개 변수를 포함 하는 SQL 문을 포함 하 고 값 연결 된 테이블 열의 데이터 형식과 호환 되지 않았습니다.|  
|22019|잘못 된 이스케이프 문자|인수 *StatementText* 포함 된를 **와 같은** 조건자와 함께 **이스케이프** 에 **여기서** 절과 이스케이프의 길이 다음 문자 **이스케이프** 1 없습니다.|  
|22025|잘못 된 이스케이프 시퀀스|인수 *StatementText* 포함 된 "**와 같은** _패턴 값_ **이스케이프** _이스케이프 문자_"에 **위치** 절 및 패턴 값의 이스케이프 문자 뒤의 문자"%"나"_"되었습니다.|  
|24000|잘못된 커서 상태|(DM)에서 커서가 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|34000|잘못된 커서 이름|\**StatementText* 배치는 포함 된 **삭제** 또는 위치를 지정 **업데이트**, 및 준비 중인 문에서 참조 하는 커서를 열 수 없습니다.|  
|3D000|잘못 된 카탈로그 이름|에 지정 된 카탈로그 이름을 *StatementText* 올바르지 않습니다.|  
|3F000|잘못 된 스키마 이름|에 지정 된 스키마 이름이 *StatementText* 올바르지 않습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText* preparable 되었거나 구문 오류가 포함 된 SQL 문을 포함 합니다.<br /><br /> **StatementText* 는 사용자는 필요한 권한이 없는 않았습니다 문이 포함 되었습니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText* 포함 된를 **CREATE TABLE** 하거나 **CREATE VIEW** 문 및 테이블 이름 또는 뷰 이름이 이미 지정 되어 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없음|\**StatementText* 포함 된를 **DROP TABLE** 또는 **DROP VIEW** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **ALTER TABLE** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE VIEW** 문 및 테이블 이름 또는 뷰를 쿼리 사양에 정의 된 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE INDEX** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **권한 부여** 또는 **해지** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **선택** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **삭제**를 **삽입**, 또는 **업데이트** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE TABLE** 문과 (참조 테이블 이외의 만들어지는 것) 제약 조건이 지정 된 테이블이 없습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText* 포함 된를 **CREATE INDEX** 문 및 지정 된 인덱스 이름이 이미 존재 합니다.|  
|42S12|인덱스가 없습니다.|\**StatementText* 포함 된를 **DROP INDEX** 문 및 지정 된 인덱스 이름이 없습니다.|  
|42S21|열이 이미|\**StatementText* 포함 된를 **ALTER TABLE** 문과에 지정 된 열을 **추가** 절 고유 하지 않거나 기본 테이블의 기존 열을 식별 합니다.|  
|42S22|열이 없습니다|\**StatementText* 포함 된 **CREATE INDEX** 문에서 하나 이상의 열 목록에 지정 된 이름이 없는 열입니다.<br /><br /> \**StatementText* 포함 된를 **GRANT** 또는 **해지** 문과 지정한 열 이름이 없습니다.<br /><br /> \**StatementText* 포함 된를 **선택**를 **삭제**를 **삽입**, 또는 **업데이트** 문 및 지정된 된 열 이름 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 된 **CREATE TABLE** 문과 (참조 테이블 이외의 만들어지는 것) 제약 조건에 지정 된 열이 없는 것입니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle*, 및 함수를 호출한 다음 다시 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) *StatementText* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLPrepare** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *TextLength* 보다 작거나 0에 있지만 같지 않음 SQL_NTS 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|동시성 설정을 정의 하는 커서 유형에 대해 올바르지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램 호출 **SQLPrepare** 준비에 대 한 데이터 원본에는 SQL 문을 보내야 합니다. 준비 된 실행에 대 한 자세한 내용은 참조 하세요. [실행 준비](../../../odbc/reference/develop-app/prepared-execution-odbc.md)합니다. 응용 프로그램은 SQL 문에서 하나 이상의 매개 변수 표식을 포함할 수 있습니다. 매개 변수 마커를 포함 하려면 응용 프로그램에 SQL 문자열에 적절 한 위치에 물음표 (?)를 포함 합니다. 매개 변수에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.  
  
> [!NOTE]  
>  응용 프로그램에서 사용 하는 경우 **SQLPrepare** 준비 및 **SQLExecute** 제출 하는 **커밋** 또는 **롤백** 문 수 없습니다 DBMS 제품 간의 상호 운용 가능 합니다. 호출에서는 커밋하거나 트랜잭션을 롤백하려면 **SQLEndTran**합니다.  
  
 드라이버는 데이터 원본에서 사용 된 SQL 형식을 사용 하 고 다음 준비를 위해 데이터 원본에 제출 하는 문을 수정할 수 있습니다. 특히 드라이버 특정 기능에 대 한 SQL 구문을 정의 하는 데 이스케이프 시퀀스를 수정 합니다. (SQL 문 문법에 대 한 참조 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 고 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) 드라이버의 경우 문 핸들은 포함 된 SQL 코드에서 문 식별자 비슷합니다. 데이터 원본에서 문을 식별자를 지 원하는 드라이버는 데이터 원본에는 문 식별자와 매개 변수 값 보낼 수 있습니다.  
  
 문이 준비 되 면 응용 프로그램은 문 핸들을 사용 하 여 이후 함수 호출의 문으로 참조. 문 핸들을 사용 하 여 연결 하 여 준비 된 문을 호출 하 여 다시 실행할 수 있습니다 **SQLExecute** 응용 프로그램에 대 한 호출을 사용 하 여 문을 해제 될 때까지 **SQLFreeStmt** SQL_DROP 옵션을 사용 하 여 또는 문 핸들에 대 한 호출에 사용 될 때까지 **SQLPrepare**하십시오 **SQLExecDirect**, 또는 카탈로그 함수 중 하나 (**SQLColumns**,  **SQLTables**등). 문을 준비 하는 응용 프로그램을 한 후 결과 집합의 형식에 대 한 정보를 요청할 수 있습니다. 일부 구현에서는 호출에 대 한 **SQLDescribeCol** 하거나 **SQLDescribeParam** 후 **SQLPrepare** 후함수를호출하는만큼효율적이지못할**SQLExecute** 나 **SQLExecDirect**합니다.  
  
 일부 드라이버 구문 오류를 반환 하거나 응용 프로그램을 호출 하는 경우 액세스 위반 수 없습니다 **SQLPrepare**합니다. 드라이버에서 구문 오류를 처리 하 고 액세스 위반을 수만 구문 오류 또는 모두 구문 오류 또는 액세스 위반입니다. 따라서 응용 프로그램 관련 함수 같은 후속 호출 하는 경우 이러한 상황을 처리 하는 일을 할 수 있어야 **SQLNumResultCols**하십시오 **SQLDescribeCol**, **SQLColAttribute**, 및 **SQLExecute**합니다.  
  
 드라이버 및 데이터 원본 기능에 따라 (모든 매개 변수가 바인딩되면) 하는 경우 문을 준비 될 때 매개 변수 정보 (예: 데이터 형식)를 검사할 수 있습니다 또는 (모든 매개 변수에 바인딩되어 있지) 하는 경우 실행 될 때입니다. 최대 상호 운용성을 위해 응용 프로그램의 동일한 문에서 새 SQL 문을 준비 하기 전에 SQL 문을 이전에 적용 하는 모든 매개 변수 바인딩을 해제 해야 합니다. 이 새 문에 적용 되 고 매개 변수 정보를 이전으로 인 한 오류를 방지할 수 있습니다.  
  
> [!IMPORTANT]  
>  명시적으로 호출 하 여 트랜잭션 커밋 **SQLEndTran** 또는 자동 커밋 모드에서 작업 하 여 데이터 원본 연결에서 모든 문에 대 한 액세스 계획을 삭제 하려면 발생할 수 있습니다. 자세한 내용은 참조에서 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식과 SQL_CURSOR_COMMIT_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 하 고 [커서 및 준비 된 문에서 영향의 트랜잭션을](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)하십시오 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), 및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|버퍼 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업을 실행합니다.|[SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문에 의해 영향을 받는 행 수를 반환 합니다.|[SQLRowCount 함수](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|커서 이름을 설정합니다.|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
