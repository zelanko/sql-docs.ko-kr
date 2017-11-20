---
title: "SQLColumnPrivileges 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b9fa1af8ad7cc84b69f3e54e7f1f7f911880bb25
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 함수(SQLColumnPrivileges Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLColumnPrivileges** 열과 지정된 된 테이블에 대 한 연결된 권한을의 목록을 반환 합니다. 결과 집합으로 지정 된 정보를 반환 하는 드라이버 *StatementHandle*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. 일부 카탈로그에 대 한 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른는 드라이버가 지원 이름 ("") 이름이 있는 경우 해당 카탈로그를 나타냅니다. *CatalogName* string 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *CatalogName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *CatalogName* 는 일반 인수 리터럴로 취급 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 스키마 이름입니다. 드라이버 일부 테이블에 대 한 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마가 없는 테이블을 나타냅니다. *SchemaName* string 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *SchemaName* 식별자로 처리 됩니다. SQL_FALSE, 이면 *SchemaName* 는 일반 인수 리터럴로 취급 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *테이블 이름*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터 수 없습니다. *TableName* string 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *TableName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *TableName* 는 일반 인수 리터럴로 취급 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
 *열 이름*  
 [입력] 열 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *ColumnName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *ColumnName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength4*  
 [입력] 문자 길이 **ColumnName*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLColumnPrivileges** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 여의 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLColumnPrivileges** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버에 의해 반환 된 Sqlstate 설명 관리자입니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|에 커서가 열린는 *StatementHandle,* 및 **SQLFetch** 또는 **SQLFetchScroll** 호출한 합니다. 이 오류는 경우 드라이버 관리자에서 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 에 커서가 열린는 *StatementHandle*, 하지만 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 합니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|*TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된는 *CatalogName* 인수는 null 포인터 되었으며는 SQL_CATALOG_NAME *정보 항목* 카탈로그 이름은 반환 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된 및 *SchemaName* 또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수는 여전히 호출 되었을 때 실행 되 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 하지만 SQL_NTS과 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값을 해당 이름에 대 한 최대 길이 값을 초과 했습니다. ("주석" 참조)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그 이름을 지정 하 고 드라이버 또는 데이터 원본 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름을 지정 하 고 드라이버 또는 데이터 원본의 스키마를 지원 하지 않습니다.<br /><br /> 검색 패턴은 문자열 열 이름에 대해 지정 된 하 고 데이터 원본에 대 한 인수에 지정 된 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_CONCURRENCY 및에서는 SQL_CURSOR_TYPE 문 특성의 현재 설정의 조합 드라이버 또는 데이터 원본에서 지원 되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버 책갈피에 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 **SQLColumnPrivileges** TABLE_CAT, table_schem 순으로 정렬, TABLE_NAME, COLUMN_NAME 및 권한 순으로 정렬 하 여 표준 결과 집합으로 결과 반환 합니다.  
  
> [!NOTE]  
>  **SQLColumnPrivileges** 모든 열에 대 한 권한을 반환할 수 있습니다. 예를 들어, 드라이버는 Oracle ROWID 등의 의사 (pseudo) 열에 대 한 권한에 대 한 정보를 반환 하지 수도 있습니다. 응용 프로그램으로 반환 되는지 여부에 관계 없이 모든 유효한 열을 사용할 수 **SQLColumnPrivileges**합니다.  
  
 VARCHAR 열의 길이; 테이블에 표시 되지 않습니다. 실제 길이 데이터 원본에 따라 달라 집니다. CATALOG_NAME SCHEMA_NAME, TABLE_NAME, COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_와 LEN, 및 SQL_MAX_COLUMN_NAME_LEN 옵션입니다.  
  
> [!NOTE]  
>  일반적으로 사용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다. *x*합니다. 열 이름 변경 응용 프로그램 열 번호에 의해 바인딩될 있기 때문에 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3입니다. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에 의해 열 8 (IS_GRANTABLE) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적는 서 수 위치를 지정 하지 않고 결과 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 참조 [카탈로그 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|설명|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1.|Varchar|카탈로그의 id입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버 카탈로그 일부 테이블을 지원 하지만 지원만, 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 카탈로그를 갖지 않는 이러한 테이블에 대 한 합니다.|  
|TABLE_SCHEM 순으로 정렬 (ODBC 1.0)|2|Varchar|스키마 식별자입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 지 원하는 스키마만, 하지만 일부 테이블에 대 한 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 스키마가 없는 해당 테이블에 대 한 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|NULL이 아닌 Varchar|테이블 식별자입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|NULL이 아닌 Varchar|열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|GRANTOR (ODBC 1.0)|5|Varchar|권한 부여는 사용자의 이름 데이터 원본에 적용할 수 없는 경우 NULL입니다.<br /><br /> 피부 여자에 게 열에 있는 값의 개체의 소유자는 모든 행에 대해 GRANTOR 열은 "(_s)"를 됩니다.|  
|피부 여 자가 (ODBC 1.0)|6|NULL이 아닌 Varchar|에 권한 부여 된 사용자 이름입니다.|  
|권한 (ODBC 1.0)|7|NULL이 아닌 Varchar|열 권한을 식별합니다. 다음 중 하나일 수 있습니다 (또는 경우 원본 데이터에서 지 원하는 다른 구현에서 정의 된):<br /><br /> 선택: 피부 여자에 게 열에 대 한 데이터를 검색할 수 있습니다.<br /><br /> INSERT의 경우: 피부 여자에 게는 연결 된 테이블에 삽입 된 새 행의 열에 대 한 데이터를 제공할 수 있습니다.<br /><br /> 업데이트: 피부 여자에 게 열에서 데이터를 업데이트할 수 있습니다.<br /><br /> 참조: 제약 조건 내에서 열을 참조 하는 grantee를 허용할 (예를 들어 고유 참조, 또는 테이블 check 제약 조건).|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|피부 여 자가 다른 사용자에 게; 권한을 부여 하려면 허용 되는지 여부를 나타냅니다. "YES", "NO" 또는 "NULL" 알 수 없거나 데이터 원본에 적용할 수 없는 경우.<br /><br /> 권한 중 하나 부여할 수 있는 또는 하지 부여할 수 있는입니다. 반환 된 결과 집합 **SQLColumnPrivileges** IS_GRANTABLE 열을 제외한 모든 열을 동일한 값을 포함 하는 두 개의 행 포함 됩니다.|  
  
## <a name="code-example"></a>코드 예  
 유사한 기능의 코드 예제를 참조 하십시오. [SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블 또는 테이블의 열을 반환합니다.|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|테이블 또는 테이블에 대 한 권한을 반환합니다.|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|데이터 원본에서 테이블의 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

