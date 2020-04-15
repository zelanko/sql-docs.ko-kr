---
title: SQLGetInfo 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303345"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetInfo는** 연결과 연결된 드라이버 및 데이터 원본에 대한 일반 정보를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *정보 입력*  
 [입력] 정보의 유형입니다.  
  
 *인포밸류Ptr*  
 [출력] 정보를 반환할 버퍼에 대한 포인터입니다. 요청된 *InfoType에* 따라 반환되는 정보는 null 종료 된 문자 문자열, SQLUSMALLINT 값, SQLUINTEGER 비트 마스크, SQLUINTEGER 플래그, SQLUINTEGER 이진 값 또는 SQLULEN 값 중 하나가 됩니다.  
  
 *InfoType* 인수가 SQL_DRIVER_HDESC 또는 SQL_DRIVER_HSTMT 경우 *InfoValuePtr* 인수는 입력 및 출력입니다. 자세한 내용은 이 함수 설명의 SQL_DRIVER_HDESC 또는 SQL_DRIVER_HSTMT 설명자 참조)를 참조하십시오.  
  
 *InfoValuePtr이* NULL인 경우 *StringLengthPtr은* *InfoValuePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] \* *InfoValuePtr* 버퍼의 길이입니다. InfoValuePtr의 값이 문자 문자열이 아니거나 *InfoValuePtr이* null 포인터인 경우 *BufferLength* 인수는 무시됩니다. * \** 드라이버는 * \*InfoValuePtr의* 크기가 *INFOType에*따라 SQLUSMALLINT 또는 SQLUINTEGER라고 가정합니다. * \*InfoValuePtr이* 유니코드 문자열인 **경우(SQLGetInfoW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다. 그렇지 않으면 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)이 반환됩니다.  
  
 *문자열길이Ptr*  
 [출력] **InfoValuePtr에서*반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환하는 버퍼에 대한 포인터입니다.  
  
 문자 데이터의 경우 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 같으면 \* *InfoValuePtr의* 정보는 *BufferLength* 바이트로 잘려null 종료 문자의 길이를 뺀 값으로 드라이버에 의해 null-종료됩니다.  
  
 다른 모든 데이터 유형의 경우 *BufferLength* 의 값은 무시되고 \*드라이버는 *InfoValuePtr의* 크기가 *InfoType*에 따라 SQLUSMALLINT 또는 SQLUINTEGER라고 가정합니다.  
  
## <a name="return-value"></a>Return Value  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetInfo** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 *경우,* 연결된 SQLSTATE 값은 SQL_HANDLE_DBC 핸들 유형 및 *연결 핸들*의 *핸들을* 사용하는 **SQLGetDiagRec를** 호출하여 가져올 수 있습니다. 다음 표에서는 **SQLGetInfo에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *InfoValuePtr* 요청된 모든 정보를 반환 할 만큼 크지 않았습니다. 따라서 정보가 잘렸습니다. 해당 잘링되지 않은 양식에서 요청된 정보의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|(DM) *InfoType에서* 요청된 정보 유형은 열린 연결이 필요합니다. ODBC에서 예약한 정보 유형 중 열린 연결 없이 SQL_ODBC_VER 반환할 수 있습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못된 특성 값|(DM) *InfoType* 인수가 SQL_DRIVER_HSTMT *InfoValuePtr이* 가리키는 값이 유효한 문 핸들이 아닙니다.<br /><br /> (DM) *InfoType* 인수가 SQL_DRIVER_HDESC 및 *InfoValuePtr에서* 가리키는 값이 유효한 설명자 핸들이 아닙니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 인수 *BufferLength에* 대해 지정된 값이 0보다 적습니다.<br /><br /> (DM) *BufferLength에* 대해 지정된 값은 홀수이고 * \*InfoValuePtr은* 유니코드 데이터 형식이었습니다.|  
|HY096|범위를 벗어난 정보 유형|인인수 *InfoType에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|선택적 필드가 구현되지 않음|인수 *InfoType에* 대해 지정된 값은 드라이버에서 지원하지 않는 드라이버 별 값입니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들에* 해당하는 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 현재 정의된 정보 유형은 이 섹션의 후반부 "정보 유형"에 표시됩니다. 다른 데이터 원본을 활용하기 위해 더 많은 것이 정의될 것으로 예상됩니다. 다양한 정보 유형은 ODBC에서 예약합니다. 드라이버 개발자는 Open Group에서 드라이버별 사용을 위해 값을 예약해야 합니다. **SQLGetInfo는** 드라이버 정의 *InfoType에*대해 유니코드 변환 또는 *번킹을* 수행하지 않습니다(ODBC *프로그래머 참조의 ODBC* [오류 코드 부록](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) 참조). 자세한 내용은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성을](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)참조하십시오. \* *InfoValuePtr에서* 반환되는 정보의 형식은 요청된 *InfoType에* 따라 다릅니다. **SQLGetInfo는** 다섯 가지 형식 중 하나로 정보를 반환합니다.  
  
-   null 종료된 문자 문자열  
  
-   SQLUSMALLINT 값  
  
-   SQLUINTEGER 비트 마스크  
  
-   SQLUINTEGER 값  
  
-   SQLUINTEGER 바이너리 값  
  
 다음 각 정보 형식의 형식은 형식 설명에 기록됩니다. 응용 프로그램은 **InfoValuePtr에서* 반환된 값을 적절히 캐스팅해야 합니다. 응용 프로그램이 SQLUINTEGER 비트 마스크에서 데이터를 검색하는 방법의 예는 "코드 예제"를 참조하십시오.  
  
 드라이버는 다음 테이블에 정의된 각 정보 형식에 대한 값을 반환해야 합니다. 정보 형식이 드라이버 또는 데이터 원본에 적용되지 않으면 드라이버는 다음 표에 나열된 값 중 하나를 반환합니다.  
  
 문자 문자열("Y" 또는 "N")  
 "N"  
  
 문자열("Y" 또는 "N"이 아님)  
 빈 문자열  
  
 SQLUSmallINT  
 0  
  
 SQLUINTEGER 비트 마스크 또는 SQLUINTEGER 바이너리 값  
 0L  
  
 예를 들어 데이터 원본이 프로시저를 지원하지 않는 경우 **SQLGetInfo는** 프로시저와 관련된 *InfoType* 값에 대해 다음 표에 나열된 값을 반환합니다.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 빈 문자열  
  
 **SQLGetInfo는** ODBC에서 사용하기 위해 예약된 정보 형식 의 범위에 있지만 드라이버에서 지원하는 ODBC 버전에 의해 정의되지 않은 *InfoType* 값에 대해 SQLSTATE HY096(잘못된 인수 값)을 반환합니다. 드라이버가 준수하는 ODBC 버전을 확인하려면 응용 프로그램에서 SQL_DRIVER_ODBC_VER 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. **SQLGetInfo는** 드라이버 별 사용을 위해 예약된 정보 형식의 범위에 있지만 드라이버에서 지원되지 않는 *InfoType* 값에 대해 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환합니다.  
  
 **SQLGetInfo에** 대한 모든 호출은 드라이버 관리자의 버전을 반환하는 *InfoType이* SQL_ODBC_VER 경우를 제외하고 열린 연결이 필요합니다.  
  
## <a name="information-types"></a>정보 유형  
 이 섹션에는 **SQLGetInfo**에서 지원하는 정보 형식이 나열되어 있습니다. 정보 유형은 범주별로 그룹화되고 사전순으로 나열됩니다. ODBC 3 *.x에* 대해 추가되거나 이름이 변경된 정보 유형도 나열됩니다.  
  
## <a name="driver-information"></a>운전자 정보  
 *InfoType* 인수의 다음 값은 활성 문 수, 데이터 원본 이름 및 인터페이스 표준 준수 수준과 같은 ODBC 드라이버에 대한 정보를 반환합니다.  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  **SQLGetInfo를**구현할 때 드라이버는 서버에서 정보를 보내거나 요청하는 횟수를 최소화하여 성능을 향상시킬 수 있습니다.  
  
## <a name="dbms-product-information"></a>DBMS 제품 정보  
 *InfoType* 인수의 다음 값은 DBMS 이름 및 버전과 같은 DBMS 제품에 대한 정보를 반환합니다.  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>데이터 소스 정보  
 *InfoType* 인수의 다음 값은 커서 특성 및 트랜잭션 기능과 같은 데이터 원본에 대한 정보를 반환합니다.  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>지원되는 SQL  
 *InfoType* 인수의 다음 값은 데이터 원본에서 지원하는 SQL 문에 대한 정보를 반환합니다. 이러한 정보 형식에 설명된 각 기능의 SQL 구문은 SQL-92 구문입니다. 이러한 정보 형식은 전체 SQL-92 문법을 완전히 설명하지 않습니다. 대신 데이터 원본이 일반적으로 서로 다른 수준의 지원을 제공하는 문법의 해당 부분을 설명합니다. 특히 SQL-92의 대부분의 DDL 문은 다룹니다.  
  
 응용 프로그램은 SQL_SQL_CONFORMANCE 정보 유형에서 지원되는 문법의 일반적인 수준을 결정하고 다른 정보 형식을 사용하여 명시된 표준 준수 수준에서의 변형을 결정해야 합니다.  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>SQL 제한  
 *InfoType* 인수의 다음 값은 식별자의 최대 길이 및 선택 목록의 최대 열 수와 같은 SQL 문의 식별자 및 절에 적용되는 제한에 대한 정보를 반환합니다. 드라이버 또는 데이터 원본에 의해 제한 사항이 부과될 수 있습니다.  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>스칼라 기능 정보  
 *InfoType* 인수의 다음 값은 데이터 원본및 드라이버에서 지원하는 스칼라 함수에 대한 정보를 반환합니다. 스칼라 함수에 대한 자세한 내용은 [부록 E: 스칼라 함수를](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)참조하십시오.  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>변환 정보  
 *InfoType* 인수의 다음 값은 데이터 원본이 **CONVERT** 스칼라 함수를 사용하여 지정된 SQL 데이터 형식을 변환할 수 있는 SQL 데이터 형식 의 목록을 반환합니다.  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>ODBC 3.x에 대해 추가된 정보 유형  
 ODBC 3 *.x에*대해 *InfoType* 인수의 다음 값이 추가되었습니다.  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>ODBC 3.x의 이름이 변경된 정보 유형  
 *INFOType* 인수의 다음 값은 ODBC 3 *.x .*  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>ODBC 3.x에서 더 이상 사용되지 않습니다.  
 *InfoType* 인수의 다음 값은 ODBC 3 *.x .* ODBC*3.x* 드라이버는 ODBC 2 *.x* 응용 프로그램과 이전 버전과의 호환성을 위해 이러한 정보 유형을 계속 지원해야 합니다. 이러한 형식에 대한 자세한 내용은 부록 G: 이전 버전과의 호환성에 대한 드라이버 지침의 [SQLGetInfo 지원을](../../../odbc/reference/appendixes/sqlgetinfo-support.md) 참조하십시오.  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>정보 유형 설명  
 다음 표에는 각 정보 유형, 정보 형식이 도입된 ODBC 버전 및 설명이 사전순으로 나열되어 있습니다.  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 문자열 문자열: 사용자가 **SQLProcedures에서**반환하는 모든 프로시저를 실행할 수 있는 경우 "Y"; 사용자가 실행할 수 없는 프로시저가 반환될 수 있는 경우 "N"입니다.  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 문자열 문자열: 사용자가 **SQLTables에서**반환하는 모든 테이블에 **SELECT** 권한을 보장하는 경우 "Y"; 사용자가 액세스할 수 없는 테이블이 반환될 수 있는 경우 "N"입니다.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 드라이버가 지원할 수 있는 최대 활성 환경 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 집계 함수에 대한 지원을 확대하는 SQLUINTEGER 비트 마스크:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **ALTER DOMAIN** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다. SQL-92 전체 수준을 준수하는 드라이버는 항상 모든 비트 마스크를 반환합니다. 반환 값 "0"은 **ALTER DOMAIN** 문이 지원되지 않음을 의미합니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 도메인 제약 조건 추가가 지원됩니다(전체 수준)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= 도메인 \<> 도메인 기본 절> 변경이 지원됩니다(전체 수준)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<= 제약 조건 이름 정의 절> 명명 도메인 제약 조건에 대 한 지원 됩니다 (중간 수준)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 드롭 도메인 제약 조건 절> 지원됩니다(전체 수준)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= 도메인 \<드롭 도메인 기본 절>> 변경이 지원됩니다(전체 수준)  
  
 다음 비트는 도메인 \<제약 조건 추가 \<> 지원되는 경우> 지원되는 제약 조건 특성을 지정합니다(SQL_AD_ADD_DOMAIN_CONSTRAINT 비트가 설정됨).  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (전체 수준)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (전체 수준)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (전체 수준)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 데이터 원본에서 지원하는 **ALTER TABLE** 문의 절을 등록하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 열> 절 추가가 지원되며 열 데이터 정렬(전체 수준)(ODBC 3.0)을 지정하는 기능이 있습니다.  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 열> 절 추가가 지원되며 열 기본값(FIPS 전환 수준)(ODBC 3.0)을 지정하는 기능이 있습니다.  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 열 추가> 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= 열 제약 조건(FIPS 전환 수준)을 지정하는 기능(ODBC 3.0)을 사용하여 열> 절 추가가 지원됩니다.  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 테이블 제약 조건 추가> 절이 지원됩니다(FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<= 제약 조건 이름 정의> 이름 지정 열 및 테이블 제약 조건(중간 수준)에 대해 지원됩니다(ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<= 드롭 컬럼> CAS가 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= \<드롭 열 기본 절>> 열 변경이 지원됩니다(중간 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<= 드롭 열> 제한이 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<= 드롭 열> 제한이 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= 열 \<변경> 설정 열 기본 절> 지원됩니다(중간 수준) (ODBC 3.0)  
  
 다음 비트는 열 \<또는 테이블 제약 조건을 지정하는 것이 지원되는 경우> 지원 제약 조건 특성을 지정합니다(SQL_AT_ADD_CONSTRAINT 비트가 설정됨).  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED(전체 수준) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (전체 수준) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 드라이버가 연결 핸들에서 비동기적으로 함수를 실행할 수 있는지 를 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_ASYNC_DBC_CAPABLE = 드라이버는 연결 기능을 비동기적으로 실행할 수 있습니다.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 드라이버는 비동기적으로 연결 기능을 실행할 수 없습니다.  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 드라이버의 비동기 지원 수준을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_AM_CONNECTION = 연결 수준 비동기 실행이 지원됩니다. 지정된 연결 핸들과 연결된 모든 문 핸들이 비동기 모드이거나 모두 동기 모드에 있습니다. 연결의 문 핸들은 비동기 모드일 수 없으며 동일한 연결의 다른 문 핸들은 동기 모드에 있고 그 반대의 경우도 마찬가지입니다.  
  
 SQL_AM_STATEMENT = 문 수준 비동기 실행이 지원됩니다. 연결 핸들과 연결된 일부 문 핸들은 비동기 모드일 수 있지만 동일한 연결의 다른 명령문 핸들은 동기 모드에 있을 수 있습니다.  
  
 SQL_AM_NONE = 비동기 모드가 지원되지 않습니다.  
  
 SQL_ASYNC_NOTIFICATION  
 드라이버가 비동기 알림을 지원하는지 나타내는 SQLUINTEGER 값은 다음과 같은 것입니다.  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** 비동기 실행 알림은 드라이버에서 지원됩니다.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** 비동기 실행 알림은 드라이버에서 지원되지 않습니다.  
  
 ODBC 비동기 연산에는 연결 수준 비동기 작업과 문 수준 비동기 작업의 두 가지 범주가 있습니다.  드라이버가 SQL_ASYNC_NOTIFICATION_CAPABLE 반환하는 경우 비동기적으로 실행할 수 있는 모든 API에 대한 알림을 지원해야 합니다.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 행 개수의 가용성과 관련하여 드라이버의 동작을 열거하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 정보 유형과 함께 사용됩니다.  
  
 SQL_BRC_ROLLED_UP = 연속INSERT, DELETE 또는 UPDATE 문에 대한 행 수는 하나로 롤업됩니다. 이 비트가 설정되지 않은 경우 각 문에 대해 행 수를 사용할 수 있습니다.  
  
 SQL_BRC_PROCEDURES = 일괄 처리가 저장 프로시저에서 실행될 때 행 수를 확인할 수 있습니다( 있는 경우). 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 롤업하거나 개별적으로 사용할 수 있습니다.  
  
 SQL_BRC_EXPLICIT = 행 카운트(있는 경우)는 **SQLExecute** 또는 **SQLExecDirect**를 호출하여 일괄 처리가 직접 실행될 때 사용할 수 있습니다. 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 롤업하거나 개별적으로 사용할 수 있습니다.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 일괄 처리에 대한 드라이버의 지원을 가리는 SQLUINTEGER 비트 마스크입니다. 다음 비트마스크는 지원되는 수준을 결정하는 데 사용됩니다.  
  
 SQL_BS_SELECT_EXPLICIT = 드라이버는 결과 집합 생성 문을 가질 수 있는 명시적 일괄 처리를 지원합니다.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 드라이버는 행 수 생성 문을 가질 수 있는 명시적 일괄 처리를 지원합니다.  
  
 SQL_BS_SELECT_PROC = 드라이버는 결과 집합 생성 문을 가질 수 있는 명시적 프로시저를 지원합니다.  
  
 SQL_BS_ROW_COUNT_PROC = 드라이버는 행 수 생성 문을 가질 수 있는 명시적 프로시저를 지원합니다.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 책갈피가 지속되는 작업을 예인하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 플래그와 함께 사용되어 책갈피가 지속되는 옵션을 결정합니다.  
  
 SQL_BP_CLOSE = 책갈피는 응용 프로그램이 SQL_CLOSE 옵션으로 **SQLFreeStmt를** 호출하거나 **SQLCloseCursor를** 호출하여 명령문과 연결된 커서를 닫은 후에 유효합니다.  
  
 SQL_BP_DELETE = 행의 책갈피는 해당 행이 삭제된 후 유효합니다.  
  
 SQL_BP_DROP = 책갈피는 응용 프로그램이 문을 삭제하기 위해 *핸들 SQL_HANDLE_STMT* **SQLFreeHandle을** 호출한 후에 유효합니다.  
  
 SQL_BP_TRANSACTION = 책갈피는 응용 프로그램이 트랜잭션을 커밋하거나 롤백한 후에 유효합니다.  
  
 SQL_BP_UPDATE = 행의 책갈피는 키 열을 포함하여 해당 행의 열이 업데이트된 후 유효합니다.  
  
 SQL_BP_OTHER_HSTMT = 한 문과 연결된 책갈피를 다른 문과 함께 사용할 수 있습니다. SQL_BP_CLOSE 또는 SQL_BP_DROP 지정하지 않는 한 첫 번째 문의 커서가 열려 있어야 합니다.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 정규화된 테이블 이름으로 카탈로그의 위치를 나타내는 SQLUSMALLINT 값:  
  
 SQL_CL_STARTSQL_CL_END  
  
 예를 들어 Xbase 드라이버는 \EMPDATA\EMP에서와 같이 디렉터리(카탈로그) 이름이 테이블 이름의 시작 부분에 있기 때문에 SQL_CL_START 반환합니다. Dbf. ORACLE Server 드라이버는 카탈로그가 테이블 이름 끝에 있으므로 SQL_CL_END 반환합니다. ADMIN.EMP@EMPDATA  
  
 SQL-92 전체 레벨 준수 드라이버는 항상 SQL_CL_START 반환합니다. 데이터 원본에서 카탈로그를 지원하지 않는 경우 값이 0으로 반환됩니다. 카탈로그가 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_CATALOG_NAME 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_QUALIFIER_LOCATION ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 문자 문자열: 서버가 카탈로그 이름을 지원하는 경우 "Y", 그렇지 않은 경우 "N".  
  
 SQL-92 전체 수준 준수 드라이버는 항상 "Y"를 반환합니다.  
  
 SQL_CATALOG_NAME_SEPARATOR(ODBC 1.0)  
 문자 문자열: 데이터 원본이 카탈로그 이름과 그 다음에 오거나 그 앞에 오는 정규화된 이름 요소 사이의 구분 기호로 정의하는 문자 또는 문자입니다.  
  
 데이터 원본에서 카탈로그를 지원하지 않으면 빈 문자열이 반환됩니다. 카탈로그가 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_CATALOG_NAME 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. SQL-92 전체 수준 준수 드라이버가 항상 ""를 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_QUALIFIER_NAME_SEPARATOR ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_CATALOG_TERM(ODBC 1.0)  
 카탈로그에 대한 데이터 원본 공급업체의 이름이 있는 문자열입니다. 예를 들어"데이터베이스" 또는 "디렉터리"를 예로 들 수 있습니다. 이 문자열은 상위, 하부 또는 혼합 대/소문자에 있을 수 있습니다.  
  
 데이터 원본에서 카탈로그를 지원하지 않으면 빈 문자열이 반환됩니다. 카탈로그가 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_CATALOG_NAME 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. SQL-92 전체 수준 준수 드라이버는 항상 "카탈로그"를 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_QUALIFIER_TERM ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_CATALOG_USAGE(ODBC 2.0)  
 카탈로그를 사용할 수 있는 문을 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 카탈로그를 사용할 수 있는 위치를 결정하는 데 사용됩니다.  
  
 SQL_CU_DML_STATEMENTS = 카탈로그는 모든 데이터 조작 언어 문에서 지원됩니다: **SELECT,** **INSERT**, **UPDATE**, **DELETE**및 지원되는 경우 업데이트 및 위치 업데이트 및 삭제 문을 **선택합니다.**  
  
 SQL_CU_PROCEDURE_INVOCATION = 카탈로그는 ODBC 프로시저 호출 문에서 지원됩니다.  
  
 SQL_CU_TABLE_DEFINITION = 카탈로그는 테이블 **만들기,** 보기 **만들기, 테이블** **변경,** **드롭 테이블**및 **DROP VIEW의**모든 테이블 정의 문에서 지원됩니다.  
  
 SQL_CU_INDEX_DEFINITION = 카탈로그는 모든 인덱스 정의 문에서 지원됩니다: **인덱스 만들기** 및 **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = 카탈로그는 모든 권한 정의 명령문에서 지원됩니다: **GRANT** 및 **해지**.  
  
 데이터 원본에서 카탈로그를 지원하지 않는 경우 값이 0으로 반환됩니다. 카탈로그가 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_CATALOG_NAME 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. SQL-92 전체 수준 준수 드라이버는 항상 이러한 모든 비트 집합과 함께 비트 마스크를 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *InfoType* SQL_QUALIFIER_USAGE ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_COLLATION_SEQ(ODBC 3.0)  
 데이터 정렬 시퀀스의 이름입니다. 이 문자열은 이 서버의 기본 문자 집합에 대한 기본 데이터 정렬의 이름을 나타내는 문자열입니다(예: 'ISO 8859-1' 또는 EBCDIC). 이를 알 수 없는 경우 빈 문자열이 반환됩니다. SQL-92 전체 수준 준수 드라이버는 항상 비어 없는 문자열을 반환합니다.  
  
 SQL_COLUMN_ALIAS(ODBC 2.0)  
 문자 문자열: 데이터 원본이 열 별칭을 지원하는 경우 "Y"; 그렇지 않으면 "N".  
  
 열 별칭은 AS 절을 사용하여 선택 목록의 열에 대해 지정할 수 있는 대체 이름입니다. SQL-92 엔트리 레벨 준수 드라이버는 항상 "Y"를 반환합니다.  
  
 SQL_CONCAT_NULL_BEHAVIOR(ODBC 1.0)  
 데이터 원본이 NULL 값 문자 형식 열과 NULL 값 문자 데이터 형식 열의 결합을 처리하는 방법을 나타내는 SQLUSMALLINT 값입니다.  
  
 SQL_CB_NULL = 결과는 NULL 값입니다.  
  
 SQL_CB_NON_NULL = 결과는 NULL이 아닌 값열 또는 열의 연결입니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 SQL_CB_NULL 반환합니다.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER 비트 마스크입니다. 비트 마스크는 *InfoType에*명명된 형식의 데이터에 대한 **CONVERT** 스칼라 함수가 있는 데이터 원본에서 지원하는 변환을 나타냅니다. 비트 마스크가 0이면 데이터 원본은 동일한 데이터 유형으로의 변환을 포함하여 명명된 형식의 데이터에서 변환을 지원하지 않습니다.  
  
 예를 들어 데이터 원본이 SQL_INTEGER 데이터를 SQL_BIGINT 데이터 유형으로 변환하는 것을 지원하는지 확인하기 위해 응용 프로그램은 *SQL_CONVERT_INTEGER InfoType을* 사용하여 **SQLGetInfo를** 호출합니다. 응용 프로그램은 반환된 비트 마스크를 사용하여 **AND** 작업을 수행하고 SQL_CVT_BIGINT. 결과 값이 0이 아닌 경우 변환이 지원됩니다.  
  
 다음 비트마스크는 지원되는 변환을 결정하는 데 사용됩니다.  
  
 SQL_CVT_BIGINT (ODBC 1.0)SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT(ODBC 1.0)SQL_CVT_INTEGER(ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH(ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME(ODBC 3.0)SQL_CVT_LONGVARBINARY(ODBC 1.0)SQL_CVT_LONGVARCHAR(ODBC 1.0)SQL_CVT_NUMERIC(ODBC 1.0)SQL_ CVT_REAL ODBC 1.0)SQL_CVT_SMALLINT (ODBC 1.0)SQL_CVT_TIME (ODBC 1.0)SQL_CVT_TIMESTAMP (ODBC 1.0)SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS(ODBC 1.0)  
 드라이버 및 관련 데이터 원본에서 지원하는 스칼라 변환 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 지원되는 변환 함수를 결정하는 데 사용됩니다.  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME(ODBC 1.0)  
 테이블 상관 관계 이름이 지원되는지 여부를 나타내는 SQLUSMALLINT 값은 다음과 같습니다.  
  
 SQL_CN_NONE = 상관 관계 이름은 지원되지 않습니다.  
  
 SQL_CN_DIFFERENT = 상관 관계 이름은 지원되지만 나타내는 테이블의 이름과 달라야 합니다.  
  
 SQL_CN_ANY = 상관 관계 이름은 지원되며 유효한 사용자 정의 이름일 수 있습니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 SQL_CN_ANY 반환합니다.  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **CREATE 어설션** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CA_CREATE_ASSERTION  
  
 다음 비트는 제약 조건 특성을 명시적으로 지정하는 기능이 지원되는 경우 지원되는 제약 조건 특성을 지정합니다(SQL_ALTER_TABLE 및 SQL_CREATE_TABLE 정보 형식 참조).  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다. 반환 값 "0"은 **CREATE 어설션** 문이 지원되지 않음을 의미합니다.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 SQL-92에 정의된 대로 데이터 원본에서 지원하는 **문자 집합 만들기** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다. 반환 값 "0"은 **CREATE CHARACTER SET** 문이 지원되지 않음을 의미합니다.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 SQL-92에 정의된 것처럼 **CREATE COLLATION** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CCOL_CREATE_COLLATION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이 옵션을 반환합니다. 반환 값 "0"은 **CREATE COLLATION** 문이 지원되지 않음을 의미합니다.  
  
 SQL_CREATE_DOMAIN(ODBC 3.0)  
 SQL-92에 정의된 대로 **CREATE DOMAIN** 문의 절을 영예하는 SQLUINTEGER 비트 마스크는 데이터 원본에서 지원됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CDO_CREATE_DOMAIN = CREATE DOMAIN 문이 지원됩니다(중간 수준).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION \<= 제약 조건 이름 정의> 도메인 제약 조건(중간 수준)의 이름을 지정하는 데 지원됩니다.  
  
 다음 비트는 열 제약 조건을 만드는 기능을 지정합니다:SQL_CDO_DEFAULT = 도메인 제약 조건 지정이 지원됩니다(중간 수준)SQL_CDO_CONSTRAINT = 도메인 기본값 지정이 지원됩니다(중간 수준)SQL_CDO_COLLATION = 도메인 데이터 정렬 지정이 지원됩니다(전체 수준).  
  
 다음 비트는 도메인 제약 조건을 지정하는 것이 지원되는 경우 지원되는 제약 조건 특성을 지정합니다(SQL_CDO_DEFAULT 설정됨).  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED(전체 레벨)SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE(전체 레벨)SQL_CDO_CONSTRAINT_DEFERRABLE(전체 레벨)SQL_CDO_CONSTRAINT_NON_DEFERRABLE(전체 레벨)  
  
 반환 값 "0"은 **CREATE DOMAIN** 문이 지원되지 않음을 의미합니다.  
  
 SQL_CREATE_SCHEMA(ODBC 3.0)  
 SQL-92에 정의된 대로 데이터 원본에서 지원하는 **CREATE SCHEMA** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL-92 중간 수준 준수 드라이버는 항상 지원되는 SQL_CS_CREATE_SCHEMA 및 SQL_CS_AUTHORIZATION 옵션을 반환합니다. SQL-92 엔트리 레벨에서도 지원되어야 하지만 반드시 SQL 문으로 지원되는 것은 아닙니다. SQL-92 전체 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다.  
  
 SQL_CREATE_TABLE(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **CREATE TABLE** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CT_CREATE_TABLE = 테이블 만들기 문이 지원됩니다. (엔트리 레벨)  
  
 SQL_CT_TABLE_CONSTRAINT = 테이블 제약 조건 지정이 지원됩니다(FIPS 전환 수준)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의> 절은 이름 열 및 테이블 제약 조건(중간 수준)에 대해 지원됩니다.  
  
 다음 비트는 임시 테이블을 만드는 기능을 지정합니다.  
  
 SQL_CT_COMMIT_PRESERVE = 삭제된 행은 커밋시 유지됩니다. (전체 레벨) SQL_CT_COMMIT_DELETE = 삭제된 행은 커밋시 삭제됩니다. (전체 레벨) SQL_CT_GLOBAL_TEMPORARY = 전역 임시 테이블을 만들 수 있습니다. (전체 레벨) SQL_CT_LOCAL_TEMPORARY = 로컬 임시 테이블을 만들 수 있습니다. (전체 레벨)  
  
 다음 비트는 열 제약 조건을 만드는 기능을 지정합니다.  
  
 SQL_CT_COLUMN_CONSTRAINT = 열 제약 조건 지정이 지원됩니다(FIPS 전환 수준)SQL_CT_COLUMN_DEFAULT = 열 기본값 지정이 지원됩니다(FIPS 전환 수준)SQL_CT_COLUMN_COLLATION = 열 데이터 정렬 지정이 지원됩니다(전체 수준).  
  
 다음 비트는 열 또는 테이블 제약 조건을 지정하는 것이 지원되는 경우 지원되는 제약 조건 특성을 지정합니다.  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED(전체 레벨)SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE(전체 레벨)SQL_CT_CONSTRAINT_DEFERRABLE(전체 레벨)SQL_CT_CONSTRAINT_NON_DEFERRABLE(전체 레벨)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 SQL-92에 정의된 대로 데이터 원본에서 지원하는 **CREATE TRANSLATION** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이러한 옵션을 반환합니다. 반환 값 "0"은 **CREATE TRANSLATION** 문이 지원되지 않음을 의미합니다.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **CREATE VIEW** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 반환 값 "0"은 **CREATE VIEW** 문이 지원되지 않음을 의미합니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 SQL_CV_CREATE_VIEW 및 SQL_CV_CHECK_OPTION 옵션을 반환합니다.  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR(ODBC 1.0)  
 **COMMIT** 작업이 커서에 미치는 영향과 데이터 원본의 준비된 명령문(트랜잭션을 커밋할 때데이터 원본의 동작)을 나타내는 SQLUSMALLINT 값입니다.  
  
 이 특성의 값은 다음 설정인 SQL_COPT_SS_PRESERVE_CURSORS 현재 상태를 반영합니다.  
  
 SQL_CB_DELETE = 커서를 닫고 준비된 문을 삭제합니다. 커서를 다시 사용하려면 응용 프로그램이 문을 다시 준비하고 다시 실행해야 합니다.  
  
 SQL_CB_CLOSE = 커서 닫기. 준비된 명령문의 경우 응용 프로그램은 **SQLPrepare를** 다시 호출하지 않고 명령문에서 **SQLExecute를** 호출할 수 있습니다. SQL ODBC 드라이버의 기본값은 SQL_CB_CLOSE. 즉, SQL ODBC 드라이버는 트랜잭션을 커밋할 때 커서를 닫습니다.  
  
 SQL_CB_PRESERVE = **COMMIT** 작업 전과 동일한 위치에서 커서를 보존합니다. 응용 프로그램은 데이터를 계속 가져오거나 커서를 닫고 다시 준비하지 않고 문을 다시 실행할 수 있습니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR(ODBC 1.0)  
 **ROLLBACK** 작업이 데이터 원본에서 커서 및 준비된 명령문에 미치는 영향을 나타내는 SQLUSMALLINT 값입니다.  
  
 SQL_CB_DELETE = 커서를 닫고 준비된 문을 삭제합니다. 커서를 다시 사용하려면 응용 프로그램이 문을 다시 준비하고 다시 실행해야 합니다.  
  
 SQL_CB_CLOSE = 커서 닫기. 준비된 명령문의 경우 응용 프로그램은 **SQLPrepare를** 다시 호출하지 않고 명령문에서 **SQLExecute를** 호출할 수 있습니다.  
  
 SQL_CB_PRESERVE = **ROLLBACK** 작업 전과 동일한 위치에서 커서를 보존합니다. 응용 프로그램은 데이터를 계속 가져오거나 커서를 닫고 다시 준비하지 않고 문을 다시 실행할 수 있습니다.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 커서 민감도에 대한 지원을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_INSENSITIVE = 문 핸들의 모든 커서는 동일한 트랜잭션 내의 다른 커서에 의해 변경된 내용을 반영하지 않고 결과 집합을 표시합니다.  
  
 SQL_UNSPECIFIED = 문 핸들의 커서가 동일한 트랜잭션 내의 다른 커서에 의해 설정된 결과에 대해 변경된 내용을 표시할지 여부는 지정되지 않습니다. 명령문 핸들의 커서는 보이지 않는 것, 일부 또는 이러한 모든 변경 내용을 표시하지 않을 수 있습니다.  
  
 SQL_SENSITIVE = 커서는 동일한 트랜잭션 내의 다른 커서에 의해 변경된 변경 사항에 민감합니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 SQL_UNSPECIFIED 옵션을 반환합니다.  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 SQL_INSENSITIVE 옵션을 반환합니다.  
  
 SQL_DATA_SOURCE_NAME(ODBC 1.0)  
 연결 중에 사용된 데이터 원본 이름이 있는 문자열입니다. 응용 프로그램이 **SQLConnect라고**하는 경우 *szDSN* 인수의 값입니다. **SQLDriverConnect** 또는 **SQLBrowseConnect라는**응용 프로그램이 드라이버에 전달된 연결 문자열의 DSN 키워드값입니다. 연결 문자열에 **DSN** 키워드(예: **DRIVER** 키워드가 포함된 경우)가 없는 경우 빈 문자열입니다.  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 문자열입니다. 데이터 원본이 READ ONLY 모드로 설정된 경우 "Y", 그렇지 않으면 "N"입니다.  
  
 이 특성은 데이터 원본 자체에만 해당됩니다. 데이터 원본에 액세스할 수 있는 드라이버의 특성이 아닙니다. 읽기/쓰기드라이버는 읽기 전용데이터 원본과 함께 사용할 수 있습니다. 드라이버가 읽기 전용인 경우 모든 데이터 원본은 읽기 전용이어야 하며 SQL_DATA_SOURCE_READ_ONLY 반환해야 합니다.  
  
 SQL_DATABASE_NAME(ODBC 1.0)  
 데이터 원본이 "데이터베이스"라는 명명된 개체를 정의하는 경우 사용 중현재 데이터베이스의 이름이 있는 문자열입니다.  
  
> [!NOTE]
>  ODBC 3 *.x에서*이 *InfoType에* 대해 반환된 값은 SQL_ATTR_CURRENT_CATALOG *특성* 인수를 사용하는 **SQLGetConnectAttr을** 호출하여 반환할 수도 있습니다.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92 datetime 리터럴을 영예로 하는 SQLUINTEGER 비트 마스크입니다. 이러한 날짜 리터럴은 SQL-92 사양에 나열된 날짜 시간 리터럴이며 ODBC에서 정의한 datetime 리터럴 이스케이프 절과는 별개입니다. ODBC 날짜 시간 리터럴 이스케이프 절에 대한 자세한 내용은 [날짜, 시간 및 타임스탬프 리터럴을](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)참조하십시오.  
  
 FIPS 전환 레벨 준수 드라이버는 항상 다음 목록의 비트에 대한 비트 마스크에서 "1" 값을 반환합니다. 값이 "0"이면 SQL-92 datetime 리터럴이 지원되지 않음을 의미합니다.  
  
 다음 비트마스크는 지원되는 리터럴을 결정하는 데 사용됩니다.  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME(ODBC 1.0)  
 드라이버가 액세스하는 DBMS 제품의 이름이 있는 문자열입니다.  
  
 SQL_DBMS_VER(ODBC 1.0)  
 드라이버에서 액세스하는 DBMS 제품의 버전을 나타내는 문자열 문자열입니다. 버전은 처음 두 자리가 주 버전이고 다음 두 자리는 부 버전이고 마지막 네 자리 숫자는 릴리스 버전인 ######형식입니다. 드라이버는 이 양식으로 DBMS 제품 버전을 렌더링해야 하지만 DBMS 제품별 버전도 추가할 수 있습니다. 예를 들어 "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 인덱스 생성 및 삭제에 대한 지원을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION(ODBC 1.0)  
 드라이버 또는 데이터 원본에서 지원하는 기본 트랜잭션 격리 수준을 나타내는 SQLUINTEGER 값 또는 데이터 원본이 트랜잭션을 지원하지 않는 경우 0입니다. 다음 용어는 트랜잭션 격리 수준을 정의하는 데 사용됩니다.  
  
 **더러운 읽기** 트랜잭션 1은 행을 변경합니다. 트랜잭션 2는 트랜잭션 1이 변경을 커밋하기 전에 변경된 행을 읽습니다. 트랜잭션 1이 변경 내용을 롤백하는 경우 트랜잭션 2는 존재하지 않는 것으로 간주되는 행을 읽습니다.  
  
 **반복할 수 없는 읽기** 트랜잭션 1은 행을 읽습니다. 트랜잭션 2는 해당 행을 업데이트하거나 삭제하고 이 변경 을 커밋합니다. 트랜잭션 1이 행을 다시 읽으려고 하면 다른 행 값을 받거나 행이 삭제되었음을 발견합니다.  
  
 **팬텀 (것)과 같은** 트랜잭션 1은 일부 검색 조건을 충족하는 행 집합을 읽습니다. 트랜잭션 2는 검색 조건과 일치하는 하나 이상의 행(삽입 또는 업데이트를 통해)을 생성합니다. 트랜잭션 1이 행을 읽는 문을 다시 실행하면 다른 행 집합이 수신됩니다.  
  
 데이터 원본이 트랜잭션을 지원하는 경우 드라이버는 다음 비트 마스크 중 하나를 반환합니다.  
  
 SQL_TXN_READ_UNCOMMITTED = 더티 읽기, 반복할 수 없는 읽기 및 팬텀이 가능합니다.  
  
 SQL_TXN_READ_COMMITTED = 더티 읽기는 불가능합니다. 반복되지 않는 읽기 및 팬텀이 가능합니다.  
  
 SQL_TXN_REPEATABLE_READ = 더티 읽기 및 반복할 수 없는 읽기는 불가능합니다. 유령이 가능합니다.  
  
 SQL_TXN_SERIALIZABLE = 트랜잭션은 직렬화할 수 있습니다. 직렬화 할 수있는 트랜잭션은 더티 읽기, 반복할 수없는 읽기 또는 팬텀을 허용하지 않습니다.  
  
 SQL_DESCRIBE_PARAMETER(ODBC 3.0)  
 문자 문자열: 매개 변수를 설명할 수 있는 경우 "Y" "N", 그렇지 않은 경우.  
  
 SQL-92 전체 수준 준수 드라이버는 **일반적으로 DESCRIBE INPUT** 문을 지원하므로 "Y"를 반환합니다. 그러나 기본 SQL 지원을 직접 지정하지는 않으므로 SQL-92 전체 수준 준수 드라이버에서도 매개 변수를 설명하는 것이 지원되지 않을 수 있습니다.  
  
 SQL_DM_VER(ODBC 3.0)  
 드라이버 관리자 버전이 있는 문자열입니다. 버전은 #.#############이라는 양식의 버전입니다.  
  
 두 자리의 첫 번째 세트는 상수 SQL_SPEC_MAJOR 의해 주어진 대로 주요 ODBC 버전입니다.  
  
 두 자리의 두 번째 집합은 상수 SQL_SPEC_MINOR 지정한 대로 부식 ODBC 버전입니다.  
  
 네 자리의 세 번째 집합은 드라이버 관리자 주요 빌드 번호입니다.  
  
 네 자리의 마지막 세트는 드라이버 관리자 마이너 빌드 번호입니다.  
  
 윈도우 7 드라이버 관리자 버전은 03.80. 윈도우 8 드라이버 관리자 버전은 03.81입니다.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 드라이버가 드라이버 인식 풀링을 지원하는지 나타내는 SQLUINTEGER 값입니다. 자세한 내용은 드라이버 [인식 연결 풀링을](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)참조하십시오.  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE 드라이버가 드라이버 인식 풀링 메커니즘을 지원할 수 있음을 나타냅니다.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 드라이버가 드라이버 인식 풀링 메커니즘을 지원할 수 없음을 나타냅니다.  
  
 드라이버는 SQL_DRIVER_AWARE_POOLING_SUPPORTED 구현할 필요가 없으며 드라이버 관리자는 드라이버의 반환 값을 존중하지 않습니다.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV(ODBC 1.0)  
 SQLULEN 값, 드라이버의 환경 핸들 또는 연결 핸들, 인수 *InfoType에*의해 결정 .  
  
 이러한 정보 유형은 드라이버 관리자만으로 구현됩니다.  
  
 SQL_DRIVER_HDESC(ODBC 3.0)  
 SQLULEN 값은 드라이버 관리자의 설명자 핸들에 의해 결정된 드라이버의 설명자 핸들로, \*응용 프로그램에서 *InfoValuePtr의* 입력에 전달되어야 합니다. 이 경우 *InfoValuePtr은* 입력 및 출력 인수입니다. \* *InfoValuePtr에서* 전달된 입력 설명자 핸들은 *ConnectionHandle*에 명시적으로 또는 암시적으로 할당되어 있어야 합니다.  
  
 응용 프로그램은 이 정보 유형으로 **SQLGetInfo를** 호출하기 전에 드라이버 관리자의 설명자 핸들의 복사본을 만들어 출력시 핸들이 덮어쓰지 않도록 해야 합니다.  
  
 이 정보 유형은 드라이버 관리자만으로 구현됩니다.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 SQLULEN 값, 로드 라이브러리의 *힌스트는* Microsoft Windows 운영 체제에서 드라이버 DLL을 로드하거나 다른 운영 체제에서 이와 동등한 드라이버를 로드할 때 드라이버 관리자로 반환됩니다. 핸들은 **SQLGetInfo**에 대한 호출에 지정된 연결 핸들에 대해서만 유효합니다.  
  
 이 정보 유형은 드라이버 관리자만으로 구현됩니다.  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 SQLULEN 값, 드라이버 관리자 문 핸들에 의해 결정 되는 드라이버의 문 \*핸들, 응용 프로그램에서 *InfoValuePtr의* 입력에 전달 해야 합니다. 이 경우 *InfoValuePtr은* 입력 및 출력 인수입니다. \* *InfoValuePtr에서* 전달된 입력 문 핸들은 연결 *핸들*인수에 할당되어 있어야 합니다.  
  
 응용 프로그램은 이 정보 형식을 사용하여 **SQLGetInfo를** 호출하기 전에 드라이버 관리자 문 핸들의 복사본을 만들어 출력시 핸들이 덮어쓰지 않도록 해야 합니다.  
  
 이 정보 유형은 드라이버 관리자만으로 구현됩니다.  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 데이터 원본에 액세스하는 데 사용되는 드라이버의 파일 이름이 있는 문자열입니다.  
  
 SQL_DRIVER_ODBC_VER(ODBC 2.0)  
 드라이버가 지원하는 ODBC 버전이 있는 문자열입니다. 버전은 처음 두 자리가 주 버전이고 다음 두 자리는 부 버전인 ####양식입니다. SQL_SPEC_MAJOR 및 SQL_SPEC_MINOR 주 및 부 버전 번호를 정의합니다. 이 설명서에 설명된 ODBC 버전의 경우 3과 0이며 드라이버는 "03.00"을 반환해야 합니다.  
  
 ODBC 드라이버 관리자는 기존 응용 프로그램에 대한 이전 버전과의 호환성을 유지하기 위해 SQLGetInfo(SQL_DRIVER_ODBC_VER)의 반환 값을 수정하지 않습니다. 드라이버는 반환할 값을 지정합니다. 그러나 C 데이터 형식 확장성을 지원하는 드라이버는 응용 프로그램이 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_ODBC_VERSION 3.8로 설정할 때 3.8(또는 그 이상)을 반환해야 합니다. 자세한 내용은 [ODBC의 C 데이터 유형을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.  
  
 SQL_DRIVER_VER(ODBC 1.0)  
 드라이버 버전과 선택적으로 드라이버에 대한 설명이 있는 문자열입니다. 최소한 버전은 처음 두 자리가 주 버전이고 다음 두 자리는 부 버전이고 마지막 네 자리 숫자는 릴리스 버전인 ######형식입니다.  
  
 SQL_DROP_ASSERTION(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP 어설션** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DA_DROP_ASSERTION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이 옵션을 반환합니다.  
  
 SQL_DROP_CHARACTER_SET(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP CHARACTER SET** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이 옵션을 반환합니다.  
  
 SQL_DROP_COLLATION(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP COLLATION** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DC_DROP_COLLATION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이 옵션을 반환합니다.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP DOMAIN** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL-92 중간 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP SCHEMA** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL-92 중간 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다.  
  
 SQL_DROP_TABLE(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP TABLE** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 전환 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_DROP_TRANSLATION(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP 번역** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DTR_DROP_TRANSLATION  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원되는 대로 이 옵션을 반환합니다.  
  
 SQL_DROP_VIEW(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **DROP VIEW** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 전환 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원하는 동적 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 특성의 첫 번째 하위 집합이 포함되어 있습니다. 두 번째 하위 집합은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA1_NEXT = 커서가 동적 커서인 경우 **SQLFetchScroll** 호출에서 SQL_FETCH_NEXT *FetchOrientation* 인수가 지원됩니다.  
  
 SQL_CA1_ABSOLUTE = 커서가 동적 커서인 경우 SQL_FETCH_FIRST, SQL_FETCH_LAST 및 SQL_FETCH_ABSOLUTE *대한 FetchOrientation* 인수는 **SQLFetchScroll** 호출에서 지원됩니다. (가져올 행 집합은 현재 커서 위치와 독립적입니다.)  
  
 SQL_CA1_RELATIVE = 커서가 동적 커서인 경우 SQL_FETCH_PRIOR 및 SQL_FETCH_RELATIVE *대한 FetchOrientation* 인수는 **SQLFetchScroll** 호출에서 지원됩니다. (가져올 행 집합은 현재 커서 위치에 따라 다릅니다. 정방향 전용 커서에서는 SQL_FETCH_NEXT 지원되므로 SQL_FETCH_NEXT 분리됩니다.  
  
 SQL_CA1_BOOKMARK = 커서가 동적 커서인 경우 **SQLFetchScroll** 호출에서 SQL_FETCH_BOOKMARK *FetchOrientation* 인수가 지원됩니다.  
  
 SQL_CA1_LOCK_EXCLUSIVE = 커서가 동적 커서인 경우 SQL_LOCK_EXCLUSIVE *LockType* 인수는 **SQLSetPos** 호출에서 지원됩니다.  
  
 SQL_CA1_LOCK_NO_CHANGE = 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 SQL_LOCK_NO_CHANGE *LockType* 인수가 지원됩니다.  
  
 SQL_CA1_LOCK_UNLOCK = SQL_LOCK_UNLOCK *LockType* 인수는 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 지원됩니다.  
  
 SQL_CA1_POS_POSITION = 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 SQL_POSITION *작업* 인수가 지원됩니다.  
  
 SQL_CA1_POS_UPDATE = 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 SQL_UPDATE *작업* 인수가 지원됩니다.  
  
 SQL_CA1_POS_DELETE = 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 SQL_DELETE *작업* 인수가 지원됩니다.  
  
 SQL_CA1_POS_REFRESH = 커서가 동적 커서인 경우 **SQLSetPos** 를 호출할 때 SQL_REFRESH *작업* 인수가 지원됩니다.  
  
 SQL_CA1_POSITIONED_UPDATE = 커서가 동적 커서인 경우 SQL 문의 현재가 지원되는 업데이트입니다. (SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로이 옵션을 반환합니다.)  
  
 SQL_CA1_POSITIONED_DELETE = 커서가 동적 커서인 경우 SQL 문의 현재가 지원되는 삭제입니다. (SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로이 옵션을 반환합니다.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = UPDATE용 SELECT SQL 문은 커서가 동적 커서인 경우 지원됩니다. (SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로이 옵션을 반환합니다.)  
  
 SQL_CA1_BULK_ADD = 커서가 동적 커서인 경우 **SQLBulkOperations** 를 호출할 때 SQL_ADD *작업* 인수가 지원됩니다.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = SQL_UPDATE_BY_BOOKMARK *작업* 인수는 커서가 동적 커서인 경우 **SQLBulkOperations** 를 호출할 때 지원됩니다.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = 커서가 동적 커서인 경우 SQL_DELETE_BY_BOOKMARK *작업* 인수는 **SQLBulkOperations** 호출에서 지원됩니다.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = 커서가 동적 커서인 경우 **SQLBulkOperations** 를 호출할 때 SQL_FETCH_BY_BOOKMARK *작업* 인수가 지원됩니다.  
  
 SQL-92 중간 수준 준수 드라이버는 일반적으로 포함된 SQL FETCH 문을 통해 스크롤 가능한 커서를 지원하기 때문에 지원되는 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 반환합니다. 그러나 기본 SQL 지원을 직접 결정하지는 않으므로 SQL-92 중간 수준 준수 드라이버의 경우에도 스크롤 가능한 커서가 지원되지 않을 수 있습니다.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원하는 동적 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 두 번째 특성 하위 집합이 포함되어 있습니다. 첫 번째 하위 집합은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 업데이트가 허용되지 않는 읽기 전용 동적 커서가 지원됩니다. (SQL_ATTR_CONCURRENCY 문 특성은 동적 커서에 대해 SQL_CONCUR_READ_ONLY 수 있습니다).  
  
 SQL_CA2_LOCK_CONCURRENCY = 행을 업데이트할 수 있는지 확인하기에 충분한 최하위 수준의 잠금을 사용하는 동적 커서가 지원됩니다. SQL_ATTR_CONCURRENCY 명령문 특성은 동적 커서에 대해 SQL_CONCUR_LOCK 수 있습니다. 이러한 잠금은 SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정된 트랜잭션 격리 수준과 일치해야 합니다.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 행 버전을 비교하는 낙관적 동시성 컨트롤을 사용하는 동적 커서가 지원됩니다. SQL_ATTR_CONCURRENCY 명령문 특성은 동적 커서에 대해 SQL_CONCUR_ROWVER 수 있습니다.  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 값을 비교하는 낙관적 동시성 컨트롤을 사용하는 동적 커서가 지원됩니다. SQL_ATTR_CONCURRENCY 명령문 특성은 동적 커서에 대해 SQL_CONCUR_VALUES 수 있습니다.  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 추가된 행이 동적 커서에 표시됩니다. 커서는 해당 행으로 스크롤할 수 있습니다. 이러한 행이 커서에 추가되는 경우 드라이버에 따라 다릅니다.  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 삭제된 행은 동적 커서에서 더 이상 사용할 수 없으며 결과 집합에 "구멍"을 두지 않습니다. 동적 커서가 삭제된 행에서 스크롤된 후에는 해당 행으로 돌아갈 수 없습니다.  
  
 SQL_CA2_SENSITIVITY_UPDATES = 행에 대한 업데이트는 동적 커서에 표시됩니다. 동적 커서가 에서 스크롤되어 업데이트된 행으로 반환되는 경우 커서에서 반환되는 데이터는 원래 데이터가 아닌 업데이트된 데이터입니다.  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 경우 **SELECT** 문에 영향을 줍니다.  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 경우 **INSERT** 문에 영향을 줍니다.  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 경우 **DELETE** 문에 영향을 줍니다.  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 경우 **UPDATE** 문에 영향을 줍니다.  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 경우 **CATALOG** 결과 집합에 영향을 줍니다.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서인 **경우 SELECT,** **INSERT,** **DELETE**및 **UPDATE** 문 및 **CATALOG** 결과 집합에 영향을 줍니다.  
  
 SQL_CA2_CRC_EXACT = 커서가 동적 커서인 경우 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드에서 정확한 행 수를 사용할 수 있습니다.  
  
 SQL_CA2_CRC_APPROXIMATE = 커서가 동적 커서인 경우 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드에서 대략적인 행 수를 사용할 수 있습니다.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 드라이버는 커서가 동적 커서일 때 시뮬레이션된 위치 업데이트 또는 delete 문이 하나의 행에만 영향을 미치지 않는다는 것을 보장하지 않습니다. 이를 보장하는 것은 응용 프로그램의 책임입니다. (명령문이 두 개 이상의 행에 영향을 주는 경우 **SQLExecute** 또는 **SQLExecDirect는** SQLSTATE 01001 [커서 작업 충돌]을 반환합니다.) 이 동작을 설정 하기 위해 응용 프로그램은 **sqlSetStmtAttr** SQL_SC_NON_UNIQUE 설정 된 SQL_ATTR_SIMULATE_CURSOR 특성을 호출 합니다.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 드라이버는 커서가 동적 커서인 경우 시뮬레이션된 위치 업데이트 또는 delete 명령문에 한 행만 영향을 주도록 합니다. 드라이버는 고유 키가 없는 경우와 같이 두 개 이상의 행에 영향을 줄 수 있더라도 항상 이러한 문을 실행합니다. (명령문이 두 개 이상의 행에 영향을 주는 경우 **SQLExecute** 또는 **SQLExecDirect는** SQLSTATE 01001 [커서 작업 충돌]을 반환합니다.) 이 동작을 설정 하기 위해 응용 프로그램은 SQL_SC_TRY_UNIQUE 설정 된 SQL_ATTR_SIMULATE_CURSOR **특성으로 SQLSetStmtAttr를** 호출 합니다.  
  
 SQL_CA2_SIMULATE_UNIQUE = 드라이버는 커서가 동적 커서인 경우 시뮬레이션된 위치 업데이트 또는 delete 명령문이 하나의 행에만 영향을 미치게 합니다. 드라이버가 지정된 문에 대해 이를 보장할 수 없는 경우 **SQLExecDirect** 또는 **SQLPrepare** 반환 SQLSTATE 01001(커서 작업 충돌). 이 동작을 설정 하기 위해 응용 프로그램은 SQL_SC_UNIQUE 설정 된 SQL_ATTR_SIMULATE_CURSOR **특성으로 SQLSetStmtAttr를** 호출 합니다.  
  
 SQL_EXPRESSIONS_IN_ORDERBY(ODBC 1.0)  
 문자 문자열: 데이터 원본이 **ORDER BY** 목록에서 식을 지원하는 경우 "Y"입니다. "N"이 아닌 경우.  
  
 SQL_FILE_USAGE(ODBC 2.0)  
 단일 계층 드라이버가 데이터 원본의 파일을 직접 처리하는 방법을 나타내는 SQLUSMALLINT 값입니다.  
  
 SQL_FILE_NOT_SUPPORTED = 드라이버가 단일 계층 드라이버가 아닙니다. 예를 들어 ORACLE 드라이버는 2계층 드라이버입니다.  
  
 SQL_FILE_TABLE = 단일 계층 드라이버는 데이터 원본의 파일을 테이블로 처리합니다. 예를 들어 Xbase 드라이버는 각 Xbase 파일을 테이블로 처리합니다.  
  
 SQL_FILE_CATALOG = 단일 계층 드라이버는 데이터 원본의 파일을 카탈로그로 처리합니다. 예를 들어 Microsoft Access 드라이버는 각 Microsoft Access 파일을 전체 데이터베이스로 처리합니다.  
  
 응용 프로그램은 사용자가 데이터를 선택하는 방법을 결정하기 위해 이 옵션을 사용할 수 있습니다. 예를 들어 Xbase 사용자는 데이터를 파일에 저장된 것으로 생각하는 반면 ORACLE 및 Microsoft Access 사용자는 일반적으로 데이터를 테이블에 저장된 것으로 간주합니다.  
  
 사용자가 Xbase 데이터 원본을 선택하면 응용 프로그램에 Windows **파일 열기** 공통 대화 상자가 표시될 수 있습니다. 사용자가 Microsoft Access 또는 ORACLE 데이터 원본을 선택하면 응용 프로그램에 사용자 지정 **테이블 선택** 대화 상자가 표시될 수 있습니다.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원하는 정방향 전용 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 특성의 첫 번째 하위 집합이 포함되어 있습니다. 두 번째 하위 집합의 경우 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(설명에서 "동적 커서"에 대해 "정방향 전용 커서"로 대체)를 참조하십시오.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원하는 정방향 전용 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 두 번째 특성 하위 집합이 포함되어 있습니다. 첫 번째 하위 집합은 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(설명에서 "동적 커서"에 대해 "정방향 전용 커서"로 대체)를 참조하십시오.  
  
 SQL_GETDATA_EXTENSIONS(ODBC 2.0)  
 **SQLGetData에**대한 확장을 확장하는 SQLUINTEGER 비트 마스크 .  
  
 다음 비트 마스크는 플래그와 함께 사용되어 드라이버가 **SQLGetData에**대해 지원하는 일반적인 확장을 결정합니다.  
  
 SQL_GD_ANY_COLUMN = **SQLGetData는** 마지막 바인딩된 열 이전의 열을 포함하여 모든 언바운드 열에 대해 호출할 수 있습니다. SQL_GD_ANY_ORDER 반환되지 않는 한 열은 오름차순으로 호출되어야 합니다.  
  
 SQL_GD_ANY_ORDER = **SQLGetData는** 임의의 순서로 언바운드 열에 대해 호출할 수 있습니다. **SQLGetData는** SQL_GD_ANY_COLUMN 반환되지 않는 한 마지막 바인딩된 열 이후의 열에 대해서만 호출할 수 있습니다.  
  
 SQL_GD_BLOCK = **SQLGetData는** **SQLSetPos를**사용하여 해당 행에 배치한 후 블록의 모든 행에 있는 언바운드 열(행 집합 크기가 1보다 큰 경우)에 대해 호출할 수 있습니다.  
  
 SQL_GD_BOUND = **SQLGetData언바운드** 열 외에 바인딩된 열에 대해 호출할 수 있습니다. 드라이버는 SQL_GD_ANY_COLUMN 반환하지 않는 한 이 값을 반환할 수 없습니다.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** 출력 매개 변수 값을 반환 하기 위해 호출할 수 있습니다. 자세한 내용은 [SQLGetData를 사용하여 출력 매개 변수 검색을](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)참조하십시오.  
  
 **SQLGetData는** 마지막 바인딩된 열 이후에 발생하는 언바운드 열에서만 데이터를 반환해야 하며, 열 수를 늘리는 순서로 호출되며 행 블록의 행에 있지 않습니다.  
  
 드라이버가 책갈피(고정 길이 또는 가변 길이)를 지원하는 경우 열 0에서 **SQLGetData** 호출을 지원해야 합니다. 이 지원은 드라이버가 **SQL_GETDATA_EXTENSIONS** *InfoType*.  
  
 SQL_GROUP_BY(ODBC 2.0)  
 **그룹 BY** 절의 열과 선택 목록의 집계되지 않은 열 간의 관계를 지정하는 SQLUSMALLINT 값입니다.  
  
 SQL_GB_COLLATE = 각 그룹화 열의 끝에 **COLLATE** 절을 지정할 수 있습니다. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** 절은 지원되지 않습니다. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY** 절은 선택 목록에 집계되지 않은 모든 열을 포함해야 합니다. 다른 열을 포함할 수 없습니다. 예를 들어 **부서별 직원 그룹에서 부서, MAX(급여)를 선택합니다.** (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY** 절은 선택 목록에 집계되지 않은 모든 열을 포함해야 합니다. 선택 목록에 없는 열을 포함할 수 있습니다. 예를 **들어, 부서별 직원 그룹별, 연령별 에서 부서, MAX(급여)를 선택합니다.** (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = **GROUP BY** 절의 열과 선택 목록은 관련이 없습니다. 선택 목록에서 그룹화되지 않은 집계되지 않은 열의 의미는 데이터 원본에 따라 다릅니다. 예를 **들어, 부서, 부서별 직원 그룹, 연령별 급여 를 선택합니다.** (ODBC 2.0)  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 SQL_GB_GROUP_BY_EQUALS_SELECT 옵션을 반환합니다. SQL-92 전체 수준 준수 드라이버는 항상 지원되는 SQL_GB_COLLATE 옵션을 반환합니다. 옵션이 지원되지 않으면 GROUP **BY** 절은 데이터 원본에서 지원되지 않습니다.  
  
 SQL_IDENTIFIER_CASE(ODBC 1.0)  
 다음과 같은 SQLUSMALLINT 값은 다음과 같습니다.  
  
 SQL_IC_UPPER = SQL의 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그의 대문자로 저장됩니다.  
  
 SQL_IC_LOWER = SQL의 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그에 소문자로 저장됩니다.  
  
 SQL_IC_SENSITIVE = SQL의 식별자는 대/소문자를 구분하며 시스템 카탈로그의 혼합 대/소문자에 저장됩니다.  
  
 SQL_IC_MIXED = SQL의 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그의 혼합 케이스에 저장됩니다.  
  
 SQL-92의 식별자는 대/소문자를 구분하지 않으므로 SQL-92(모든 수준)를 엄격하게 준수하는 드라이버는 지원되는 SQL_IC_SENSITIVE 옵션을 반환하지 않습니다.  
  
 SQL_IDENTIFIER_QUOTE_CHAR(ODBC 1.0)  
 SQL 문에서 인용(구분) 식별자의 시작 및 종료 구분기호로 사용되는 문자열입니다. (ODBC 함수에 인수로 전달된 식별자는 인용할 필요가 없습니다.) 데이터 원본에서 인용된 식별자를 지원하지 않으면 공백이 반환됩니다.  
  
 이 문자열은 연결 특성 SQL_ATTR_METADATA_ID SQL_TRUE 설정된 경우 카탈로그 함수 인수를 인용하는 데도 사용할 수 있습니다.  
  
 SQL-92의 식별자 따옴표 문자는 이중 따옴표(")이므로 SQL-92를 엄격하게 준수하는 드라이버는 항상 double 따옴표 문자를 반환합니다.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 드라이버에서 지원하는 CREATE INDEX 문의 키워드를 여과하는 SQLUINTEGER 비트마스크입니다.  
  
 SQL_IK_NONE = 어떤 키워드도 지원되지 않습니다.  
  
 SQL_IK_ASC = ASC 키워드가 지원됩니다.  
  
 SQL_IK_DESC = DESC 키워드가 지원됩니다.  
  
 SQL_IK_ALL = 모든 키워드가 지원됩니다.  
  
 CREATE INDEX 문이 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_DLL_INDEX 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 드라이버에서 지원하는 INFORMATION_SCHEMA 뷰를 가리는 SQLUINTEGER 비트 마스크입니다. INFORMATION_SCHEMA 보기 및 내용은 SQL-92에 정의되어 있습니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 뷰를 결정하는 데 사용됩니다.  
  
 SQL_ISV_ASSERTIONS = 지정된 사용자가 소유한 카탈로그의 어설션을 식별합니다. (전체 레벨)  
  
 SQL_ISV_CHARACTER_SETS = 지정된 사용자가 액세스할 수 있는 카탈로그의 문자 집합을 식별합니다. (중급 수준)  
  
 SQL_ISV_CHECK_CONSTRAINTS = 지정된 사용자가 소유한 CHECK 제약 조건을 식별합니다. (중급 수준)  
  
 SQL_ISV_COLLATIONS = 지정된 사용자가 액세스할 수 있는 카탈로그의 문자 데이터 정렬을 식별합니다. (전체 레벨)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 카탈로그에 정의된 도메인에 종속되고 지정된 사용자가 소유한 카탈로그의 열을 식별합니다. (중급 수준)  
  
 SQL_ISV_COLUMN_PRIVILEGES = 지정된 사용자가 사용할 수 있거나 부여된 영구 테이블의 열에 대한 권한을 식별합니다. (FIPS 과도 수준)  
  
 SQL_ISV_COLUMNS = 지정된 사용자가 액세스할 수 있는 영구 테이블의 열을 식별합니다. (FIPS 과도 수준)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = CONSTRAINT_TABLE_USAGE 보기와 유사하게 지정된 사용자가 소유한 다양한 제약 조건에 대해 열이 식별됩니다. (중급 수준)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 제약 조건(참조, 고유 및 어설션)에서 사용되고 지정된 사용자가 소유하는 테이블을 식별합니다. (중급 수준)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 지정된 사용자가 액세스할 수 있는 도메인 제약 조건(카탈로그의 도메인)을 식별합니다. (중급 수준)  
  
 SQL_ISV_DOMAINS = 사용자가 액세스할 수 있는 카탈로그에 정의된 도메인을 식별합니다. (중급 수준)  
  
 SQL_ISV_KEY_COLUMN_USAGE = 지정된 사용자가 키로 제한된 카탈로그에 정의된 열을 식별합니다. (중급 수준)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 지정된 사용자가 소유한 참조 제약 조건을 식별합니다. (중급 수준)  
  
 SQL_ISV_SCHEMATA = 지정된 사용자가 소유한 스키마를 식별합니다. (중급 수준)  
  
 SQL_ISV_SQL_LANGUAGES = SQL 구현에서 지원하는 SQL 준수 수준, 옵션 및 방언을 식별합니다. (중급 수준)  
  
 SQL_ISV_TABLE_CONSTRAINTS = 지정된 사용자가 소유한 테이블 제약 조건을 식별합니다. (중급 수준)  
  
 SQL_ISV_TABLE_PRIVILEGES = 지정된 사용자가 사용할 수 있거나 부여된 영구 테이블의 권한을 식별합니다. (FIPS 과도 수준)  
  
 SQL_ISV_TABLES = 지정된 사용자가 액세스할 수 있는 카탈로그에 정의된 영구 테이블을 식별합니다. (FIPS 과도 수준)  
  
 SQL_ISV_TRANSLATIONS = 지정된 사용자가 액세스할 수 있는 카탈로그의 문자 번역을 식별합니다. (전체 레벨)  
  
 SQL_ISV_USAGE_PRIVILEGES = 지정된 사용자가 사용할 수 있거나 소유한 카탈로그 개체의 사용 권한을 식별합니다. (FIPS 과도 수준)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 지정된 사용자가 소유한 카탈로그 보기가 종속되는 열을 식별합니다. (중급 수준)  
  
 SQL_ISV_VIEW_TABLE_USAGE = 지정된 사용자가 소유한 카탈로그 보기가 종속되는 테이블을 식별합니다. (중급 수준)  
  
 SQL_ISV_VIEWS = 지정된 사용자가 액세스할 수 있는 이 카탈로그에 정의된 테이블이 정의되어 있는 테이블을 식별합니다. (FIPS 과도 수준)  
  
 SQL_INSERT_STATEMENT(ODBC 3.0)  
 **INSERT** 문에 대한 지원을 나타내는 SQLUINTEGER 비트 마스크:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_INTEGRITY(ODBC 1.0)  
 문자 문자열: 데이터 원본이 무결성 향상 기능을 지원하는 경우 "Y"; "N"이 아닌 경우.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_ODBC_SQL_OPT_IEF ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원하는 키 집합 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 특성의 첫 번째 하위 집합이 포함되어 있습니다. 두 번째 하위 집합의 경우 SQL_KEYSET_CURSOR_ATTRIBUTES2 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(설명에서 "동적 커서"에 대해 "키집합 기반 커서"로 대체)를 참조하십시오.  
  
 SQL-92 중간 수준 준수 드라이버는 일반적으로 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 지원 되는 반환, 드라이버는 포함 된 SQL FETCH 문을 통해 스크롤 가능한 커서를 지원 하기 때문에. 그러나 기본 SQL 지원을 직접 결정하지는 않으므로 SQL-92 중간 수준 준수 드라이버의 경우에도 스크롤 가능한 커서가 지원되지 않을 수 있습니다.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원하는 키 집합 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 두 번째 특성 하위 집합이 포함되어 있습니다. 첫 번째 하위 집합은 SQL_KEYSET_CURSOR_ATTRIBUTES1 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(설명에서 "동적 커서"에 대해 "키집합 기반 커서"로 대체)를 참조하십시오.  
  
 SQL_KEYWORDS(ODBC 2.0)  
 모든 데이터 원본 별 키워드의 쉼표 로 구분된 목록이 포함된 문자열입니다. 이 목록에는 ODBC와 관련된 키워드 또는 데이터 원본과 ODBC에서 모두 사용하는 키워드가 포함되어 있지 않습니다. 이 목록은 예약된 모든 키워드를 나타냅니다. 상호 운용 가능한 응용 프로그램은 개체 이름에 이러한 단어를 사용해서는 안 됩니다.  
  
 ODBC 키워드 목록은 [부록 C: SQL 문법의](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) [예약 키워드를](../../../odbc/reference/appendixes/reserved-keywords.md) 참조하십시오. **SQL_ODBC_KEYWORDS #define** 값에는 ODBC 키워드의 쉼표로 구분된 목록이 포함되어 있습니다.  
  
 부록 C: SQL 문법  
  
 SQL_LIKE_ESCAPE_CLAUSE(ODBC 2.0)  
 문자 문자열: 데이터 원본이 백분율 문자에 대한 이스케이프 문자를 지원하는 경우 "Y"(%) 및 **LIKE** 조건자에서 문자(_)를 강조하고 드라이버는 **LIKE** 조건자 이스케이프 문자를 정의하기 위한 ODBC 구문을 지원합니다. 그렇지 않으면 "N".  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 드라이버가 지정된 연결에서 지원할 수 있는 비동기 모드에서 활성 동시 문의 최대 수를 지정하는 SQLUINTEGER 값입니다. 특정 제한이 없거나 제한을 알 수 없는 경우 이 값은 0입니다.  
  
 SQL_MAX_BINARY_LITERAL_LEN(ODBC 2.0)  
 SQL 문에서 이진 리터럴의 최대 **길이(SQLGetTypeInfo에서**반환되는 리터럴 접두사 및 접미사를 제외한 헥사드문자 수)를 지정하는 SQLUINTEGER 값입니다. 예를 들어, 이진 리터럴 0xFFAA의 길이는 4입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_CATALOG_NAME_LEN(ODBC 1.0)  
 데이터 원본에서 카탈로그 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 전체 레벨 준수 드라이버가 최소 128을 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_MAX_QUALIFIER_NAME_LEN ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 SQL 문에서 문자 리터럴의 최대 **길이(SQLGetTypeInfo에서**반환되는 문자 접두사 및 접미사를 제외한 문자 수)를 지정하는 SQLUINTEGER 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_COLUMN_NAME_LEN(ODBC 1.0)  
 데이터 원본에서 열 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 18을 반환합니다. FIPS 중급 레벨 준수 드라이버는 적어도 128을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY(ODBC 2.0)  
 **그룹 BY** 절에서 허용되는 최대 열 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버가 6개 이상 반환됩니다. FIPS 중급 레벨 준수 드라이버가 15개 이상 반환됩니다.  
  
 SQL_MAX_COLUMNS_IN_INDEX(ODBC 2.0)  
 인덱스에서 허용되는 최대 열 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY(ODBC 2.0)  
 **ORDER BY** 절에서 허용되는 최대 열 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버가 6개 이상 반환됩니다. FIPS 중급 레벨 준수 드라이버가 15개 이상 반환됩니다.  
  
 SQL_MAX_COLUMNS_IN_SELECT(ODBC 2.0)  
 선택 목록에서 허용되는 최대 열 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버가 100개 이상 반환됩니다. FIPS 중급 레벨 준수 드라이버가 250개 이상 반환됩니다.  
  
 SQL_MAX_COLUMNS_IN_TABLE(ODBC 2.0)  
 테이블에서 허용되는 최대 열 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버가 100개 이상 반환됩니다. FIPS 중급 레벨 준수 드라이버가 250개 이상 반환됩니다.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES(ODBC 1.0)  
 드라이버가 연결을 지원할 수 있는 최대 활성 문의 수를 지정하는 SQLUSMALLINT 값입니다. 문은 결과가 보류 중인 경우, **SELECT** 작업의 행을 의미하는 "결과"라는 용어또는 **INSERT,** **UPDATE**또는 **DELETE** 작업의 영향을 받는 행(예: 행 수)의 영향을 받거나 NEED_DATA 상태인 경우 활성으로 정의됩니다. 이 값은 드라이버 또는 데이터 원본에 의해 부과된 제한을 반영할 수 있습니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_ACTIVE_STATEMENTS ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_MAX_CURSOR_NAME_LEN(ODBC 1.0)  
 데이터 원본에서 커서 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 18을 반환합니다. FIPS 중급 레벨 준수 드라이버는 적어도 128을 반환합니다.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 드라이버가 환경에 대해 지원할 수 있는 최대 활성 연결 수를 지정하는 SQLUSMALLINT 값입니다. 이 값은 드라이버 또는 데이터 원본에 의해 부과된 제한을 반영할 수 있습니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_ACTIVE_CONNECTIONS ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 데이터 원본이 사용자 정의 이름에 대해 지원하는 문자의 최대 크기를 나타내는 SQLUSMALLINT입니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 18을 반환합니다. FIPS 중급 레벨 준수 드라이버는 적어도 128을 반환합니다.  
  
 SQL_MAX_INDEX_SIZE(ODBC 2.0)  
 인덱스의 결합된 필드에 허용되는 최대 바이트 수를 지정하는 SQLUINTEGER 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 데이터 원본에서 프로시저 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 테이블에서 단일 행의 최대 길이를 지정하는 SQLUINTEGER 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 2,000명의 드라이버를 반환합니다. FIPS 중급 레벨 준수 드라이버는 최소 8,000명의 드라이버를 반환합니다.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG(ODBC 3.0)  
 문자열 문자열: SQL_MAX_ROW_SIZE 정보 형식에 대해 반환되는 최대 행 크기가 행의 모든 SQL_LONGVARCHAR 및 SQL_LONGVARBINARY 열의 길이를 포함하는 경우 "Y"입니다. 그렇지 않으면 "N".  
  
 SQL_MAX_SCHEMA_NAME_LEN(ODBC 1.0)  
 데이터 원본에서 스키마 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 18을 반환합니다. FIPS 중급 레벨 준수 드라이버는 적어도 128을 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_MAX_OWNER_NAME_LEN ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_MAX_STATEMENT_LEN(ODBC 2.0)  
 SQL 문의 최대 길이(공백을 포함한 문자 수)를 지정하는 SQLUINTEGER 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MAX_TABLE_NAME_LEN(ODBC 1.0)  
 데이터 원본에서 테이블 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버는 최소 18을 반환합니다. FIPS 중급 레벨 준수 드라이버는 적어도 128을 반환합니다.  
  
 SQL_MAX_TABLES_IN_SELECT(ODBC 2.0)  
 **SELECT** 문의 **FROM** 절에서 허용되는 최대 테이블 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 FIPS 엔트리 레벨 준수 드라이버가 15명 이상 반환됩니다. FIPS 중급 레벨 준수 드라이버가 50개 이상 반환됩니다.  
  
 SQL_MAX_USER_NAME_LEN(ODBC 2.0)  
 데이터 원본에서 사용자 이름의 최대 길이를 지정하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_MULT_RESULT_SETS(ODBC 1.0)  
 문자 문자열: 데이터 원본이 여러 결과 집합을 지원하는 경우 "Y", 그렇지 않은 경우 "N"입니다.  
  
 여러 결과 집합에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 SQL_MULTIPLE_ACTIVE_TXN(ODBC 1.0)  
 문자 문자열: 드라이버가 동시에 두 개 이상의 활성 트랜잭션을 지원하는 경우 "Y", "N"은 언제든지 하나의 트랜잭션만 활성화할 수 있는 경우입니다.  
  
 분산 트랜잭션의 경우 이 정보 유형에 대해 반환된 정보는 적용되지 않습니다.  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 문자열: 데이터 원본에 긴 데이터 값(데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 별 데이터 형식)의 길이가 필요한 경우 해당 값이 데이터 원본으로 전송되기 전에 "N"입니다. 자세한 내용은 [SQLBind매개 변수 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md) 및 [SQLSetPos 함수를](../../../odbc/reference/syntax/sqlsetpos-function.md)참조하십시오.  
  
 SQL_NON_NULLABLE_COLUMNS(ODBC 1.0)  
 데이터 원본이 열에서 NOT NULL을 지원하는지 여부를 지정하는 SQLUSMALLINT 값입니다.  
  
 SQL_NNC_NULL = 모든 열은 null이어야 합니다.  
  
 SQL_NNC_NON_NULL = 열은 null 수 없습니다. 데이터 원본은 **CREATE TABLE** 문에서 **NOT NULL** 열 제약 조건을 지원합니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버가 SQL_NNC_NON_NULL 반환합니다.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 NULL이 결과 집합에서 정렬되는 위치를 지정하는 SQLUSMALLINT 값입니다.  
  
 SQL_NC_END = NULL은 ASC 또는 DESC 키워드에 관계없이 결과 집합의 끝에 정렬됩니다.  
  
 SQL_NC_HIGH = NULL은 ASC 또는 DESC 키워드에 따라 결과 집합의 하이엔드에서 정렬됩니다.  
  
 SQL_NC_LOW = NULL은 ASC 또는 DESC 키워드에 따라 결과 집합의 로우엔드에서 정렬됩니다.  
  
 SQL_NC_START = NULL은 ASC 또는 DESC 키워드에 관계없이 결과 집합의 시작 부분에 정렬됩니다.  
  
 SQL_NUMERIC_FUNCTIONS(ODBC 1.0)  
 참고: 정보 유형은 ODBC 1.0에 도입되었습니다. 각 비트마스크는 도입된 버전으로 레이블이 지정됩니다.  
  
 드라이버 및 관련 데이터 원본에서 지원하는 스칼라 숫자 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 지원되는 숫자 함수를 결정하는 데 사용됩니다.  
  
 SQL_FN_NUM_ABS(ODBC 1.0)SQL_FN_NUM_ACOS(ODBC 1.0)SQL_FN_NUM_ASIN(ODBC 1.0)SQL_FN_NUM_ATAN(ODBC 1.0)SQL_FN_NUM_ATAN2(ODBC 1.0)SQL_FN_NUM_CEILING(ODBC 1.0)SQL_FN_NUM_COS(ODBC 1.0)SQL_FN_NUM_COT SQL_FN_NUM_COS(ODBC 1.0)SQL_FN_NUM_DEGREES(ODBC 1.0)SQL_FN_NUM_EXP(ODBC 1.0)SQL_FN_NUM_FLOOR SQL_FN_NUM_LOG(SQL_FN_ SQL_FN_NUM_LOG10 ODBC 1.0)SQL_FN_NUM_LOG NUM_MOD (ODBC 1.0)SQL_FN_NUM_PI (ODBC 1.0)SQL_FN_NUM_POWER (ODBC 2.0)SQL_FN_NUM_RADIANS (ODBC 2.0)SQL_FN_NUM_RAND (ODBC 2.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_SIGN SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SQRT SQL_FN_NUM_TAN (ODBC 1.0)SQL_FN_NUM_TRUNCATE  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 드라이버가 준수하는 ODBC*3.x* 인터페이스의 수준을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_OIC_CORE: 모든 ODBC 드라이버가 준수해야 하는 최소 수준입니다. 이 수준에는 연결 함수, SQL 문을 준비하고 실행하기 위한 함수, 기본 결과 집합 메타데이터 함수, 기본 카탈로그 함수 등과 같은 기본 인터페이스 요소가 포함됩니다.  
  
 SQL_OIC_LEVEL1: 핵심 표준 규정 준수 수준 기능과 스크롤 가능한 커서, 북마크, 위치 업데이트 및 삭제 등을 포함한 수준입니다.  
  
 SQL_OIC_LEVEL2: 레벨 1 표준 준수 수준 기능 및 민감한 커서와 같은 고급 기능을 포함하는 수준; 북마크별로 업데이트, 삭제 및 새로 고침; 저장 절차 지원; 기본 및 외래 키에 대한 카탈로그 기능; 다중 카탈로그 지원; 등등.  
  
 자세한 내용은 [인터페이스 적합성 수준을](../../../odbc/reference/develop-app/interface-conformance-levels.md)참조하십시오.  
  
 SQL_ODBC_VER(ODBC 1.0)  
 드라이버 관리자가 준수하는 ODBC 버전이 있는 문자열입니다. 버전은 처음 두 자리가 주 버전이고 다음 두 자리는 부 버전인 ###.0000 양식입니다. 이 방법은 드라이버 관리자에서만 구현됩니다.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 드라이버 및 데이터 원본에서 지원하는 외부 조인 유형을 예인하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 지원되는 형식을 결정하는 데 사용됩니다.  
  
 SQL_OJ_LEFT = 왼쪽 외부 조인이 지원됩니다.  
  
 SQL_OJ_RIGHT = 오른쪽 외부 조인이 지원됩니다.  
  
 SQL_OJ_FULL = 전체 외부 조인이 지원됩니다.  
  
 SQL_OJ_NESTED = 중첩된 외부 조인이 지원됩니다.  
  
 SQL_OJ_NOT_ORDERED = 외부 조인의 ON 절에 있는 열 이름은 **OUTER JOIN** 절의 해당 테이블 이름과 동일한 순서일 필요가 없습니다.  
  
 SQL_OJ_INNER = 내부 조인(왼쪽 외부 조인의 오른쪽 테이블 또는 오른쪽 외부 조인의 왼쪽 테이블)도 내부 조인에 사용할 수 있습니다. 내부 테이블이 없는 전체 외부 조인에는 적용되지 않습니다.  
  
 SQL_OJ_ALL_COMPARISON_OPS = ON 절의 비교 연산자는 ODBC 비교 연산자 중 어느 일 수 있습니다. 이 비트가 설정되지 않은 경우 외부 조인에서 equals(=) 비교 연산자만 사용할 수 있습니다.  
  
 이러한 옵션이 지원되는 대로 반환되지 않으면 외부 join 절이 지원되지 않습니다.  
  
 SQL-92에 정의된 SELECT 문의 관계형 조인 연산자 지원에 대한 자세한 내용은 SQL_SQL92_RELATIONAL_JOIN_OPERATORS 참조하세요.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT(ODBC 2.0)  
 문자열 문자열: **ORDER BY** 절의 열이 선택 목록에 있어야 하는 경우 "Y"입니다. 그렇지 않으면 "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS(ODBC 3.0)  
 매개 변수화된 실행에서 행 개수의 가용성과 관련하여 드라이버 의 속성을 열거하는 SQLUINTEGER입니다. 다음 값이 있습니다.  
  
 SQL_PARC_BATCH = 각 매개변수 집합에 대해 개별 행 수를 사용할 수 있습니다. 이는 개념적으로 배열에 설정된 각 매개 변수에 대해 하나씩 SQL 문의 일괄 처리를 생성하는 드라이버와 동일합니다. 확장 된 오류 정보는 SQL_PARAM_STATUS_PTR 설명자 필드를 사용 하 여 검색할 수 있습니다.  
  
 SQL_PARC_NO_BATCH = 사용 가능한 행 수는 하나뿐이며, 이는 전체 매개 변수 배열에 대한 명령문 실행으로 인한 누적 행 수입니다. 이는 개념적으로 전체 매개 변수 배열과 함께 문을 하나의 원자 단위로 처리하는 것과 동일합니다. 오류는 하나의 문이 실행된 경우와 동일하게 처리됩니다.  
  
 SQL_PARAM_ARRAY_SELECTS(ODBC 3.0)  
 결과 집합의 가용성에 관한 드라이버의 속성을 매개 변수로 만든 실행에서 등록하는 SQLUINTEGER입니다. 다음 값이 있습니다.  
  
 SQL_PAS_BATCH = 매개 변수 집합당 사용할 수 있는 하나의 결과 집합이 있습니다. 이는 개념적으로 배열에 설정된 각 매개 변수에 대해 하나씩 SQL 문의 일괄 처리를 생성하는 드라이버와 동일합니다.  
  
 SQL_PAS_NO_BATCH = 전체 매개 변수 배열에 대한 명령문 실행으로 인한 누적 결과 집합을 나타내는 결과 집합이 하나만 있습니다. 이는 개념적으로 전체 매개 변수 배열과 함께 문을 하나의 원자 단위로 처리하는 것과 동일합니다.  
  
 SQL_PAS_NO_SELECT = 드라이버는 매개 변수 배열로 결과 집합 생성 문을 실행할 수 없습니다.  
  
 SQL_PROCEDURE_TERM(ODBC 1.0)  
 프로시저에 대한 데이터 원본 공급업체의 이름이 있는 문자열입니다. 예를 들어 "데이터베이스 프로시저", "저장 프로시저", "프로시저", "패키지" 또는 "저장된 쿼리"를 예로 들 수 있습니다.  
  
 SQL_PROCEDURES(ODBC 1.0)  
 문자 문자열: 데이터 원본이 프로시저를 지원하고 드라이버가 ODBC 프로시저 호출 구문을 지원하는 경우 "Y"입니다. 그렇지 않으면 "N".  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 **SQLSetPos의**지원 작업을 예인하는 SQLINTEGER 비트 마스크.  
  
 다음 비트마스크는 플래그와 함께 사용되어 지원되는 옵션을 결정합니다.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE(ODBC 2.0)  
 다음과 같은 SQLUSMALLINT 값은 다음과 같습니다.  
  
 SQL_IC_UPPER = SQL의 quoted 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그의 대문자로 저장됩니다.  
  
 SQL_IC_LOWER = SQL의 quoted 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그에 소문자로 저장됩니다.  
  
 SQL_IC_SENSITIVE = SQL의 quoted 식별자는 대/소문자를 구분하며 시스템 카탈로그의 혼합 대/소문자에 저장됩니다. SQL-92를 준수하는 데이터베이스에서는 항상 대/소문자를 구분합니다.  
  
 SQL_IC_MIXED = SQL의 quoted 식별자는 대/소문자를 구분하지 않으며 시스템 카탈로그의 혼합 대/소문자에 저장됩니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 SQL_IC_SENSITIVE 반환합니다.  
  
 SQL_ROW_UPDATES(ODBC 1.0)  
 문자 문자열: 키집합 기반 또는 혼합 커서가 가져온 모든 행에 대해 행 버전 또는 값을 유지 관리하므로 행이 마지막으로 인출된 이후 모든 사용자가 행에 대해 수행한 업데이트를 검색할 수 있는 경우 "Y"입니다. (삭제 또는 삽입이 아닌 업데이트에만 적용됩니다.) 드라이버는 **SQLFetchScroll가** 호출될 때 행 상태 배열에 SQL_ROW_UPDATED 플래그를 반환할 수 있습니다. 그렇지 않으면 "N"입니다.  
  
 SQL_SCHEMA_TERM(ODBC 1.0)  
 스키마에 대한 데이터 원본 공급업체의 이름이 있는 문자열입니다. 예를 들어 "소유자", "권한 부여 ID" 또는 "스키마"를 예로 들 수 있습니다.  
  
 문자 문자열은 상위, 하부 또는 혼합 대/소문자로 반환할 수 있습니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 "스키마"를 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_OWNER_TERM ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_SCHEMA_USAGE(ODBC 2.0)  
 스키마를 사용할 수 있는 문을 열거하는 SQLUINTEGER 비트 마스크는 다음과 같이 합니다.  
  
 SQL_SU_DML_STATEMENTS = 스키마는 모든 데이터 조작 언어 문에서 지원됩니다: **SELECT,** **INSERT,** **UPDATE**, **DELETE**및 지원되는 경우 업데이트 및 위치 업데이트 및 삭제 문을 **선택합니다.**  
  
 SQL_SU_PROCEDURE_INVOCATION = 스키마는 ODBC 프로시저 호출 문에서 지원됩니다.  
  
 SQL_SU_TABLE_DEFINITION = 스키마는 테이블 **만들기,** 보기 **만들기, 테이블** **변경,** **드롭 테이블**및 **DROP VIEW의**모든 테이블 정의 문에서 지원됩니다.  
  
 SQL_SU_INDEX_DEFINITION = 스키마는 모든 인덱스 정의 문에서 지원됩니다: **인덱스 만들기** 및 **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = 스키마는 모든 권한 정의 명령문에서 지원됩니다: **GRANT** 및 **해지**.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로 SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION 및 SQL_SU_PRIVILEGE_DEFINITION 옵션을 반환합니다.  
  
 이 *InfoType은* ODBC 2.0 *infoType* SQL_OWNER_USAGE ODBC 3.0의 이름이 바뀌었습니다.  
  
 SQL_SCROLL_OPTIONS(ODBC 1.0)  
 참고: 정보 유형은 ODBC 1.0에 도입되었습니다. 각 비트마스크는 도입된 버전으로 레이블이 지정됩니다.  
  
 스크롤 가능한 커서에 지원되는 스크롤 옵션을 가리는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 지원되는 옵션을 결정하는 데 사용됩니다.  
  
 SQL_SO_FORWARD_ONLY = 커서가 앞으로만 스크롤됩니다. (ODBC 1.0)  
  
 SQL_SO_STATIC = 결과 집합의 데이터는 정적입니다. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 드라이버가 결과 집합의 모든 행에 대한 키를 저장하고 사용합니다. (ODBC 1.0)  
  
 SQL_SO_DYNAMIC = 드라이버는 행 집합의 모든 행에 대한 키를 유지합니다(키 집합 크기는 행 집합 크기와 동일합니다). (ODBC 1.0)  
  
 SQL_SO_MIXED = 드라이버는 키 집합의 모든 행에 대한 키를 유지하고 키 집합 크기는 행 집합 크기보다 큽습니다. 커서는 키집합 내부에서 키집합을 기반으로 하며 키 집합 외부에서 동적입니다. (ODBC 1.0)  
  
 스크롤 가능한 커서에 대한 자세한 내용은 [스크롤 가능한 커서 를](../../../odbc/reference/develop-app/scrollable-cursors.md)참조하십시오.  
  
 SQL_SEARCH_PATTERN_ESCAPE(ODBC 1.0)  
 패턴 일치 메타 문자 밑줄(_) 및 백분율 기호(%)를 사용할 수 있는 이스케이프 문자로 드라이버가 지원하는 것을 지정하는 문자 문자열 검색 패턴에서 유효한 문자로 표시됩니다. 이 이스케이프 문자는 검색 문자열을 지원하는 카탈로그 함수 인수에만 적용됩니다. 이 문자열이 비어 있으면 드라이버는 검색 패턴 이스케이프 문자를 지원하지 않습니다.  
  
 이 정보 형식은 **LIKE** 조건자에서 이스케이프 문자에 대한 일반적인 지원을 나타내지 않으므로 SQL-92에는 이 문자 문자열에 대한 요구 사항이 포함되지 않습니다.  
  
 이 *InfoType은* 카탈로그 기능으로 제한됩니다. 검색 패턴 문자열에서 이스케이프 문자의 사용에 대한 설명은 [패턴 값 인수를](../../../odbc/reference/develop-app/pattern-value-arguments.md)참조하십시오.  
  
 SQL_SERVER_NAME(ODBC 1.0)  
 실제 데이터 원본별 서버 이름이 있는 문자열입니다. **SQLConnect,** **SQLDriverConnect**및 **SQLBrowseConnect**에서 데이터 원본 이름을 사용할 때 유용합니다.  
  
 SQL_SPECIAL_CHARACTERS(ODBC 2.0)  
 데이터 원본에서 테이블 이름, 열 이름 또는 인덱스 이름과 같은 식별자 이름에 사용할 수 있는 모든 특수 문자(즉, z, A~ Z, 0 ~ 9 및 밑줄)를 제외한 모든 특수 문자가 포함된 문자열입니다. 예를 들어 "#$^"입니다. 식별자가 이러한 문자 중 하나 이상을 포함하는 경우 식별자는 구분된 식별자여야 합니다.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 드라이버에서 지원하는 SQL-92 수준을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_SC_SQL92_ENTRY = 엔트리 레벨 SQL-92 를 준수합니다.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 과도 수준 준수.  
  
 SQL_SC_SQL92_FULL = 전체 수준의 SQL-92를 준수합니다.  
  
 SQL_SC_ SQL92_INTERMEDIATE = 중간 수준의 SQL-92 를 준수합니다.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 SQL-92에 정의된 대로 드라이버 및 관련 데이터 원본에서 지원하는 datetime 스칼라 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 datetime 함수를 결정하는 데 사용됩니다.  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 SQL-92에 정의된 대로 **DELETE** 문에서 외부 키에 대해 지원되는 규칙을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 절을 결정하는 데 사용됩니다.  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 전환 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 SQL-92에 정의된 대로 **UPDATE** 문에서 외래 키에 대해 지원되는 규칙을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 절을 결정하는 데 사용됩니다.  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL-92 전체 수준 준수 드라이버는 항상 지원 되는 이러한 모든 옵션을 반환 합니다.  
  
 SQL_SQL92_GRANT (ODBC 3.0)  
 SQL-92에 정의된 대로 **GRANT** 문에서 지원되는 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 절을 결정하는 데 사용됩니다.  
  
 SQL_SG_DELETE_TABLE(엔트리 레벨)SQL_SG_INSERT_COLUMN(엔트리 레벨)SQL_SG_INSERT_TABLE(엔트리 레벨) SQL_SG_REFERENCES_TABLE(엔트리 레벨)SQL_SG_REFERENCES_COLUMN(엔트리 레벨)SQL_SG_SELECT_TABLE(엔트리 레벨)SQL_SG_UPDATE_COLUMN(엔트리 레벨)SQL_SG_UPDATE_TABLE(엔트리 레벨) SQL_SG_USAGE_ON_DOMAIN(FIPS 과도 수준)SQL_SG_USAGE_ON_CHARACTER_SET(FIPS 과도 수준)SQL_SG_USAGE_ON_COLLATION(FIPS 과도 수준)SQL_SG_USAGE_ON_TRANSLATION 레벨)SQL_SG_WITH_GRANT_OPTION (엔트리 레벨)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3.0)  
 SQL-92에 정의된 대로 드라이버 및 관련 데이터 원본에서 지원하는 숫자 값 스칼라 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 지원되는 숫자 함수를 결정하는 데 사용됩니다.  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 SQL-92에 정의된 대로 **SELECT** 문에서 지원되는 조건어를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 옵션을 결정하는 데 사용됩니다.  
  
 SQL_SP_BETWEEN(엔트리 레벨)SQL_SP_COMPARISON(엔트리 레벨)SQL_SP_EXISTS(엔트리 레벨)SQL_SP_IN SQL_SP_ISNOTNULL(엔트리 레벨)SQL_SP_ISNOTNULL(엔트리 레벨)SQL_SP_ISNULL(엔트리 레벨)SQL_SP_MATCH_FULL(엔트리 레벨 SQL_SP_LIKE)SQL_SP_MATCH_FULL(엔트리 레벨)SQL_SP_MATCH_PARTIAL SQL_SP_MATCH_FULL(전체 레벨)SQL_SP_MATCH_UNIQUE_FULL SQL_SP_MATCH_UNIQUE_PARTIAL(전체 SQL_SP_OVERLAPS 레벨)SQL_SP_MATCH_UNIQUE_PARTIAL(FIPS 과도 수준)SQL_SP_QUANTIFIED_COMPARISON SQL_SP_UNIQUE (엔트리 레벨)SQL_SP_UNIQUE  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS (ODBC 3.0)  
 SQL-92에 정의된 대로 **SELECT** 문에서 지원되는 관계형 조인 연산자를 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 옵션을 결정하는 데 사용됩니다.  
  
 SQL_SRJO_CORRESPONDING_CLAUSE(중간 수준)SQL_SRJO_CROSS_JOIN(중간 수준)SQL_SRJO_EXCEPT_JOIN(중간 수준)SQL_SRJO_FULL_OUTER_JOIN(중간 수준) SQL_SRJO_INNER_JOIN(중급 수준)SQL_SRJO_INTERSECT_JOIN(중급 수준)SQL_SRJO_LEFT_OUTER_JOIN(FIPS 과도 수준)SQL_SRJO_NATURAL_JOIN(FIPS 과도 수준)SQL_SRJO_RIGHT_OUTER_JOIN(FIPS 과도 수준)SQL_SRJO_UNION_JOIN(전체 수준)  
  
 SQL_SRJO_INNER_JOIN **내부 조인** 기능이 아니라 INNER JOIN 구문에 대한 지원을 나타냅니다. **내부 조인** 구문에 대한 지원은 FIPS 전환이며 내부 조인 기능에 대한 지원은 **ENTRY입니다.**  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **해지** 문에서 지원되는 절을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 절을 결정하는 데 사용됩니다.  
  
 SQL_SR_CASCADE(FIPS 과도수준) SQL_SR_DELETE_TABLE(엔트리 레벨)SQL_SR_GRANT_OPTION_FOR(중간 수준) SQL_SR_INSERT_COLUMN(중간 수준)SQL_SR_INSERT_TABLE(엔트리 레벨)SQL_SR_REFERENCES_COLUMN(엔트리 레벨)SQL_SR_REFERENCES_TABLE(엔트리 레벨)SQL_SR_RESTRICT(엔트리 레벨)SQL_SR_SELECT_TABLE(엔트리 레벨)SQL_SR_UPDATE_COLUMN SQL_SR_UPDATE_TABLE(엔트리 레벨)SQL_SR_USAGE_ON_DOMAIN(FIPS 과도기 수준)SQL_SR_USAGE_ON_CHARACTER_ SET(FIPS 과도 수준)SQL_SR_USAGE_ON_COLLATION(FIPS 과도 수준)SQL_SR_USAGE_ON_TRANSLATION(FIPS 과도 수준)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 SQL-92에 정의된 대로 **SELECT** 문에서 지원되는 행 값 생성자 식을 열거하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 데이터 원본에서 지원하는 옵션을 결정하는 데 사용됩니다.  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS (ODBC 3.0)  
 SQL-92에 정의된 대로 드라이버 및 관련 데이터 원본에서 지원하는 문자열 스칼라 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 문자열 함수를 결정하는 데 사용됩니다.  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 SQL-92에 정의된 대로 지원되는 값 식을 영예하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 데이터 원본에서 지원하는 옵션을 결정하는 데 사용됩니다.  
  
 SQL_SVE_CASE(중급 수준)SQL_SVE_CAST(FIPS 과도 수준)SQL_SVE_COALESCE(중급 수준)SQL_SVE_NULLIF  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 드라이버가 준수하는 CLI 표준 또는 표준을 예인하는 SQLUINTEGER 비트 마스크입니다. 다음 비트마스크는 드라이버가 준수하는 수준을 결정하는 데 사용됩니다.  
  
 SQL_SCC_XOPEN_CLI_VERSION1: 드라이버는 오픈 그룹 CLI 버전 1을 준수합니다.  
  
 SQL_SCC_ISO92_CLI: 드라이버는 ISO 92 CLI를 준수합니다.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원하는 정적 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 특성의 첫 번째 하위 집합이 포함되어 있습니다. 두 번째 하위 집합의 경우 SQL_STATIC_CURSOR_ATTRIBUTES2 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(설명에서 "동적 커서"로 "정적 커서"로 대체)를 참조하십시오.  
  
 SQL-92 중간 수준 준수 드라이버는 일반적으로 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 지원 되는 반환, 드라이버는 포함 된 SQL FETCH 문을 통해 스크롤 가능한 커서를 지원 하기 때문에. 그러나 기본 SQL 지원을 직접 결정하지는 않으므로 SQL-92 중간 수준 준수 드라이버의 경우에도 스크롤 가능한 커서가 지원되지 않을 수 있습니다.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 드라이버에서 지원하는 정적 커서의 특성을 설명하는 SQLUINTEGER 비트 마스크입니다. 이 비트마스크에는 두 번째 특성 하위 집합이 포함되어 있습니다. 첫 번째 하위 집합은 SQL_STATIC_CURSOR_ATTRIBUTES1 참조하십시오.  
  
 다음 비트마스크는 지원되는 특성을 결정하는 데 사용됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 이러한 비트 마스크에 대한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(설명에서 "동적 커서"로 "정적 커서"로 대체)를 참조하십시오.  
  
 SQL_STRING_FUNCTIONS(ODBC 1.0)  
 참고: 정보 유형은 ODBC 1.0에 도입되었습니다. 각 비트마스크는 도입된 버전으로 레이블이 지정됩니다.  
  
 드라이버 및 관련 데이터 원본에서 지원하는 스칼라 문자열 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 문자열 함수를 결정하는 데 사용됩니다.  
  
 SQL_FN_STR_ASCII(ODBC 1.0)SQL_FN_STR_BIT_LENGTH(ODBC 3.0)SQL_FN_STR_CHAR(ODBC 3.0)SQL_FN_STR_CHAR_LENGTH(ODBC 3.0)SQL_FN_STR_CHARACTER_LENGTH(ODBC 3.0)SQL_FN_STR_CONCAT(ODBC 3.0)SQL_FN_STR_DIFFERENCE(ODBC 1.0)SQL_FN_STR_INSERT(ODBC 1.0)SQL_FN_STR_LCASE(ODBC 1.0)SQL_FN_STR_LEFT(ODBC 1.0)SQL_FN_STR_LENGTH SQL_FN_STR_LOCATE(ODBC 1.0 SQL_FN_STR_LTRIM)SQL_FN_STR_LOCATE 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 응용 프로그램이 *string_exp1* *string_exp2*및 시작 인수를 사용하여 **LOCATE** 스칼라 함수를 호출하고 인수를 *시작할* 수 있는 경우 드라이버는 SQL_FN_STR_LOCATE 비트 마스크를 반환합니다. 응용 프로그램이 *string_exp1* 및 *string_exp2* 인수만 사용하여 LOCATE 스칼라 함수를 호출할 수 있는 경우 드라이버는 SQL_FN_STR_LOCATE_2 비트마스크를 반환합니다. **LOCATE** 스칼라 기능을 완전히 지원하는 드라이버는 두 비트마스크를 모두 반환합니다.  
  
 자세한 내용은 부록 [E의 문자열 함수,](../../../odbc/reference/appendixes/string-functions.md) "스칼라 함수"를 참조하십시오.  
  
 SQL_SUBQUERIES(ODBC 2.0)  
 하위 쿼리를 지원하는 조건자 열거하는 SQLUINTEGER 비트 마스크:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES 비트 마스크는 하위 쿼리를 지원하는 모든 술어가 상관 하위 쿼리를 지원한다는 것을 나타냅니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 이러한 모든 비트가 설정된 비트 마스크를 반환합니다.  
  
 SQL_SYSTEM_FUNCTIONS(ODBC 1.0)  
 드라이버 및 관련 데이터 원본에서 지원하는 스칼라 시스템 기능을 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 지원되는 시스템 함수를 결정하는 데 사용됩니다.  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM(ODBC 1.0)  
 테이블에 대 한 데이터 원본 공급 업체의 이름이 있는 문자열; 예를 들어 "테이블" 또는 "파일"을 예로 들 수 있습니다.  
  
 이 문자열은 상위, 하부 또는 혼합 대/소문자에 있을 수 있습니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 "테이블"을 반환합니다.  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 타임스탬프ADD 스칼라 함수에 대해 드라이버 및 관련 데이터 원본에서 지원하는 타임스탬프 간격을 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 간격을 결정하는 데 사용됩니다.  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 전환 레벨 준수 드라이버는 항상 이러한 모든 비트가 설정된 비트 마스크를 반환합니다.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 TIMESTAMPDIFF 스칼라 함수에 대한 드라이버 및 관련 데이터 원본에서 지원하는 타임스탬프 간격을 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 간격을 결정하는 데 사용됩니다.  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 전환 레벨 준수 드라이버는 항상 이러한 모든 비트가 설정된 비트 마스크를 반환합니다.  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 참고: 정보 유형은 ODBC 1.0에 도입되었습니다. 각 비트마스크는 도입된 버전으로 레이블이 지정됩니다.  
  
 드라이버 및 관련 데이터 원본에서 지원하는 스칼라 날짜 및 시간 함수를 열거하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원되는 날짜 및 시간 함수를 결정하는 데 사용됩니다.  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0)SQL_FN_TD_CURRENT_TIME (ODBC 3.0)SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0)SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK (ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR SQL_FN_TD_MINUTE (ODBC 1.0 SQL_FN_TD_MONTH)SQL_FN_TD_MINUTE 1.0)SQL_FN_TD_MONTHNAME(ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0)SQL_FN_TD_QUARTER (ODBC 1.0)SQL_FN_TD_SECOND (ODBC 1.0)SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE(ODBC 1.0)  
 참고: 정보 유형은 ODBC 1.0에 도입되었습니다. 각 반환 값은 도입된 버전으로 레이블이 지정됩니다.  
  
 드라이버 또는 데이터 원본의 트랜잭션 지원을 설명하는 SQLUSMALLINT 값:  
  
 SQL_TC_NONE = 트랜잭션이 지원되지 않습니다. (ODBC 1.0)  
  
 SQL_TC_DML = 트랜잭션에는 DML(데이터 조작 언어) 문만 포함할 수**있습니다(SELECT**, **INSERT**, **UPDATE**, **DELETE).** 트랜잭션에서 발생한 DDL(데이터 정의 언어) 명령문은 오류를 일으킵니다. (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = 트랜잭션에는 DML 문만 포함될 수 있습니다. 트랜잭션에서 발생하는 DDL**문(테이블**만들기, **DROP INDEX**등)은 트랜잭션을 커밋합니다. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 트랜잭션에는 DML 문만 포함될 수 있습니다. 트랜잭션에서 발생한 DDL 문은 무시됩니다. (ODBC 2.0)  
  
 SQL_TC_ALL = 트랜잭션에는 DDL 문과 DML 문이 임의의 순서로 포함될 수 있습니다. (ODBC 1.0)  
  
 (SQL-92에서는 트랜잭션 지원이 필수이므로 SQL-92 준수 드라이버[모든 수준]는 SQL_TC_NONE 반환되지 않습니다.)  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 드라이버 또는 데이터 원본에서 사용할 수 있는 트랜잭션 격리 수준을 예인하는 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트마스크는 플래그와 함께 사용되어 지원되는 옵션을 결정합니다.  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 이러한 격리 수준에 대한 설명은 SQL_DEFAULT_TXN_ISOLATION 대한 설명을 참조하십시오.  
  
 트랜잭션 격리 수준을 설정하려면 응용 프로그램이 **SQLSetConnectAttr을** 호출하여 SQL_ATTR_TXN_ISOLATION 특성을 설정합니다. 자세한 내용은 [SQLSetConnectAttr 함수를](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)참조하십시오.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 SQL_TXN_SERIALIZABLE 반환합니다. FIPS 전환 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_UNION(ODBC 2.0)  
 **UNION** 절에 대한 지원을 등록하는 SQLUINTEGER 비트 마스크:  
  
 SQL_U_UNION = 데이터 원본은 **UNION** 절을 지원합니다.  
  
 SQL_U_UNION_ALL = 데이터 원본은 **UNION** 절의 **ALL** 키워드를 지원합니다. **(SQLGetInfo는** 이 경우 SQL_U_UNION SQL_U_UNION_ALL 모두 반환합니다.  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로 이러한 옵션을 모두 반환합니다.  
  
 SQL_USER_NAME(ODBC 1.0)  
 로그인 이름과 다를 수 있는 특정 데이터베이스에 사용되는 이름이 있는 문자열입니다.  
  
 SQL_XOPEN_CLI_YEAR(ODBC 3.0)  
 ODBC 드라이버 관리자 버전이 완전히 준수하는 Open Group 사양의 게시 연도를 나타내는 문자열입니다.  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 문자열 문자열: 사용자가 **SQLProcedures에서**반환하는 모든 프로시저를 실행할 수 있는 경우 "Y"; 사용자가 실행할 수 없는 프로시저가 반환될 수 있는 경우 "N"입니다.  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 문자열 문자열: 사용자가 **SQLTables에서**반환하는 모든 테이블에 **SELECT** 권한을 보장하는 경우 "Y"; 사용자가 액세스할 수 없는 테이블이 반환될 수 있는 경우 "N"입니다.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 드라이버가 지원할 수 있는 최대 활성 환경 수를 지정하는 SQLUSMALLINT 값입니다. 지정된 제한이 없거나 제한을 알 수 없는 경우 이 값은 0으로 설정됩니다.  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 집계 함수에 대한 지원을 확대하는 SQLUINTEGER 비트 마스크:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 엔트리 레벨 준수 드라이버는 항상 지원되는 대로 이러한 모든 옵션을 반환합니다.  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 데이터 원본에서 지원하는 SQL-92에 정의된 대로 **ALTER DOMAIN** 문의 절을 영예하는 SQLUINTEGER 비트 마스크입니다. SQL-92 전체 수준을 준수하는 드라이버는 항상 모든 비트 마스크를 반환합니다. 반환 값 "0"은 **ALTER DOMAIN** 문이 지원되지 않음을 의미합니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 도메인 제약 조건 추가가 지원됩니다(전체 수준)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= 도메인 \<> 도메인 기본 절> 변경이 지원됩니다(전체 수준)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<= 제약 조건 이름 정의 절> 명명 도메인 제약 조건에 대 한 지원 됩니다 (중간 수준)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 드롭 도메인 제약 조건 절> 지원됩니다(전체 수준)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= 도메인 \<드롭 도메인 기본 절>> 변경이 지원됩니다(전체 수준)  
  
 다음 비트는 도메인 \<제약 조건 추가 \<> 지원되는 경우> 지원되는 제약 조건 특성을 지정합니다(SQL_AD_ADD_DOMAIN_CONSTRAINT 비트가 설정됨).  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (전체 수준)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (전체 수준)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (전체 수준)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 데이터 원본에서 지원하는 **ALTER TABLE** 문의 절을 등록하는 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원해야 하는 SQL-92 또는 FIPS 준수 수준은 각 비트 마스크 옆에 괄호로 표시됩니다.  
  
 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 열> 절 추가가 지원되며 열 데이터 정렬(전체 수준)(ODBC 3.0)을 지정하는 기능이 있습니다.  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 열> 절 추가가 지원되며 열 기본값(FIPS 전환 수준)(ODBC 3.0)을 지정하는 기능이 있습니다.  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 열 추가> 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= 열 제약 조건(FIPS 전환 수준)을 지정하는 기능(ODBC 3.0)을 사용하여 열> 절 추가가 지원됩니다.  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 테이블 제약 조건 추가> 절이 지원됩니다(FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<= 제약 조건 이름 정의> 이름 지정 열 및 테이블 제약 조건(중간 수준)에 대해 지원됩니다(ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<= 드롭 컬럼> CAS가 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= \<드롭 열 기본 절>> 열 변경이 지원됩니다(중간 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<= 드롭 열> 제한이 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<= 드롭 열> 제한이 지원됩니다(FIPS 과도 수준) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= 열 \<변경> 설정 열 기본 절> 지원됩니다(중간 수준) (ODBC 3.0)  
  
 다음 비트는 열 \<또는 테이블 제약 조건을 지정하는 것이 지원되는 경우> 지원 제약 조건 특성을 지정합니다(SQL_AT_ADD_CONSTRAINT 비트가 설정됨).  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED(전체 수준) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (전체 수준) (ODBC 3.0)  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 드라이버의 비동기 지원 수준을 나타내는 SQLUINTEGER 값입니다.  
  
 SQL_AM_CONNECTION = 연결 수준 비동기 실행이 지원됩니다. 지정된 연결 핸들과 연결된 모든 문 핸들이 비동기 모드이거나 모두 동기 모드에 있습니다. 연결의 문 핸들은 비동기 모드일 수 없으며 동일한 연결의 다른 문 핸들은 동기 모드에 있고 그 반대의 경우도 마찬가지입니다.  
  
 SQL_AM_STATEMENT = 문 수준 비동기 실행이 지원됩니다. 연결 핸들과 연결된 일부 문 핸들은 비동기 모드일 수 있지만 동일한 연결의 다른 명령문 핸들은 동기 모드에 있을 수 있습니다.  
  
 SQL_AM_NONE = 비동기 모드가 지원되지 않습니다.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 행 수의 가용성과 관련하여 드라이버의 동작을 열거하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 정보 유형과 함께 사용됩니다.  
  
 SQL_BRC_ROLLED_UP = 연속INSERT, DELETE 또는 UPDATE 문에 대한 행 수는 하나로 롤업됩니다. 이 비트가 설정되지 않은 경우 각 문에 대해 행 수를 사용할 수 있습니다.  
  
 SQL_BRC_PROCEDURES = 일괄 처리가 저장 프로시저에서 실행될 때 행 수를 확인할 수 있습니다( 있는 경우). 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 롤업하거나 개별적으로 사용할 수 있습니다.  
  
 SQL_BRC_EXPLICIT = 행 카운트(있는 경우)는 **SQLExecute** 또는 **SQLExecDirect**를 호출하여 일괄 처리가 직접 실행될 때 사용할 수 있습니다. 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 롤업하거나 개별적으로 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 **SQLGetInfo는** **InfoValuePtr에서*SQLUINTEGER 비트 마스크로 지원되는 옵션 의 목록을 반환합니다. 각 옵션에 대한 비트 마스크는 플래그와 함께 사용하여 옵션이 지원되는지 여부를 결정합니다.  
  
 예를 들어 응용 프로그램은 다음 코드를 사용하여 SUBSTRING 스칼라 함수가 연결과 연결된 드라이버에서 지원되는지 여부를 확인할 수 있습니다.  
  
 **SQLGetInfo를**사용하는 또 다른 예는 [SQLTable 함수를](../../../odbc/reference/syntax/sqltables-function.md)참조하십시오.  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>관련 함수  
 연결 특성의 설정 반환  
 [SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 드라이버가 함수를 지원하는지 여부를 결정합니다.  
 [SQLGetFunctions 함수](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 문 특성의 설정 반환  
 [SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 데이터 원본의 데이터 형식에 대한 정보 반환  
 [SQLGetTypeInfo 함수](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
