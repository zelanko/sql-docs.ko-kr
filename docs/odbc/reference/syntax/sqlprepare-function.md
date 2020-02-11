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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005760"
---
# <a name="sqlprepare-function"></a>SQLPrepare 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlprepare** 는 실행을 위해 SQL 문자열을 준비 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *StatementText*  
 입력 SQL 텍스트 문자열입니다.  
  
 *TextLength*  
 입력 문자에서 **StatementText* 의 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlprepare** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO을 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlprepare** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목을 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|구현 작업 조건 때문에 지정 된 문 특성이 잘못 되었습니다. 따라서 유사한 값이 일시적으로 대체 되었습니다. (**SQLGetStmtAttr** 를 호출 하 여 임시로 대체 된 값을 확인할 수 있습니다.) 대체 값은 커서가 닫힐 때까지 *StatementHandle* 에 대해 유효 합니다. 변경할 수 있는 문 특성은 SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|\**StatementText* 에 **INSERT** 문이 포함 되어 있고 삽입할 값의 수가 파생 테이블의 수준과 일치 하지 않습니다.|  
|21S02|파생 테이블의 수준이 열 목록과 일치 하지 않습니다.|\**StatementText* 에 **CREATE VIEW** 문이 포함 되어 있고 지정 된 이름의 수가 쿼리 사양에서 정의한 파생 테이블과 동일한 수준이 아닙니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|**StatementText* 에 리터럴 또는 매개 변수가 포함 된 SQL 문이 포함 되어 있고 값이 연결 된 테이블 열의 데이터 형식과 호환 되지 않습니다.|  
|22019|잘못 된 이스케이프 문자|인수 *StatementText* 에는 **Where** 절에 **이스케이프** 를 사용 하 여 **LIKE** 조건자가 포함 되어 **있으며 이스케이프 문자 뒤의** 길이는 1과 같지 않습니다.|  
|22025|이스케이프 시퀀스가 잘못 되었습니다.|인수 *StatementText* 에 **WHERE** 절에 "**LIKE** _pattern value_ **이스케이프** _이스케이프 문자_"가 포함 되어 있고 패턴 값의 이스케이프 문자 다음에 나오는 문자가 "%"도 아니고 "_"도 아닙니다.|  
|24000|잘못된 커서 상태|(DM) *StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|34000|잘못된 커서 이름|\**StatementText* 에 위치가 지정 된 **DELETE** 또는 위치 지정 **업데이트가**포함 되어 있으며 준비 중인 문에 의해 참조 된 커서가 열려 있지 않습니다.|  
|가는 000|카탈로그 이름이 잘못 되었습니다.|*StatementText* 에 지정 된 카탈로그 이름이 잘못 되었습니다.|  
|3F000|스키마 이름이 잘못 되었습니다.|*StatementText* 에 지정 된 스키마 이름이 잘못 되었습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText* 에 preparable 되지 않았거나 구문 오류가 포함 된 SQL 문이 포함 되어 있습니다.<br /><br /> **StatementText* 에는 사용자에 게 필요한 권한이 없는 문이 포함 되어 있습니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText* 에 **CREATE TABLE** 또는 **CREATE VIEW** 문이 포함 되어 있으며 지정 된 테이블 이름 또는 뷰 이름이 이미 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없습니다.|\**StatementText* 에 **Drop TABLE** 또는 **drop VIEW** 문이 포함 되어 있고 지정 된 테이블 이름이 나 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 에 **ALTER table** 문이 포함 되어 있고 지정한 테이블 이름이 없습니다.<br /><br /> \**StatementText* 에 **CREATE VIEW** 문이 포함 되어 있고 쿼리 사양에 정의 된 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 에 **CREATE INDEX** 문이 포함 되어 있고 지정한 테이블 이름이 없습니다.<br /><br /> \**StatementText* 에 **GRANT** 또는 **REVOKE** 문이 포함 되어 있고 지정 된 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 에 **SELECT** 문이 포함 되어 있고 지정 된 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 에 **DELETE**, **INSERT**또는 **UPDATE** 문이 포함 되어 있고 지정한 테이블 이름이 없습니다.<br /><br /> \**StatementText* 에 **CREATE TABLE** 문이 포함 되어 있으며 제약 조건에 지정 된 테이블 (생성 되는 테이블이 아닌 테이블 참조)이 존재 하지 않습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText* 에 **CREATE index** 문이 포함 되어 있고 지정한 인덱스 이름이 이미 존재 합니다.|  
|42S12|인덱스를 찾을 수 없음|\**StatementText* 에 **DROP INDEX** 문이 포함 되어 있고 지정한 인덱스 이름이 없습니다.|  
|42S21|열이 이미 있습니다.|\**StatementText* 에 **ALTER TABLE** 문이 포함 되어 있고 **ADD** 절에 지정 된 열이 고유 하지 않거나 기본 테이블의 기존 열을 식별 합니다.|  
|42S22|열을 찾을 수 없음|\**StatementText* 에 **CREATE INDEX** 문이 포함 되어 있고 열 목록에 지정 된 열 이름 중 하나 이상이 존재 하지 않습니다.<br /><br /> \**StatementText* 에 **GRANT** 또는 **REVOKE** 문이 포함 되어 있고 지정한 열 이름이 없습니다.<br /><br /> \**StatementText* 에 **SELECT**, **DELETE**, **INSERT**또는 **UPDATE** 문이 포함 되어 있고 지정한 열 이름이 없습니다.<br /><br /> \**StatementText* 에 **CREATE TABLE** 문이 포함 되어 있으며 제약 조건에 지정 된 열 (생성 되는 열이 아닌 테이블 참조)이 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) *StatementText* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlprepare** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Textlength* 가 0 보다 작거나 같지만 SQL_NTS와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|정의 된 커서 유형에 대 한 동시성 설정이 잘못 되었습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 준비를 위해 **Sqlprepare** 를 호출 하 여 데이터 원본에 SQL 문을 보냅니다. 준비 된 실행에 대 한 자세한 내용은 [준비 된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)을 참조 하세요. 응용 프로그램은 SQL 문에 하나 이상의 매개 변수 표식을 포함할 수 있습니다. 매개 변수 표식을 포함 하기 위해 응용 프로그램은 적절 한 위치에 있는 SQL 문자열에 물음표 (?)를 포함 합니다. 매개 변수에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
> [!NOTE]  
>  응용 프로그램에서 **Sqlprepare** 를 사용 하 여 **COMMIT** 또는 **ROLLBACK** 문을 **제출할 때이** 를 준비 하는 경우 DBMS 제품 간에 상호 운용할 수 없습니다. 트랜잭션을 커밋하거나 롤백하려면 **Sqlendtran**을 호출 합니다.  
  
 드라이버는 데이터 원본에서 사용 하는 SQL 형식을 사용 하도록 문을 수정한 다음 준비를 위해 데이터 원본에 제출할 수 있습니다. 특히 드라이버는 특정 기능에 대 한 SQL 구문을 정의 하는 데 사용 되는 이스케이프 시퀀스를 수정 합니다. SQL 문 문법에 대 한 설명은 ODBC 및 [부록 C: Sql 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) [의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 를 참조 하세요. 드라이버의 경우 문 핸들은 포함 된 SQL 코드의 문 식별자와 비슷합니다. 데이터 원본에서 문 식별자를 지 원하는 경우 드라이버는 문 식별자와 매개 변수 값을 데이터 원본으로 보낼 수 있습니다.  
  
 문을 준비한 후 응용 프로그램은 문 핸들을 사용 하 여 이후 함수 호출에서 문을 참조 합니다. 응용 프로그램이 SQL_DROP 옵션을 사용 하 여 **SQLFreeStmt** 호출을 사용 하거나 **sqlexecute**, **sqlexecdirect**또는 카탈로그 함수 (**sqlexecute**, **sqlexecute**등) 중 하나에 대 한 호출에서 문 핸들을 사용할 **때까지 문** 핸들과 연결 된 준비 된 문을 다시 실행할 수 있습니다. 응용 프로그램에서 문을 준비한 후에는 결과 집합의 형식에 대 한 정보를 요청할 수 있습니다. 일부 구현에서는 **Sqlprepare** 후에 **SQLDescribeCol** 또는 **SQLDescribeParam** 를 호출 하는 것이 **sqlprepare** 또는 **sqlexecdirect**이후에 함수를 호출 하는 것 만큼 효율적이 지 않을 수 있습니다.  
  
 응용 프로그램에서 **Sqlprepare**를 호출 하는 경우 일부 드라이버는 구문 오류 또는 액세스 위반을 반환할 수 없습니다. 드라이버는 구문 오류와 액세스 위반, 구문 오류 또는 구문 오류 또는 액세스 위반을 처리할 수 있습니다. 따라서 응용 프로그램은 **Sqlnumresultcols**, **SQLDescribeCol**, **Sqlcolattribute**및 **sqlexecute**와 같은 후속 관련 함수를 호출할 때 이러한 조건을 처리할 수 있어야 합니다.  
  
 드라이버 및 데이터 원본의 기능에 따라 문이 준비 될 때 (모든 매개 변수가 바인딩되어 있는 경우) 또는 실행 될 때 (모든 매개 변수가 바인딩되지 않은 경우) 매개 변수 정보 (예: 데이터 형식)를 확인할 수 있습니다. 상호 운용성을 최대화 하려면 응용 프로그램이 동일한 문에 새 SQL 문을 준비 하기 전에 이전 SQL 문에 적용 된 모든 매개 변수를 바인딩 해제 해야 합니다. 이렇게 하면 이전 매개 변수 정보가 새 문에 적용 되기 때문에 발생 하는 오류를 방지할 수 있습니다.  
  
> [!IMPORTANT]  
>  **Sqlendtran** 을 명시적으로 호출 하거나 자동 커밋 모드로 작업 하 여 트랜잭션을 커밋하면 데이터 원본에서 연결의 모든 문에 대 한 액세스 계획을 삭제할 수 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식 및 [커서와 준비 된 문의 트랜잭션 효과](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)를 참조 하세요.  
  
## <a name="code-example"></a>코드 예  
 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [Sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md)및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수에 버퍼 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문의 영향을 받는 행 수 반환|[SQLRowCount 함수(SQLRowCount Function)](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
