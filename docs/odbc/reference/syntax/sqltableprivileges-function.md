---
title: SQLTablePrivileges 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe1b3a3420ad882136b13b131938169dbdb224bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233551"
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLTablePrivileges** 테이블과 각 테이블과 연결 된 권한 목록을 반환 합니다. 드라이버는 결과 집합으로 지정 된 문에 대 한 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *CatalogName*  
 [입력] 테이블 카탈로그입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *CatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *CatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *CatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 스키마 이름에 대 한 검색 패턴을 문자열입니다. 드라이버를 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 테이블을 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *SchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *SchemaName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *TableName*  
 [입력] 테이블 이름에 대 한 검색 패턴을 문자열입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *TableName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *TableName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLTablePrivileges** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLTablePrivileges** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 앞 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 . 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** sql_no_data가 반환 되지 않은 및 드라이버에 의해 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. **SQLTablePrivileges** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된  *StatementHandle*합니다. 그런 다음 **SQLTablePrivileges** 에서 다시 호출 된 함수는 *StatementHandle*합니다.<br /><br /> **SQLTablePrivileges** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된  *StatementHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *CatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목* 반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 하며 *SchemaName* 또는 *TableName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLTablePrivileges** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.<br /><br /> 이름 길이 인수 중 하나의 값을는 해당 한정자 또는 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그를 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마를 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.<br /><br /> 테이블 스키마, 테이블 이름 또는 열 이름에 대 한 지정 된 문자열 검색 패턴 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 합니다 *SchemaName* 하 고 *TableName* 인수 검색 패턴을 허용 합니다. 올바른 검색 패턴에 대 한 자세한 내용은 참조 하세요. [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
 **SQLTablePrivileges** TABLE_CAT, table_schem 순, TABLE_NAME, 권한 및 피부 여자에 게 표준 결과 집합으로 결과 반환 합니다.  
  
 TABLE_CAT 고 table_schem 순, TABLE_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, 및 SQL_MAX_TABLE_NAME_LEN 옵션을 사용 하 여 합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다 *.x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 7 (IS_GRANTABLE) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 것이 아니라 결과 집합의 끝에서 카운트다운 여 드라이버별 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 테이블에 대 한 합니다.|  
|TABLE_SCHEM 순 (ODBC 1.0)|2|Varchar|스키마 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 테이블에 대 한 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|NULL이 아닌 Varchar|테이블 이름입니다.|  
|GRANTOR (ODBC 1.0)|4|Varchar|권한을 부여할 사용자의 이름 데이터 원본에 해당 하지 않는 경우 NULL입니다.<br /><br /> 피부 여자에 게 열의 값은 개체의 소유자는 모든 행에 대해 GRANTOR 열에 "(_s)" 됩니다.|  
|피부 여 자가 (ODBC 1.0)|5|NULL이 아닌 Varchar|부여 된 권한을 부여한 사용자 이름입니다.|  
|권한 (ODBC 1.0)|6|NULL이 아닌 Varchar|테이블 권한입니다. 다음 오류 또는 데이터 소스 관련 권한 중 하나일 수 있습니다.<br /><br /> 선택 합니다. 피부 여자에 게는 테이블의 하나 이상의 열에 대 한 데이터를 검색 하도록 허용 됩니다.<br /><br /> INSERT의 경우: 피부 여자에 게 테이블에 하나 이상의 열에 대 한 데이터를 포함 하는 새 행을 삽입할 수 있습니다.<br /><br /> 업데이트: 피부 여자에 게는 테이블의 하나 이상의 열에서 데이터를 업데이트 하도록 허용 됩니다.<br /><br /> 삭제: 피부 여자에 게는 테이블에서 데이터의 행을 삭제 하도록 허용 됩니다.<br /><br /> 참조: 피부 여자에 게 제약 조건 내에 있는 테이블의 하나 이상의 열을 참조할 때 허용 됩니다 (예를 들어, 고유, 참조, 또는 check 제약 조건 테이블).<br /><br /> 피부 여 자가 지정된 된 테이블 권한에서 허용 하는 작업의 범위는 데이터 원본에 따라 결정 됩니다. 예를 들어 UPDATE 권한은 피부 여자 하나의 데이터 원본에서 테이블의 모든 열 그리고 다른 데이터 원본에서 grantor가 UPDATE 권한을는 열만 업데이트를 허용 될 수 있습니다.|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|다른 사용자에 게 권한을 부여할 피부 여자에 게 허용 되는지 여부를 나타냅니다. "YES", "아니요" 또는 데이터 원본에 적용할 수 없거나 알 수 없는 경우 NULL입니다.<br /><br /> 권한을은 부여할 수 있는 되었거나 하나만 부여할 수 없습니다. 반환한 결과 집합 **SQLColumnPrivileges** IS_GRANTABLE 열을 제외한 모든 열에는 동일한 값을 포함 하는 두 개의 행이 포함 되지 않는 합니다.|  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제를 참조 하세요 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|열 또는 열에 대 한 권한을 반환합니다.|[SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|테이블 또는 테이블에 열을 반환합니다.|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|테이블 통계 및 인덱스를 반환합니다.|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|데이터 원본에서 테이블의 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
