---
title: SQLColumn특전 함수 | 마이크로 소프트 문서
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
ms.openlocfilehash: e94c5524bcde3023bae3298c8dbb6d03347a0b8e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301270"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 함수(SQLColumnPrivileges Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLColumnPrivileges는** 지정된 테이블에 대한 열 및 관련 권한 목록을 반환합니다. 드라이버는 지정된 *StatementHandle*에 설정된 결과로 정보를 반환합니다.  
  
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
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색하는 경우와 같이 드라이버가 일부 카탈로그에 대한 이름을 지원하지만 다른 카탈로그에는 지원하지 않는 경우 빈 문자열("")은 이름이 없는 카탈로그를 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *CatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] **카탈로그 이름의*문자 길이 .  
  
 *스키마 이름*  
 [입력] 스키마 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다. *스키마Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *SchemaName은* 식별자로 처리됩니다. SQL_FALSE 경우 *스키마이름은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이2*  
 [입력] **스키마 이름의*문자 길이입니다.  
  
 *Tablename*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터가 될 수 없습니다. *TableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *TableName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE *경우 TableName은* 일반 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이3*  
 [입력] **테이블 네임의*문자 길이 .  
  
 *ColumnName*  
 [입력] 열 이름에 대한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *ColumnName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *ColumnName은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이4*  
 [입력] **열 이름의*문자 길이 .  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLColumnPrivileges** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 유형* 및 *명령문* *핸들* 핸들을 **호출** 하 여 가져올 수 있습니다. 다음 표에서는 **SQLColumnPrivileges에서 일반적으로 반환되는 SQLSTATE** 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서* 커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|*TableName* 인수는 null 포인터였습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *스키마Name* 또는 *ColumnName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 이 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 이름의 최대 길이 값을 초과했습니다. ("댓글"참조))|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|카탈로그 이름이 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 스키마 이름이 지정되었으며 드라이버 또는 데이터 원본은 스키마를 지원하지 않습니다.<br /><br /> 열 이름에 대해 문자열 검색 패턴이 지정되었으며 데이터 원본은 해당 인수에 대한 검색 패턴을 지원하지 않습니다.<br /><br /> SQL_CONCURRENCY 및 SQL_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLColumnPrivileges는** TABLE_CAT, TABLE_SCHEM, TABLE_NAME, COLUMN_NAME 및 권한에 따라 정렬된 표준 결과 집합으로 결과를 반환합니다.  
  
> [!NOTE]  
>  **SQLColumn프리특권은** 모든 열에 대한 권한을 반환하지 않을 수 있습니다. 예를 들어 드라이버는 Oracle ROWID와 같은 의사 열에 대한 권한에 대한 정보를 반환하지 않을 수 있습니다. 응용 프로그램은 **SQLColumnPrivileges에**의해 반환되는지 여부에 관계없이 유효한 열을 사용할 수 있습니다.  
  
 VARCHAR 열의 길이는 표에 표시되지 않습니다. 실제 길이는 데이터 원본에 따라 다릅니다. CATALOG_NAME, SCHEMA_NAME, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 ODBC 3의 경우 다음 열의 이름이 변경되었습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 8(IS_GRANTABLE)을 초과하는 추가 열은 드라이버가 정의할 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 식별자; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에는 지원하지 않는 경우 카탈로그가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|스키마 식별자; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 스키마가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_NAME (ODBC 1.0)|3|바르카르 는 NULL이 아닙니다.|테이블 식별자입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|바르카르 는 NULL이 아닙니다.|열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|그랜터 (ODBC 1.0)|5|Varchar|권한을 부여한 사용자의 이름입니다. 데이터 원본에 적용되지 않는 경우 NULL입니다.<br /><br /> GRANTEE 열의 값이 개체의 소유자인 모든 행의 경우 GRANTOR 열은 "_SYSTEM"이 됩니다.|  
|그랜테 (ODBC 1.0)|6|바르카르 는 NULL이 아닙니다.|권한이 부여된 사용자의 이름입니다.|  
|권한(ODBC 1.0)|7|바르카르 는 NULL이 아닙니다.|열 권한을 식별합니다. 다음 중 하나일 수 있습니다(또는 구현 정의 시 데이터 원본에서 지원하는 다른 것)일 수 있습니다.<br /><br /> SELECT: 수혜자는 열에 대한 데이터를 검색할 수 있습니다.<br /><br /> INSERT: 받는 사람은 연결된 테이블에 삽입된 새 행의 열에 대한 데이터를 제공할 수 있습니다.<br /><br /> 업데이트: 수혜자는 열의 데이터를 업데이트할 수 있습니다.<br /><br /> 참조: 받는 사람은 제약 조건 내의 열을 참조할 수 있습니다(예: 고유, 참조 또는 테이블 검사 제약 조건).|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|수혜자가 다른 사용자에게 권한을 부여할 수 있는지 여부를 나타냅니다. 데이터 원본에 알 수 없거나 적용할 수 없는 경우 "예", "아니오" 또는 "NULL"입니다.<br /><br /> 권한은 부여가능하거나 부여할 수 없지만 둘 다 부여할 수는 없습니다. **SQLColumnPrivileges에서** 반환하는 결과 집합에는 IS_GRANTABLE 열을 제외한 모든 열에 동일한 값이 포함된 두 개의 행이 포함되지 않습니다.|  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제는 [SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블 또는 테이블의 열 반환|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|테이블 또는 테이블에 대한 권한 반환|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|데이터 원본의 테이블 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
