---
title: SQLProcedureColumns 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306854"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 함수(SQLProcedureColumns Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLProcedureColumns** 는 입력 및 출력 매개 변수 목록과 지정 된 프로시저에 대 한 결과 집합을 구성 하는 열을 반환 합니다. 드라이버는 지정 된 문의 결과 집합으로 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *CatalogName*  
 입력 프로시저 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 프로시저에 대 한 카탈로그를 지원 하지만 다른 Dbms에서 데이터를 검색 하는 경우와 같이 빈 문자열 ("")은 카탈로그가 없는 프로시저를 나타냅니다. *CatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 프로시저 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 프로시저에 대 한 스키마를 지원 하지만 다른 Dbms에서 데이터를 검색 하는 경우 처럼 빈 문자열 ("")은 스키마가 없는 프로시저를 나타냅니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 되 고 대/소문자는 중요 하지 않습니다. SQL_FALSE 되는 경우 *SchemaName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *ProcName*  
 입력 프로시저 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *ProcName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *ProcName* 는 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **ProcName*의 문자 길이입니다.  
  
 *ColumnName*  
 입력 열 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *ColumnName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *ColumnName* 은 패턴 값 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength4*  
 입력 **ColumnName*의 문자 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLProcedureColumns** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLProcedureColumns** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고, **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLError** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName*, *ProcName*또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. SQLProcedureColumns 함수가 호출 될 때이 aynschronous 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 카탈로그, 스키마, 프로시저 또는 열 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|프로시저 카탈로그가 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 프로시저 스키마를 지정 했으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> 프로시저 스키마, 프로시저 이름 또는 열 이름에 문자열 검색 패턴을 지정 했으며 데이터 원본에서 이러한 인수 중 하나 이상에 대 한 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 프로시저 매개 변수와 프로시저에서 반환 하는 결과 집합을 구성 하는 열 (있는 경우)에 대 한 정보를 검색 하기 위해 문 실행 전에 일반적으로 사용 됩니다. 자세한 내용은 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)를 참조하세요.  
  
> [!NOTE]  
>  **SQLProcedureColumns** 는 프로시저에서 사용 하는 모든 열을 반환 하지 않을 수 있습니다. 예를 들어 드라이버는 프로시저에서 사용 되는 매개 변수에 대 한 정보만 반환 하 고 생성 되는 결과 집합의 열은 반환 하지 않을 수 있습니다.  
  
 *SchemaName*, *ProcName*및 *ColumnName* 인수는 검색 패턴을 허용 합니다. 유효한 검색 패턴에 대 한 자세한 내용은 [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)를 참조 하세요.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 **SQLProcedureColumns** 는 PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME 및 COLUMN_TYPE를 기준으로 정렬 된 표준 결과 집합으로 결과를 반환 합니다. 반환 값의 이름, 프로시저 호출에 있는 각 매개 변수의 이름 (호출 순서) 및 프로시저에서 반환 하는 결과 집합의 각 열 이름 (열 순서)에 따라 각 프로시저에 대해 열 이름이 반환 됩니다.  
  
 응용 프로그램은 결과 집합의 끝을 기준으로 드라이버 특정 열을 바인딩해야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME 및 COLUMN_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
 ODBC 3의 열 이름은 다음과 같습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|프로시저 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 다음 열이 ODBC 3 용 **SQLProcedureColumns** 에서 반환 된 결과 집합에 추가 되었습니다. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 19 (IS_NULLABLE) 외의 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 액세스할 수 있어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|프로시저 카탈로그 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버에서 일부 프로시저에 대 한 카탈로그를 지 원하는 경우에는 카탈로그가 없는 프로시저에 대해 빈 문자열 ("")을 반환 합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 이름; 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 프로시저의 스키마를 지원 하지 않는 경우 스키마가 없는 프로시저에 대해 빈 문자열 ("")을 반환 합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar not NULL|프로시저 이름입니다. 이름이 없는 프로시저의 경우 빈 문자열이 반환 됩니다.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar not NULL|프로시저 열 이름입니다. 드라이버는 이름이 없는 프로시저 열에 대해 빈 문자열을 반환 합니다.|  
|COLUMN_TYPE (ODBC 2.0)|5|NULL이 아닌 Smallint|프로시저 열을 매개 변수 또는 결과 집합 열로 정의 합니다.<br /><br /> SQL_PARAM_TYPE_UNKNOWN: 프로시저 열은 형식을 알 수 없는 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: 프로시저 열은 입력 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: 프로시저 열은 입/출력 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: 프로시저 열은 OUTPUT 매개 변수입니다. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: 프로시저 열은 프로시저의 반환 값입니다. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: 프로시저 열이 결과 집합 열입니다. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. Datetime 및 interval 데이터 형식의 경우이 열은 간결한 데이터 형식 (예: SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH)을 반환 합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 형식에서 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar not NULL|데이터 원본 종속 데이터 형식 이름입니다. 예를 들면 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 2.0)|8|정수|데이터 원본에 대 한 프로시저 열의 열 크기입니다. 열 크기를 적용할 수 없는 데이터 형식에 대해서는 NULL이 반환 됩니다. 전체 자릿수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|BUFFER_LENGTH (ODBC 2.0)|9|정수|SQL_C_DEFAULT 지정 된 경우 **SQLGetData** 또는 **sqlfetch** 작업에서 전송 된 데이터의 길이 (바이트)입니다. 숫자 데이터의 경우이 크기는 데이터 원본에 저장 된 데이터의 크기와 다를 수 있습니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)(부록 D: 데이터 형식)를 참조 하세요.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|데이터 원본에 대 한 프로시저 열의 소수 자릿수입니다. 10 진수가 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다. 10 진수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)(부록 D: 데이터 형식)를 참조 하세요.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|숫자 데이터 형식의 경우 10 또는 2입니다.<br /><br /> 10 인 경우 COLUMN_SIZE 및 DECIMAL_DIGITS의 값은 열에 허용 되는 소수 자릿수를 제공 합니다. 예를 들어 10 진수 (12, 5) 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 12 및 DECIMAL_DIGITS 5로 반환 됩니다. FLOAT 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 15 및 NULL DECIMAL_DIGITS를 반환할 수 있습니다.<br /><br /> 2 인 경우 COLUMN_SIZE 및 DECIMAL_DIGITS의 값이 열에서 허용 되는 비트 수를 제공 합니다. 예를 들어 FLOAT 열은 NUM_PREC_RADIX 2, 53 COLUMN_SIZE, NULL DECIMAL_DIGITS를 반환할 수 있습니다.<br /><br /> NUM_PREC_RADIX이 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다.|  
|NULLABLE (ODBC 2.0)|12|NULL이 아닌 Smallint|프로시저 열이 NULL 값을 허용 하는지 여부를 나타냅니다.<br /><br /> SQL_NO_NULLS: 프로시저 열에는 NULL 값이 허용 되지 않습니다.<br /><br /> SQL_NULLABLE: 프로시저 열은 NULL 값을 허용 합니다.<br /><br /> SQL_NULLABLE_UNKNOWN: 프로시저 열에 NULL 값이 허용 되는 경우에는 알 수 없습니다.|  
|설명 (ODBC 2.0)|13|Varchar|프로시저 열에 대 한 설명입니다.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|열의 기본값입니다.<br /><br /> NULL이 기본값으로 지정 된 경우이 열은 따옴표로 묶지 않고 NULL입니다. 기본값을 잘림 없이 표현할 수 없는 경우이 열에는 바깥쪽 작은따옴표 없이 잘린 기호가 포함 됩니다. 기본값이 지정 되지 않은 경우이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값은 잘린 값이 포함 된 경우를 제외 하 고 새 열 정의를 생성 하는 데 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|NULL이 아닌 Smallint|설명자의 SQL_DESC_TYPE 필드에 표시 되는 SQL 데이터 형식의 값입니다. 이 열은 datetime 및 interval 데이터 형식을 제외 하 고는 DATA_TYPE 열과 동일 합니다.<br /><br /> Datetime 및 interval 데이터 형식의 경우 결과 집합의 SQL_DATA_TYPE 필드는 SQL_INTERVAL 또는 SQL_DATETIME를 반환 하 고 SQL_DATETIME_SUB 필드는 특정 interval 또는 datetime 데이터 형식의 하위 코드를 반환 합니다. [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Datetime 및 interval 데이터 형식에 대 한 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|정수|문자 또는 이진 데이터 형식 열의 최대 길이 (바이트)입니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|18|NULL이 아닌 Integer|입력 및 출력 매개 변수의 경우 프로시저 정의에서 매개 변수의 서 수 위치 (1부터 시작 하는 매개 변수 순서를 늘립니다.) 반환 값 (있는 경우)의 경우 0이 반환 됩니다. 결과 집합 열의 경우 결과 집합의 첫 번째 열이 number 1 인 결과 집합에서 열의 서 수 위치입니다. 결과 집합이 여러 개 있는 경우에는 드라이버 관련 방식으로 열 서 수 위치가 반환 됩니다.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|열에 Null이 포함 되어 있지 않으면 "NO"입니다.<br /><br /> 열에 Null이 포함 될 수 있는 경우 "YES"입니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 반환되는 값은 NULLABLE 열에 반환되는 값과 다릅니다. NULL을 허용 하는 열에 대 한 설명을 참조 하세요.|  
  
## <a name="code-example"></a>코드 예  
 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터 원본에서 프로시저 목록 반환|[SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
