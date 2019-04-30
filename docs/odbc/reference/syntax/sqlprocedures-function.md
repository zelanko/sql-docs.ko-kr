---
title: SQLProcedures 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260406eddd6caef88035376a764c3e140547e6c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186137"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLProcedures** 특정 데이터 원본에 저장 된 프로시저 이름 목록을 반환 합니다. *프로시저* 는 일반적인 용어에 설명 하는 데는 *실행 개체*, 또는 입력 및 출력 매개 변수를 사용 하 여 호출할 수 있는 명명된 된 엔터티입니다. 프로시저에 대 한 자세한 내용은 참조는 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *CatalogName*  
 [입력] 프로시저 카탈로그입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *CatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *CatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *CatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 프로시저 스키마 이름에 대 한 검색 패턴을 문자열입니다. 드라이버를 일부 프로시저의 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 해당 프로시저를 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *SchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *SchemaName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *ProcName*  
 [입력] 프로시저 이름에 대 한 검색 패턴을 문자열입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *ProcName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *ProcName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **ProcName*합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLProcedures** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLProcedures** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 하지 않은 한 경우 드라이버에서 반환 됩니다 **SQLFetch** 또는**SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *CatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목* 반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 하며 *SchemaName* 또는 *ProcName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 함수가 호출 되었을 때이 비동기 함수 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.<br /><br /> 이름 길이 인수 중 하나의 값을 해당 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|프로시저 카탈로그를 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 프로시저 스키마를 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.<br /><br /> 프로시저 스키마 또는 프로시저 이름에 지정 된 문자열 검색 패턴 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 이 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLProcedures** 요청한 범위의 모든 프로시저를 나열 합니다. 사용자 수 또는 이러한 절차 중 하나를 실행할 수 있는 권한이 없을 수 있습니다. 내게 필요한 옵션을 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_ACCESSIBLE_PROCEDURES 정보 값을 확인 합니다. 그렇지 않은 경우 응용 프로그램 사용자가 실행할 수 있는 절차를 선택 하는 상황을 처리할 수 있어야 합니다. 이 정보를 어떻게 사용할 수 있는지에 대 한 자세한 내용은 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 **SQLProcedures** PROCEDURE_CAT, PROCEDURE_SCHEMA, 및 PROCEDURE_NAME 표준 결과 집합으로 결과 반환 합니다.  
  
> [!NOTE]  
>  **SQLProcedures** 모든 프로시저를 반환할 수 있습니다. 응용 프로그램에서 반환 되는지 여부에 관계 없이 유효한 모든 절차를 따르면 **SQLProcedures**합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다 *.x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|프로시저 _OWNER|프로시저 _SCHEM|  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM, 및 PROCEDURE_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, 및 SQL_MAX_PROCEDURE_ NAME_LEN 옵션입니다.  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 8 (PROCEDURE_TYPE) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 것이 아니라 결과 집합의 끝에서 카운트다운 여 드라이버별 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|프로시저 카탈로그 id입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 프로시저의 아니라 다른 다양 한 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 식별자입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 프로시저의 아니라 다른 다양 한 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|NULL이 아닌 Varchar|프로시저 식별자입니다.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|해당 사항 없음|나중에 사용하도록 예약되어 있습니다. 이러한 결과 열에 반환 되는 데이터 응용 프로그램 안 됩니다.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|해당 사항 없음|나중에 사용하도록 예약되어 있습니다. 이러한 결과 열에 반환 되는 데이터 응용 프로그램 안 됩니다.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|해당 사항 없음|나중에 사용하도록 예약되어 있습니다. 이러한 결과 열에 반환 되는 데이터 응용 프로그램 안 됩니다.|  
|설명 (ODBC 2.0)|7|Varchar|절차의 설명입니다.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|프로시저 유형을 정의합니다.<br /><br /> SQL_PT_UNKNOWN: 프로시저에 값을 반환 하는지 확인할 수 없습니다.<br /><br /> SQL_PT_PROCEDURE: 반환된 된 개체는 프로시저입니다. 즉,이 경우 반환 값<br /><br /> SQL_PT_FUNCTION: 반환된 된 개체는 함수입니다. 즉, 반환 값에 있습니다.|  
  
 합니다 *SchemaName* 하 고 *ProcName* 인수 검색 패턴을 허용 합니다. 올바른 검색 패턴에 대 한 자세한 내용은 참조 하세요. [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보를 반환합니다.|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|프로시저 열 설정 매개 변수 및 결과 반환 합니다.|[SQLProcedureColumns 함수](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|저장된 프로시저 호출 구문|[문 실행](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
