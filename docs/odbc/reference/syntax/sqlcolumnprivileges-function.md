---
description: SQLColumnPrivileges 함수(SQLColumnPrivileges Function)
title: SQLColumnPrivileges 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29ac9ba44c0627e0aa72cc9e1bec087357864bb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448789"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 함수(SQLColumnPrivileges Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **Sqlcolumnprivileges** 지정 된 테이블에 대 한 열 및 관련 된 권한 목록을 반환 합니다. 드라이버는 지정 된 *StatementHandle*에 대 한 결과 집합으로 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 입력 문 핸들입니다.  
  
 *CatalogName*  
 입력 카탈로그 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 카탈로그의 이름을 지원 하지만 다른 Dbms에서 데이터를 검색 하는 경우 처럼 빈 문자열 ("")은 이름이 없는 카탈로그를 나타냅니다. *CatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 스키마 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")은 스키마가 없는 테이블을 나타냅니다. *SchemaName* 에는 문자열 검색 패턴을 사용할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 됩니다. SQL_FALSE 되는 경우 *SchemaName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *TableName*  
 입력 테이블 이름입니다. 이 인수는 null 포인터 일 수 없습니다. *TableName* 은 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *TableName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *TableName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **TableName*의 문자 길이입니다.  
  
 *ColumnName*  
 입력 열 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *ColumnName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *ColumnName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength4*  
 입력 **ColumnName*의 문자 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcolumnprivileges** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **Sqlcolumnprivileges** 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고, **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|*TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName* 또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 이름에 대 한 최대 길이 값을 초과 했습니다. "설명"을 참조 하십시오.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그 이름이 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름이 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> 열 이름에 대해 문자열 검색 패턴을 지정 했으며 데이터 원본에서 해당 인수에 대 한 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_CONCURRENCY 및 SQL_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **Sqlcolumnprivileges** TABLE_CAT, TABLE_SCHEM, TABLE_NAME, COLUMN_NAME 및 권한에 따라 정렬 된 표준 결과 집합으로 결과를 반환 합니다.  
  
> [!NOTE]  
>  **Sqlcolumnprivileges** 모든 열에 대 한 권한을 반환 하지 않을 수 있습니다. 예를 들어 드라이버는 Oracle ROWID와 같은 의사 (pseudo) 열에 대 한 권한 정보를 반환 하지 않을 수 있습니다. 응용 프로그램은 **Sqlcolumnprivileges**반환 하는지 여부에 관계 없이 모든 유효한 열을 사용할 수 있습니다.  
  
 VARCHAR 열의 길이는 테이블에 표시 되지 않습니다. 실제 길이는 데이터 원본에 따라 달라 집니다. CATALOG_NAME, SCHEMA_NAME, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 ODBC 3의 열 이름은 다음과 같습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 8 (IS_GRANTABLE)을 초과 하는 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 액세스할 수 있어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 식별자 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|스키마 식별자 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|테이블 식별자입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|열 이름입니다. 드라이버는 이름이 없는 열에 대해 빈 문자열을 반환 합니다.|  
|GRANTOR (ODBC 1.0)|5|Varchar|권한을 부여한 사용자의 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다.<br /><br /> 피부 여자 열의 값이 개체의 소유자 인 모든 행에 대해 GRANTOR 열은 "_SYSTEM"이 됩니다.|  
|피부 여자 (ODBC 1.0)|6|Varchar not NULL|권한이 부여 된 사용자의 이름입니다.|  
|권한 (ODBC 1.0)|7|Varchar not NULL|열 권한을 식별 합니다. 다음 중 하나일 수 있습니다 (또는 구현 정의 시 데이터 소스에서 지 원하는 다른 항목).<br /><br /> SELECT: 피부 여자는 열에 대 한 데이터를 검색할 수 있습니다.<br /><br /> INSERT: 피부 여자는 연결 된 테이블에 삽입 된 새 행에 열에 대 한 데이터를 제공할 수 있습니다.<br /><br /> 업데이트: 피부 여자는 열의 데이터를 업데이트할 수 있습니다.<br /><br /> 참조: 피부 여자는 제약 조건 (예: unique, 참조 또는 테이블 check 제약 조건) 내의 열을 참조할 수 있습니다.|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|피부 여자에서 다른 사용자에 게 권한을 부여할 수 있는지 여부를 나타냅니다. 데이터 원본에 적용할 수 없거나 알 수 없는 경우 "YES", "NO" 또는 "NULL"입니다.<br /><br /> 권한은 부여할 수 있는 또는 not 부여할 수 있는 중 하나입니다. **Sqlcolumnprivileges** 반환 하는 결과 집합에는 IS_GRANTABLE 열을 제외한 모든 열에 동일한 값이 포함 된 두 개의 행이 포함 되지 않습니다.|  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제는 [Sqlcolumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블이 나 테이블의 열 반환|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|테이블 또는 테이블에 대 한 권한 반환|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|데이터 원본에 있는 테이블 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
