---
title: SQLPrepare 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306884"
---
# <a name="sqlprepare-function"></a>SQLPrepare 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLPrepare** 실행을 위해 SQL 문자열을 준비합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *명령문 텍스트*  
 [입력] SQL 텍스트 문자열입니다.  
  
 *TextLength*  
 [입력] **문자* 텍스트의 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLPrepare** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLPrepare에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|구현 작업 조건으로 인해 지정된 문 특성이 잘못되었기 때문에 유사한 값이 일시적으로 대체되었습니다. **(SQLGetStmtAttr** 일시적으로 대체 된 값이 무엇인지 확인 하려면 호출할 수 있습니다.) 대체 값은 커서가 닫혀있을 때까지 *StatementHandle에* 대해 유효합니다. 변경할 수 있는 명령문 특성은 SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_MAX_ROWS SQL_ATTR_SIMULATE_CURSOR SQL_ATTR_MAX_LENGTH SQL_ATTR_KEYSET_SIZE.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치하지 않음|\**StatementText* **INSERT** 문을 포함 하 고 삽입 할 값의 수가 파생 된 테이블의 정도와 일치 하지 않습니다.|  
|21S02|파생 테이블의 정도가 열 목록과 일치하지 않음|\**StatementText* **CREATE VIEW** 문을 포함 하 고 지정 된 이름 수는 쿼리 사양에 의해 정의 된 파생 된 테이블과 같지 않습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|**StatementText리터럴* 또는 매개 변수를 포함 하는 SQL 문을 포함 하 고 값이 관련 된 테이블 열의 데이터 형식과 호환 되지 않습니다.|  
|22019|유효하지 않은 이스케이프 문자|인수 *StatementText는* **WHERE** 절에서 **ESCAPE가** 있는 **LIKE** 조건어를 포함하고 **ESCAPE** 다음 의 이스케이프 문자의 길이는 1과 같지 않았습니다.|  
|22025|잘못된 이스케이프 시퀀스|인수 *문텍스트에는* **WHERE** 절에 **"LIKE** _패턴 값_ **ESCAPE** _ESCAPE 문자"가_포함되어 있으며 패턴 값의 이스케이프 문자 다음 문자는 "%" 또는 "_"가 아닙니다.|  
|24000|잘못된 커서 상태|(DM) *명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll가** 호출되었습니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|34000|잘못된 커서 이름|\**StatementText* 위치 **삭제** 또는 위치 **업데이트**포함 되 고 준비 되는 문에서 참조 하는 커서가 열려 있지 않았습니다.|  
|3D000|카탈로그 이름이 잘못되었습니다.|*StatementText에* 지정된 카탈로그 이름이 잘못되었습니다.|  
|3F000|잘못된 스키마 이름|*StatementText에* 지정된 스키마 이름이 잘못되었습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText에는* 비교할 수 없거나 구문 오류가 포함된 SQL 문이 포함되어 있습니다.<br /><br /> **StatementText에는* 사용자에게 필요한 권한이 없는 문이 포함되어 있습니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText에는* **CREATE 테이블** 또는 **CREATE VIEW** 문이 포함되어 있으며 지정된 테이블 이름 또는 뷰 이름이 이미 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없습니다.|\**StatementText에는* **DROP 테이블** 또는 **DROP VIEW** 문이 포함되어 있으며 지정된 테이블 이름 또는 뷰 이름이 없습니다.<br /><br /> \**StatementText는* **ALTER TABLE** 문을 포함하고 지정된 테이블 이름이 존재하지 않았습니다.<br /><br /> \**StatementText* **CREATE VIEW** 문을 포함 하 고 쿼리 사양에 의해 정의 된 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* **CREATE INDEX** 문을 포함 하 고 지정 된 테이블 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* **는 GRANT** 또는 **해지** 문을 포함하고 지정된 테이블 이름 또는 뷰 이름이 존재하지 않습니다.<br /><br /> \**StatementText* **SELECT** 문을 포함 하 고 지정 된 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText는* **DELETE**, **INSERT**또는 **UPDATE** 문을 포함하고 지정된 테이블 이름이 존재하지 않습니다.<br /><br /> \**StatementText는* **CREATE TABLE** 문을 포함하고 제약 조건에 지정된 테이블(생성되는 테이블이 아닌 테이블을 참조)은 존재하지 않았습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText에는* **CREATE INDEX** 문이 포함되었으며 지정된 인덱스 이름이 이미 존재했습니다.|  
|42S12|인덱스를 찾을 수 없습니다.|\**StatementTextDROP* **INDEX** 문을 포함 하 고 지정 된 인덱스 이름이 존재 하지 않았습니다.|  
|42S21|열이 이미 있습니다.|\**StatementText는* **ALTER TABLE** 문을 포함하고 **ADD** 절에 지정된 열은 고유하지 않거나 기본 테이블의 기존 열을 식별합니다.|  
|42S22|열을 찾을 수 없습니다.|\**StatementText* **에는 CREATE INDEX** 문이 포함되었으며 열 목록에 지정된 열 이름 중 하나 이상이 존재하지 않았습니다.<br /><br /> \**StatementText는* **GRANT** 또는 **해지** 문을 포함하고 지정된 열 이름이 없습니다.<br /><br /> \**StatementText* **SELECT,** **DELETE**, **INSERT**또는 **UPDATE** 문을 포함 하 고 지정 된 열 이름이 없습니다.<br /><br /> \**StatementText는* **CREATE TABLE** 문을 포함하고 제약 조건에 지정된 열(생성되는 테이블이 아닌 테이블을 참조)은 존재하지 않았습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle에서*호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) *문텍스트는* null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLPrepare** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 TextLength는* 0보다 작거나 같지만 SQL_NTS 같지 는 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|정의된 커서 유형에 대해 동시성 설정이 잘못되었습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLPrepare를** 호출하여 준비를 위해 데이터 원본에 SQL 문을 보냅니다. 준비된 실행에 대한 자세한 내용은 [준비된 실행을](../../../odbc/reference/develop-app/prepared-execution-odbc.md)참조하십시오. 응용 프로그램은 SQL 문에 하나 이상의 매개 변수 마커를 포함할 수 있습니다. 매개 변수 마커를 포함하기 위해 응용 프로그램은 적절한 위치에 물음표(?)를 SQL 문자열에 포함시됩니다. 매개 변수에 대한 자세한 내용은 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
> [!NOTE]  
>  응용 프로그램이 **SQLPrepare를** 사용하여 준비하고 **SQLExecute를** 사용하여 **COMMIT** 또는 **ROLLBACK** 문을 제출하는 경우 DBMS 제품 간에 상호 운용되지 않습니다. 트랜잭션을 커밋하거나 롤백하려면 **SQLEndTran**을 호출합니다.  
  
 드라이버는 명령문을 수정하여 데이터 원본에서 사용하는 SQL 형식을 사용한 다음 준비를 위해 데이터 원본에 제출할 수 있습니다. 특히 드라이버는 특정 기능에 대한 SQL 구문을 정의하는 데 사용되는 이스케이프 시퀀스를 수정합니다. SQL 문 문법에 대한 설명은 ODBC 및 [부록 C: SQL 문법의](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) [이스케이프 시퀀스를](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 참조하십시오. 드라이버의 경우 문 핸들은 포함된 SQL 코드의 문 식별자와 유사합니다. 데이터 원본이 문 식별자를 지원하는 경우 드라이버는 데이터 원본에 문 식별자 및 매개 변수 값을 보낼 수 있습니다.  
  
 문을 준비 한 후 응용 프로그램은 문 핸들을 사용 하 여 이후 함수 호출에서 문을 참조 합니다. 문 핸들과 연결된 준비된 문은 응용 프로그램이 SQL_DROP 옵션을 사용하여 **SQLFreeStmt를** 호출하여 문을 해제할 때까지 또는 **SQLPrepare,** **SQLExecDirect**또는 카탈로그 함수 중**하나(SQLColumns,** **SQLTable**등)에 대한 호출에서 문 핸들이 사용될 때까지 **SQLExecute를** 호출하여 다시 실행할 수 있습니다. 응용 프로그램이 문을 준비하면 결과 집합의 형식에 대한 정보를 요청할 수 있습니다. 일부 구현의 경우 SQLPrepare **후** **SQLDescribeCol** 또는 **SQLDescribeParam을** 호출하는 것이 **SQLExecute** 또는 **SQLExecDirect**다음 함수를 호출하는 것만큼 효율적이지 않을 수 있습니다.  
  
 일부 드라이버는 응용 프로그램에서 **SQLPrepare**를 호출할 때 구문 오류 또는 액세스 위반을 반환할 수 없습니다. 드라이버는 구문 오류 및 액세스 위반, 구문 오류만 처리하거나 구문 오류나 액세스 위반을 처리할 수 있습니다. 따라서 응용 프로그램은 **SQLNumResultCols,** **SQLDescribeCol,** **SQLColAttribute**및 **SQLExecute와**같은 후속 관련 함수를 호출할 때 이러한 조건을 처리할 수 있어야 합니다.  
  
 드라이버 및 데이터 원본의 기능에 따라 문이 준비될 때(모든 매개 변수가 바인딩된 경우) 또는 실행 될 때(모든 매개 변수가 바인딩되지 않은 경우) 매개 변수 정보(예: 데이터 형식)를 확인할 수 있습니다. 최대 상호 운용성을 위해 응용 프로그램은 동일한 명령문에 새 SQL 문을 준비하기 전에 이전 SQL 문에 적용된 모든 매개 변수를 바인딩 해제해야 합니다. 이렇게 하면 새 문에 적용 되는 이전 매개 변수 정보로 인해 오류를 방지합니다.  
  
> [!IMPORTANT]  
>  **SQLEndTran을** 명시적으로 호출하거나 자동 커밋 모드에서 작업하여 트랜잭션을 커밋하면 데이터 원본이 연결의 모든 문에 대한 액세스 계획을 삭제할 수 있습니다. 자세한 내용은 [SQLGetInfo의](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형 및 [커서 및 준비된 명령문에 대한 트랜잭션의 효과를](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 [SQLBind매개 변수,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|명령문 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|명령문에 영향을 받는 행 수 반환|[SQLRowCount 함수(SQLRowCount Function)](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
