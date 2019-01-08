---
title: SQLGetInfo 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0878b7c0d6e7cea6f1dcdc90fa7e78a2680546b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204892"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetInfo** 연결과 관련 된 드라이버 및 데이터 원본에 대 한 일반 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *정보 항목*  
 [입력] 정보의 유형입니다.  
  
 *InfoValuePtr*  
 [출력] 정보를 반환 하는 버퍼에 대 한 포인터입니다. 에 따라 합니다 *정보 항목* 요청에서 반환 되는 정보 중 하나가 됩니다 다음: null로 끝나는 문자열 "," SQLUSMALLINT 값을 ","는 SQLUINTEGER 비트 마스크 "," SQLUINTEGER 플래그 "," SQLUINTEGER 이진 값을 또는 SQLULEN 값입니다.  
  
 경우는 *정보 항목* 인수가 SQL_DRIVER_HDESC 이거나 SQL_DRIVER_HSTMT, 합니다 *InfoValuePtr* 인수는 모두 입력 및 출력 합니다. (자세한 내용은이 함수 설명의 뒷부분에 나오는 SQL_DRIVER_HDESC 또는 SQL_DRIVER_HSTMT 설명자 참조).  
  
 경우 *InfoValuePtr* 가 null 인 경우 *StringLengthPtr* 바이트 (문자 데이터에 대 한 null 종료 문자 제외)의 총 수를 반환 여전히가 가리키는 버퍼에서 반환할 사용 가능한 *InfoValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 길이 \* *InfoValuePtr* 버퍼입니다. 경우에 값  *\*InfoValuePtr* 문자 문자열이 아닙니다 이거나 *InfoValuePtr* 가 null 포인터인 경우를 *BufferLength* 인수는 무시 됩니다. 가정 드라이버의 크기  *\*InfoValuePtr* SQLUSMALLINT 인지 SQLUINTEGER를 기반으로 합니다 *정보 항목*합니다. 하는 경우  *\*InfoValuePtr* 는 유니코드 문자열 (호출할 때 **SQLGetInfoW**), *BufferLength* SQLSTATE HY090 (그렇지 않은 경우 인수는 짝수; 이어야 합니다 문자열 또는 버퍼 길이가 잘못 되었습니다)가 반환 됩니다.  
  
 *StringLengthPtr*  
 [출력] (문자 데이터에 대 한 null 종료 문자를 제외한) 바이트의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용할 수 있습니다 **InfoValuePtr*합니다.  
  
 문자 데이터를 반환할 수 있는 바이트 수가 보다 크거나 같은 경우에 대 한 *BufferLength*에 있는 정보 \* *InfoValuePtr* 잘립니다  *BufferLength* null 종료의 길이 뺀 값 바이트 문자 및 드라이버에 의해 null로 종결 됩니다.  
  
 다른 모든 유형의 데이터를 값에 대 한 *BufferLength* 무시 됩니다 드라이버의 크기를 가정 \* *InfoValuePtr* 인지 SQLUSMALLINT SQLUINTEGER을 따라는  *정보 항목*합니다.  
  
## <a name="return-value"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetInfo** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 SQL_HANDLE_DBC와 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetInfo** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *InfoValuePtr* 충분히 요청된 된 모든 정보를 반환할 수 없습니다. 따라서 정보가 잘렸습니다. 잘리지 않은 형태의 요청 된 정보의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다.|(DM)에서 요청 된 정보의 유형을 *정보 항목* 열린 연결이 필요 합니다. ODBC에서 예약 정보 유형 중 SQL_ODBC_VER만 열려 있는 연결 없이 반환할 수 있습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|(DM)는 *정보 항목* 인수가 SQL_DRIVER_HSTMT, 및 가리키는 값 *InfoValuePtr* 유효한 문 핸들을 없습니다.<br /><br /> (DM)는 *정보 항목* 인수가 SQL_DRIVER_HDESC, 및 가리키는 값 *InfoValuePtr* 유효한 설명자 핸들 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.<br /><br /> (DM)에 대 한 지정 된 값 *BufferLength* 홀수, 및  *\*InfoValuePtr* 유니코드 데이터 형식 이었습니다.|  
|HY096|정보 유형 범위를 벗어났습니다.|인수에 지정 된 값 *정보 항목* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|구현 되지 않은 선택적 필드|인수에 지정 된 값 *정보 항목* 드라이버에서 지원 되지 않는 드라이버 관련 값.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 현재 정의 된 정보 유형에 "정보 유형"이이 섹션 뒷부분에서에 표시 됩니다. 다른 데이터 원본 활용 하기 위해 정의 더 예상 됩니다. ODBC;에서 예약 되어 다양 한 정보 유형 드라이버 개발자는 Open Group에서 자신의 드라이버별 사용에 대 한 값을 예약 해야 합니다. **SQLGetInfo** 변환을 수행 하지 않은 유니코드 또는 *썽킹* (참조 [부록 a: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) 의 합니다 *ODBC 프로그래머 참조*)에 대 한 드라이버에서 정의한 *InfoTypes*합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다. 반환 되는 정보의 형식을 \* *InfoValuePtr* 종속 합니다 *정보 항목* 요청 합니다. **SQLGetInfo** 는 5 가지 형식 중 하나에서 정보를 반환 합니다.  
  
-   Null로 끝나는 문자열  
  
-   SQLUSMALLINT 값을  
  
-   SQLUINTEGER 비트 마스크  
  
-   SQLUINTEGER 값  
  
-   SQLUINTEGER 이진 값  
  
 형식에 대해 다음 정보 유형만 형식 설명에 표시 됩니다. 응용 프로그램에 반환 되는 값을 캐스팅 해야 **InfoValuePtr* 적절 하 게 합니다. 응용 프로그램 SQLUINTEGER 비트 마스크에서 데이터를 검색할 수 하는 방법의 예제를 "코드 예제에서는"을 참조 하세요.  
  
 드라이버는 다음 테이블에 정의 된 각 정보 형식에 대 한 값을 반환 해야 합니다. 정보 유형을 드라이버나 데이터 원본에 적용 되지 않습니다, 경우 드라이버는 다음 표에 나열 된 값 중 하나를 반환 합니다.  
  
 문자열 ("Y" 또는 "N")  
 "N"  
  
 문자열 (없습니다: "Y" 또는 "N")  
 빈 문자열  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER 비트 마스크 또는 SQLUINTEGER 이진 값  
 0 L  
  
 예를 들어, 데이터 원본 프로시저를 지원 하지 않는 경우 **SQLGetInfo** 의 값에 대해 다음 표에 나열 된 값을 반환 *정보 항목* 프로시저에 관련 된 합니다.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 빈 문자열  
  
 **SQLGetInfo** SQLSTATE HY096 반환 (잘못 된 인수 값)의 값에 대해 *정보 항목* 정보 유형 ODBC에서 사용 하도록 예약된의 범위 내에 있지만 ODBC 드라이버에서 지원 되는 버전에서 정의 되지 않은 합니다. 어떤 버전의 ODBC 드라이버를 준수를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_DRIVER_ODBC_VER 정보 형식을 사용 하 여 합니다. **SQLGetInfo** SQLSTATE HYC00를 반환 합니다 (선택적 기능이 구현 되지 않음)의 값에 대해 *정보 항목* 정보 유형 드라이버별 용도로 예약된의 범위 내에 있지만 드라이버에서 지원 되지 않습니다.  
  
 에 대 한 모든 호출 **SQLGetInfo** 경우를 제외 하 고 연결을 열어야 합니다 *정보 항목* SQL_ODBC_VER 드라이버 관리자의 버전을 반환 하는 합니다.  
  
## <a name="information-types"></a>정보 유형  
 이 섹션에서 지원 되는 정보 유형을 나열 **SQLGetInfo**합니다. 정보 유형 해커나 그룹화 되 고 사전순으로 나열 됩니다. ODBC 3에 대 한 변경 되거나 추가 된 정보 유형 *.x* 도 나열 됩니다.  
  
## <a name="driver-information"></a>드라이버 정보  
 다음 값을 *정보 항목* 인수 활성 문, 데이터 원본 이름 및 인터페이스 표준 준수 수준 수와 같은 ODBC 드라이버에 대 한 정보를 반환 합니다.  
  
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
>  구현 하는 경우 **SQLGetInfo**, 드라이버 정보 전송 또는 서버에서 요청 하는 횟수를 최소화 하 여 성능을 향상 시킬 수 있습니다.  
  
## <a name="dbms-product-information"></a>DBMS 제품 정보  
 다음 값을 *정보 항목* 인수 DBMS 이름과 버전을 같은 DBMS 제품에 대 한 정보를 반환 합니다.  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>데이터 원본 정보  
 다음 값을 *정보 항목* 인수 커서 특징 및 트랜잭션 기능을 같은 데이터 원본에 대 한 정보를 반환 합니다.  
  
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
  
## <a name="supported-sql"></a>지원 되는 SQL  
 다음 값을 *정보 항목* 인수는 데이터 원본에서 지 원하는 SQL 문에 대 한 정보를 반환 합니다. 이러한 정보 유형을 설명 하는 각 기능의 SQL 구문은 SQL-92 구문을 표시 합니다. 이러한 정보 유형을 전체 SQL-92 문법을 철저히 설명 하지는 않습니다. 대신 이러한 부분 데이터에 대 한 원본 일반적으로 다양 한 수준의 지원 제공 하는 문법 설명 합니다. 특히 대부분의 SQL-92에 DDL 문 설명 합니다.  
  
 응용 프로그램 일반 SQL_SQL_CONFORMANCE 정보 형식에서 지원 되는 문법 수준을 확인 하 고 다른 정보 형식을 사용 하 여 명시 된 표준 준수 수준에서 결정 해야 합니다.  
  
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
 다음 값을 *정보 항목* 인수 식별자와 식별자 및 select 목록에 있는 열의 최대 수의 최대 길이 등의 SQL 문에서 절에 적용 된 제한에 대 한 정보를 반환 합니다. 제한 사항 드라이버 또는 데이터 원본에서 적용할 수 있습니다.  
  
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
  
## <a name="scalar-function-information"></a>스칼라 함수 정보  
 다음 값을 *정보 항목* 인수는 스칼라 함수를 데이터 원본 및 드라이버 지원에 대 한 정보를 반환 합니다. 스칼라 함수에 대 한 자세한 내용은 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)합니다.  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>변환 정보  
 다음 값을 *정보 항목* 인수에는 데이터 원본을 사용 하 여 지정 된 SQL 데이터 형식 변환 수는 SQL 데이터 형식의 목록을 반환 합니다 **변환** 스칼라 함수:  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>ODBC에 대 한 추가 정보 유형 3.x  
 다음 값을 *정보 항목* ODBC 3에 대 한 인수를 추가한 *.x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>정보 유형으로 이름이 바뀐 경우 ODBC 3.x  
 다음 값을 *정보 항목* ODBC 3에 대 한 인수를 바뀌었습니다 *.x*합니다.  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>ODBC에서 지원 되지 않는 정보 유형 3.x  
 다음 값을 *정보 항목* ODBC 3에서 되지 인수 *.x*합니다. ODBC 3 *.x* 드라이버는 ODBC 2를 사용 하 여 이전 버전과 호환성을 위해 이러한 정보 유형을 지원 하기 위해 계속 해야 *.x* 응용 프로그램입니다. (이러한 형식에 대 한 자세한 내용은 참조 하세요. [SQLGetInfo 지원](../../../odbc/reference/appendixes/sqlgetinfo-support.md) 부록 g:에서 드라이버 지침 이전 버전과 호환성에 대 한 합니다.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>정보 유형 설명  
 다음 표에서 각 정보 유형, 해당 설명과 도입 된 ODBC의 버전에 사전순으로 나열 됩니다.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 문자열: "Y" 사용자에서 반환 된 모든 프로시저를 실행할 수 있다면 **SQLProcedures**; 사용자를 실행할 수 없는지 반환 하는 "N" 프로시저 있을 수 있습니다.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 문자열: "Y" 사용자 보장 되는 경우 **선택** 반환한 모든 테이블에 대 한 권한을 **SQLTables**; 사용자에 액세스할 수 없습니다. 반환 하는 "N" 테이블이 있을 수 있습니다.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 활성 환경에 드라이버를 지원할 수 있는 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 집계 함수에 대 한 지원을 열거 SQLUINTEGER 비트 마스크:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **ALTER 도메인** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다. SQL-92 Full 수준 규격 드라이버는 항상 모든 비트 마스크를 반환 합니다. 즉 "0"의 반환 값을 **ALTER 도메인** 문은 지원 되지 않습니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 추가 도메인 제약 조건이 지원 됩니다 (전체 수준)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 도메인 > \<set 도메인 기본 절 >은 지원 (전체 수준)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의 절 > 도메인 제약 조건 (중간 수준) 이름 지정에  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop 도메인 제약 조건 절 >은 지원 (전체 수준)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 도메인 > \<drop 도메인 기본 절 >은 지원 (전체 수준)  
  
 지원 되는 다음 비트를 지정 \<제약 조건 특성 > 경우 \<도메인 제약 조건 추가 > 지원 됩니다 (SQL_AD_ADD_DOMAIN_CONSTRAINT 비트 설정 됨):  
  
 (전체 수준) SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (전체 수준) (전체 수준) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **ALTER TABLE** 데이터 원본에서 지 원하는 문입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<열 추가 > 열 데이터 정렬 (전체 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<열 추가 > 열의 기본값 (FIPS 전환 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<열 추가 >은 (FIPS 전환 수준)를 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<열 추가 > 열 제약 조건 (FIPS 전환 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<테이블 제약 조건 추가 > 절은 지원 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의 > 이름 열 및 테이블 제약 조건 (중간 수준)은 지원 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<열 > CASCADE 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 열 > \<drop 열 기본 절 >은 (중간 수준)를 지원 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<열 > 제한 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<열 > 제한 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 열 > \<set 열 기본 절 >은 (중간 수준)를 지원 (ODBC 3.0)  
  
 다음 비트 지정 지원 \<제약 조건 특성 > 열 또는 테이블 제약 조건을 지정 하는 경우 (SQL_AT_ADD_CONSTRAINT 비트 설정 됨):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (전체 수준) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 경우 드라이버에서 실행할 수 있습니다 함수 비동기적으로 연결 핸들을 표시 하는 SQLUINTEGER 값입니다.  
  
 SQL_ASYNC_DBC_CAPABLE = 드라이버 연결 함수를 비동기적으로 실행할 수 있습니다.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 드라이버 연결 함수를 비동기적으로 실행 되지 않습니다 수 있습니다.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 드라이버에서 비동기 지원의 수준을 지정 하는 SQLUINTEGER 값:  
  
 SQL_AM_CONNECTION = 연결 수준 비동기 실행은 지원 됩니다. 비동기 모드에 있는 지정 된 연결 핸들에 연결 된 모든 문 핸들 또는 동기 모드에서 모두. 같은 연결에서 다른 문 핸들은 동기 모드에서 이동 하 고 그 반대의 경우도 마찬가지 비동기 모드 연결에서 문 핸들 일 수 없습니다.  
  
 SQL_AM_STATEMENT = Statement 수준 비동기 실행은 지원 됩니다. 동기 모드에서 동일한 연결에서 다른 문 핸들은 비동기 모드로 연결 핸들에 연결 된 몇 가지 문 핸들 수 있습니다.  
  
 SQL_AM_NONE 비동기 = 모드가 지원 되지 않습니다.  
  
 SQL_ASYNC_NOTIFICATION  
 드라이버에서 비동기 알림을 지원 하는 경우를 지정 하는 SQLUINTEGER 값:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** 비동기 실행 알림이 드라이버에서 지원 됩니다.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** 비동기 실행 알림이 드라이버에서 지원 되지 않습니다.  
  
 ODBC 비동기 작업의 두 종류: 연결 수준 비동기 작업 및 문 수준 비동기 작업입니다.  드라이버 SQL_ASYNC_NOTIFICATION_CAPABLE 반환 하는 경우 비동기적으로 실행할 수 있는 모든 Api에 대 한 알림을 지원 해야 합니다.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 행의 가용성을 기준으로 드라이버의 동작을 열거 하는 SQLUINTEGER 비트 마스크를 계산 합니다. 다음 비트 마스크는 정보 형식과 함께 사용 됩니다.  
  
 SQL_BRC_ROLLED_UP 행 개수 = 연속 INSERT, DELETE 또는 UPDATE 문을 하나로 롤업 됩니다. 이 비트가 설정 되어 있지 않으면 행 개수 각 문에 대해 사용할 수 있습니다.  
  
 SQL_BRC_PROCEDURES, 사용 가능한 경우 저장된 프로시저의 일괄 처리 실행 될 때 행 개수 =. 행 개수를 사용할 수 있는 또는 SQL_BRC_ROLLED_UP 비트에 따라 개별적으로 사용할 수 있는 롤백할 수 있습니다.  
  
 SQL_BRC_EXPLICIT, 사용 가능한 경우 직접 호출 하 여 일괄 처리 실행 될 때 행 개수 = **SQLExecute** 하거나 **SQLExecDirect**합니다. 행 개수를 사용할 수 있는 또는 SQL_BRC_ROLLED_UP 비트에 따라 개별적으로 사용할 수 있는 롤백할 수 있습니다.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 일괄 처리에 대 한 드라이버의 지원을 열거 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크 수준을 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_BS_SELECT_EXPLICIT = 드라이버 지원 명시적 일괄 처리를 수 있는 결과 집합 문을 생성 합니다.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 드라이버 지원 명시적 일괄 처리를 행 개수 생성 문을 사용할 수 있습니다.  
  
 SQL_BS_SELECT_PROC = 수 있는 결과 집합 문을 생성 하는 드라이버 지원 명시적 절차입니다.  
  
 SQL_BS_ROW_COUNT_PROC = 행 개수 생성 문을 포함할 수 있는 드라이버 지원 명시적 절차입니다.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 책갈피 유지 하는 작업을 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 책갈피 옵션 유지 결정할 플래그와 함께 사용 됩니다.  
  
 SQL_BP_CLOSE = 책갈피 응용 프로그램이 호출 후 유효 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 하 여 또는 **SQLCloseCursor** 문과 사용 하 여 연결 된 커서를 닫습니다.  
  
 SQL_BP_DELETE = 책갈피 행은 해당 행이 삭제 된 후 유효 합니다.  
  
 SQL_BP_DROP = 책갈피 응용 프로그램이 호출 후 유효 **SQLFreeHandle** 사용 하 여를 *HandleType* 을 호출 문을 삭제 하 여 합니다.  
  
 SQL_BP_TRANSACTION = 응용 프로그램에 커밋 또는 트랜잭션을 롤백합니다 후 책갈피가 유효 합니다.  
  
 SQL_BP_UPDATE 책갈피 = 해당 행의 모든 열 업데이트 된 후, 키 열을 포함 하는 행이 올바르면이 대 한 합니다.  
  
 SQL_BP_OTHER_HSTMT 하 나와 연결 된 책갈피 = 문은 다른 문을 사용 하 여 사용할 수 있습니다. SQL_BP_CLOSE 또는 SQL_BP_DROP를 지정 하지 않으면 첫 번째 문에서 커서 열려 있어야 합니다.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 정규화 된 테이블 이름에 카탈로그의 위치를 나타내는 SQLUSMALLINT 값:  
  
 SQL_CL_STARTSQL_CL_END  
  
 예를 들어는 Xbase 드라이버 디렉터리 (카탈로그) 이름이 \EMPDATA\EMP와 같이 테이블 이름으로 시작 되어 SQL_CL_START를 반환 합니다. DBF 합니다. 카탈로그에서와 같이 테이블 이름 끝에는 ORACLE Server 드라이버를 SQL_CL_END 반환 ADMIN.EMP@EMPDATA합니다.  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 SQL_CL_START를 항상 반환 됩니다. 카탈로그 데이터 원본에서 지원 되지 않는 경우 0 값 반환 됩니다. 카탈로그를 지원 하는지 여부를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_NAME 정보 형식을 사용 하 여 합니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_QUALIFIER_LOCATION 합니다.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 문자열: "Y" 서버에서 지 원하는 경우 카탈로그 이름 또는 "N" 하지 않는 경우.  
  
 SQL-92 Full 수준-와 호환 되는 드라이버는 항상 "Y"를 반환 합니다.  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 문자열: 카탈로그 이름 뒤 또는 앞에 정규화 된 이름 요소 사이의 구분 기호로 데이터 원본을 정의 하는 문자입니다.  
  
 카탈로그 데이터 원본에서 지원 되지 않는 경우 빈 문자열이 반환 됩니다. 카탈로그를 지원 하는지 여부를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_NAME 정보 형식을 사용 하 여 합니다. SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다 "."입니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_QUALIFIER_NAME_SEPARATOR 합니다.  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 카탈로그; 데이터 원본 공급 업체의 이름 사용 하 여 문자열 예를 들어, "database" 또는 "directory"입니다. 이 문자열은 위쪽, 아래쪽, 또는 혼합의 경우 수 있습니다.  
  
 카탈로그 데이터 원본에서 지원 되지 않는 경우 빈 문자열이 반환 됩니다. 카탈로그를 지원 하는지 여부를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_NAME 정보 형식을 사용 하 여 합니다. SQL-92 Full 수준-와 호환 되는 드라이버는 항상 "catalog"을 반환 합니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_QUALIFIER_TERM 합니다.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 카탈로그를 사용할 수 있는 문을 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 카탈로그를 사용할 수 있는 확인 하는 데 사용 됩니다.  
  
 SQL_CU_DML_STATEMENTS = 카탈로그는 모든 데이터 조작 언어 문에서 지원 됩니다. **선택**, **삽입**, **업데이트**를 **삭제**을 지원 하 고 **업데이트에 대 한 선택** 위치 지정 업데이트 및 삭제 하 고 문입니다.  
  
 SQL_CU_PROCEDURE_INVOCATION = ODBC 프로시저 호출 문에 카탈로그 지원 됩니다.  
  
 SQL_CU_TABLE_DEFINITION = 모든 테이블 정의 문에 카탈로그 지원 됩니다. **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**를 **DROP TABLE**, 및 **DROP VIEW**합니다.  
  
 SQL_CU_INDEX_DEFINITION = 모든 인덱스 정의 문에 카탈로그 지원 됩니다. **인덱스를 만들** 하 고 **DROP INDEX**합니다.  
  
 SQL_CU_PRIVILEGE_DEFINITION = 모든 권한 정의 문에 카탈로그 지원 됩니다. **권한 부여** 하 고 **해지**합니다.  
  
 카탈로그 데이터 원본에서 지원 되지 않는 경우 0 값 반환 됩니다. 카탈로그를 지원 하는지 여부를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_NAME 정보 형식을 사용 하 여 합니다. SQL-92 Full 수준-와 호환 되는 드라이버는 항상 이러한 비트 집합의 모든 비트 마스크를 반환 합니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_QUALIFIER_USAGE 합니다.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 데이터 정렬 시퀀스의 이름입니다. 이 기본 문자 집합을이 서버에 대 한 기본 데이터 정렬의 이름을 나타내는 문자열 (예를 들어, ' ISO 8859-1' 또는 EBCDIC). 이 알 수 없는 경우 빈 문자열이 반환 됩니다. SQL-92 Full 수준-와 호환 되는 드라이버는 항상 비어 있지 않은 문자열을 반환 합니다.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 문자열: 데이터 원본에 열 별칭;에서 지 원하는 경우 "Y" 그렇지 않으면 "N"입니다.  
  
 열 별칭은 AS 절을 사용 하면 select 목록의 열에 대해 지정할 수 있는 대체 이름. SQL-92 항목 수준-와 호환 되는 드라이버는 항상 "Y"를 반환 합니다.  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 데이터 원본 연결 된 NULL 처리 하는 방법을 나타내는 SQLUSMALLINT 값을 NULL이 아닌 값 가진된 문자 데이터 형식 열을 사용 하 여 문자 데이터 형식 열을 반환 합니다.  
  
 SQL_CB_NULL = 결과 NULL을 반환 합니다.  
  
 SQL_CB_NON_NULL = 결과 NULL이 아닌 값을 가진 열의 연결 합니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 SQL_CB_NULL를 항상 반환 됩니다.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER 비트 마스크입니다. 비트 마스크를 사용 하 여 데이터 원본에서 지 원하는 변환 나타냅니다 합니다 **변환** 에 명명 된 형식의 데이터에 대 한 스칼라 함수는 *정보 항목*합니다. 비트 마스크가 0 인 경우 데이터 원본 데이터에서 동일한 데이터 형식으로 변환을 포함 하는 명명 된 형식의 모든 변환을 지원 하지 않습니다.  
  
 예를 들어를 데이터 원본 지원 SQL_INTEGER 데이터 SQL_BIGINT 데이터 형식으로 변환 하는 경우 확인 하려면 응용 프로그램 호출 **SQLGetInfo** 사용 하 여 합니다 *정보 항목* SQL_CONVERT_INTEGER입니다. 응용 프로그램이 수행 하는 **AND** SQL_CVT_BIGINT 고 반환 된 비트 마스크를 사용 하 여 작업 합니다. 결과 값을 0이 아닌 경우 변환이 지원 됩니다.  
  
 다음 비트 마스크는 변환이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (ODBC 1.0) SQL_CVT_BIGINT SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL (ODBC 1.0) SQL_CVT_SMALLINT SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) 타임 스탬프 (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 변환 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 변환 함수 확인에 사용 됩니다.  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 테이블 상관 관계 이름을 지원 되는지 여부를 나타내는 SQLUSMALLINT 값:  
  
 SQL_CN_NONE = 상관 관계 이름이 지원 되지 않습니다.  
  
 SQL_CN_DIFFERENT = 상관 관계 이름을 지원 되지만 나타내는 테이블의 이름과에서 달라 야 합니다.  
  
 SQL_CN_ANY = 상관 관계 이름 지 및 모든 유효한 사용자 정의 이름이 될 수 있습니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 SQL_CN_ANY를 항상 반환 됩니다.  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **어설션을 만들** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA_CREATE_ASSERTION  
  
 제약 조건 속성을 명시적으로 지정 하는 기능이 지원 되는 경우 지원 되는 제약 조건 특성을 지정 하는 다음 비트 (SQL_ALTER_TABLE 및 SQL_CREATE_TABLE 정보 유형 참조).  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원. 즉 "0"의 반환 값을 **어설션을 만듭니다** 문은 지원 되지 않습니다.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **문자 집합 만들기** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원. 즉 "0"의 반환 값을 **문자 집합 만들기** 문은 지원 되지 않습니다.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **데이터 정렬을 만듭니다** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_CCOL_CREATE_COLLATION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는이 옵션을 항상 반환 됩니다. 즉 "0"의 반환 값을 **만들 데이터 정렬을** 문은 지원 되지 않습니다.  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **도메인 만들기** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CDO_CREATE_DOMAIN = 도메인 만들기 문은 지원 됩니다 (중간 수준).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의 > 도메인 제약 조건 (중간 수준) 명명에 대 한 지원 됩니다.  
  
 열 제약 조건: SQL_CDO_DEFAULT를 만들 수를 지정 하는 다음 비트 = 도메인 제약 조건을 지정 하는 (중간 수준) SQL_CDO_CONSTRAINT = 도메인 기본값을 지정 하는 (중간 수준) SQL_CDO_COLLATION = 도메인 데이터 정렬을 지정 하는 (전체 수준)  
  
 도메인 제약 조건을 지정 하는 경우 지원 되는 제약 조건 특성을 지정 하는 다음 비트 (SQL_CDO_DEFAULT 설정 됨):  
  
 (전체 수준) SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (전체 수준) SQL_CDO_CONSTRAINT_DEFERRABLE SQL_CDO_CONSTRAINT_NON_DEFERRABLE (전체 수준)  
  
 즉 "0"의 반환 값을 **도메인 만들기** 문은 지원 되지 않습니다.  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **CREATE SCHEMA** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL-92 중간 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_CS_CREATE_SCHEMA 및 SQL_CS_AUTHORIZATION 옵션을 항상 반환 됩니다. 이러한 개체도 지원 해야 하지만 SQL 문으로 반드시 SQL-92 항목 수준입니다. SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **CREATE TABLE** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CT_CREATE_TABLE =은 CREATE TABLE 문은 지원 됩니다. (항목 수준)  
  
 SQL_CT_TABLE_CONSTRAINT = 테이블 제약 조건을 지정 하는 (FIPS 전환 수준)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =는 \<제약 조건 이름 정의 > 절은 열 및 테이블 제약 조건 (중간 수준) 명명에 대 한 지원  
  
 다음 비트를 임시 테이블을 만들 수를 지정 합니다.  
  
 SQL_CT_COMMIT_PRESERVE = 삭제 된 행이 커밋에 유지 됩니다. (전체 수준) SQL_CT_COMMIT_DELETE = 삭제 된 행이 커밋 시 삭제 됩니다. (전체 수준) SQL_CT_GLOBAL_TEMPORARY = 전역 임시 테이블을 만들 수 있습니다. (전체 수준) SQL_CT_LOCAL_TEMPORARY = 로컬 임시 테이블을 만들 수 있습니다. (전체 수준)  
  
 다음 비트를 지정할 열 제약 조건을 만들 수 있습니다.  
  
 SQL_CT_COLUMN_CONSTRAINT = 열 제약 조건을 지정 하는 (FIPS 전환 수준) SQL_CT_COLUMN_DEFAULT = 열 기본값을 지정 하는 (FIPS 전환 수준) SQL_CT_COLUMN_COLLATION = 열 데이터 정렬 지정 (전체 수준)를 지원합니다.  
  
 열 또는 테이블 제약 조건을 지정 하는 경우 다음 비트를 지원 되는 제약 조건 속성을 지정 합니다.  
  
 (전체 수준) SQL_CT_CONSTRAINT_INITIALLY_DEFERRED SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (전체 수준) SQL_CT_CONSTRAINT_DEFERRABLE SQL_CT_CONSTRAINT_NON_DEFERRABLE (전체 수준)  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **만드는 번역** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는 이러한 옵션을 항상 반환 됩니다. 즉 "0"의 반환 값을 **번역 만들기** 문은 지원 되지 않습니다.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **CREATE VIEW** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 즉 "0"의 반환 값을 **CREATE VIEW** 문은 지원 되지 않습니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_CV_CREATE_VIEW 및 SQL_CV_CHECK_OPTION 옵션을 항상 반환 됩니다.  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 나타내는 SQLUSMALLINT 값을 어떻게를 **커밋** 커서 및 준비 된 문 (트랜잭션을 커밋할 때 데이터 원본의 동작) 데이터 원본 작업에 영향을 줍니다.  
  
 이 특성의 값은 다음 설정의 현재 상태를 반영 합니다. SQL_COPT_SS_PRESERVE_CURSORS 합니다.  
  
 SQL_CB_DELETE = 닫기 커서 및 준비 된 문을 삭제 합니다. 커서를 사용 하려면 다시 응용 프로그램 reprepare 하며 문을 다시 실행 하려고 합니다.  
  
 SQL_CB_CLOSE = 커서를 닫습니다. 준비 된 문에 대 한 응용 프로그램이 호출할 수 있습니다 **SQLExecute** 호출 하지 않고 문에서 **SQLPrepare** 다시 합니다. SQL ODBC 드라이버에 대 한 기본값인 SQL_CB_CLOSE 사용 됩니다. 즉, SQL ODBC 드라이버는 트랜잭션을 커밋하는 경우에 사용자를 닫습니다.  
  
 SQL_CB_PRESERVE 이전과 동일한 위치에 유지 커서 = 합니다 **커밋** 작업 합니다. 데이터를 인출 하는 응용 프로그램을 계속 하거나 커서를 닫고를 다시 다시 준비 하지 않고 문을 실행 합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 나타내는 SQLUSMALLINT 값을 어떻게를 **롤백** 커서 및 데이터 원본에서 준비 된 문을 작업에 영향을 줍니다.  
  
 SQL_CB_DELETE = 닫기 커서 및 준비 된 문을 삭제 합니다. 커서를 사용 하려면 다시 응용 프로그램 reprepare 하며 문을 다시 실행 하려고 합니다.  
  
 SQL_CB_CLOSE = 커서를 닫습니다. 준비 된 문에 대 한 응용 프로그램이 호출할 수 있습니다 **SQLExecute** 호출 하지 않고 문에서 **SQLPrepare** 다시 합니다.  
  
 SQL_CB_PRESERVE 이전과 동일한 위치에 유지 커서 = 합니다 **롤백** 작업 합니다. 데이터를 인출 하는 응용 프로그램을 계속 하거나 커서를 닫고 및 해당 repreparing 없이 문을 다시 수 있습니다.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 커서 민감도 대 한 지원을 표시 하는 SQLUINTEGER 값:  
  
 SQL_INSENSITIVE = 동일한 트랜잭션 내에서 모든 다른 커서에서 모든 커서 결과 집합에 수행한 모든 변경 내용을 반영 하지 않고 문 핸들 표시 합니다.  
  
 SQL_UNSPECIFIED = 문 핸들에서 커서를 변경 하는지 여부 표시를 동일한 트랜잭션 내의 다른 커서에 의해 결과 집합에 대 한 지정 되지 않습니다. 문 핸들 커서 수 표시 되도록 none, 일부 또는 모든 변경.  
  
 SQL_SENSITIVE = 커서는 동일한 트랜잭션 내의 다른 커서에 의해 수행 된 변경에 민감합니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_UNSPECIFIED 옵션을 항상 반환 됩니다.  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_INSENSITIVE 옵션을 항상 반환 됩니다.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 연결 하는 동안 사용 된 데이터 원본 이름의 문자열입니다. 응용 프로그램 호출 **SQLConnect**의 값을 *szDSN* 인수. 응용 프로그램 호출 **SQLDriverConnect** 또는 **SQLBrowseConnect**, 드라이버에 전달 된 연결 문자열에는 DSN 키워드의 값입니다. 연결 문자열에 포함 되어 있지 않으면 합니다 **DSN** 키워드 (같은 경우에 **드라이버** 키워드), 빈 문자열입니다.  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1.0)  
 문자열입니다. "Y"이 고, 그렇지 않으면 데이터 원본 읽기 전용 모드를 "N"로 설정 된 경우.  
  
 이 특성은 자체 데이터 원본에만 적용 됩니다. 데이터 원본에 액세스할 수 있는 드라이버의 특징 아닙니다. 데이터 원본에 읽기 전용인 지 읽기/쓰기 되는 드라이버를 사용할 수 있습니다. 드라이버가 읽기 전용 이면 읽기 전용 이어야 합니다 모든 데이터 원본이 고 SQL_DATA_SOURCE_READ_ONLY 반환 해야 합니다.  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 데이터 원본 "데이터베이스" 라고 명명 된 개체를 정의 하는 경우 문자를 사용 하 여, 현재 데이터베이스의 이름으로 문자열입니다.  
  
> [!NOTE]
>  ODBC 3에서 *.x*에 값이 반환 *정보 항목* 호출 하 여 반환 될 수 있습니다 **SQLGetConnectAttr** 사용 하 여는 *특성* SQL_ATTR_CURRENT_CATALOG의 인수입니다.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 데이터 원본에서 지 원하는 SQL-92 날짜/시간 리터럴 열거 SQLUINTEGER 비트 마스크입니다. 이러한 SQL-92 사양에 나열 된 날짜/시간 리터럴 및은 ODBC 정의 된 날짜/시간 리터럴 이스케이프 절에서 별도 참고 합니다. ODBC 날짜/시간 리터럴 이스케이프 절에 대 한 자세한 내용은 참조 하세요. [날짜, 시간 및 타임 스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)합니다.  
  
 항상 FIPS 전환 수준-와 호환 되는 드라이버를 다음 목록에 있는 비트에 대 한 비트 마스크의 "1" 값을 반환 합니다. 값이 "0" 이면 SQL-92 datetime 리터럴이 지원 되지 않습니다.  
  
 다음 비트 마스크는 리터럴을 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 드라이버에서 액세스 하는 DBMS 제품 이름의 문자열입니다.  
  
 SQL_DBMS_VER (ODBC 1.0)  
 드라이버에서 액세스 한 DBMS 제품의 버전을 나타내는 문자열입니다. 폼의 버전은 # #. # #. # # #, 여기서 처음 두 숫자는 주 버전, 다음 두 자리는 부 버전, 되며 마지막 4 자리 릴리스 버전입니다. 드라이버는 DBMS 제품 버전을이 형식으로 렌더링 해야 하지만 DBMS 특정 제품 버전을 추가할 수도 있습니다. 예를 들어, "04.01.0000 4.1 Rdb"입니다.  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 SQLUINTEGER 나타내는 값을 생성 및 인덱스의 삭제에 대 한 지원:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 데이터 원본에서 드라이버 또는 데이터 원본 또는 경우에는 0에서 지 원하는 기본 트랜잭션 격리 수준을 표시 하는 SQLUINTEGER 값에는 트랜잭션을 지원 하지 않습니다. 다음 용어는 트랜잭션 격리 수준을 정의 하는 데 사용 됩니다.  
  
 **커밋되지 않은 읽기** 트랜잭션 1 행을 변경 합니다. 트랜잭션 2 트랜잭션 1 변경 내용을 커밋하기 전에 변경된 된 행을 읽습니다. 트랜잭션 1 변경 롤백되면 존재 하지로 간주 되는 행 2 트랜잭션 읽기 됩니다.  
  
 **반복 하지 않는 읽기** 트랜잭션 1 행을 읽습니다. 트랜잭션 2 업데이트 또는 해당 행을 삭제 하 고이 변경을 커밋합니다. 트랜잭션 1에 행을 다시 읽고 하려고 하는 경우 다른 행 값을 수신 또는 행이 삭제 되어 검색 됩니다.  
  
 **Phantom** 트랜잭션 1 몇 가지 검색 기준을 만족 하는 행 집합을 읽습니다. 트랜잭션 2 검색 조건과 일치 하는 삽입 또는 업데이트) (통해 하나 이상의 행을 생성 합니다. 트랜잭션 1에 행을 읽는 문을 reexecutes, 하는 경우 다른 행 집합을 받습니다.  
  
 데이터 소스에서 트랜잭션을 지원 드라이버가 다음 비트 마스크의 하나를 반환 합니다.  
  
 SQL_TXN_READ_UNCOMMITTED 귀찮은 = 읽기, 반복할 수 없는 읽기 및 가상 있을 수 있습니다.  
  
 SQL_TXN_READ_COMMITTED 귀찮은 = 읽기 가능 하지 않습니다. 반복 되지 않는 읽기 및 가상 있을 수 있습니다.  
  
 SQL_TXN_REPEATABLE_READ 귀찮은 = 읽기 및 읽기가 가능 하지 않습니다. 팬텀 있을 수 있습니다.  
  
 Sql_txn_serializable로 = 트랜잭션은 serializable입니다. 더티 읽기, 반복할 수 없는 읽기 또는 팬텀 직렬화 가능 트랜잭션을 허용 하지 않습니다.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 문자열: "Y" 매개 변수를 설명할 수 있습니다. "N", 그렇지 않은 경우입니다.  
  
 SQL-92 Full 수준을 준수 하는 드라이버에서 지원 하기 때문에 일반적으로 "Y"를 반환 합니다 **설명 입력** 문입니다. 그러나이 지정 하지 않으므로 직접 기본 SQL 지원, 매개 변수를 설명 하는 지원 되지 않는, SQL-92 Full 수준-와 호환 되는 드라이버에도 합니다.  
  
 SQL_DM_VER (ODBC 3.0)  
 드라이버 관리자의 버전 문자열입니다. 폼의 버전은 # #. # #. # # #. # # # 여기서:  
  
 첫 번째 두 자리 집합이 상수 SQL_SPEC_MAJOR에서 제공 하는 주요 ODBC 버전입니다.  
  
 두 자릿수 두 번째 집합이 상수 SQL_SPEC_MINOR에서 제공 하는 부 ODBC 버전입니다.  
  
 네 자리 숫자의 세 번째 집합이 드라이버 관리자 주 빌드 번호입니다.  
  
 마지막 4 자리 숫자 집합 드라이버 관리자 부 빌드입니다.  
  
 Windows 7 드라이버 관리자 버전 03.80입니다. Windows 8 드라이버 관리자 버전 03.81입니다.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 지정 하는 SQLUINTEGER 값 드라이버가 드라이버 인식 풀링을 지원 합니다. (자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE는 드라이버가 드라이버 인식 풀링 메커니즘을 지원할 수 있는지를 나타냅니다.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE는 드라이버가 드라이버 인식 풀링 메커니즘을 지원할 수 없습니다 나타냅니다.  
  
 드라이버는 SQL_DRIVER_AWARE_POOLING_SUPPORTED 구현 하지 않아도 및 드라이버 관리자는 드라이버의 반환 값을 인식 하지 못합니다 됩니다.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 SQLULEN 값, 드라이버의 환경 핸들 또는 인수에 의해 결정 되는 연결 핸들 *정보 항목*합니다.  
  
 이러한 정보 유형은 드라이버 관리자에 의해 단독으로 구현 됩니다.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 SQLULEN 값을 입력에서 전달 되어야 하는 드라이버 관리자의 설명자 핸들에 의해 결정 하는 드라이버의 설명자 핸들 \* *InfoValuePtr* 응용 프로그램에서 합니다. 이 예에서 *InfoValuePtr* 는 입력 및 출력 인수입니다. 전달 된 입력된 설명자 핸들 \* *InfoValuePtr* 할당 되어야 합니다 명시적 또는 암시적으로 *ConnectionHandle*합니다.  
  
 응용 프로그램 처리를 호출 하기 전에 드라이버 관리자의 설명자의 복사본을 확인 해야 **SQLGetInfo** 이 정보 유형과 핸들을 출력에서 덮어쓰지 않습니다 되도록 합니다.  
  
 이 정보 유형은 드라이버 관리자에 의해 단독으로 구현 됩니다.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 SQLULEN 값을 *hinst* 부하 라이브러리에서 드라이버 관리자에는 Microsoft Windows 운영 체제 또는 다른 운영 체제에 해당 하는 드라이버 DLL이 로드 될 때 반환 합니다. 핸들에 대 한 호출에 지정 된 연결 핸들에 대해서만 유효 **SQLGetInfo**합니다.  
  
 이 정보 유형은 드라이버 관리자에 의해 단독으로 구현 됩니다.  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 SQLULEN 값을 입력에서 전달 되어야 하는 드라이버 관리자 문 핸들에 의해 결정 하는 드라이버의 문 핸들 \* *InfoValuePtr* 응용 프로그램에서 합니다. 이 예에서 *InfoValuePtr* 는 입력 및 출력 인수입니다. 전달 된 입력된 문 핸들 \* *InfoValuePtr* 인수에 할당 합니다 *ConnectionHandle*합니다.  
  
 응용 프로그램 드라이버 관리자의 문의 복사본 호출 하기 전에 처리 해야 합니다. **SQLGetInfo** 이 정보 유형과 핸들을 출력에서 덮어쓰지 않았는지 확인 합니다.  
  
 이 정보 유형은 드라이버 관리자에 의해 단독으로 구현 됩니다.  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 데이터 원본에 액세스 하는 데 사용 하는 드라이버 파일 이름의 문자열입니다.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 드라이버에서 지 원하는 ODBC의 버전을 사용 하 여 문자열입니다. 폼의 버전은 # #. # #, 여기서 때 처음 두 숫자는 주 버전 및 다음 두 자리는 부 버전. SQL_SPEC_MAJOR 및 SQL_SPEC_MINOR 주 및 부 버전 번호를 정의합니다. 이 설명서에 설명 된 odbc 버전의 경우 3과 0 이며 드라이버 "03.00"를 반환 해야 합니다.  
  
 ODBC 드라이버 관리자는 기존 응용 프로그램에 대 한 이전 버전과 호환성을 유지 하기 위해 SQLGetInfo(SQL_DRIVER_ODBC_VER)의 반환 값을 수정 하지 않습니다. 드라이버는 값이 반환 됩니다 지정 합니다. 그러나 C 데이터 형식 확장성을 지 원하는 드라이버를 3.8 (또는 이상) 경우에 반환 해야 합니다 응용 프로그램 호출 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 3.8로 설정 합니다. 자세한 내용은 [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 드라이버의 버전 및 드라이버에 대 한 설명을 선택적으로 사용 하 여 문자열입니다. 폼의 버전은 최소한 # #. # #. # # #, 여기서 처음 두 숫자는 주 버전, 다음 두 자리는 부 버전, 되며 마지막 4 자리 릴리스 버전입니다.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **어설션을 삭제** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_DA_DROP_ASSERTION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는이 옵션을 항상 반환 됩니다.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **문자 집합 삭제** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는이 옵션을 항상 반환 됩니다.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **데이터 정렬 DROP** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_DC_DROP_COLLATION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는이 옵션을 항상 반환 됩니다.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **DROP 도메인** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL-92 중간 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **DROP SCHEMA** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL-92 중간 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **DROP TABLE** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 전환 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **DROP 번역** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인에 사용 됩니다.  
  
 SQL_DTR_DROP_TRANSLATION  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 지원 되는이 옵션을 항상 반환 됩니다.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **DROP VIEW** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 전환 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원 되는 동적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 첫 번째 하위 집합을 포함 하는 비트이 마스크 두 번째 하위 집합을 SQL_DYNAMIC_CURSOR_ATTRIBUTES2를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA1_NEXT = *FetchOrientation* SQL_FETCH_NEXT의 인수에 대 한 호출에서 지원 됩니다 **SQLFetchScroll** 때 커서는 동적 커서.  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* SQL_FETCH_FIRST, SQL_FETCH_LAST, 및 SQL_FETCH_ABSOLUTE 인수에 대 한 호출에서 지원 됩니다 **SQLFetchScroll** 때 커서는 동적 커서. (인출 되는 행 집합은 현재 커서 위치와 무관 합니다.)  
  
 SQL_CA1_RELATIVE = *FetchOrientation* SQL_FETCH_PRIOR 고 SQL_FETCH_RELATIVE 인수에 대 한 호출에서 지원 됩니다 **SQLFetchScroll** 때 커서는 동적 커서. (현재 커서 위치에 인출 되는 행 집합에 따라 다릅니다. Note는이에서 분리 되어 SQL_FETCH_NEXT 있으므로 정방향 전용 커서는 SQL_FETCH_NEXT만 지원 됩니다.)  
  
 SQL_CA1_BOOKMARK = *FetchOrientation* SQL_FETCH_BOOKMARK의 인수에 대 한 호출에서 지원 됩니다 **SQLFetchScroll** 때 커서는 동적 커서.  
  
 SQL_CA1_LOCK_EXCLUSIVE = *LockType* SQL_LOCK_EXCLUSIVE의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_LOCK_NO_CHANGE = *LockType* SQL_LOCK_NO_CHANGE의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_LOCK_UNLOCK = *LockType* SQL_LOCK_UNLOCK의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_POS_POSITION =를 *작업이* SQL_POSITION의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_POS_UPDATE =를 *작업이* SQL_UPDATE의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_POS_DELETE =를 *작업이* SQL_DELETE의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_POS_REFRESH =를 *작업이* SQL_REFRESH의 인수에 대 한 호출에서 지원 됩니다 **SQLSetPos** 때 커서는 동적 커서.  
  
 SQL_CA1_POSITIONED_UPDATE =는 업데이트는 현재 SQL 문을 커서 동적 커서의 경우 지원 됩니다. (SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션으로 지원 됩니다.)  
  
 SQL_CA1_POSITIONED_DELETE = 삭제는 현재의 SQL 문은 커서는 동적 커서를 가져갈 때 지원 됩니다. (SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션으로 지원 됩니다.)  
  
 SQL_CA1_SELECT_FOR_UPDATE 커서는 동적 커서를 가져갈 때 UPDATE SQL 문에 사용할 선택 =. (SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션으로 지원 됩니다.)  
  
 SQL_CA1_BULK_ADD =를 *작업이* SQL_ADD의 인수에 대 한 호출에서 지원 됩니다 **SQLBulkOperations** 때 커서는 동적 커서.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK =를 *작업이* SQL_UPDATE_BY_BOOKMARK의 인수에 대 한 호출에서 지원 됩니다 **SQLBulkOperations** 때 커서는 동적 커서.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK =를 *작업이* SQL_DELETE_BY_BOOKMARK의 인수에 대 한 호출에서 지원 됩니다 **SQLBulkOperations** 때 커서는 동적 커서.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK =를 *작업이* SQL_FETCH_BY_BOOKMARK의 인수에 대 한 호출에서 지원 됩니다 **SQLBulkOperations** 때 커서는 동적 커서.  
  
 SQL-92 중간 수준-와 호환 되는 드라이버를 일반적으로 돌아가지 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE, 및 SQL_CA1_RELATIVE 옵션을 지원 하 고, 포함된 된 SQL 페치 문을 통해 스크롤 가능 커서를 지원 하기 때문에. 그러나이 확인 하지 때문에 직접 기본 SQL 지원, 스크롤 가능 커서 지원 되지, SQL-92 중간 수준-와 호환 되는 드라이버에 대해서도 합니다.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원 되는 동적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 두 번째 하위 집합을 포함 하는 비트이 마스크 첫 번째 하위 집합을 SQL_DYNAMIC_CURSOR_ATTRIBUTES1를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 읽기 전용는 업데이트할 수 없습니다, 동적 커서를 사용할 수 있습니다. (문 특성 SQL_ATTR_CONCURRENCY 동적 커서에 대 한 SQL_CONCUR_READ_ONLY 수 있음).  
  
 SQL_CA2_LOCK_CONCURRENCY 최하위 수준을 사용 하는 동적 커서 = 되도록 충분 한 잠금의 지원는 행을 업데이트할 수 있습니다. (문 특성 SQL_ATTR_CONCURRENCY 동적 커서에 대 한 SQL_CONCUR_LOCK 수 있습니다.) 이러한 잠금은 SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정 된 트랜잭션 격리 수준에 부합 해야 합니다.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 동적 커서의 행 버전 비교은 낙관적 동시성 제어를 사용 하 여 지원 됩니다. (문 특성 SQL_ATTR_CONCURRENCY 동적 커서에 대 한 SQL_CONCUR_ROWVER 수 있습니다.)  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 동적 커서는 낙관적 동시성 제어 비교 값을 사용 하 여 지원 됩니다. (문 특성 SQL_ATTR_CONCURRENCY 동적 커서에 대 한 SQL_CONCUR_VALUES 수 있습니다.)  
  
 SQL_CA2_SENSITIVITY_ADDITIONS Added = 행 동적 커서;에 표시 됩니다. 해당 행에 커서를 스크롤할 수입니다. (드라이버에 따라 다릅니다는 커서에 이러한 행이 추가 하는 위치입니다.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 삭제 된 행에는 동적 커서를 사용할 수 없게 됩니다 및 "구멍" 결과 집합에 두지 마십시오 동적 커서는 삭제 된 행을 스크롤하면 후에 해당 행을 반환할 수 없습니다.  
  
 SQL_CA2_SENSITIVITY_UPDATES = 행에 대 한 업데이트는 동적 커서에 표시 됩니다. 동적 커서에서 스크롤 하는 업데이트 된 행을 반환 하는 경우 커서에 의해 반환 되는 데이터는 업데이트 된 데이터를 원래 데이터가 아니라입니다.  
  
 SQL_CA2_MAX_ROWS_SELECT = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **선택** 문을 커서는 동적 커서.  
  
 SQL_CA2_MAX_ROWS_INSERT = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **삽입** 문을 커서는 동적 커서.  
  
 SQL_CA2_MAX_ROWS_DELETE = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **삭제** 문을 커서는 동적 커서.  
  
 SQL_CA2_MAX_ROWS_UPDATE = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **업데이트** 문을 커서는 동적 커서.  
  
 SQL_CA2_MAX_ROWS_CATALOG = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **카탈로그** 커서는 동적 커서를 가져갈 때 결과 집합입니다.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = The SQL_ATTR_MAX_ROWS 문 특성에 영향을 줍니다 **선택**를 **삽입**합니다 **삭제**, 및 **업데이트** 문 및 **카탈로그** 커서는 동적 커서를 가져갈 때 결과 집합을 합니다.  
  
 SQL_CA2_CRC_EXACT 정확한 = 커서는 동적 커서를 가져갈 때 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드를 행 개수는 사용할 수 있습니다.  
  
 SQL_CA2_CRC_APPROXIMATE 근사 = 커서는 동적 커서를 가져갈 때 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드를 행 개수는 사용할 수 있습니다.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE 드라이버 = 것을 보장 하지는 시뮬레이션 된 업데이트 위치 또는 delete 문은 커서는 동적 커서를 가져갈 때 하나의 행만 영향이 것은이 보장 하기 위해 응용 프로그램의 책임입니다. (문을 둘 이상의 행에 영향을 주 면 **SQLExecute** 또는 **SQLExecDirect** SQLSTATE 01001 [커서 작업이 충돌]를 반환 합니다.) 이 동작을 호출 하 여 응용 프로그램을 설정 하려면 **SQLSetStmtAttr** 는 SQL_ATTR_SIMULATE_CURSOR를 사용 하 여 특성이 SQL_SC_NON_UNIQUE로 설정 합니다.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE =는 시뮬레이션 된 위치 지정된 update 또는 delete 문을 영향을 줍니다 하나의 행만 커서는 동적 커서를 가져갈 때 드라이버 하려고 합니다. 드라이버는 항상 이러한 문에서 실행 때와 같이 둘 이상의 행에 영향을 줄 수 있습니다 하는 경우에 고유 키가 있습니다. (문을 둘 이상의 행에 영향을 주 면 **SQLExecute** 또는 **SQLExecDirect** SQLSTATE 01001 [커서 작업이 충돌]를 반환 합니다.) 이 동작을 호출 하 여 응용 프로그램을 설정 하려면 **SQLSetStmtAttr** 는 SQL_ATTR_SIMULATE_CURSOR를 사용 하 여 특성이 SQL_SC_TRY_UNIQUE로 설정 합니다.  
  
 SQL_CA2_SIMULATE_UNIQUE 드라이버 = 시뮬레이션 된 배치 업데이트 또는 delete 문을 커서는 동적 커서를 가져갈 때 하나의 행만 영향이 있습니다. 드라이버는이 지정 된 문에서 보장할 수 없습니다 하는 경우 **SQLExecDirect** 하거나 **SQLPrepare** SQLSTATE 01001 (커서 작업이 충돌)를 반환 합니다. 이 동작을 호출 하 여 응용 프로그램을 설정 하려면 **SQLSetStmtAttr** 는 SQL_ATTR_SIMULATE_CURSOR를 사용 하 여 특성이 SQL_SC_UNIQUE로 설정 합니다.  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 문자열: 데이터 원본 식을 지 원하는 경우 "Y"를 **ORDER BY** 목록 "N" 하지 않는 경우입니다.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 단일 계층 드라이버를이 파일 데이터 원본에서 직접 처리 하는 방법을 나타내는 SQLUSMALLINT 값:  
  
 SQL_FILE_NOT_SUPPORTED = 드라이버가 지원 되지 않는 단일 계층 드라이버입니다. 예를 들어, ORACLE 드라이버를는 2 계층 드라이버입니다.  
  
 SQL_FILE_TABLE = 테이블로 데이터 원본에는 단일 계층 드라이버 처리 파일. 예를 들어, Xbase 드라이버를 테이블로 각 Xbase 파일을 처리합니다.  
  
 SQL_FILE_CATALOG = 카탈로그를 데이터 원본에서 단일 계층 드라이버 처리 파일. 예를 들어, Microsoft Access 드라이버는 전체 데이터베이스를 각 Microsoft Access 파일을 처리합니다.  
  
 응용 프로그램 사용자 데이터를 선택 하는 방법을 결정 하는 데 사용할 수 있습니다. 예를 들어, ORACLE 및 Microsoft Access 사용자가 일반적으로 생각 하는 데이터 테이블에 저장 하는 반면 Xbase 사용자 파일에 저장 된 데이터의 생각 경우가 많습니다.  
  
 사용자가는 Xbase 데이터 소스를 선택 하면 응용 프로그램의 Windows를 표시할 수 있습니다 **파일 열기** 공용 대화 상자, Microsoft Access 또는 ORACLE 데이터 원본을 선택 하면 응용 프로그램 사용자 지정을 표시할 수 있습니다  **테이블 선택** 대화 상자.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원 되는 정방향 전용 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 첫 번째 하위 집합을 포함 하는 비트이 마스크 두 번째 하위 집합을 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 참조 (및 설명에 "동적 커서"에 대 한 "정방향 전용 커서"으로 대체).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원 되는 정방향 전용 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 두 번째 하위 집합을 포함 하는 비트이 마스크 첫 번째 하위 집합을 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 참조 (및 설명에 "동적 커서"에 대 한 "정방향 전용 커서"으로 대체).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 확장을 열거 하는 SQLUINTEGER 비트 마스크 **SQLGetData**합니다.  
  
 다음 비트 마스크는 플래그와 함께 드라이버 지원에 대 한 일반적인 확장 기능을 확인 하는 데 사용 됩니다 **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** 바인딩된 마지막 열 전에 포함 하 여 모든 바인딩되지 않은 열에 대해 호출할 수 있습니다. 참고 SQL_GD_ANY_ORDER에도 반환 하지 않는 한 열 번호를 오름차순 순서 대로 열을 호출 해야 합니다.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** 순서에 관계 없이 바인딩되지 않은 열에 대해 호출할 수 있습니다. 사실은 **SQLGetData** 바인딩된 마지막 열 SQL_GD_ANY_COLUMN에도 반환 하지 않는 한 후 열에 대해서만 호출할 수 있습니다.  
  
 SQL_GD_BLOCK = **SQLGetData** 사용 하 여 행에 위치 지정 후 데이터 (행 집합 크기가 1 보다 큰) 블록의 모든 행에 바인딩되지 않은 열에 대해 호출할 수 있습니다 **SQLSetPos**합니다.  
  
 SQL_GD_BOUND = **SQLGetData** 바인딩되지 않은 열 외에 바인딩된 열에 대해 호출할 수 있습니다. 드라이버는 SQL_GD_ANY_COLUMN도 반환 하지 않는 한이 값을 반환할 수 없습니다.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** 출력 매개 변수 값을 반환 하도록 호출 될 수 있습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
 **SQLGetData** 데이터 바인딩된 마지막 열을 한 후에 발생 하는 바인딩되지 않은 열 에서만에서 열 수를 늘리면의 순서로 호출 됩니다 및 행 블록의 행에 없는 반환 해야 합니다.  
  
 호출 하는 드라이버 (고정 길이 또는 가변 길이) 책갈피를 지 원하는 경우 지원 해야 합니다 **SQLGetData** 0 열에 있습니다. 이 지원은에 대 한 호출에 대 한 드라이버 반환 하는 것에 관계 없이 **SQLGetInfo** SQL_GETDATA_EXTENSIONS를 사용 하 여 *정보 항목*합니다.  
  
 SQL_GROUP_BY (ODBC 2.0)  
 열 간에 관계를 지정 하는 SQLUSMALLINT 값을 **GROUP BY** 절과 select 목록의 집계 열:  
  
 SQL_GB_COLLATE = **COLLATE** 각 그룹화 열 끝에 절을 지정할 수 있습니다. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** 절은 지원 되지 않습니다. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = 합니다 **GROUP BY** 절에 select 목록의 집계 열을 모두 포함 해야 합니다. 다른 열을 포함할 수 없습니다. 예를 들어 **DEPT, MAX(SALARY)에서 직원 그룹 선택 BY DEPT**합니다. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = 합니다 **GROUP BY** 절에 select 목록의 집계 열을 모두 포함 해야 합니다. Select 목록에 없는 열을 포함할 수 있습니다. 예를 들어 **DEPT, MAX(SALARY)에서 직원 그룹 선택 BY DEPT, 사용 기간**합니다. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION =에서 열을 **GROUP BY** 절과 select 목록에 관련이 없습니다. Select 목록의 집계, 그룹화 되지 않은 열의 의미를 데이터 원본에 따라 결정 됩니다. 예를 들어 **DEPT, 급여에서 직원 그룹 선택 BY DEPT, 사용 기간**합니다. (ODBC 2.0)  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_GB_GROUP_BY_EQUALS_SELECT 옵션을 항상 반환 됩니다. SQL-92 Full 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_GB_COLLATE 옵션을 항상 반환 됩니다. None 옵션은 지원 되는 경우는 **GROUP BY** 절은 데이터 원본에서 지원 되지 않습니다.  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 SQLUSMALLINT 다음과 같이 값:  
  
 SQL_IC_UPPER = SQL에서 식별자 대/소문자 구분 하지 않으며에 저장 된 시스템 카탈로그에서 대문자입니다.  
  
 SQL_IC_LOWER = SQL에서 식별자 대/소문자 구분 하지 않으며 시스템 카탈로그에서 소문자에 저장 됩니다.  
  
 Sql_ic_sensitive입니다 = SQL에서 식별자 대/소문자 구분 및 혼합 된 경우 시스템 카탈로그에에서 저장 됩니다.  
  
 Sql_ic_mixed입니다 = SQL에서 식별자 대/소문자 구분 하지 않으며 시스템 카탈로그에서 대/소문자를 혼합된에 저장 됩니다.  
  
 SQL-92에 식별자를 대/소문자 구분 하지 않습니다 이기 때문에 지원 되는 SQL-92 (모든 수준)를 엄격 하 게 준수 하는 드라이버 sql_ic_sensitive입니다 옵션을 반환 하지 않습니다.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 따옴표 붙은의 시작 및 끝 구분 기호로 사용 되는 문자열 (구분) SQL 문에서 식별자입니다. (ODBC 함수에 인수로 전달 된 식별자 않아도 따옴표로 묶을 수 있습니다.) 데이터 원본에서 따옴표 붙은 식별자를 지원 하지 않으면, blank가 반환 됩니다.  
  
 이 문자열을 연결 특성 SQL_ATTR_METADATA_ID SQL_TRUE로 설정 된 경우 카탈로그 함수 인수를 따옴표로 사용할 수도 있습니다.  
  
 SQL-92에 식별자 따옴표 문자로 큰따옴표 (") 이기 때문에 따르는 드라이버를 엄격 하 게 SQL-92에 항상 반환 됩니다 큰따옴표 문자.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 드라이버에서 지원 되는 CREATE INDEX 문에서 키워드를 열거 하는 SQLUINTEGER 비트 마스크:  
  
 SQL_IK_NONE = 지원 되지 않습니다 키워드입니다.  
  
 SQL_IK_ASC = ASC 키워드는 지원 합니다.  
  
 SQL_IK_DESC = DESC 키워드는 지원 합니다.  
  
 SQL_IK_ALL = All 키워드는 지원 합니다.  
  
 CREATE INDEX 문의 지원 되는지 여부를 보려는 응용 프로그램 호출 **SQLGetInfo** SQL_DLL_INDEX 정보 형식을 사용 하 여 합니다.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 드라이버에서 지원 되는 뷰는 INFORMATION_SCHEMA에 열거 SQLUINTEGER 비트 마스크입니다. 에서는 뷰와의 내용을 INFORMATION_SCHEMA SQL-92에 정의 되어 있습니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 보기에서 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_ISV_ASSERTIONS = 지정된 된 사용자가 소유 하는 카탈로그의 어설션을 식별 합니다. (전체 수준)  
  
 SQL_ISV_CHARACTER_SETS = 지정된 된 사용자가 액세스할 수 있는 카탈로그의 문자 집합을 나타냅니다. (중간 수준)  
  
 SQL_ISV_CHECK_CONSTRAINTS 나타냅니다 확인 = 지정된 된 사용자가 소유 하는 제약 조건입니다. (중간 수준)  
  
 SQL_ISV_COLLATIONS = 지정된 된 사용자가 액세스할 수 있는 카탈로그에 대 한 문자 데이터 정렬을 식별 합니다. (전체 수준)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 카탈로그에 정의 된 도메인에 따라 달라 집니다는 지정된 된 사용자가 소유 하는 카탈로그에 대 한 열을 나타냅니다. (중간 수준)  
  
 SQL_ISV_COLUMN_PRIVILEGES = 사용할 수 있거나 부여한 지정된 된 사용자가 영구 테이블의 열에 대 한 권한을 식별 합니다. (FIPS 전환 수준)  
  
 SQL_ISV_COLUMNS = 지정된 된 사용자가 액세스할 수 있는 영구 테이블의 열을 식별 합니다. (FIPS 전환 수준)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE 근사치 = CONSTRAINT_TABLE_USAGE 뷰를 열은 지정된 된 사용자가 소유 하는 다양 한 제약 조건을 식별 합니다. (중간 수준)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 제약 조건으로 사용 되는 테이블을 식별 (참조, 고유 및 어설션을), 지정된 된 사용자가 소유 하 고 있습니다. (중간 수준)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 지정된 된 사용자가 액세스할 수 있는 (카탈로그에 도메인)의 도메인 제약 조건을 식별 합니다. (중간 수준)  
  
 SQL_ISV_DOMAINS = 사용자가 액세스할 수 있는 카탈로그에 정의 된 도메인을 나타냅니다. (중간 수준)  
  
 SQL_ISV_KEY_COLUMN_USAGE = 지정된 된 사용자가 키로 제한 되는 카탈로그에 정의 되는 나타냅니다 열입니다. (중간 수준)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 지정된 된 사용자가 소유 하는 참조 제약 조건을 식별 합니다. (중간 수준)  
  
 SQL_ISV_SCHEMATA = 지정된 된 사용자가 소유한 스키마를 식별 합니다. (중간 수준)  
  
 SQL_ISV_SQL_LANGUAGES = SQL 구현에서 지 원하는 SQL 적합성 수준, 옵션 및 언어를 나타냅니다. (중간 수준)  
  
 SQL_ISV_TABLE_CONSTRAINTS = 지정된 된 사용자가 소유한 테이블 제약 조건을 식별 합니다. (중간 수준)  
  
 SQL_ISV_TABLE_PRIVILEGES = 영구 테이블에 사용할 수 있거나 부여한 지정된 된 사용자가 권한을 식별 합니다. (FIPS 전환 수준)  
  
 SQL_ISV_TABLES = 지정된 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 영구 테이블을 나타냅니다. (FIPS 전환 수준)  
  
 SQL_ISV_TRANSLATIONS = 지정된 된 사용자가 액세스할 수 있는 카탈로그에 대 한 문자 변환을 나타냅니다. (전체 수준)  
  
 SQL_ISV_USAGE_PRIVILEGES =가 사용할 수 있거나 지정된 된 사용자가 소유 하는 카탈로그 개체에서 사용 권한을 나타냅니다. (FIPS 전환 수준)  
  
 SQL_ISV_VIEW_COLUMN_USAGE 나타냅니다 지정된 된 사용자가 소유 하는 카탈로그 뷰는 기반이 열 = 다릅니다. (중간 수준)  
  
 SQL_ISV_VIEW_TABLE_USAGE 지정된 된 사용자가 소유 하는 카탈로그 뷰는 기반이 테이블 나타냅니다 = 다릅니다. (중간 수준)  
  
 SQL_ISV_VIEWS = 지정된 된 사용자가 액세스할 수 있는이 카탈로그에 표시 된 테이블 정의 나타냅니다. (FIPS 전환 수준)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 원하는 것으로 표시 하는 SQLUINTEGER 비트 마스크 **삽입** 문:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_INTEGRITY (ODBC 1.0)  
 문자열: 데이터 원본에는 무결성 향상 기능이;에서 지 원하는 경우 "Y" "N" 하지 않는 경우입니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_ODBC_SQL_OPT_IEF 합니다.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원 되는 키 집합 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 첫 번째 하위 집합을 포함 하는 비트이 마스크 두 번째 하위 집합을 SQL_KEYSET_CURSOR_ATTRIBUTES2를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (보고 "키 집합 커서" 설명에서 "동적 커서"에 대 한 대체).  
  
 SQL-92 중간 수준-와 호환 되는 드라이버는 일반적으로 반환 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE, 및 SQL_CA1_RELATIVE 옵션 지원 드라이버가 포함된 된 SQL 페치 문을 통해 스크롤 가능 커서를 지원 하기 때문에 합니다. 그러나이 확인 하지 때문에 직접 기본 SQL 지원, 스크롤 가능 커서 지원 되지, SQL-92 중간 수준-와 호환 되는 드라이버에 대해서도 합니다.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원 되는 키 집합 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 두 번째 하위 집합을 포함 하는 비트이 마스크 첫 번째 하위 집합을 SQL_KEYSET_CURSOR_ATTRIBUTES1를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (보고 "키 집합 커서" 설명에서 "동적 커서"에 대 한 대체).  
  
 SQL_KEYWORDS (ODBC 2.0)  
 모든 데이터 소스 특정 키워드의 쉼표로 구분 된 목록을 포함 하는 문자열입니다. 이 목록은 특정 odbc 키워드 또는 데이터 원본 및 ODBC 모두에서 사용 되는 키워드를 포함 하지 않습니다. 이 목록은 모든 예약 된 키워드입니다. 상호 운용 가능한 응용 프로그램 개체 이름에이 예약어를 사용 해야 합니다.  
  
 ODBC 키워드 목록은 참조 하세요 [예약어](../../../odbc/reference/appendixes/reserved-keywords.md) 에서 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다. 합니다 **#define** 값 SQL_ODBC_KEYWORDS ODBC 키워드의 쉼표로 구분 된 목록을 포함 합니다.  
  
 부록 C: SQL 문법  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 문자열: 백분율 문자 (%)에 대 한 데이터 소스에서 이스케이프 문자를 지원 하는 경우 "Y" 및 밑줄 (_)에서 문자를 **와 같은** 조건자 및 드라이버를 정의 하기 위한 ODBC 구문을 지원함을 **와 같은** 조건자 이스케이프 문자 "N"이 고 그렇지 합니다.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 드라이버는 지정된 된 연결을 지원할 수 있는 비동기 모드에서 활성 동시 문의 최대 수를 지정 하는 SQLUINTEGER 값입니다. 특정 제한이 또는 알 수 없는 경우이 값이 0으로 설정 합니다.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 최대 길이 지정 하는 SQLUINTEGER 값 (16 진수 문자를 제외 된 리터럴 접두사 및 접미사 반환한 수가 **SQLGetTypeInfo**) 이진 리터럴을 SQL 문에서 합니다. 예를 들어, 이진 리터럴 0xFFAA 길이는 4에 있습니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 데이터 원본에서 카탈로그 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 전체 수준-와 호환 되는 드라이버를 최소한 128을 반환 됩니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_MAX_QUALIFIER_NAME_LEN 합니다.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 최대 길이 지정 하는 SQLUINTEGER 값 (리터럴 접두사와 접미사 반환한 제외 하 고 문자 수가 **SQLGetTypeInfo**)는 SQL 문의 리터럴 문자. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 데이터 원본에서 열 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 18 자 이상이 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 128을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 허용 되는 열의 최대 수를 지정 하는 SQLUSMALLINT 값을 **GROUP BY** 절. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버는 적어도 6을 반환 합니다. FIPS 중간 수준-와 호환 되는 드라이버는 적어도 15를 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 인덱스의 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 허용 되는 열의 최대 수를 지정 하는 SQLUSMALLINT 값을 **ORDER BY** 절. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버는 적어도 6을 반환 합니다. FIPS 중간 수준-와 호환 되는 드라이버는 적어도 15를 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 선택 목록에서 사용할 수 있는 열의 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버는 적어도 100 개를 반환 합니다. FIPS 중간 수준-와 호환 되는 드라이버는 250 이상 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 테이블의 열 수의 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버는 적어도 100 개를 반환 합니다. FIPS 중간 수준-와 호환 되는 드라이버는 250 이상 반환 합니다.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 활성 문 드라이버에 대 한 연결을 지원할 수 있는 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 행이 포함 된 용어 "결과" 의미를 보류 중인 결과가 있으면 활성으로 문을 정의 **선택** 작업이 나 영향을 받는 행을 **삽입**, **업데이트**, 또는 **삭제** 작업 (예: 행 개수) NEED_DATA 상태의 인스턴스인 경우. 이 값은 드라이버 또는 데이터 원본에 따른 제한을 반영할 수 있습니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_ACTIVE_STATEMENTS 합니다.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 데이터 원본에서 커서 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 18 자 이상이 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 128을 반환 합니다.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 환경에 대 한 드라이버를 지원할 수 있는 활성 연결의 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 이 값은 드라이버 또는 데이터 원본에 따른 제한을 반영할 수 있습니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_ACTIVE_CONNECTIONS 합니다.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 사용자 정의 이름에 대 한 데이터 원본에서 지 자에서 최대 크기를 나타내는 SQLUSMALLINT 합니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 18 자 이상이 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 128을 반환 합니다.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 인덱스의 결합 된 필드에 허용 된 바이트의 최대 수를 지정 하는 SQLUINTEGER 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 데이터 원본에 프로시저 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 테이블의 단일 행의 최대 길이 지정 하는 SQLUINTEGER 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 2,000 이상 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 8,000 개 이상 반환 합니다.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 문자열: 행에서 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR를 모두 열 길이 포함 하는 "Y" SQL_MAX_ROW_SIZE 정보 유형에 대 한 최대 행 크기를 반환 하는 경우 "N"이 고 그렇지 합니다.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 데이터 소스의 스키마 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 18 자 이상이 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 128을 반환 합니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_MAX_OWNER_NAME_LEN 합니다.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 SQL 문의 최대 길이 (문자를 포함 하 여 공백 수)를 지정 하는 SQLUINTEGER 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 데이터 원본에 테이블 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버를 18 자 이상이 반환 됩니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 128을 반환 합니다.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 허용 하는 테이블의 최대 수를 지정 하는 SQLUSMALLINT 값을 **FROM** 절을 **선택** 문입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 FIPS 항목 수준-와 호환 되는 드라이버는 적어도 15를 반환 합니다. FIPS 중간 수준-와 호환 되는 드라이버는 최소한 50을 반환 합니다.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 데이터 원본에 사용자 이름의 최대 길이 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없는 또는 길이 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 문자열: "Y" 없으면 데이터 원본에서 여러 결과 집합을 "N"를 지원 합니다.  
  
 여러 결과 집합에 대 한 자세한 내용은 참조 하세요. [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 문자열: "Y" 드라이버만 언제 든 지 하나의 트랜잭션만 활성화할 수 있습니다 동시 "N"에 둘 이상의 활성 트랜잭션을 지 원하는 경우.  
  
 이 정보 유형에 대해 반환 되는 정보는 분산된 트랜잭션의 경우 적용 되지 않습니다.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 문자열: 그렇지 않은 경우 데이터 원본이 전에 해당 값 데이터 형식 이어서 SQL_LONGVARBINARY, SQL_LONGVARCHAR, long 데이터 소스 관련 데이터 형식이 long 데이터 값의 길이 해야 하는 경우 "Y"는 "N" 데이터 원본에 전송 됩니다. 자세한 내용은 [SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md) 하 고 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 데이터 원본 열에 NOT NULL을 지원 하는지 여부를 지정 하는 SQLUSMALLINT 값:  
  
 SQL_NNC_NULL = 모든 열이 null을 허용 해야 합니다.  
  
 SQL_NNC_NON_NULL = 열이 nullable 일 수 없습니다. (데이터 원본 지원 합니다 **NOT NULL** 열 제약 조건 **CREATE TABLE** 문.)  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 SQL_NNC_NON_NULL 반환 됩니다.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 Null 결과 집합을 정렬 되는 위치를 지정 하는 SQLUSMALLINT 값:  
  
 SQL_NC_END = Null ASC 또는 DESC 키워드에 관계 없이 결과 집합의 끝에 정렬 됩니다.  
  
 SQL_NC_HIGH = Null 높은 ASC 또는 DESC 키워드에 따라 결과 집합 끝에 정렬 됩니다.  
  
 SQL_NC_LOW = Null 낮은 ASC 또는 DESC 키워드에 따라 결과 집합 끝에 정렬 됩니다.  
  
 SQL_NC_START = Null ASC 또는 DESC 키워드에 관계 없이 결과 집합의 시작 부분에 정렬 됩니다.  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 참고: 정보 유형 ODBC 1.0;에 도입 합니다. 각 비트 마스크는 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 숫자 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 숫자 함수를 결정 하는 데 사용 됩니다.  
  
 (ODBC 1.0) SQL_FN_NUM_ABS SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_ SQL_FN_NUM_DEGREES (ODBC 2.0) (ODBC 1.0) FN_NUM_EXP SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_ SQL_FN_NUM_POWER (ODBC 2.0) (ODBC 2.0) NUM_ROUND SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 ODBC 3 수준을 표시 하는 SQLUINTEGER 값 *.x* 드라이버를 준수 하는 인터페이스입니다.  
  
 SQL_OIC_CORE: 모든 ODBC 드라이버는 최소 수준 준수 해야 합니다. 이 수준은 연결 함수, 준비 하 고 SQL 문을 실행 하는 함수, 기본 결과 집합 메타 데이터 함수, 기본 카탈로그 함수 등과 같은 기본 인터페이스 요소를 포함 합니다.  
  
 SQL_OIC_LEVEL1: Core 스크롤 가능 커서를 포함 하는 표준 준수 수준 기능, 책갈피, 배치를 포함 하 여 수준을 업데이트 및 삭제를 등에입니다.  
  
 SQL_OIC_LEVEL2: 중요 한 커서;와 같은 고급 기능도 수준 1 표준 준수 수준 기능을 비롯 한 수준 업데이트, 삭제 및 책갈피;에서 새로 고침 저장된 프로시저 지원 합니다. 기본 및 외래 키에 대 한 카탈로그 함수 다중 카탈로그 지원. 등에입니다.  
  
 자세한 내용은 [인터페이스 적합성 수준](../../../odbc/reference/develop-app/interface-conformance-levels.md)합니다.  
  
 SQL_ODBC_VER (ODBC 1.0)  
 버전의 ODBC 드라이버 관리자는 준수 하는 문자열입니다. 폼의 버전은 # #. # #. 0000, 여기에서 처음 두 숫자는 주 버전 하 고 다음 두 자리는 부 버전. 드라이버 관리자에만 구현 됩니다.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 드라이버 및 데이터 원본에서 지 원하는 외부 조인 형식 열거 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 어떤 형식이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_OJ_LEFT = Left outer join이 지원 됩니다.  
  
 SQL_OJ_RIGHT = Right outer join이 지원 됩니다.  
  
 SQL_OJ_FULL = Full outer join이 지원 됩니다.  
  
 SQL_OJ_NESTED 중첩 = 외부 조인은 지원 됩니다.  
  
 SQL_OJ_NOT_ORDERED = 외부 조인의 ON 절에는 이름에서 해당 테이블 이름으로 동일한 순서로 없는 열을 **OUTER JOIN** 절.  
  
 SQL_OJ_INNER = 내부 테이블 (왼쪽 우선 외부 조인 오른쪽 테이블) 또는 오른쪽 우선 외부 조인의 왼쪽된 테이블 inner join에 사용할 수도 있습니다. 내부 테이블을 없는 완전 외부 조인에는 적용 되지 않습니다.  
  
 SQL_OJ_ALL_COMPARISON_OPS 비교 = ON 절에서 연산자는 ODBC 비교 연산자 중 하나일 수 있습니다. 이 비트가 설정 되어 있지 않으면 등호 (=) 비교 연산자만 외부 조인에 사용할 수 있습니다.  
  
 이러한 옵션에 지원 되는 반환 되 면 외부 조인 절 없이 사용할 수 있습니다.  
  
 SELECT 문에서 관계형 조인 연산자는 지원에 대 한 정보에 대 한 SQL-92에 정의 된 대로 SQL_SQL92_RELATIONAL_JOIN_OPERATORS 참조 합니다.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 문자열: "Y" 경우의 열을 **ORDER BY** 절은 선택 목록에에 있어야 합니다.이 고, 그렇지 "N"입니다.  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 행의 가용성에 대 한 드라이버의 속성을 열거 하는 SQLUINTEGER 매개 변수가 있는 실행 수 있습니다. 에 다음 값:  
  
 SQL_PARC_BATCH = 개인 행 개수 매개 변수의 각 집합에 대해 사용할 수 있습니다. 각 매개 변수 배열에 있는 설정에 대 한 SQL 문의 일괄 처리를 생성 하는 드라이버를 개념적으로 동일 합니다. SQL_PARAM_STATUS_PTR 설명자 필드를 사용 하 여 확장된 오류 정보를 검색할 수 있습니다.  
  
 SQL_PARC_NO_BATCH = 매개 변수의 전체 배열에 대 한 문의 실행 결과 누적 행 수에는 하나의 행 개수를 사용할 수 있습니다. 원자 단위로 완료 매개 변수 배열 함께 문을 처리 하는 방법에 개념적으로 동일 합니다. 오류는 한 문이 실행 된 것 처럼 동일한 처리 됩니다.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 결과의 가용성에 대 한 드라이버의 속성을 열거 하는 SQLUINTEGER 매개 변수가 있는 실행을 설정 합니다. 에 다음 값:  
  
 SQL_PAS_BATCH = 결과가 두 개 매개 변수 집합에 따라 사용할 수 있는 설정입니다. 각 매개 변수 배열에 있는 설정에 대 한 SQL 문의 일괄 처리를 생성 하는 드라이버를 개념적으로 동일 합니다.  
  
 SQL_PAS_NO_BATCH = 누적 결과 나타내는 하나의 결과 집합을 사용할 수 있는 매개 변수의 전체 배열에 대 한 문 실행에서 결과 집합이 있습니다. 원자 단위로 완료 매개 변수 배열 함께 문을 처리 하는 방법에 개념적으로 동일 합니다.  
  
 SQL_PAS_NO_SELECT = 드라이버는 결과 집합 생성 문 매개 변수 배열을 사용 하 여 실행할 수 없도록 합니다.  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 프로시저; 데이터 원본 공급 업체의 이름 사용 하 여 문자열 예를 들어 "데이터베이스 프로시저", "저장된 프로시저", "procedure", "패키지" 또는 "저장된 쿼리"입니다.  
  
 SQL_PROCEDURES (ODBC 1.0)  
 문자열: 프로시저 및 드라이버 데이터 원본에서 지 원하는 경우 "Y" ODBC 프로시저 호출 구문; 지원 "N"이 고 그렇지 합니다.  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 지원 작업을 열거 하는 SQLINTEGER 비트 마스크 **SQLSetPos**합니다.  
  
 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하려면 플래그와 함께 사용 됩니다.  
  
 (ODBC 2.0) SQL_POS_POSITION SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 SQLUSMALLINT 다음과 같이 값:  
  
 SQL_IC_UPPER 따옴표 붙은 = SQL에서 식별자 대/소문자 구분 하지 않으며에 저장 된 시스템 카탈로그에서 대문자입니다.  
  
 SQL_IC_LOWER 따옴표 붙은 = SQL에서 식별자 대/소문자 구분 하지 않으며 시스템 카탈로그에서 소문자에 저장 됩니다.  
  
 Sql_ic_sensitive입니다 따옴표 붙은 = SQL에서 식별자 대/소문자 구분 및 혼합 된 경우 시스템 카탈로그에에서 저장 됩니다. (SQL 92 규격 데이터베이스의 따옴표 붙은 식별자는 항상 대/소문자 구분입니다.)  
  
 Sql_ic_mixed입니다 따옴표 붙은 = SQL에서 식별자 대/소문자 구분 하지 않으며 시스템 카탈로그에서 대/소문자를 혼합된에 저장 됩니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 sql_ic_sensitive 입니다를 항상 반환 됩니다.  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 문자열: "Y" 키 집합 커서 또는 혼합 커서 모두에 대 한 값 또는 행 버전을 유지 하는 경우 행을 인출 하 고 따라서 행이 마지막으로 인출 된 이후 모든 사용자가 행에 수행 된 모든 업데이트를 검색할 수 있습니다. (이에 적용 됩니다 업데이트, 삭제 또는 삽입 합니다.) 드라이버 행 상태로 SQL_ROW_UPDATED 플래그를 반환할 수 있습니다 때 배열 **SQLFetchScroll** 라고 합니다. 그렇지 않으면 "N"입니다.  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 스키마에 대 한 데이터 원본 공급 업체의 이름 가진 문자열 예를 들어, "소유자", "권한 부여 ID" 또는 "Schema".  
  
 위쪽, 아래쪽, 또는 혼합의 경우 문자열을 반환할 수 있습니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버는 항상 "schema"를 반환 합니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_OWNER_TERM 합니다.  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 스키마 사용 될 수 있는 문을 열거 SQLUINTEGER 비트 마스크:  
  
 SQL_SU_DML_STATEMENTS = 스키마는 모든 데이터 조작 언어 문에서 지원 됩니다. **선택**, **삽입**, **업데이트**를 **삭제**을 지원 하 고 **업데이트에 대 한 선택** 위치 지정 업데이트 및 삭제 하 고 문입니다.  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 프로시저 호출 문에 스키마를 지원 합니다.  
  
 SQL_SU_TABLE_DEFINITION = 모든 테이블 정의 문에 스키마를 지원 합니다. **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**를 **DROP TABLE**, 및 **DROP VIEW**합니다.  
  
 SQL_SU_INDEX_DEFINITION = 모든 인덱스 정의 문에 스키마를 지원 합니다. **인덱스를 만들** 하 고 **DROP INDEX**합니다.  
  
 SQL_SU_PRIVILEGE_DEFINITION = 모든 권한 정의 문에 스키마를 지원 합니다. **권한 부여** 하 고 **해지**합니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 지 원하는 대로 SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION, 및 SQL_SU_PRIVILEGE_DEFINITION 옵션을 항상 반환 됩니다.  
  
 이렇게 *정보 항목* ODBC 2.0에서 ODBC 3.0 바뀌었습니다 *정보 항목* SQL_OWNER_USAGE 합니다.  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 참고: 정보 유형 ODBC 1.0;에 도입 합니다. 각 비트 마스크는 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 스크롤 가능 커서에 대 한 지원 되는 스크롤 옵션을 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SO_FORWARD_ONLY = 앞으로 커서만 스크롤합니다. ODBC (1.0)  
  
 SQL_SO_STATIC 데이터 = 결과 집합은 정적입니다. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 드라이버 저장 하 고 결과 집합의 모든 행에 대 한 키를 사용 합니다. ODBC (1.0)  
  
 SQL_SO_DYNAMIC = 드라이버 유지 (키 집합 크기는 행 집합 크기와 동일) 행 집합의 모든 행에 대 한 키입니다. ODBC (1.0)  
  
 SQL_SO_MIXED 드라이버 유지 키 = keyset, 키 집합 크기의 모든 행이 행 집합 크기 보다 큽니다. 키 집합 내에서 키 집합 커서와 키 집합 외부 동적 커서가 있습니다. ODBC (1.0)  
  
 스크롤 가능 커서에 대 한 정보를 참조 하세요 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 드라이버에서 지 원하는 작업 검색 패턴에서 유효한 문자로 패턴 일치 메타 문자가 밑줄 (_) 및 백분율 기호 (%)의 사용을 허용 하는 이스케이프 문자로 지정 하는 문자열입니다. 이 이스케이프 문자는 검색 문자열을 지 원하는 해당 카탈로그 함수 인수에만 적용 됩니다. 이 문자열이 비어 있으면 드라이버는 검색 패턴 이스케이프 문자를 지원 하지 않습니다.  
  
 이 정보 유형은 일반 지원에서 이스케이프 문자를 인식 하지 못하기 때문에 합니다 **같은** 조건자 SQL-92에 없는이 문자열에 대 한 요구 사항입니다.  
  
 이렇게 *정보 항목* 카탈로그 함수로 제한 됩니다. 검색 패턴 문자열의 이스케이프 문자 사용에 대 한 참조 [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
 SQL_SERVER_NAME (ODBC 1.0)  
 문자열을 실제 데이터 소스 관련 서버 이름입니다. 데이터 원본 이름 중에 사용 되는 경우에 유용 **SQLConnect**를 **SQLDriverConnect**, 및 **SQLBrowseConnect**합니다.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 테이블 이름, 열 이름 또는 데이터 원본에서 인덱스 이름 등을 식별자 이름에서 사용할 수 있는 모든 특수 문자 (즉, a ~ z, A ~ Z, 0-9 및 밑줄을 제외한 모든 문자)를 포함 하는 문자열입니다. 예를 들어, "#$^"입니다. 식별자의 이러한 문자 하나 이상 있으면 식별자에 구분된 식별자 여야 합니다.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 드라이버에서 지 원하는 SQL-92 수준을 표시 하는 SQLUINTEGER 값:  
  
 SQL_SC_SQL92_ENTRY 항목 수준 SQL-92 규격 =.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 전환 level 규정을 준수 합니다.  
  
 SQL_SC_SQL92_FULL = 전체 level SQL-92 규격입니다.  
  
 SQL_SC_ SQL92_INTERMEDIATE 중간 수준 SQL-92 규격 =.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 SQL-92에 정의 된 대로 드라이버 및 연결 된 데이터 원본에서 지원 되는 datetime 스칼라 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 날짜/시간 함수를 결정 하는 데 사용 됩니다.  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 외래 키에 대 한 지원 되는 규칙을 열거 하는 SQLUINTEGER 비트 마스크를 **삭제** SQL-92에 정의 된 대로 문입니다.  
  
 다음 비트 마스크는 절은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 전환 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 외래 키에 대 한 지원 되는 규칙을 열거 하는 SQLUINTEGER 비트 마스크를 **업데이트** SQL-92에 정의 된 대로 문입니다.  
  
 다음 비트 마스크는 절은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL-92 Full 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 지원 되는 절을 열거 하는 SQLUINTEGER 비트 마스크를 **부여** SQL-92에 정의 된 대로 문입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (항목 수준) SQL_SG_DELETE_TABLE SQL_SG_INSERT_COLUMN (중간 수준) SQL_SG_INSERT_TABLE (항목 수준) (항목 수준) SQL_SG_REFERENCES_TABLE SQL_SG_REFERENCES_COLUMN (항목 수준) (항목 수준) SQL_SG_SELECT_TABLE SQL_SG_UPDATE_COLUMN ( 항목 수준) (항목 수준) SQL_SG_UPDATE_TABLE SQL_SG_USAGE_ON_DOMAIN (FIPS 전환 수준) (FIPS 전환 수준) SQL_SG_USAGE_ON_CHARACTER_SET SQL_SG_USAGE_ON_COLLATION (FIPS 전환 수준) SQL_SG_USAGE_ON_TRANSLATION (FIPS 전환 수준) SQL_SG_WITH_GRANT_OPTION (항목 수준)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 SQL-92에 정의 된 대로 드라이버 및 연결 된 데이터 원본에서 지원 되는 숫자 값 스칼라 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 숫자 함수를 결정 하는 데 사용 됩니다.  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 지원 되는 조건자를 열거 하는 SQLUINTEGER 비트 마스크를 **선택** SQL-92에 정의 된 대로 문입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크 옵션은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (항목 수준) SQL_SP_BETWEEN SQL_SP_COMPARISON (항목 수준) SQL_SP_EXISTS (항목 수준) SQL_SP_IN (항목 수준) SQL_SP_ISNOTNULL (항목 수준) SQL_SP_ISNULL (항목 수준) SQL_SP_LIKE (항목 수준) (전체 수준) SQL_SP_MATCH_FULL SQL_SP_MATCH_PARTIAL (전체 수준) (전체 수준) SQL_SP_MATCH_UNIQUE_FULL SQL_SP_MATCH_UNIQUE_PARTIAL (전체 수준) SQL_SP_OVERLAPS (FIPS 전환 수준) (항목 수준) SQL_SP_QUANTIFIED_COMPARISON SQL_SP_UNIQUE (항목 수준)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 지원 되는 관계형 조인 연산자를 열거 하는 SQLUINTEGER 비트 마스크를 **선택** SQL-92에 정의 된 대로 문입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크 옵션은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (중간 수준) SQL_SRJO_CORRESPONDING_CLAUSE SQL_SRJO_CROSS_JOIN (전체 수준) SQL_SRJO_EXCEPT_JOIN (중간 수준) SQL_SRJO_FULL_OUTER_JOIN (중간 수준) (FIPS 전환 수준) SQL_SRJO_INNER_JOIN SQL_SRJO_INTERSECT_JOIN (중간 수준) (FIPS 전환 수준) SQL_SRJO_LEFT_OUTER_JOIN SQL_SRJO_NATURAL_JOIN (FIPS 전환 수준) (FIPS 전환 수준) SQL_SRJO_RIGHT_OUTER_JOIN SQL_SRJO_UNION_JOIN (전체 수준)  
  
 SQL_SRJO_INNER_JOIN 원하는 것으로 표시 합니다 **INNER JOIN** 구문에는 내부 조인 기능이 없습니다. 에 대 한 지원 합니다 **내부 조인** 반면의 구문은 FIPS 전환, 내부 조인 기능에 대 한 지원은 **항목**합니다.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 지원 되는 절을 열거 하는 SQLUINTEGER 비트 마스크를 **REVOKE** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SR_CASCADE (FIPS 전환 수준) SQL_SR_DELETE_TABLE (항목 수준) (중간 수준) SQL_SR_GRANT_OPTION_FOR SQL_SR_INSERT_TABLE (항목 수준) SQL_SR_REFERENCES_COLUMN (항목 수준) SQL_SR_ SQL_SR_INSERT_COLUMN (중간 수준) (항목 수준) REFERENCES_TABLE SQL_SR_RESTRICT (FIPS 전환 수준) SQL_SR_SELECT_TABLE (항목 수준) SQL_SR_UPDATE_TABLE (항목 수준) SQL_SR_USAGE_ON_DOMAIN (FIPS 전환 수준) SQL_SR_USAGE_ON_ SQL_SR_UPDATE_COLUMN (항목 수준) CHARACTER_SET (FIPS 전환 수준) (FIPS 전환 수준) SQL_SR_USAGE_ON_COLLATION SQL_SR_USAGE_ON_TRANSLATION (FIPS 전환 수준)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 지원 되는 행 값 생성자 식을 열거 하는 SQLUINTEGER 비트 마스크를 **선택** SQL-92에 정의 된 대로 문입니다. 다음 비트 마스크 옵션은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 SQL-92에 정의 된 대로 드라이버 및 연결 된 데이터 원본을 지 원하는 문자열 스칼라 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 마스크 문자열 함수를 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 SQL-92에 정의 된 대로 지원 값 식 열거 SQLUINTEGER 비트 마스크입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크 옵션은 데이터 원본에 의해 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (중간 수준) SQL_SVE_CASE SQL_SVE_CAST (FIPS 전환 수준) (중간 수준) SQL_SVE_COALESCE SQL_SVE_NULLIF (중간 수준)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 드라이버를 준수 하는 CLI 표준 또는 표준 열거 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 드라이버를 준수 하는 수준을 결정 하는 데 사용 됩니다.  
  
 SQL_SCC_XOPEN_CLI_VERSION1: 드라이버에서 열린 그룹 CLI 버전 1 준수합니다.  
  
 SQL_SCC_ISO92_CLI: ISO 92 CLI를 사용 하 여 드라이버를 준수합니다.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 드라이버에서 지원 되는 정적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 첫 번째 하위 집합을 포함 하는 비트이 마스크 두 번째 하위 집합을 SQL_STATIC_CURSOR_ATTRIBUTES2를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 참조 (및 설명에 "동적 커서"에 대 한 "정적 커서"으로 대체).  
  
 SQL-92 중간 수준-와 호환 되는 드라이버는 일반적으로 반환 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE, 및 SQL_CA1_RELATIVE 옵션 지원 드라이버가 포함된 된 SQL 페치 문을 통해 스크롤 가능 커서를 지원 하기 때문에 합니다. 그러나이 확인 하지 때문에 직접 기본 SQL 지원, 스크롤 가능 커서 지원 되지, SQL-92 중간 수준-와 호환 되는 드라이버에 대해서도 합니다.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 드라이버에서 지원 되는 정적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 특성의 두 번째 하위 집합을 포함 하는 비트이 마스크 첫 번째 하위 집합을 SQL_STATIC_CURSOR_ATTRIBUTES1를 참조 하세요.  
  
 다음 비트 마스크는 어떤 특성이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 이러한 비트 마스크의 설명에 대 한 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 참조 (및 설명에 "동적 커서"에 대 한 "정적 커서"으로 대체).  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 참고: 정보 유형 ODBC 1.0;에 도입 합니다. 각 비트 마스크는 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 문자열 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 마스크 문자열 함수를 지원 되는지 확인 하는 데 사용 됩니다.  
  
 (ODBC 1.0) SQL_FN_STR_ASCII SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) (ODBC 1.0) SQL_FN_STR_CONCAT SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) (ODBC 1.0) SQL_FN_STR_REPEAT SQL_FN_ (ODBC 1.0) STR_REPLACE SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 응용 프로그램 호출 수를 **찾기** 사용 하 여 스칼라 함수는 *string_exp1*를 *string_exp2*, 및 *시작* 인수, 드라이버 SQL_FN_STR_LOCATE 비트 마스크를 반환합니다. 응용 프로그램에만 사용 하 여 찾기 스칼라 함수 호출 수를 *string_exp1* 하 고 *string_exp2* 인수 드라이버 SQL_FN_STR_LOCATE_2 비트 마스크를 반환 합니다. 완벽 하 게 지 원하는 드라이버는 **찾기** 스칼라 함수는 모두를 나타내는 비트 마스크를 반환 합니다.  
  
 (자세한 내용은 [문자열 함수](../../../odbc/reference/appendixes/string-functions.md) 부록 E, "스칼라 함수입니다.")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 하위 쿼리를 지 원하는 조건자 열거 SQLUINTEGER 비트 마스크:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES 비트 마스크 하위 쿼리를 지 원하는 모든 조건자 상관된 하위 쿼리를 지원 한다는 것을 나타냅니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버는 항상 모든 이러한 비트가 설정 되는 비트 마스크를 반환 합니다.  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 시스템 함수를 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 시스템 함수를 결정 하는 데 사용 됩니다.  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 문자열 테이블을 데이터 원본 공급 업체의 이름 예를 들어, "table" 또는 "file"입니다.  
  
 이 문자열은 위쪽, 아래쪽, 또는 혼합의 경우 수 있습니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버는 항상 "table"을 반환 합니다.  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 드라이버 및 TIMESTAMPADD 스칼라 함수에 대 한 연결 된 데이터 원본에서 지 원하는 타임 스탬프 간격 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 간격 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 전환 수준-와 호환 되는 드라이버는 항상 모든 이러한 비트가 설정 되는 비트 마스크를 반환 합니다.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 드라이버 및 TIMESTAMPDIFF 스칼라 함수에 대 한 연결 된 데이터 원본에서 지 원하는 타임 스탬프 간격 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 간격 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 전환 수준-와 호환 되는 드라이버는 항상 모든 이러한 비트가 설정 되는 비트 마스크를 반환 합니다.  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1.0)  
 참고: 정보 유형 ODBC 1.0;에 도입 합니다. 각 비트 마스크는 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 스칼라 날짜 및 시간 함수 드라이버 및 연결 된 데이터 원본에서 지 원하는 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 지원 되는 날짜 및 시간 함수를 결정 하는 데 사용 됩니다.  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) (ODBC 3.0) SQL_FN_TD_CURRENT_TIME SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) (ODBC 1.0) SQL_FN_TD_CURDATE SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK ( 1.0 ODBC) (ODBC 1.0) SQL_FN_TD_DAYOFYEAR SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ 두 번째 (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 참고: 정보 유형 ODBC 1.0;에 도입 합니다. 각 반환 값은 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 드라이버 또는 데이터 원본에 트랜잭션 지원을 설명 하는 SQLUSMALLINT 값:  
  
 SQL_TC_NONE = 트랜잭션이 지원 되지 않습니다. ODBC (1.0)  
  
 SQL_TC_DML = 트랜잭션 데이터 조작 언어 (DML) 문만 포함 될 수 있습니다 (**선택**, **삽입**, **업데이트**하십시오 **삭제** ). 트랜잭션 원인에서 오류가 발생 하는 DDL (데이터 정의 언어) 문이 있습니다. ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = 트랜잭션을 DML 문만 포함 될 수 있습니다. DDL 문 (**CREATE TABLE**를 **DROP INDEX**등) 트랜잭션이 발생 하는 트랜잭션이 커밋된 것으로 발생 합니다. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 트랜잭션을 DML 문만 포함 될 수 있습니다. 트랜잭션에서 발생 하는 DDL 문이 무시 됩니다. (ODBC 2.0)  
  
 SQL_TC_ALL = DDL 문 및 DML 문을 순서에 관계 없이 트랜잭션을 포함할 수 있습니다. ODBC (1.0)  
  
 (트랜잭션 지원 SQL-92에 필수 이기 때문에 [수준] SQL-92와 호환 되는 드라이버를 반환 하지 않습니다 SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1.0)  
 드라이버 또는 데이터 원본에서 사용할 수 있는 트랜잭션 격리 수준을 열거 SQLUINTEGER 비트 마스크입니다.  
  
 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하는 데 플래그와 함께 사용 됩니다.  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 이러한 격리 수준의 설명 SQL_DEFAULT_TXN_ISOLATION 설명은 참조 하세요.  
  
 트랜잭션 격리 수준을 설정 하려면 응용 프로그램 호출 **SQLSetConnectAttr** SQL_ATTR_TXN_ISOLATION 특성을 설정 합니다. 자세한 내용은 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 지 원하는 대로 항상 sql_txn_serializable로 반환 됩니다. FIPS 전환 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_UNION (ODBC 2.0)  
 에 대 한 지원 열거 하는 SQLUINTEGER 비트 마스크를 **UNION** 절:  
  
 SQL_U_UNION 데이터 원본에서 지 원하는 = 합니다 **UNION** 절.  
  
 SQL_U_UNION_ALL 데이터 원본에서 지 원하는 = 합니다 **모든** 키워드는 **UNION** 절. (**SQLGetInfo** SQL_U_UNION와 SQL_U_UNION_ALL이 경우에 반환 합니다.)  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다 두이 옵션 모두 지원.  
  
 SQL_USER_NAME (ODBC 1.0)  
 로그인 이름과 다를 수 있는 특정 데이터베이스에 사용 되는 이름의 문자열입니다.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 게시 된 버전의 ODBC 드라이버 관리자 완전히 준수 Open Group 사양의 연도 나타내는 문자열입니다.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 문자열: "Y" 사용자에서 반환 된 모든 프로시저를 실행할 수 있다면 **SQLProcedures**; 사용자를 실행할 수 없는지 반환 하는 "N" 프로시저 있을 수 있습니다.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 문자열: "Y" 사용자 보장 되는 경우 **선택** 반환한 모든 테이블에 대 한 권한을 **SQLTables**; 사용자에 액세스할 수 없습니다. 반환 하는 "N" 테이블이 있을 수 있습니다.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 활성 환경에 드라이버를 지원할 수 있는 최대 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 또는 알 수 없는 경우이 값은 0으로 설정 됩니다.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 집계 함수에 대 한 지원을 열거 SQLUINTEGER 비트 마스크:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 항목 수준-와 호환 되는 드라이버를 항상 반환 됩니다이 옵션을 모두 지원.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **ALTER 도메인** 문, 데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 합니다. SQL-92 Full 수준 규격 드라이버는 비트 마스크의 모든 항상 반환 됩니다. 즉 "0"의 반환 값을 **ALTER 도메인** 문은 지원 되지 않습니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 추가 도메인 제약 조건이 지원 됩니다 (전체 수준)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 도메인 > \<set 도메인 기본 절 >은 지원 (전체 수준)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의 절 > 도메인 제약 조건 (중간 수준) 이름 지정에  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop 도메인 제약 조건 절 >은 지원 (전체 수준)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 도메인 > \<drop 도메인 기본 절 >은 지원 (전체 수준)  
  
 지원 되는 다음 비트를 지정 \<제약 조건 특성 > 경우 \<도메인 제약 조건 추가 > 지원 됩니다 (SQL_AD_ADD_DOMAIN_CONSTRAINT 비트 설정 됨):  
  
 (전체 수준) SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (전체 수준) (전체 수준) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 절을 열거 하는 SQLUINTEGER 비트 마스크를 **ALTER TABLE** 데이터 원본에서 지 원하는 문입니다.  
  
 이 기능을 지원 해야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆 괄호 안에 표시 됩니다.  
  
 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<열 추가 > 열 데이터 정렬 (전체 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<열 추가 > 열의 기본값 (FIPS 전환 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<열 추가 >은 (FIPS 전환 수준)를 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<열 추가 > 열 제약 조건 (FIPS 전환 수준)를 지정 하는 기능을 사용 하 여 절은 지원 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<테이블 제약 조건 추가 > 절은 지원 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<제약 조건 이름 정의 > 이름 열 및 테이블 제약 조건 (중간 수준)은 지원 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<열 > CASCADE 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 열 > \<drop 열 기본 절 >은 (중간 수준)를 지원 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<열 > 제한 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<열 > 제한 지원 됩니다 (FIPS 전환 수준) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 열 > \<set 열 기본 절 >은 (중간 수준)를 지원 (ODBC 3.0)  
  
 다음 비트 지정 지원 \<제약 조건 특성 > 열 또는 테이블 제약 조건을 지정 하는 경우 (SQL_AT_ADD_CONSTRAINT 비트 설정 됨):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (전체 수준) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (전체 수준) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 드라이버에서 비동기 지원의 수준을 표시 하는 SQLUINTEGER 값:  
  
 SQL_AM_CONNECTION = 연결 수준 비동기 실행은 지원 됩니다. 비동기 모드에 있는 지정 된 연결 핸들에 연결 된 모든 문 핸들 또는 동기 모드에서 모두. 같은 연결에서 다른 문 핸들은 동기 모드에서 이동 하 고 그 반대의 경우도 마찬가지 비동기 모드 연결에서 문 핸들 일 수 없습니다.  
  
 SQL_AM_STATEMENT = Statement 수준 비동기 실행은 지원 됩니다. 동기 모드에서 동일한 연결에서 다른 문 핸들은 비동기 모드로 연결 핸들에 연결 된 몇 가지 문 핸들 수 있습니다.  
  
 SQL_AM_NONE 비동기 = 모드가 지원 되지 않습니다.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 행의 가용성을 기준으로 드라이버의 동작을 열거 하는 SQLUINTEGER 비트 마스크를 계산 합니다. 다음 비트 마스크는 정보 형식과 함께 사용 됩니다.  
  
 SQL_BRC_ROLLED_UP 행 개수 = 연속 INSERT, DELETE 또는 UPDATE 문을 하나로 롤업 됩니다. 이 비트가 설정 되어 있지 않으면 행 개수 각 문에 대해 사용할 수 있습니다.  
  
 SQL_BRC_PROCEDURES, 사용 가능한 경우 저장된 프로시저의 일괄 처리 실행 될 때 행 개수 =. 행 개수를 사용할 수 있는 또는 SQL_BRC_ROLLED_UP 비트에 따라 개별적으로 사용할 수 있는 롤백할 수 있습니다.  
  
 SQL_BRC_EXPLICIT, 사용 가능한 경우 직접 호출 하 여 일괄 처리 실행 될 때 행 개수 = **SQLExecute** 하거나 **SQLExecDirect**합니다. 행 개수를 사용할 수 있는 또는 SQL_BRC_ROLLED_UP 비트에 따라 개별적으로 사용할 수 있는 롤백할 수 있습니다.  
  
## <a name="example"></a>예제  
 **SQLGetInfo** 는 SQLUINTEGER 비트 마스크에 지원 되는 옵션의 목록을 반환 합니다 **InfoValuePtr*합니다. 각 옵션에 대 한 비트 마스크 옵션이 지원 되는지 여부를 결정 하는 플래그와 함께 사용 됩니다.  
  
 예를 들어, 응용 프로그램 SUBSTRING 스칼라 함수 연결과 관련 된 드라이버에 의해 지원 되는지 여부를 확인 하려면 다음 코드를 사용할 수 있습니다.  
  
 다른 예제를 사용 하 여 **SQLGetInfo**를 참조 하십시오 [SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)합니다.  
  
```  
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
 연결 특성의 설정을 반환합니다.  
 [SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 드라이버는 함수를 지원 하는지 여부를 결정 합니다.  
 [SQLGetFunctions 함수](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 반환 문 특성 설정  
 [SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 데이터 원본 데이터 형식에 대 한 정보를 반환합니다.  
 [SQLGetTypeInfo 함수](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
