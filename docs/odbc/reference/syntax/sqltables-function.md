---
title: "SQLTables 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLTables
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLTables
helpviewer_keywords: SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 207415fc333cbc4373454b815ad27431c07c8d61
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-function"></a>SQLTables 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: Open Group  
  
 **요약**  
 **SQLTables** 테이블, 카탈로그 또는 스키마 이름 및 특정 데이터 원본에 저장 되는 테이블 형식 목록을 반환 합니다. 드라이버 정보 결과 집합으로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들에 대 한 결과 검색 합니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. *CatalogName* 인수 검색 패턴 SQL_ODBC_VERSION 환경 특성이 SQL_OV_ODBC3 경우 받으며 SQL_OV_ODBC2 설정 된 경우 검색 패턴 허용 되지 않습니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 있지만 대 한 드라이버를 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 경우 ("") 카탈로그를 갖지 않는 이러한 테이블을 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *CatalogName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *CatalogName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다. 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버 일부 테이블에 대 한 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마가 없는 테이블을 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *SchemaName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *SchemaName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *테이블 이름*  
 [입력] 테이블 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *TableName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *TableName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
 *TableType*  
 [입력] 테이블 형식에 맞게 목록입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성에는에 아무런 영향을 주지는 *TableType* 인수입니다. *TableType* SQL_ATTR_METADATA_ID 설정에 관계 없이 값 목록 인수입니다.  
  
 *NameLength4*  
 [입력] 문자 길이 **TableType*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLTables** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLTables** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|에 커서가 열린는 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출한 합니다. 이 오류는 경우 드라이버 관리자에서 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** sql_no_data가 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 에 커서가 열린는 *StatementHandle*, 하지만 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 합니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된는 *CatalogName* 인수는 null 포인터 되었으며는 SQL_CATALOG_NAME *정보 항목* 카탈로그 이름은 반환 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된 및 *SchemaName* 또는 *TableName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 SQLTables가 호출 될 때 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 길이 인수 중 하나의 값이 0 보다 작은 하지만 SQL_NTS과 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값을 해당 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그를 지정 하 고 드라이버 또는 데이터 원본 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마가 지정 하 고 드라이버 또는 데이터 원본의 스키마를 지원 하지 않습니다.<br /><br /> String 검색 패턴 카탈로그 이름, 테이블 스키마 또는 테이블 이름에 대해 지정 된 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정의 조합 드라이버 또는 데이터 원본에서 지원 되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버 책갈피에 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLTables** 요청된 된 범위에 모든 테이블을 나열 합니다. 사용자 수 또는 이러한 테이블 중 하나에 대 한 선택 권한이 없을 수 있습니다. 내게 필요한 옵션을 확인 하려면 응용 프로그램는 다음을 수행할 수 있습니다.  
  
-   호출 **SQLGetInfo** SQL_ACCESSIBLE_TABLES 정보 유형을 확인 합니다.  
  
-   호출 **SQLTablePrivileges** 각 테이블에 대 한 권한을 확인 합니다.  
  
 그렇지 않으면 응용 프로그램 수 있어야 사용자가을 표를 선택 하는 상황을 처리 **선택** 권한이 부여 되지 않습니다.  
  
 *SchemaName* 및 *TableName* 인수 검색 패턴에 동의 합니다. *CatalogName* 인수 검색 패턴 SQL_ODBC_VERSION 환경 특성이 SQL_OV_ODBC3 경우 받으며 SQL_OV_ODBC2 설정 된 경우 검색 패턴 허용 되지 않습니다. ODBC 3 SQL_OV_ODBC3 설정*.x* 드라이버에 해당 와일드 카드 문자를 입력 해야 합니다는 *CatalogName* 인수는 문자 그대로 처리 하려면 이스케이프 되어야 합니다. 올바른 검색 패턴에 대 한 자세한 내용은 참조 [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
> [!NOTE]  
>  일반적으로 사용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 에 대해 정의 된 다음과 같은 특별 한 의미 체계를 지원 하기 위해 카탈로그, 스키마 및 테이블 형식 열거는 *CatalogName*, *SchemaName*, *TableName*, 및  *TableType* 의 인수 **SQLTables**:  
  
-   경우 *CatalogName* 변수가 sql_all_catalogs이 고 *SchemaName* 및 *TableName* 빈 문자열이 결과 집합의 데이터 원본에 대 한 올바른 카탈로그 목록을 포함 합니다. (TABLE_CAT 열을 제외한 모든 열에 Null이 포함 될.)  
  
-   경우 *SchemaName* SQL_ALL_SCHEMAS은 및 *CatalogName* 및 *TableName* 는 빈 문자열로 결과 집합의 데이터 원본에 대해 유효한 스키마 목록을 포함 합니다. (Table_schem 순으로 정렬 열을 제외한 모든 열에 Null이 포함 될.)  
  
-   경우 *TableType* SQL_ALL_TABLE_TYPES은 및 *CatalogName*, *SchemaName*, 및 *TableName* 는 빈 문자열로 결과 집합 데이터 원본에 대 한 올바른 테이블 형식 목록이 포함 되어 있습니다. (TABLE_TYPE 열을 제외한 모든 열에 Null이 포함 될.)  
  
 경우 *TableType* 는 빈 문자열이 아닌지 관심 있는 형식에 대 한 쉼표로 구분 된 값 목록을 포함 해야 각 작은따옴표 (')로 묶을 수 있습니다, 또는 값, 따옴표가 없는 예: '테이블', '보기' 또는 테이블을 보고 합니다. 응용 프로그램에 테이블 형식 항상 지정 해야에 대문자로; 드라이버는 그대로 데이터 원본에 필요한 테이블 형식을 변환 합니다. 데이터 원본이 지정 된 테이블 형식을 지원 하지 않는 경우 **SQLTables** 해당 유형에 대 한 모든 결과 반환 하지 않습니다.  
  
 **SQLTables** TABLE_TYPE, TABLE_CAT, table_schem 순으로 정렬, 및 TABLE_NAME 순으로 정렬 하 여 표준 결과 집합으로 결과 반환 합니다. 이 정보를 어떻게 사용할 수 있는지에 대 한 정보를 참조 하십시오. [카탈로그 데이터의 사용 하 여](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
 TABLE_CAT, table_schem 순으로 정렬, 및 TABLE_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, 및 SQL_MAX_TABLE_NAME_LEN 정보 형식입니다.  
  
 ODBC 3에 대 한 다음 열의 이름이 바뀌었습니다*.x*합니다. 열 이름 변경 응용 프로그램 열 번호에 의해 바인딩될 있기 때문에 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3*.x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에 의해 열 5 (설명) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 결과 명시적 서 수 위치를 지정 하는 대신 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 참조 [카탈로그 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버 카탈로그 일부 테이블을 지원 하지만 지원만, 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 카탈로그를 갖지 않는 이러한 테이블에 대 한 합니다.|  
|TABLE_SCHEM 순으로 정렬 (ODBC 1.0)|2|Varchar|스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 지 원하는 스키마만, 하지만 일부 테이블에 대 한 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 스키마가 없는 해당 테이블에 대 한 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|테이블 이름입니다.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|테이블 형식 이름입니다. 다음 중 하나: "TABLE", "보기", "시스템 테이블", "전역 임시", "로컬 임시", "별칭", "동의어", 또는 데이터 원본에 따른 특정 형식 이름입니다.<br /><br /> "별칭" 및 "동의어"의 의미는 드라이버 마다 다릅니다.|  
|설명 (ODBC 1.0)|5|Varchar|테이블의 설명입니다.|  
  
## <a name="example"></a>예제  
 다음 샘플 코드 핸들 및 연결 해제 하지 않습니다. 참조 [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md) 및 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md) 에 대 한 코드 예제를 핸들 및 문을 해제 합니다.  
  
```  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|하나 이상의 열에 대 한 권한을 반환합니다.|[SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|테이블 또는 테이블의 열을 반환합니다.|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|테이블 통계 및 인덱스를 반환합니다.|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|테이블 또는 테이블에 대 한 권한을 반환합니다.|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
