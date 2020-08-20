---
description: SQLSpecialColumns 함수
title: SQLSpecialColumns 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca29bf8bbef30296ad1aef17bda6890b23da8fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476069"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 그룹 열기  
  
 **요약**  
 **SQLSpecialColumns** 는 지정 된 테이블 내의 열에 대 한 다음 정보를 검색 합니다.  
  
-   테이블에서 행을 고유 하 게 식별 하는 최적의 열 집합입니다.  
  
-   트랜잭션에 의해 행의 값이 업데이트 될 때 자동으로 업데이트 되는 열입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *IdentifierType*  
 입력 반환할 열의 유형입니다. 다음 값 중 하나여야 합니다.  
  
 SQL_BEST_ROWID: 열에서 값을 검색 하 여 지정 된 테이블의 모든 행을 고유 하 게 식별할 수 있는 최적의 열 또는 열 집합을 반환 합니다. 열은이 목적을 위해 특별히 디자인 된 의사 열 (Oracle ROWID 또는 Ingres TID) 또는 테이블에 대 한 고유 인덱스의 열이 될 수 있습니다.  
  
 SQL_ROWVER: 지정 된 테이블의 열 (있는 경우)을 반환 합니다 .이 열은 모든 트랜잭션에 의해 행의 값이 업데이트 될 때 (SQLBase ROWID 또는 Sybase 타임 스탬프 처럼) 데이터 원본에 의해 자동으로 업데이트 됩니다.  
  
 *CatalogName*  
 입력 테이블의 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지 원하는 경우 빈 문자열 ("")은 카탈로그가 없는 테이블을 나타냅니다. *CatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 테이블에 대 한 스키마 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")은 스키마가 없는 테이블을 나타냅니다. *SchemaName* 에는 문자열 검색 패턴을 사용할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 되 고 대/소문자는 중요 하지 않습니다. SQL_FALSE 되는 경우 *SchemaName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *TableName*  
 입력 테이블 이름입니다. 이 인수는 null 포인터 일 수 없습니다. *TableName* 은 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *TableName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *TableName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **TableName*의 문자 길이입니다.  
  
 *범위*  
 입력 Rowid에 필요한 최소 범위입니다. 반환 된 rowid의 범위는 클 수 있습니다. 다음 중 하나여야 합니다.  
  
 SQL_SCOPE_CURROW: rowid는 해당 행에 배치 되는 동안에만 유효 합니다. 행이 다른 트랜잭션에 의해 업데이트 되거나 삭제 된 경우에는 나중에 rowid를 사용 하 여 다시 선택할 때 행이 반환 되지 않을 수 있습니다.  
  
 SQL_SCOPE_TRANSACTION: rowid는 현재 트랜잭션이 지속 되는 동안 유효 하도록 보장 됩니다.  
  
 SQL_SCOPE_SESSION: rowid는 트랜잭션 경계를 넘어 세션 기간 동안 유효 하도록 보장 됩니다.  
  
 *Null 허용*  
 입력 NULL 값을 가질 수 있는 특수 열을 반환할지 여부를 결정 합니다. 다음 중 하나여야 합니다.  
  
 SQL_NO_NULLS: NULL 값을 가질 수 있는 특수 열을 제외 합니다. 일부 드라이버는 SQL_NO_NULLS을 지원할 수 없으며, SQL_NO_NULLS 지정 된 경우 이러한 드라이버는 빈 결과 집합을 반환 합니다. 이 경우 응용 프로그램을 준비 하 고 반드시 필요한 경우에만 SQL_NO_NULLS 요청 해야 합니다.  
  
 SQL_NULLABLE: NULL 값을 가질 수 있는 경우에도 특수 열을 반환 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSpecialColumns** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSpecialColumns** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch 또는** **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고 **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|*TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName* 인수가 null 포인터 였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLSpecialColumns** 가 호출 될 때이 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> 길이 인수 중 하나의 값이 해당 이름에 대 한 최대 길이 값을 초과 했습니다. *InfoType* 값으로 **SQLGetInfo** 를 호출 하 여 각 이름의 최대 길이를 가져올 수 있습니다: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN 또는 SQL_MAX_TABLE_NAME_LEN.|  
|HY097|열 유형이 범위를 벗어났습니다.|(DM) 잘못 된 *IdentifierType* 값이 지정 되었습니다.|  
|HY098|범위 유형이 범위를 벗어났습니다.|(DM) 잘못 된 *범위* 값이 지정 되었습니다.|  
|HY099|Nullable 형식이 범위를 벗어났습니다.|(DM) 잘못 된 *Null 허용* 값이 지정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그가 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마가 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 *IdentifierType* 인수가 SQL_BEST_ROWID 경우 **SQLSpecialColumns** 은 테이블의 각 행을 고유 하 게 식별 하는 열을 반환 합니다. 이러한 열은 항상 *선택 목록* 또는 **WHERE** 절에서 사용할 수 있습니다. 테이블의 열에 대해 다양 한 정보를 반환 하는 데 사용 되는 **Sqlcolumns**는 각 행을 고유 하 게 식별 하는 열을 반환 하거나 트랜잭션에 의해 행의 값이 업데이트 될 때 자동으로 업데이트 되는 열을 반환 하지 않을 수 있습니다. 예를 들어 **Sqlcolumns** 는 Oracle 의사 열 ROWID를 반환 하지 않을 수 있습니다. 이러한 열을 반환 하는 데 **SQLSpecialColumns** 를 사용 하는 이유입니다. 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 테이블의 각 행을 고유 하 게 식별 하는 열이 없는 경우 **SQLSpecialColumns** 는 행이 없는 행 집합을 반환 합니다. 문에서 **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 후속 호출이 SQL_NO_DATA을 반환 합니다.  
  
 *IdentifierType*, *Scope*또는 *Nullable* 인수가 데이터 원본에서 지원 되지 않는 특성을 지정 하는 경우 **SQLSpecialColumns** 는 빈 결과 집합을 반환 합니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName*, *SchemaName*및 *TableName* 인수는 식별자로 처리 되므로 특정 상황에서 null 포인터로 설정할 수 없습니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 **SQLSpecialColumns** 는 결과를 범위에 따라 정렬 된 표준 결과 집합으로 반환 합니다.  
  
 ODBC 3.x에 대해 다음 열의 이름이 바뀌었습니다 *.* 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC *3.x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 COLUMN_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 8 (PSEUDO_COLUMN)을 초과 하는 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 액세스할 수 있어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|범위 (ODBC 1.0)|1|Smallint|Rowid의 실제 범위입니다. 다음 값 중 하나를 포함 합니다.<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> *IdentifierType* 가 SQL_ROWVER 되 면 NULL이 반환 됩니다. 각 값에 대 한 설명은이 섹션의 앞부분에 나오는 "구문"의 *범위* 설명을 참조 하십시오.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar not NULL|열 이름입니다. 드라이버는 이름이 없는 열에 대해 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|3|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. 유효한 ODBC SQL 데이터 형식 목록은 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar not NULL|데이터 원본 종속 데이터 형식 이름입니다. 예를 들면 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 1.0)|5|정수|데이터 원본의 열 크기입니다. 열 크기와 관련 된 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하십시오.|  
|BUFFER_LENGTH (ODBC 1.0)|6|정수|SQL_C_DEFAULT 지정 된 경우 **SQLGetData** 또는 **sqlfetch** 작업에서 전송 된 데이터의 길이 (바이트)입니다. 숫자 데이터의 경우이 크기는 데이터 원본에 저장 된 데이터의 크기와 다를 수 있습니다. 이 값은 문자 또는 이진 데이터에 대 한 COLUMN_SIZE 열과 동일 합니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하세요.|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|데이터 원본에 있는 열의 소수 자릿수입니다. 10 진수가 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다. 10 진수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하세요.|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|열이 Oracle ROWID와 같은 의사 (pseudo) 열 인지 여부를 나타냅니다.<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **참고:**  최대 상호 운용성을 위해, 의사 (PSEUDO) 열은 **SQLGetInfo**에서 반환 된 식별자 따옴표 문자로 따옴표로 묶지 않아야 합니다.|  
  
 응용 프로그램에서 SQL_BEST_ROWID 값을 검색 한 후에는이 값을 사용 하 여 정의 된 범위 내에서 해당 행을 다시 선택할 수 있습니다. **SELECT** 문은 행을 반환 하지 않거나 행 하나를 반환 하도록 보장 됩니다.  
  
 응용 프로그램에서 rowid 열을 기준으로 행을 다시 선택 하 고 행을 찾을 수 없는 경우 응용 프로그램은 행이 삭제 되었거나 rowid 열이 수정 된 것으로 간주할 수 있습니다. 반대는 그렇지 않습니다. rowid가 변경 되지 않은 경우에도 행의 다른 열이 변경 될 수 있습니다.  
  
 열 형식 SQL_BEST_ROWID에 대해 반환 되는 열은 행 집합에서 최신 데이터를 검색 하기 위해 결과 집합 내에서 앞뒤로 스크롤해야 하는 응용 프로그램에 유용 합니다. Rowid의 열 하나는 해당 행에 배치 되는 동안 변경 되지 않습니다.  
  
 행에 커서가 배치 되지 않은 경우에도 rowid의 열이 유효 하 게 유지 될 수 있습니다. 응용 프로그램은 결과 집합의 범위 열을 확인 하 여이를 확인할 수 있습니다.  
  
 SQL_ROWVER 열 형식에 대해 반환 되는 열은 행이 rowid를 사용 하 여 ac 하는 동안 지정 된 행의 열이 업데이트 되었는지 여부를 확인 하는 기능이 필요한 응용 프로그램에 유용 합니다. 예를 들어 rowid를 사용 하 여 행을 다시 선택할 때 응용 프로그램은 SQL_ROWVER 열에 있는 이전 값을 가져온 값과 비교할 수 있습니다. SQL_ROWVER 열의 값이 이전 값과 다를 경우 응용 프로그램은 디스플레이의 데이터가 변경 되었음을 사용자에 게 경고할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제는 [Sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블이 나 테이블의 열 반환|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키 열 반환|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
