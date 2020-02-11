---
title: SQLColumns 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8de1a2053913ee0339c58a4a27ccd45772487e77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118671"
---
# <a name="sqlcolumns-function"></a>SQLColumns 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 그룹 열기  
  
 **요약**  
 **Sqlcolumns** 지정 된 테이블의 열 이름 목록을 반환 합니다. 드라이버는 지정 된 *StatementHandle*에 대 한 결과 집합으로이 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *CatalogName*  
 입력 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서는 카탈로그를 지원 하지 않는 경우 빈 문자열 ("")에는 카탈로그가 없는 테이블이 표시 됩니다. *CatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")에는 스키마가 없는 테이블이 표시 됩니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 되 고 대/소문자는 중요 하지 않습니다. SQL_FALSE 되는 경우 *SchemaName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *TableName*  
 입력 테이블 이름에 대 한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *TableName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *TableName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **TableName*의 문자 길이입니다.  
  
 *ColumnName*  
 입력 열 이름에 대 한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *ColumnName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *ColumnName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength4*  
 입력 **ColumnName*의 문자 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcolumns** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqlcolumns** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고, **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle* 에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName*, *TableName*또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **Sqlcolumns** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 카탈로그 또는 이름에 대 한 최대 길이 값을 초과 했습니다. *InfoType* 값으로 **SQLGetInfo** 를 호출 하 여 각 카탈로그 또는 이름의 최대 길이를 가져올 수 있습니다. "설명"을 참조 하십시오.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그 이름이 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름이 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> 스키마 이름, 테이블 이름 또는 열 이름에 대해 문자열 검색 패턴을 지정 했으며 데이터 원본이 이러한 인수 중 하나 이상에 대 한 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 일반적으로 문을 실행 하기 전에 데이터 원본의 카탈로그에서 테이블의 열에 대 한 정보를 검색 하는 데 사용 됩니다. **Sqlcolumns** 는 **sqlcolumns**에서 반환 하는 모든 유형의 항목에 대 한 데이터를 검색 하는 데 사용할 수 있습니다. 기본 테이블 외에도 뷰, 동의어, 시스템 테이블 등이 포함 될 수 있습니다. 반대로 **Sqlcolattribute** 및 **SQLDescribeCol** 함수는 결과 집합의 열을 설명 하 고 **sqlnumresultcols** 함수는 결과 집합의 열 수를 반환 합니다. 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 **Sqlcolumns** TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 ORDINAL_POSITION를 기준으로 정렬 된 표준 결과 집합으로 결과를 반환 합니다.  
  
> [!NOTE]  
>  응용 프로그램이 ODBC 2를 사용 하 여 작동 하는 경우 *x* 드라이버는 결과 집합에 ORDINAL_POSITION 열이 반환 되지 않습니다. 따라서 ODBC 2로 작업 하는 경우 *x* 드라이버, **sqlcolumns** 에서 반환 된 열 목록의 열 순서는 응용 프로그램에서 해당 테이블의 모든 열에 대해 SELECT 문을 수행할 때 반환 되는 열의 순서와 동일할 필요는 없습니다.  
  
> [!NOTE]  
>  **Sqlcolumns** 는 모든 열을 반환 하지 않을 수 있습니다. 예를 들어 드라이버는 Oracle ROWID와 같은 의사 (pseudo) 열에 대 한 정보를 반환 하지 않을 수 있습니다. 응용 프로그램은 **Sqlcolumns**에서 반환 되는 모든 유효한 열을 사용할 수 있습니다.  
>   
>  **SQLStatistics** 에 의해 반환 될 수 있는 일부 열은 **sqlcolumns**에서 반환 되지 않습니다. 예를 들어 **Sqlcolumns** 는 급여 + 혜택 또는 DEPT = 0012와 같이 식이나 필터에 대해 만들어진 인덱스의 열을 반환 하지 않습니다.  
  
 VARCHAR 열의 길이는 테이블에 표시 되지 않습니다. 실제 길이는 데이터 원본에 따라 달라 집니다. TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
 ODBC 3의 열 이름은 다음과 같습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 다음 열이 ODBC 3 용 **Sqlcolumns** 에서 반환 된 결과 집합에 추가 되었습니다. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 18 (IS_NULLABLE)을 초과 하는 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 대 한 액세스 권한을 얻어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열<br /><br /> number|데이터 형식|주석|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|스키마 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|테이블 이름입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|열 이름. 드라이버는 이름이 없는 열에 대해 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|5|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. Datetime 및 interval 데이터 형식의 경우이 열은 SQL_DATETIME 또는 SQL_INTERVAL와 같이 간결 하지 않은 데이터 형식 대신 SQL_TYPE_DATE 또는 SQL_INTERVAL_YEAR_TO_MONTH 같은 간결한 데이터 형식을 반환 합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 형식에서 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.<br /><br /> ODBC 3에 대해 반환 되는 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램은 다를 수 있습니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.|  
|TYPE_NAME (ODBC 1.0)|6|Varchar not NULL|데이터 원본 종속 데이터 형식 이름입니다. 예를 들면 "CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 1.0)|7|정수|DATA_TYPE SQL_CHAR 또는 SQL_VARCHAR 경우이 열에는 열의 최대 길이가 포함 됩니다. Datetime 데이터 형식의 경우 값이 문자로 변환 될 때 값을 표시 하는 데 필요한 총 문자 수입니다. 숫자 데이터 형식의 경우 NUM_PREC_RADIX 열에 따라 전체 자릿수 또는 열에 허용 되는 총 비트 수 중 하나입니다. 간격 데이터 형식의 경우 간격 리터럴의 문자 표현에 있는 문자 수입니다 (간격 선행 전체 자릿수에 정의 됨). 자세한 내용은 부록 D: 데이터 형식의 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md) 를 참조 하세요. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|BUFFER_LENGTH (ODBC 1.0)|8|정수|SQL_C_DEFAULT 지정 된 경우 SQLGetData, SQLFetch 또는 SQLFetchScroll 작업에서 전송 된 데이터의 길이 (바이트)입니다. 숫자 데이터의 경우이 크기는 데이터 원본에 저장 된 데이터의 크기와 다를 수 있습니다. 이 값은 문자 데이터의 COLUMN_SIZE 열과 다를 수 있습니다. 길이에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|소수점 오른쪽에 있는 유효 자릿수의 총 수입니다. SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP의 경우이 열에는 소수 자릿수 초 구성 요소의 자릿수가 포함 됩니다. 다른 데이터 형식의 경우이 숫자는 데이터 원본에 있는 열의 10 진수입니다. 시간 구성 요소를 포함 하는 간격 데이터 형식의 경우이 열에는 소수점이 하 자릿수 (소수 자릿수 초)가 포함 됩니다. 시간 구성 요소가 포함 되지 않은 간격 데이터 형식의 경우이 열은 0입니다. 10 진수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요. DECIMAL_DIGITS이 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|숫자 데이터 형식의 경우 10 또는 2입니다. 10 인 경우 COLUMN_SIZE 및 DECIMAL_DIGITS 값은 열에 허용 되는 소수 자릿수를 제공 합니다. 예를 들어 10 진수 (12, 5) 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 12 및 DECIMAL_DIGITS 5로 반환 됩니다. FLOAT 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 15 및 NULL DECIMAL_DIGITS를 반환할 수 있습니다.<br /><br /> 2 인 경우 COLUMN_SIZE 및 DECIMAL_DIGITS의 값이 열에서 허용 되는 비트 수를 제공 합니다. 예를 들어 FLOAT 열은 2의 기 수, 53의 COLUMN_SIZE 및 NULL DECIMAL_DIGITS를 반환할 수 있습니다.<br /><br /> NUM_PREC_RADIX이 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다.|  
|NULLABLE (ODBC 1.0)|11|NULL이 아닌 Smallint|열에 NULL 값을 포함할 수 없는 경우 SQL_NO_NULLS 합니다.<br /><br /> 열이 NULL 값을 허용 하는지 여부를 SQL_NULLABLE 합니다.<br /><br /> 열이 NULL 값을 허용 하는지 여부를 알 수 없는 경우에 SQL_NULLABLE_UNKNOWN 합니다.<br /><br /> 이 열에 대해 반환 되는 값은 IS_NULLABLE 열에 대해 반환 되는 값과 다릅니다. NULLABLE 열은 열이 Null을 허용 하지만 열이 Null을 허용 하지 않는다는 확신을 나타낼 수 없다는 확신을 나타냅니다. IS_NULLABLE 열은 열이 Null을 허용 하지 않음을 확신 하는 것으로 표시 되지만 열이 Null을 허용 한다는 확신을 나타낼 수 없습니다.|  
|설명 (ODBC 1.0)|12|Varchar|열에 대 한 설명입니다.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|열의 기본값입니다. 이 열의 값은 따옴표로 묶여 있는 경우 문자열로 해석 되어야 합니다.<br /><br /> NULL이 기본값으로 지정 된 경우이 열은 따옴표로 묶지 않고 NULL입니다. 기본값을 잘림 없이 표현할 수 없는 경우이 열에는 작은 따옴표를 포함 하지 않고 잘린 부분이 포함 됩니다. 기본값이 지정 되지 않은 경우이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값은 잘린 값이 포함 된 경우를 제외 하 고 새 열 정의를 생성 하는 데 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|NULL이 아닌 Smallint|IRD의 SQL_DESC_TYPE 레코드 필드에 표시 되는 SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. 이 열은 datetime 및 interval 데이터 형식을 제외 하 고는 DATA_TYPE 열과 동일 합니다. 이 열은 DATETIME 및 INTERVAL 데이터 형식에 대 한 간결한 데이터 형식 (예: SQL_TYPE_DATE 또는 SQL_INTERVAL_YEAR_TO_MONTH) 대신 간결한 데이터 형식 (예: SQL_DATETIME 또는 SQL_INTERVAL)을 반환 합니다. 이 열이 SQL_DATETIME 또는 SQL_INTERVAL를 반환 하는 경우에는 SQL_DATETIME_SUB 열에서 특정 데이터 형식을 확인할 수 있습니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 형식에서 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.<br /><br /> ODBC 3에 대해 반환 되는 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램은 다를 수 있습니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|Datetime 및 interval 데이터 형식에 대 한 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다. Datetime 및 interval 하위 항목에 대 한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "SQL_DESC_DATETIME_INTERVAL_CODE"을 참조 하십시오.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|정수|문자 또는 이진 데이터 형식 열의 최대 길이 (바이트)입니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|17|NULL이 아닌 Integer|테이블에 있는 열의 서수 위치입니다. 테이블의 첫 번째 열 번호는 1입니다.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|열에 Null이 포함 되어 있지 않으면 "NO"입니다.<br /><br /> 열에 Null이 포함 될 수 있는 경우 "YES"입니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 대해 반환 되는 값은 NULLABLE 열에 대해 반환 되는 값과 다릅니다. NULL을 허용 하는 열에 대 한 설명을 참조 하세요.|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 **Sqlcolumns**에서 반환 된 결과 집합에 대 한 버퍼를 선언 합니다. **Sqlcolumns** 를 호출 하 여 EMPLOYEE 테이블의 각 열을 설명 하는 결과 집합을 반환 합니다. 그런 다음 **SQLBindCol** 를 호출 하 여 결과 집합의 열을 버퍼에 바인딩합니다. 마지막으로 응용 프로그램은 **Sqlfetch** 를 사용 하 여 데이터의 각 행을 인출 하 고 처리 합니다.  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|하나 이상의 열에 대 한 권한 반환|[SQLColumnPrivileges 함수(SQLColumnPrivileges Function)](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수(SQLFetchScroll Function)](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|행을 고유 하 게 식별 하는 열 또는 트랜잭션에 의해 자동으로 업데이트 되는 열 반환|[SQLSpecialColumns 함수](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|데이터 원본에 있는 테이블 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
|테이블 또는 테이블에 대 한 권한 반환|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
