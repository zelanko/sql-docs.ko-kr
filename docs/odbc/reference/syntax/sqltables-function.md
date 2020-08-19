---
description: SQLTables 함수
title: SQLTables 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1eb095849362914074e2c1e7f02166db2712894
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421047"
---
# <a name="sqltables-function"></a>SQLTables 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 그룹 열기  
  
 **요약**  
 **Sqltables** 는 특정 데이터 원본에 저장 된 테이블, 카탈로그 또는 스키마 이름 및 테이블 형식 목록을 반환 합니다. 드라이버는 정보를 결과 집합으로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 입력 검색 결과에 대 한 문 핸들입니다.  
  
 *CatalogName*  
 입력 카탈로그 이름입니다. SQL_ODBC_VERSION 환경 특성이 SQL_OV_ODBC3 되는 경우 *CatalogName* 인수는 검색 패턴을 허용 합니다. SQL_OV_ODBC2 설정 된 경우 검색 패턴을 허용 하지 않습니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지 원하는 경우에는 빈 문자열 ("")에 카탈로그가 없는 테이블이 표시 됩니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")에는 스키마가 없는 테이블이 표시 됩니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 되 고 대/소문자는 중요 하지 않습니다. SQL_FALSE 되는 경우 *SchemaName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *TableName*  
 입력 테이블 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *TableName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *TableName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **TableName*의 문자 길이입니다.  
  
 *TableType*  
 입력 일치 시킬 테이블 형식의 목록입니다.  
  
 SQL_ATTR_METADATA_ID statement 특성은 *TableType* 인수에 영향을 주지 않습니다. *TableType* 는 SQL_ATTR_METADATA_ID의 설정에 관계 없이 값 목록 인수입니다.  
  
 *NameLength4*  
 입력 **TableType*의 문자 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqltables** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하면 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqltables** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch 또는** **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고 **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName* 또는 *TableName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 SQLTables가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그가 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마가 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> 카탈로그 이름, 테이블 스키마 또는 테이블 이름에 대해 문자열 검색 패턴을 지정 했으며 데이터 원본이 이러한 인수 중 하나 이상에 대 한 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **Sqltables** 는 요청 된 범위의 모든 테이블을 나열 합니다. 사용자에 게 이러한 테이블에 대 한 선택 권한이 있거나 없을 수도 있습니다. 내게 필요한 옵션을 확인 하기 위해 응용 프로그램은 다음을 수행할 수 있습니다.  
  
-   **SQLGetInfo** 를 호출 하 고 SQL_ACCESSIBLE_TABLES 정보 유형을 확인 합니다.  
  
-   **Sqltableprivileges** 을 호출 하 여 각 테이블에 대 한 권한을 확인 합니다.  
  
 그렇지 않으면 응용 프로그램은 사용자가 **SELECT** 권한이 부여 되지 않은 테이블을 선택 하는 상황을 처리할 수 있어야 합니다.  
  
 *SchemaName* 및 *TableName* 인수는 검색 패턴을 허용 합니다. SQL_ODBC_VERSION 환경 특성이 SQL_OV_ODBC3 되는 경우 *CatalogName* 인수는 검색 패턴을 허용 합니다. SQL_OV_ODBC2 설정 된 경우 검색 패턴을 허용 하지 않습니다. SQL_OV_ODBC3 설정 된 경우 ODBC*3.x 드라이버에서* *CatalogName* 인수의 와일드 카드 문자를 이스케이프 처리 하 여 리터럴로 처리 해야 합니다. 유효한 검색 패턴에 대 한 자세한 내용은 [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)를 참조 하세요.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 카탈로그, 스키마 및 테이블 형식의 열거를 지원 하기 위해 다음과 같은 특수 한 의미 체계가 **Sqltables**의 *CatalogName*, *SchemaName*, *TableName*및 *TableType* 인수에 대해 정의 됩니다.  
  
-   *CatalogName* 이 SQL_ALL_CATALOGS이 고 *SchemaName* 및 *TableName* 이 빈 문자열인 경우 결과 집합에는 데이터 원본에 대 한 유효한 카탈로그 목록이 포함 됩니다. TABLE_CAT 열을 제외한 모든 열에는 Null이 포함 됩니다.  
  
-   *SchemaName* 이 SQL_ALL_SCHEMAS이 고 *CatalogName* 및 *TableName* 이 빈 문자열인 경우 결과 집합에는 데이터 원본에 대 한 유효한 스키마 목록이 포함 됩니다. TABLE_SCHEM 열을 제외한 모든 열에는 Null이 포함 됩니다.  
  
-   *TableType* 이 SQL_ALL_TABLE_TYPES이 고 *CatalogName*, *SchemaName*및 *TableName* 이 빈 문자열인 경우 결과 집합에는 데이터 원본에 대 한 유효한 테이블 형식 목록이 포함 됩니다. TABLE_TYPE 열을 제외한 모든 열에는 Null이 포함 됩니다.  
  
 *TableType* 이 빈 문자열이 아니면 관심 있는 형식의 쉼표로 구분 된 값 목록을 포함 해야 합니다. 각 값은 작은따옴표 (') 또는 따옴표 붙지 않은 (예: ' TABLE ', ' VIEW ' 또는 TABLE, VIEW)로 묶을 수 있습니다. 응용 프로그램은 항상 대문자로 테이블 형식을 지정 해야 합니다. 드라이버는 데이터 원본에 필요한 경우로 테이블 형식을 변환 해야 합니다. 데이터 원본에서 지정 된 테이블 형식을 지원 하지 않는 경우 **Sqltables** 는 해당 형식에 대 한 결과를 반환 하지 않습니다.  
  
 **Sqltables** 는 TABLE_TYPE, TABLE_CAT, TABLE_SCHEM 및 TABLE_NAME를 기준으로 정렬 된 표준 결과 집합으로 결과를 반환 합니다. 이 정보를 사용 하는 방법에 대 한 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
 TABLE_CAT, TABLE_SCHEM 및 TABLE_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN 및 SQL_MAX_TABLE_NAME_LEN 정보 형식을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
 ODBC 3.x에 대해 다음 열의 이름이*바뀌었습니다.* 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3.x*열*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 5 (설명)를 제외한 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 대 한 액세스 권한을 얻어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|스키마 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|테이블 이름입니다.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|테이블 형식 이름; 다음 중 하나: "테이블", "뷰", "시스템 테이블", "전역 임시", "로컬 임시", "별칭", "동의어" 또는 데이터 원본 관련 형식 이름입니다.<br /><br /> "별칭" 및 "동의어"의 의미는 드라이버 마다 다릅니다.|  
|설명 (ODBC 1.0)|5|Varchar|테이블에 대 한 설명입니다.|  
  
## <a name="example"></a>예제  
 다음 샘플 코드에서는 핸들 및 연결을 해제 하지 않습니다. 코드 샘플에서 핸들 및 문을 해제 하려면 [Sqlfreehandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md) 및 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md) 를 참조 하세요.  
  
```cpp  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|하나 이상의 열에 대 한 권한 반환|[SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|테이블이 나 테이블의 열 반환|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|테이블 또는 테이블에 대 한 권한 반환|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
