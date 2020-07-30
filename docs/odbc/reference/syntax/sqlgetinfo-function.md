---
title: SQLGetInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
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
ms.openlocfilehash: 9a88eb1a4aff7d166a81bbf6ec64ae2b878fd5fa
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363383"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 함수

**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetInfo** 는 연결과 관련 된 드라이버 및 데이터 원본에 대 한 일반 정보를 반환 합니다.  
  
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

 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *InfoType*  
 입력 정보의 유형입니다.  
  
 *InfoValuePtr*  
 출력 정보를 반환할 버퍼에 대 한 포인터입니다. 요청 된 *InfoType* 에 따라 반환 되는 정보는 null로 끝나는 문자열, SQLUSMALLINT 값, SQLUINTEGER 비트 마스크, SQLUINTEGER 플래그, SQLUINTEGER 이진 값 또는 SQLULEN 값 중 하나가 됩니다.  
  
 *InfoType* 인수가 SQL_DRIVER_HDESC 또는 SQL_DRIVER_HSTMT 이면 *Infovalueptr* 인수는 입력 및 출력입니다. 자세한 내용은이 함수 설명의 뒷부분에 나오는 SQL_DRIVER_HDESC 또는 SQL_DRIVER_HSTMT 설명자를 참조 하세요.)  
  
 *Infovalueptr* 이 NULL 인 경우 *StringLengthPtr* 는 계속 해 서 *infovalueptr*에서 가리키는 버퍼에 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 합니다.  
  
 *BufferLength*  
 입력 \* *Infovalueptr* 버퍼의 길이입니다. * \* Infovalueptr* 의 값이 문자열이 아니거나 *infovalueptr* 이 null 포인터인 경우 *bufferlength* 인수는 무시 됩니다. 드라이버는 *InfoType*를 기준으로 * \* infovalueptr* 의 크기가 SQLUSMALLINT 또는 SQLUINTEGER 라고 가정 합니다. * \* Infovalueptr* 이 유니코드 문자열이 면 ( **SQLGetInfoW**호출 시) *bufferlength* 인수는 짝수 여야 합니다. 그렇지 않으면 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)이 반환 됩니다.  
  
 *StringLengthPtr*  
 출력 **Infovalueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 null 종료 문자 제외)를 반환할 버퍼에 대 한 포인터입니다.  
  
 문자 데이터의 경우 반환할 수 있는 바이트 수가 *Bufferlength*보다 크거나 같은 경우 \* *infovalueptr* 의 정보는 *bufferlength* 바이트에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
 다른 모든 유형의 데이터에 대해서는 *Bufferlength* 의 값이 무시 되 고 드라이버에서 \* *INFOTYPE*에 따라 *INFOSQLUSMALLINT eptr* 의 크기가 SQLUINTEGER 인 것으로 가정 합니다.  
  
## <a name="returns"></a>반환  

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  

 **SQLGetInfo** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_DBC의 *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetInfo** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목을 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *infovalueptr* 이 너무 작아서 요청 된 모든 정보를 반환할 수 없습니다. 따라서 정보가 잘렸습니다. 잘림 형식의 요청 된 정보 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|(DM) *InfoType* 에서 요청 된 정보 형식에는 열린 연결이 필요 합니다. ODBC에서 예약 된 정보 유형 중 SQL_ODBC_VER 열려 있는 연결 없이 반환 될 수 있습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|(DM) *InfoType* 인수가 SQL_DRIVER_HSTMT 되었으며 *Infovalueptr* 이 가리키는 값이 올바른 문 핸들이 아닙니다.<br /><br /> (DM) *InfoType* 인수가 SQL_DRIVER_HDESC 되었으며 *Infovalueptr* 이 가리키는 값이 올바른 설명자 핸들이 아닙니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우<br /><br /> (DM) *Bufferlength* 에 지정 된 값은 홀수이 고 * \* Infovalueptr* 은 유니코드 데이터 형식 이었습니다.|  
|HY096|정보 유형이 범위를 벗어남|*InfoType* 인수에 지정 된 값이 드라이버에서 지원 되는 ODBC 버전에 적합 하지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택 필드가 구현 되지 않음|*InfoType* 인수에 지정 된 값이 드라이버에서 지원 하지 않는 드라이버 관련 값입니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>의견  

 현재 정의 된 정보 형식은이 섹션의 뒷부분에 나오는 "정보 형식"에 표시 됩니다. 다른 데이터 원본을 활용 하기 위해 더 많은 것이 정의 되어야 합니다. 정보 유형 범위는 ODBC에서 예약 됩니다. 드라이버 개발자는 Open Group에서 고유한 드라이버별 사용에 대 한 값을 예약 해야 합니다. **SQLGetInfo** 는 유니코드 변환 또는 *썽킹* 을 수행 하지 않습니다 (부록 A: *Odbc 프로그래머 참조*의 [odbc 오류 코드](../appendixes/appendix-a-odbc-error-codes.md) 참조 *).* 자세한 내용은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)을 참조 하세요. \* *Infovalueptr* 에서 반환 되는 정보의 형식은 요청 된 *InfoType* 에 따라 달라 집니다. **SQLGetInfo** 는 다음 5 가지 형식 중 하나로 정보를 반환 합니다.  
  
- Null로 끝나는 문자열입니다.  
  
- SQLUSMALLINT 값  
  
- SQLUINTEGER 비트 마스크  
  
- SQLUINTEGER 값  
  
- SQLUINTEGER 이진 값  
  
 다음 각 정보 유형의 형식은 형식의 설명에 나와 있습니다. 응용 프로그램은 적절 하 게 **Infovalueptr* 에서 반환 된 값을 캐스팅 해야 합니다. 응용 프로그램이 SQLUINTEGER 비트 마스크에서 데이터를 검색 하는 방법에 대 한 예제는 "코드 예제"를 참조 하십시오.  
  
 드라이버는 다음 표에 정의 된 각 정보 유형에 대 한 값을 반환 해야 합니다. 드라이버 또는 데이터 원본에 정보 유형이 적용 되지 않는 경우 드라이버는 다음 표에 나열 된 값 중 하나를 반환 합니다.  

|정보 유형|값|
|-|-|
|문자열 ("Y" 또는 "N")|"N"|
|문자열 ("Y" 또는 "N" 아님)|빈 문자열|
|SQLUSMALLINT|0|
|SQLUINTEGER 비트 마스크 또는 SQLUINTEGER binary 값|0L|
  
 예를 들어 데이터 원본이 프로시저를 지원 하지 않는 경우 **SQLGetInfo** 는 프로시저와 관련 된 *InfoType* 의 값에 대 한 다음 표에 나열 된 값을 반환 합니다.  

|InfoType|값|
|-|-|
|SQL_PROCEDURES|"N"|
|SQL_ACCESSIBLE_PROCEDURES|"N"|
|SQL_MAX_PROCEDURE_NAME_LEN|0|
|SQL_PROCEDURE_TERM|빈 문자열|
  
 **SQLGetInfo** 는 odbc에서 사용 하도록 예약 되었지만 드라이버에서 지 원하는 odbc 버전에 의해 정의 되지 않은 정보 형식의 범위에 있는 *InfoType* 값에 대해 SQLSTATE HY096 (잘못 된 인수 값)을 반환 합니다. 드라이버가 준수 하는 ODBC 버전을 확인 하기 위해 응용 프로그램은 SQL_DRIVER_ODBC_VER 정보 형식으로 **SQLGetInfo** 를 호출 합니다. **SQLGetInfo** 는 드라이버별 사용을 위해 예약 되었지만 드라이버에서 지원 하지 않는 정보 형식의 범위에 있는 *InfoType* 값에 대해 SQLSTATE HYC00 (선택 가능한 기능을 구현 하지 않음)를 반환 합니다.  
  
 *InfoType* 가 SQL_ODBC_VER 되는 경우를 제외 하 고 모든 **SQLGetInfo** 호출에는 드라이버 관리자의 버전을 반환 하는 연결이 열려 있어야 합니다.  
  
## <a name="information-types"></a>정보 유형  

 이 섹션에서는 **SQLGetInfo**에서 지 원하는 정보 유형을 나열 합니다. 정보 유형은 그룹화 된 사용할지 사전순으로 나열 됩니다. ODBC 3.x에 대해 추가 되거나 이름이 바뀐 정보 유형도*나열 됩니다.*  
  
## <a name="driver-information"></a>드라이버 정보  

 *InfoType* 인수의 다음 값은 활성 문 수, 데이터 원본 이름, 인터페이스 표준 호환성 수준 등 ODBC 드라이버에 대 한 정보를 반환 합니다.  

:::row:::
    :::column:::
        SQL_ACTIVE_ENVIRONMENTS  
        SQL_ASYNC_DBC_FUNCTIONS  
        SQL_ASYNC_MODE  
        SQL_ASYNC_NOTIFICATION  
        SQL_BATCH_ROW_COUNT  
        SQL_BATCH_SUPPORT  
        SQL_DATA_SOURCE_NAME  
        SQL_DRIVER_AWARE_POOLING_SUPPORTED  
        SQL_DRIVER_HDBC  
        SQL_DRIVER_HDESC  
        SQL_DRIVER_HENV  
        SQL_DRIVER_HLIB  
        SQL_DRIVER_HSTMT  
        SQL_DRIVER_NAME  
        SQL_DRIVER_ODBC_VER  
        SQL_DRIVER_VER  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES1  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES2  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1  
    :::column-end:::
    :::column:::
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2  
        SQL_FILE_USAGE  
        SQL_GETDATA_EXTENSIONS  
        SQL_INFO_SCHEMA_VIEWS  
        SQL_KEYSET_CURSOR_ATTRIBUTES1  
        SQL_KEYSET_CURSOR_ATTRIBUTES2  
        SQL_MAX_ASYNC_CONCURRENT_STATEMENTS  
        SQL_MAX_CONCURRENT_ACTIVITIES  
        SQL_MAX_DRIVER_CONNECTIONS  
        SQL_ODBC_INTERFACE_CONFORMANCE  
        SQL_ODBC_STANDARD_CLI_CONFORMANCE  
        SQL_ODBC_VER  
        SQL_PARAM_ARRAY_ROW_COUNTS  
        SQL_PARAM_ARRAY_SELECTS  
        SQL_ROW_UPDATES  
        SQL_SEARCH_PATTERN_ESCAPE  
        SQL_SERVER_NAME  
        SQL_STATIC_CURSOR_ATTRIBUTES1  
        SQL_STATIC_CURSOR_ATTRIBUTES2  
    :::column-end:::
:::row-end:::

> [!NOTE]  
> **SQLGetInfo**를 구현할 때 드라이버가 서버에서 정보를 보내거나 요청 하는 횟수를 최소화 하 여 성능을 향상 시킬 수 있습니다.  
  
## <a name="dbms-product-information"></a>DBMS 제품 정보  

 *InfoType* 인수의 다음 값은 dbms 이름 및 버전과 같은 dbms 제품에 대 한 정보를 반환 합니다.  

:::row:::
    :::column:::
        SQL_DATABASE_NAME  
        SQL_DBMS_NAME  
    :::column-end:::
    :::column:::
        SQL_DBMS_VER  
    :::column-end:::
:::row-end:::

## <a name="data-source-information"></a>데이터 원본 정보  

 *InfoType* 인수의 다음 값은 데이터 원본에 대 한 정보를 반환 합니다 (예: 커서 특성 및 트랜잭션 기능).  

:::row:::
    :::column:::
        SQL_ACCESSIBLE_PROCEDURES  
        SQL_ACCESSIBLE_TABLES  
        SQL_BOOKMARK_PERSISTENCE  
        SQL_CATALOG_TERM  
        SQL_COLLATION_SEQ  
        SQL_CONCAT_NULL_BEHAVIOR  
        SQL_CURSOR_COMMIT_BEHAVIOR  
        SQL_CURSOR_ROLLBACK_BEHAVIOR  
        SQL_CURSOR_SENSITIVITY  
        SQL_DATA_SOURCE_READ_ONLY  
        SQL_DEFAULT_TXN_ISOLATION  
        SQL_DESCRIBE_PARAMETER  
    :::column-end:::
    :::column:::
        SQL_MULT_RESULT_SETS  
        SQL_MULTIPLE_ACTIVE_TXN  
        SQL_NEED_LONG_DATA_LEN  
        SQL_NULL_COLLATION  
        SQL_PROCEDURE_TERM  
        SQL_SCHEMA_TERM  
        SQL_SCROLL_OPTIONS  
        SQL_TABLE_TERM  
        SQL_TXN_CAPABLE  
        SQL_TXN_ISOLATION_OPTION  
        SQL_USER_NAME  
    :::column-end:::
:::row-end:::

## <a name="supported-sql"></a>지원 되는 SQL  

 *InfoType* 인수의 다음 값은 데이터 원본에서 지원 되는 SQL 문에 대 한 정보를 반환 합니다. 이러한 정보 형식에서 설명 하는 각 기능의 SQL 구문은 SQL-92 구문입니다. 이러한 정보 유형은 전체 SQL-92 문법을 철저히 설명 하지는 않습니다. 대신 일반적으로 다양 한 수준의 지원을 제공 하는 데이터 원본에 대 한 문법의 부분을 설명 합니다. 특히 SQL-92의 대부분의 DDL 문은 검사 됩니다.  
  
 응용 프로그램은 SQL_SQL_CONFORMANCE 정보 유형에 서 지원 되는 문법의 일반 수준을 결정 하 고 다른 정보 유형을 사용 하 여 명시 된 표준 준수 수준에서의 변형을 결정 해야 합니다.  

:::row:::
    :::column:::
        SQL_AGGREGATE_FUNCTIONS  
        SQL_ALTER_DOMAIN  
        SQL_ALTER_SCHEMA  
        SQL_ALTER_TABLE  
        SQL_ANSI_SQL_DATETIME_LITERALS  
        SQL_CATALOG_LOCATION  
        SQL_CATALOG_NAME  
        SQL_CATALOG_NAME_SEPARATOR  
        SQL_CATALOG_USAGE  
        SQL_COLUMN_ALIAS  
        SQL_CORRELATION_NAME  
        SQL_CREATE_ASSERTION  
        SQL_CREATE_CHARACTER_SET  
        SQL_CREATE_COLLATION  
        SQL_CREATE_DOMAIN  
        SQL_CREATE_SCHEMA  
        SQL_CREATE_TABLE  
        SQL_CREATE_TRANSLATION  
        SQL_DDL_INDEX  
        SQL_DROP_ASSERTION  
        SQL_DROP_CHARACTER_SET  
        SQL_DROP_COLLATION  
        SQL_DROP_DOMAIN  
        SQL_DROP_SCHEMA  
    :::column-end:::
    :::column:::
        SQL_DROP_TABLE  
        SQL_DROP_TRANSLATION  
        SQL_DROP_VIEW  
        SQL_EXPRESSIONS_IN_ORDERBY  
        SQL_GROUP_BY  
        SQL_IDENTIFIER_CASE  
        SQL_IDENTIFIER_QUOTE_CHAR  
        SQL_INDEX_KEYWORDS  
        SQL_INSERT_STATEMENT  
        SQL_INTEGRITY  
        SQL_KEYWORDS  
        SQL_LIKE_ESCAPE_CLAUSE  
        SQL_NON_NULLABLE_COLUMNS  
        SQL_OJ_CAPABILITIES  
        SQL_ORDER_BY_COLUMNS_IN_SELECT  
        SQL_OUTER_JOINS  
        SQL_PROCEDURES  
        SQL_QUOTED_IDENTIFIER_CASE  
        SQL_SCHEMA_USAGE  
        SQL_SPECIAL_CHARACTERS  
        SQL_SQL_CONFORMANCE  
        SQL_SUBQUERIES  
        SQL_UNION  
    :::column-end:::
:::row-end:::

## <a name="sql-limits"></a>SQL 제한  

 다음 *InfoType* 인수의 값은 SQL 문의 식별자 및 절에 적용 되는 제한에 대 한 정보를 반환 합니다 (예: 최대 식별자 길이 및 select 목록에 있는 최대 열 수). 드라이버 또는 데이터 원본에 의해 제한 사항이 적용 될 수 있습니다.  

:::row:::
    :::column:::
        SQL_MAX_BINARY_LITERAL_LEN  
        SQL_MAX_CATALOG_NAME_LEN  
        SQL_MAX_CHAR_LITERAL_LEN  
        SQL_MAX_COLUMN_NAME_LEN  
        SQL_MAX_COLUMNS_IN_GROUP_BY  
        SQL_MAX_COLUMNS_IN_INDEX  
        SQL_MAX_COLUMNS_IN_ORDER_BY  
        SQL_MAX_COLUMNS_IN_SELECT  
        SQL_MAX_COLUMNS_IN_TABLE  
        SQL_MAX_CURSOR_NAME_LEN  
    :::column-end:::
    :::column:::
        SQL_MAX_IDENTIFIER_LEN  
        SQL_MAX_INDEX_SIZE  
        SQL_MAX_PROCEDURE_NAME_LEN  
        SQL_MAX_ROW_SIZE  
        SQL_MAX_ROW_SIZE_INCLUDES_LONG  
        SQL_MAX_SCHEMA_NAME_LEN  
        SQL_MAX_STATEMENT_LEN  
        SQL_MAX_TABLE_NAME_LEN  
        SQL_MAX_TABLES_IN_SELECT  
        SQL_MAX_USER_NAME_LEN  
    :::column-end:::
:::row-end:::

## <a name="scalar-function-information"></a>스칼라 함수 정보  

 *InfoType* 인수의 다음 값은 데이터 원본 및 드라이버에서 지 원하는 스칼라 함수에 대 한 정보를 반환 합니다. 스칼라 함수에 대 한 자세한 내용은 [부록 E: 스칼라 함수](../appendixes/appendix-e-scalar-functions.md)를 참조 하세요.  

:::row:::
    :::column:::
        SQL_CONVERT_FUNCTIONS  
        SQL_NUMERIC_FUNCTIONS  
        SQL_STRING_FUNCTIONS  
        SQL_SYSTEM_FUNCTIONS  
    :::column-end:::
    :::column:::
        SQL_TIMEDATE_ADD_INTERVALS  
        SQL_TIMEDATE_DIFF_INTERVALS  
        SQL_TIMEDATE_FUNCTIONS  
    :::column-end:::
:::row-end:::

## <a name="conversion-information"></a>변환 정보  

 다음 *InfoType* 인수의 값은 데이터 원본이 지정 된 sql 데이터 형식을 **convert** 스칼라 함수로 변환할 수 있는 sql 데이터 형식 목록을 반환 합니다.  

:::row:::
    :::column:::
        SQL_CONVERT_BIGINT  
        SQL_CONVERT_BINARY  
        SQL_CONVERT_BIT  
        SQL_CONVERT_CHAR  
        SQL_CONVERT_DATE  
        SQL_CONVERT_DECIMAL  
        SQL_CONVERT_DOUBLE  
        SQL_CONVERT_FLOAT  
        SQL_CONVERT_INTEGER  
        SQL_CONVERT_INTERVAL_DAY_TIME  
        SQL_CONVERT_INTERVAL_YEAR_MONTH  
    :::column-end:::
    :::column:::
        SQL_CONVERT_LONGVARBINARY  
        SQL_CONVERT_LONGVARCHAR  
        SQL_CONVERT_NUMERIC  
        SQL_CONVERT_REAL  
        SQL_CONVERT_SMALLINT  
        SQL_CONVERT_TIME  
        SQL_CONVERT_TIMESTAMP  
        SQL_CONVERT_TINYINT  
        SQL_CONVERT_VARBINARY  
        SQL_CONVERT_VARCHAR  
    :::column-end:::
:::row-end:::

## <a name="information-types-added-for-odbc-3x"></a>ODBC 3.x 용으로 추가 된 정보 유형  

 ODBC 3.x에 대해 다음과 같은 *InfoType* 인수 값이 추가 되었습니다.  

:::row:::
    :::column:::
        SQL_ACTIVE_ENVIRONMENTS  
        SQL_AGGREGATE_FUNCTIONS  
        SQL_ALTER_DOMAIN  
        SQL_ALTER_SCHEMA  
        SQL_ANSI_SQL_DATETIME_LITERALS  
        SQL_ASYNC_DBC_FUNCTIONS  
        SQL_ASYNC_MODE  
        SQL_ASYNC_NOTIFICATION  
        SQL_BATCH_ROW_COUNT  
        SQL_BATCH_SUPPORT  
        SQL_CATALOG_NAME  
        SQL_COLLATION_SEQ  
        SQL_CONVERT_INTERVAL_DAY_TIME  
        SQL_CONVERT_INTERVAL_YEAR_MONTH  
        SQL_CREATE_ASSERTION  
        SQL_CREATE_CHARACTER_SET  
        SQL_CREATE_COLLATION  
        SQL_CREATE_DOMAIN  
        SQL_CREATE_SCHEMA  
        SQL_CREATE_TABLE  
        SQL_CREATE_TRANSLATION  
        SQL_CURSOR_SENSITIVITY  
        SQL_DDL_INDEX  
        SQL_DESCRIBE_PARAMETER  
        SQL_DM_VER  
    :::column-end:::
    :::column:::
        SQL_DRIVER_AWARE_POOLING_SUPPORTED  
        SQL_DRIVER_HDESC  
        SQL_DROP_ASSERTION  
        SQL_DROP_CHARACTER_SET  
        SQL_DROP_COLLATION  
        SQL_DROP_DOMAIN  
        SQL_DROP_SCHEMA  
        SQL_DROP_TABLE  
        SQL_DROP_TRANSLATION  
        SQL_DROP_VIEW  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES1  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES2  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2  
        SQL_INFO_SCHEMA_VIEWS  
        SQL_INSERT_STATEMENT  
        SQL_KEYSET_CURSOR_ATTRIBUTES1  
        SQL_KEYSET_CURSOR_ATTRIBUTES2  
        SQL_MAX_ASYNC_CONCURRENT_STATEMENTS  
        SQL_MAX_IDENTIFIER_LEN  
        SQL_PARAM_ARRAY_ROW_COUNTS  
        SQL_PARAM_ARRAY_SELECTS  
        SQL_STATIC_CURSOR_ATTRIBUTES1  
        SQL_STATIC_CURSOR_ATTRIBUTES2  
        SQL_XOPEN_CLI_YEAR  
    :::column-end:::
:::row-end:::

## <a name="information-types-renamed-for-odbc-3x"></a>ODBC 3.x의 이름을 바꾼 정보 형식  

 ODBC 3.x의 *InfoType* 인수 값이 다음과 같이 변경 되었습니다.  

|이전 이름|새 이름|  
|-|-|  
|SQL_ACTIVE_CONNECTIONS|SQL_MAX_DRIVER_CONNECTIONS|
|SQL_ACTIVE_STATEMENTS|SQL_MAX_CONCURRENT_ACTIVITIES|
|SQL_MAX_OWNER_NAME_LEN|SQL_MAX_SCHEMA_NAME_LEN|
|SQL_MAX_QUALIFIER_NAME_LEN|SQL_MAX_CATALOG_NAME_LEN|
|SQL_ODBC_SQL_OPT_IEF|SQL_INTEGRITY|
|SQL_OWNER_TERM|SQL_SCHEMA_TERM|
|SQL_OWNER_USAGE|SQL_SCHEMA_USAGE|
|SQL_QUALIFIER_LOCATION|SQL_CATALOG_LOCATION|
|SQL_QUALIFIER_NAME_SEPARATOR|SQL_CATALOG_NAME_SEPARATOR|
|SQL_QUALIFIER_TERM|SQL_CATALOG_TERM|
|SQL_QUALIFIER_USAGE|SQL_CATALOG_USAGE|
  
## <a name="information-types-deprecated-in-odbc-3x"></a>ODBC 3.x에서 사용 되지 않는 정보 형식  

 *InfoType* 인수의 다음 값은 ODBC 3.x에서 더 이상 사용 되지 않습니다. Odbc 3.x 드라이버는 이전 버전의 ODBC 2.x 응용 프로그램과의 호환성을 위해 계속 이러한 정보 유형을 지원 해야 합니다. 이러한 형식에 대 한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [SQLGetInfo 지원](../appendixes/sqlgetinfo-support.md) 을 참조 하세요.  

:::row:::
    :::column:::
        SQL_FETCH_DIRECTION  
        SQL_LOCK_TYPES  
        SQL_ODBC_API_CONFORMANCE  
        SQL_ODBC_SQL_CONFORMANCE  
    :::column-end:::
    :::column:::
        SQL_POS_OPERATIONS  
        SQL_POSITIONED_STATEMENTS  
        SQL_SCROLL_CONCURRENCY  
        SQL_STATIC_SENSITIVITY  
    :::column-end:::
:::row-end:::

## <a name="information-type-descriptions"></a>정보 형식 설명  

다음 표에는 각 정보 형식, 해당 형식이 도입 된 ODBC 버전 및 해당 설명이 사전순으로 나와 있습니다.  
  
|Information Type|ODBC 버전|설명|
|-|-|-|
|SQL_ACCESSIBLE_PROCEDURES|1.0|문자열: "Y"-사용자가 **sqlprocedures**에서 반환 된 모든 프로시저를 실행할 수 있는 경우 "N"-사용자가 실행할 수 없는 프로시저가 반환 될 수 있습니다.|
|SQL_ACCESSIBLE_TABLES|1.0|문자열: "Y"-사용자에 게 **sqltables**에서 반환 된 모든 테이블에 대 한 **SELECT** 권한이 보장 되는 경우 "N"-사용자가 액세스할 수 없는 테이블이 반환 될 수 있습니다.|
|SQL_ACTIVE_ENVIRONMENTS|3.0|드라이버에서 지원할 수 있는 최대 활성 환경 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.|
|SQL_AGGREGATE_FUNCTIONS|3.0|집계 함수에 대 한 지원을 열거 하는 SQLUINTEGER 비트 마스크:<br/>SQL_AF_ALL<br/>SQL_AF_AVG<br/>SQL_AF_COUNT<br/>SQL_AF_DISTINCT<br/>SQL_AF_MAX<br/>SQL_AF_MIN<br/>SQL_AF_SUM<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_ALTER_DOMAIN|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **ALTER DOMAIN** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다. SQL-92 전체 수준 호환 드라이버는 항상 모든 비트 마스크를 반환 합니다. 반환 값이 "0" 이면 **ALTER DOMAIN** 문이 지원 되지 않음을 의미 합니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_AD_ADD_DOMAIN_CONSTRAINT = 도메인 제약 조건 추가가 지원 됩니다 (전체 수준).<br/>SQL_AD_ADD_DOMAIN_DEFAULT = \<alter domain> \<set domain default clause> (전체 수준)이 지원 됩니다.<br/>SQL_AD_CONSTRAINT_NAME_DEFINITION = \<constraint name definition clause> 은 명명 도메인 제약 조건 (중간 수준)에 대해 지원 됩니다.<br/>SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop domain constraint clause> (전체 수준)이 지원 됩니다.<br/>SQL_AD_DROP_DOMAIN_DEFAULT = \<alter domain> \<drop domain default clause> (전체 수준)이 지원 됩니다.<br/><br/>다음 비트는가 지원 되는 경우 지원 되는를 지정 합니다 \<constraint attributes> \<add domain constraint> (SQL_AD_ADD_DOMAIN_CONSTRAINT 비트가 설정 됨).<br/>SQL_AD_ADD_CONSTRAINT_DEFERRABLE (전체 수준)<br/>SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (전체 수준)<br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (전체 수준)<br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)|
|SQL_ALTER_TABLE|2.0|데이터 원본에서 지 원하는 **ALTER TABLE** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_AT_ADD_COLUMN_COLLATION = \<add column> 절이 지원 되며 열 데이터 정렬을 지정 하는 기능 (전체 수준) (ODBC 3.0)<br/>SQL_AT_ADD_COLUMN_DEFAULT = \<add column> 절이 지원 되며 열 기본값을 지정 하는 기능 (FIPS 전환 수준) (ODBC 3.0)<br/>SQL_AT_ADD_COLUMN_SINGLE = \<add column> 지원 됨 (FIPS 전환 수준) (ODBC 3.0)<br/>\<add column>열 제약 조건 (FIPS 전환 수준)을 지정 하는 기능을 사용 하는 SQL_AT_ADD_CONSTRAINT = 절이 지원 됩니다 (ODBC 3.0).<br/>SQL_AT_ADD_TABLE_CONSTRAINT = \<add table constraint> 절이 지원 됨 (FIPS 전환 수준) (ODBC 3.0)<br/>SQL_AT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 열 이름 및 테이블 제약 조건에 대해 지원 됩니다 (중간 수준) (ODBC 3.0).<br/>SQL_AT_DROP_COLUMN_CASCADE = \<drop column> CASCADE가 지원 됨 (FIPS 전환 수준) (ODBC 3.0)<br/>SQL_AT_DROP_COLUMN_DEFAULT = \<alter column> \<drop column default clause> 지원 됨 (중간 수준) (ODBC 3.0)<br/>SQL_AT_DROP_COLUMN_RESTRICT = \<drop column> 제한 (FIPS 전환 수준) (ODBC 3.0)이 지원 됩니다.<br/>SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)<br/>SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<drop column> 제한 (FIPS 전환 수준) (ODBC 3.0)이 지원 됩니다.<br/>SQL_AT_SET_COLUMN_DEFAULT = \<alter column> \<set column default clause> 지원 됨 (중간 수준) (ODBC 3.0)<br/><br/>다음 비트는 \<constraint attributes> 열 또는 테이블 제약 조건 지정이 지원 되는 경우 (SQL_AT_ADD_CONSTRAINT 비트가 설정 됨)에 대 한 지원을 지정 합니다.<br/>SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (전체 수준) (ODBC 3.0)<br/>SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준) (ODBC 3.0)<br/>SQL_AT_CONSTRAINT_DEFERRABLE (전체 수준) (ODBC 3.0)<br/>SQL_AT_CONSTRAINT_NON_DEFERRABLE (전체 수준) (ODBC 3.0)|
|SQL_ASYNC_DBC_FUNCTIONS|3.8|드라이버가 연결 핸들에서 비동기적으로 함수를 실행할 수 있는지 여부를 나타내는 SQLUINTEGER 값입니다.<br/><br/>SQL_ASYNC_DBC_CAPABLE = 드라이버가 비동기적으로 연결 함수를 실행할 수 있습니다.<br/>SQL_ASYNC_DBC_NOT_CAPABLE = 드라이버는 연결 함수를 비동기적으로 실행할 수 없습니다.|
|SQL_ASYNC_MODE|3.0|드라이버의 비동기 지원 수준을 나타내는 SQLUINTEGER 값입니다.<br/><br/>SQL_AM_CONNECTION = 연결 수준 비동기 실행이 지원 됩니다. 지정 된 연결 핸들과 연결 된 모든 문 핸들이 비동기 모드 이거나 모두 동기 모드입니다. 연결에 대 한 문 핸들은 비동기 모드에 있을 수 있지만 동일한 연결의 다른 문 핸들은 동기 모드에 있을 수 있으며 그 반대의 경우도 마찬가지입니다.<br/>SQL_AM_STATEMENT = 문 수준 비동기 실행이 지원 됩니다. 연결 핸들과 연결 된 일부 문 핸들은 비동기 모드에 있을 수 있지만 동일한 연결의 다른 문 핸들은 동기 모드입니다.<br/>SQL_AM_NONE = 비동기 모드는 지원 되지 않습니다.|
|SQL_ASYNC_NOTIFICATION|3.8|드라이버가 비동기 알림을 지원 하는지 여부를 나타내는 SQLUINTEGER 값입니다.<br/><br/>SQL_ASYNC_NOTIFICATION_CAPABLE = 드라이버에서 비동기 실행 알림을 지원 합니다.<br/>SQL_ASYNC_NOTIFICATION_NOT_CAPABLE = 드라이버에서 비동기 실행 알림을 지원 하지 않습니다.<br/><br/>ODBC 비동기 작업에는 연결 수준 비동기 작업과 문 수준 비동기 작업 이라는 두 가지 범주가 있습니다.  드라이버가 SQL_ASYNC_NOTIFICATION_CAPABLE을 반환 하는 경우 비동기적으로 실행할 수 있는 모든 Api에 대 한 알림을 지원 해야 합니다.|
|SQL_BATCH_ROW_COUNT|3.0|행 개수의 가용성과 관련 하 여 드라이버의 동작을 열거 하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 정보 형식과 함께 사용 됩니다.<br/><br/>SQL_BRC_ROLLED_UP = 연속 INSERT, DELETE 또는 UPDATE 문의 행 개수가 하나로 롤업 됩니다. 이 비트가 설정 되지 않은 경우 각 문에 대해 행 개수를 사용할 수 있습니다.<br/>SQL_BRC_PROCEDURES = 행 개수 (있는 경우)는 저장 프로시저에서 일괄 처리가 실행 될 때 사용할 수 있습니다. 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 겹쳐서 표시 하거나 개별적으로 사용할 수 있습니다.<br/>SQL_BRC_EXPLICIT = 행 개수 (있는 경우)는 **Sqlexecute** 또는 **sqlexecdirect**를 호출 하 여 일괄 처리가 직접 실행 될 때 사용할 수 있습니다. 행 수를 사용할 수 있는 경우 SQL_BRC_ROLLED_UP 비트에 따라 겹쳐서 표시 하거나 개별적으로 사용할 수 있습니다.|
|SQL_BATCH_SUPPORT|3.0|일괄 처리에 대 한 드라이버의 지원을 열거 하는 SQLUINTEGER 비트 마스크입니다. 지원 되는 수준을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/><br/>SQL_BS_SELECT_EXPLICIT = 드라이버는 결과 집합 생성 문을 포함할 수 있는 명시적 일괄 처리를 지원 합니다.<br/>SQL_BS_ROW_COUNT_EXPLICIT = 드라이버가 행 개수 생성 문을 포함할 수 있는 명시적 일괄 처리를 지원 합니다.<br/>SQL_BS_SELECT_PROC = 드라이버는 결과 집합을 생성 하는 문을 포함할 수 있는 명시적 프로시저를 지원 합니다.<br/>SQL_BS_ROW_COUNT_PROC = 드라이버는 행 개수 생성 문을 포함할 수 있는 명시적 프로시저를 지원 합니다.|
|SQL_BOOKMARK_PERSISTENCE|2.0|책갈피를 유지 하는 작업을 열거 하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 플래그와 함께 사용 되어 책갈피를 유지 하는 옵션을 결정 합니다.<br/><br/>SQL_BP_CLOSE = 응용 프로그램이 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하 고 문과 연결 된 커서를 **SQLCloseCursor** 하는 경우 유효 합니다.<br/>SQL_BP_DELETE = 행의 책갈피는 해당 행이 삭제 된 후 유효 합니다.<br/>SQL_BP_DROP = 응용 프로그램이 *HandleType* of SQL_HANDLE_STMT를 사용 하 여 **sqlfreehandle** 을 호출 하 고 문을 삭제 한 후에 유효 합니다.<br/>SQL_BP_TRANSACTION = 응용 프로그램이 트랜잭션을 커밋하거나 롤백하는 경우 책갈피가 유효 합니다.<br/>SQL_BP_UPDATE = 행의 책갈피는 키 열을 포함 하 여 해당 행의 열이 업데이트 된 후에 유효 합니다.<br/>SQL_BP_OTHER_HSTMT = 한 문과 연결 된 책갈피를 다른 문과 함께 사용할 수 있습니다. SQL_BP_CLOSE 또는 SQL_BP_DROP을 지정 하지 않으면 첫 번째 문에 있는 커서가 열려 있어야 합니다.|
|SQL_CATALOG_LOCATION|2.0|정규화 된 테이블 이름에서 카탈로그의 위치를 나타내는 SQLUSMALLINT 값입니다.<br/><br/>SQL_CL_START<br/>SQL_CL_END<br/>예를 들어 Xbase 드라이버는 \EMPDATA\EMP.에서와 같이 디렉터리 (카탈로그) 이름이 테이블 이름의 시작 부분에 있기 때문에 SQL_CL_START를 반환 합니다. DBF. ORACLE Server 드라이버는와 같이 카탈로그가 테이블 이름의 끝에 있기 때문에 SQL_CL_END를 반환 합니다 ADMIN.EMP@EMPDATA .<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 SQL_CL_START 반환 합니다. 데이터 원본에서 카탈로그를 지원 하지 않는 경우 값 0이 반환 됩니다. 카탈로그가 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_NAME 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_QUALIFIER_LOCATION에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_CATALOG_NAME|3.0|문자열은 "Y" (서버에서 카탈로그 이름을 지 원하는 경우)이 고, 그렇지 않으면 "N"입니다.<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 "Y"를 반환 합니다.|
|SQL_CATALOG_NAME_SEPARATOR|1.0|문자열: 데이터 소스가 카탈로그 이름과 앞 이나 뒤에 오는 정규화 된 이름 요소 사이의 구분 기호로 정의 되는 문자입니다.<br/><br/>데이터 원본에서 카탈로그를 지원 하지 않는 경우 빈 문자열이 반환 됩니다. 카탈로그가 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_NAME 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다. SQL-92 전체 수준 규격 드라이버는 항상 "."를 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_CATALOG_TERM|1.0|카탈로그에 대 한 데이터 원본 공급 업체의 이름을 포함 하는 문자열입니다. 예를 들면 "database" 또는 "directory"입니다. 이 문자열은 대문자나 소문자 또는 mixed 일 수 있습니다.<br/><br/>데이터 원본에서 카탈로그를 지원 하지 않는 경우 빈 문자열이 반환 됩니다. 카탈로그가 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_NAME 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다. SQL-92 전체 수준 규격 드라이버는 항상 "catalog"를 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_QUALIFIER_TERM에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_CATALOG_USAGE|2.0|카탈로그를 사용할 수 있는 문을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>다음 비트 마스크는 카탈로그를 사용할 수 있는 위치를 결정 하는 데 사용 됩니다.<br/>SQL_CU_DML_STATEMENTS = 카탈로그는 모든 데이터 조작 언어 문에서 지원 됩니다. **select**, **INSERT**, **UPDATE**, **DELETE**, 지원 되는 경우 **update** 및 DELETE 문을 선택 합니다.<br/>SQL_CU_PROCEDURE_INVOCATION = 카탈로그는 ODBC 프로시저 호출 문에서 지원 됩니다.<br/>SQL_CU_TABLE_DEFINITION = 카탈로그는 **CREATE TABLE**, **CREATE VIEW**, **ALTER Table**, **drop table**및 **drop view**와 같은 모든 테이블 정의 문에서 지원 됩니다.<br/>SQL_CU_INDEX_DEFINITION = 카탈로그는 **CREATE index** 및 **DROP INDEX**에서 지원 됩니다.<br/>SQL_CU_PRIVILEGE_DEFINITION = 카탈로그는 **GRANT** 및 **REVOKE**의 모든 권한 정의 문에서 지원 됩니다.<br/><br/>데이터 원본에서 카탈로그를 지원 하지 않는 경우 값 0이 반환 됩니다. 카탈로그가 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_NAME 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다. SQL-92 전체 수준 규격 드라이버는 항상 이러한 모든 비트가 설정 된 비트 마스크를 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_QUALIFIER_USAGE에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_COLLATION_SEQ|3.0|데이터 정렬 시퀀스의 이름입니다. 이는이 서버에 대 한 기본 문자 집합에 대 한 기본 데이터 정렬의 이름을 나타내는 문자열입니다 (예: ' ISO 8859-1 ' 또는 EBCDIC). 이를 알 수 없으면 빈 문자열이 반환 됩니다. SQL-92 전체 수준 규격 드라이버는 항상 비어 있지 않은 문자열을 반환 합니다.|
|SQL_COLUMN_ALIAS|2.0|문자열: 데이터 원본이 열 별칭을 지 원하는 경우 "Y"입니다. 그렇지 않으면 "N"입니다.<br/><br/>열 별칭은 select 목록의 열에 AS 절을 사용 하 여 지정할 수 있는 대체 이름입니다. SQL-92 항목 수준 호환 드라이버는 항상 "Y"를 반환 합니다.|
|SQL_CONCAT_NULL_BEHAVIOR|1.0|데이터 원본에서 null이 아닌 값 문자 데이터 형식 열이 포함 된 NULL 값 문자 데이터 형식 열의 연결을 처리 하는 방법을 나타내는 SQLUSMALLINT 값입니다.<br/>SQL_CB_NULL = 결과가 NULL 값입니다.<br/>SQL_CB_NON_NULL = Result는 NULL이 아닌 값 열 또는 열을 연결 합니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 SQL_CB_NULL 반환 합니다.|
|SQL_CONVERT_BIGINT<br/>SQL_CONVERT_BINARY<br/>SQL_CONVERT_BIT<br/>SQL_CONVERT_CHAR<br/>SQL_CONVERT_GUID<br/>SQL_CONVERT_DATE<br/>SQL_CONVERT_DECIMAL<br/>SQL_CONVERT_DOUBLE<br/>SQL_CONVERT_FLOAT<br/>SQL_CONVERT_INTEGER<br/>SQL_CONVERT_INTERVAL_YEAR_MONTH<br/>SQL_CONVERT_INTERVAL_DAY_TIME<br/>SQL_CONVERT_LONGVARBINARY<br/>SQL_CONVERT_LONGVARCHAR<br/>SQL_CONVERT_NUMERIC<br/>SQL_CONVERT_REAL<br/>SQL_CONVERT_SMALLINT<br/>SQL_CONVERT_TIME<br/>SQL_CONVERT_TIMESTAMP<br/>SQL_CONVERT_TINYINT<br/>SQL_CONVERT_VARBINARY<br/>SQL_CONVERT_VARCHAR|1.0|SQLUINTEGER 비트 마스크입니다. 비트 마스크는 *InfoType*에서 명명 된 형식의 데이터에 대 한 **CONVERT** 스칼라 함수를 사용 하 여 데이터 원본에서 지원 되는 변환을 나타냅니다. 비트 마스크가 0 이면 데이터 소스는 동일한 데이터 형식으로의 변환을 포함 하 여 명명 된 형식의 데이터에서 변환을 지원 하지 않습니다.<br/><br/>예를 들어 데이터 원본에서 SQL_INTEGER 데이터를 SQL_BIGINT 데이터 형식으로 변환할 수 있는지 확인 하기 위해 응용 프로그램은 SQL_CONVERT_INTEGER의 *InfoType* 를 사용 하 여 **SQLGetInfo** 를 호출 합니다. 응용 프로그램은 반환 된 비트 마스크 및 SQL_CVT_BIGINT으로 **and** 작업을 수행 합니다. 결과 값이 0이 아닌 경우 변환이 지원 됩니다.<br/><br/>다음 비트 마스크는 지원 되는 변환을 결정 하는 데 사용 됩니다.<br/>SQL_CVT_BIGINT (ODBC 1.0)<br/>SQL_CVT_BINARY (ODBC 1.0)<br/>SQL_CVT_BIT (ODBC 1.0)<br/>SQL_CVT_GUID (ODBC 3.5)<br/>SQL_CVT_CHAR (ODBC 1.0)<br/>SQL_CVT_DATE (ODBC 1.0)<br/>SQL_CVT_DECIMAL (ODBC 1.0)<br/>SQL_CVT_DOUBLE (ODBC 1.0)<br/>SQL_CVT_FLOAT (ODBC 1.0)<br/>SQL_CVT_INTEGER (ODBC 1.0)<br/>SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)<br/>SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)<br/>SQL_CVT_LONGVARBINARY (ODBC 1.0)<br/>SQL_CVT_LONGVARCHAR (ODBC 1.0)<br/>SQL_CVT_NUMERIC (ODBC 1.0)<br/>SQL_CVT_REAL (ODBC 1.0)<br/>SQL_CVT_SMALLINT (ODBC 1.0)<br/>SQL_CVT_TIME (ODBC 1.0)<br/>SQL_CVT_TIMESTAMP (ODBC 1.0)<br/>SQL_CVT_TINYINT (ODBC 1.0)<br/>SQL_CVT_VARBINARY (ODBC 1.0)<br/>SQL_CVT_VARCHAR (ODBC 1.0)|
|SQL_CONVERT_FUNCTIONS|1.0|드라이버 및 연결 된 데이터 원본에서 지원 되는 스칼라 변환 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>다음 비트 마스크는 지원 되는 변환 함수를 결정 하는 데 사용 됩니다.<br/>SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT|
|SQL_CORRELATION_NAME|1.0|테이블 상관 관계 이름이 지원 되는지 여부를 나타내는 SQLUSMALLINT 값입니다.<br/>SQL_CN_NONE = 상관 관계 이름은 지원 되지 않습니다.<br/>SQL_CN_DIFFERENT = 상관 관계 이름은 지원 되지만 해당 이름이 나타내는 테이블의 이름과 달라 야 합니다.<br/>SQL_CN_ANY = 상관 관계 이름은 지원 되며 모든 유효한 사용자 정의 이름일 수 있습니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 SQL_CN_ANY 반환 합니다.|
|SQL_CREATE_ASSERTION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE ASSERTION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA_CREATE_ASSERTION<br/><br/>다음 비트는 제약 조건 특성을 명시적으로 지정 하는 기능이 지원 되는 경우 지원 되는 제약 조건 특성을 지정 합니다 (SQL_ALTER_TABLE 및 SQL_CREATE_TABLE 정보 형식 참조).<br/>SQL_CA_CONSTRAINT_INITIALLY_DEFERRED<br/>SQL_CA_CONSTRAINT_INITIALLY_IMMEDIATE<br/>SQL_CA_CONSTRAINT_DEFERRABLE<br/>SQL_CA_CONSTRAINT_NON_DEFERRABLE<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다. 반환 값이 "0" 이면 **CREATE ASSERTION** 문이 지원 되지 않음을 의미 합니다.|
|SQL_CREATE_CHARACTER_SET|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE CHARACTER SET** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CCS_CREATE_CHARACTER_SET<br/>SQL_CCS_COLLATE_CLAUSE<br/>SQL_CCS_LIMITED_COLLATION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다. 반환 값이 "0" 이면 **CREATE CHARACTER SET** 문이 지원 되지 않음을 의미 합니다.|
|SQL_CREATE_COLLATION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE COLLATION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CCOL_CREATE_COLLATION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다. 반환 값이 "0" 이면 **CREATE COLLATION** 문이 지원 되지 않습니다.|
|SQL_CREATE_DOMAIN|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE DOMAIN** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CDO_CREATE_DOMAIN = CREATE DOMAIN 문이 지원 됩니다 (중간 수준).<br/>SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 은 도메인 제약 조건 이름 (중간 수준)을 지원 합니다.<br/><br/>다음 비트는 열 제약 조건을 만들 수 있는 기능을 지정 합니다.<br/>SQL_CDO_DEFAULT = 도메인 제약 조건 지정이 지원 됩니다 (중간 수준).<br/>SQL_CDO_CONSTRAINT = 도메인 기본값 지정이 지원 됩니다 (중간 수준).<br/>SQL_CDO_COLLATION = 도메인 데이터 정렬 지정이 지원 됩니다 (전체 수준).<br/><br/>다음 비트는 도메인 제약 조건 지정이 지원 되는 경우 지원 되는 제약 조건 특성을 지정 합니다 (SQL_CDO_DEFAULT 설정 됨).<br/>SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (전체 수준)<br/>SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)<br/>SQL_CDO_CONSTRAINT_DEFERRABLE (전체 수준)<br/>SQL_CDO_CONSTRAINT_NON_DEFERRABLE (전체 수준)<br/><br/>반환 값이 "0" 이면 **CREATE DOMAIN** 문이 지원 되지 않음을 의미 합니다.|
|SQL_CREATE_SCHEMA|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE SCHEMA** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CS_CREATE_SCHEMA<br/>SQL_CS_AUTHORIZATION<br/>SQL_CS_DEFAULT_CHARACTER_SET<br/><br/>SQL-92 중간 수준 규격 드라이버는 항상 SQL_CS_CREATE_SCHEMA 및 SQL_CS_AUTHORIZATION 옵션을 지원 되는 것으로 반환 합니다. 이러한 항목은 sql 문이 아닌 SQL-92 항목 수준 에서도 지원 되어야 합니다. SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_CREATE_TABLE|3.0|데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 **CREATE TABLE** 문에서 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CT_CREATE_TABLE = CREATE TABLE 문이 지원 됩니다. (항목 수준)<br/>SQL_CT_TABLE_CONSTRAINT = 테이블 제약 조건 지정이 지원 됩니다 (FIPS 전환 수준).<br/>SQL_CT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 절은 명명 열 및 테이블 제약 조건에 대해 지원 됩니다 (중간 수준).<br/><br/>다음 비트에서는 임시 테이블을 만들 수 있는 기능을 지정 합니다.<br/>SQL_CT_COMMIT_PRESERVE = 삭제 된 행은 커밋 시 보존 됩니다. (전체 수준)<br/>SQL_CT_COMMIT_DELETE = 삭제 된 행은 커밋 시 삭제 됩니다. (전체 수준)<br/>SQL_CT_GLOBAL_TEMPORARY = 전역 임시 테이블을 만들 수 있습니다. (전체 수준)<br/>SQL_CT_LOCAL_TEMPORARY = 로컬 임시 테이블을 만들 수 있습니다. (전체 수준)<br/><br/>다음 비트는 열 제약 조건을 만들 수 있는 기능을 지정 합니다.<br/>SQL_CT_COLUMN_CONSTRAINT = 열 제약 조건 지정이 지원 됩니다 (FIPS 전환 수준).<br/>SQL_CT_COLUMN_DEFAULT = 열 기본값 지정이 지원 됩니다 (FIPS 전환 수준).<br/>SQL_CT_COLUMN_COLLATION = 열 데이터 정렬 지정이 지원 됩니다 (전체 수준).<br/><br/>다음 비트는 열 또는 테이블 제약 조건을 지정할 때 지원 되는 제약 조건 특성을 지정 합니다.<br/>SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (전체 수준)<br/>SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (전체 수준)<br/>SQL_CT_CONSTRAINT_DEFERRABLE (전체 수준)<br/>SQL_CT_CONSTRAINT_NON_DEFERRABLE (전체 수준)|
|SQL_CREATE_TRANSLATION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE TRANSLATION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CTR_CREATE_TRANSLATION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 옵션을 반환 합니다. 반환 값이 "0" 이면 **CREATE TRANSLATION** 문이 지원 되지 않음을 의미 합니다.|
|SQL_CREATE_VIEW|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **CREATE VIEW** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CV_CREATE_VIEW<br/>SQL_CV_CHECK_OPTION<br/>SQL_CV_CASCADED<br/>SQL_CV_LOCAL<br/><br/>반환 값이 "0" 이면 **CREATE VIEW** 문이 지원 되지 않음을 의미 합니다.<br/><br/>SQL-92 항목 수준 규격 드라이버는 항상 SQL_CV_CREATE_VIEW 및 SQL_CV_CHECK_OPTION 옵션을 지원 되는 것으로 반환 합니다.<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_CURSOR_COMMIT_BEHAVIOR|1.0|**커밋** 작업이 데이터 원본의 커서 및 준비 문에 영향을 주는 방식을 나타내는 SQLUSMALLINT 값입니다 (트랜잭션을 커밋하는 경우 데이터 원본의 동작).<br/><br/>이 특성의 값은 SQL_COPT_SS_PRESERVE_CURSORS 다음 설정의 현재 상태를 반영 합니다.<br/>SQL_CB_DELETE = 커서를 닫고 준비 된 문을 삭제 합니다. 커서를 다시 사용 하려면 응용 프로그램에서 문을 다시 준비 하 고 다시 실행 해야 합니다.<br/>SQL_CB_CLOSE = 커서를 닫습니다. 준비 된 문의 경우 응용 프로그램은 **Sqlexecute** 를 다시 호출 하지 않고 문에서 **sqlexecute** 를 호출할 수 있습니다. SQL ODBC 드라이버의 기본값은 SQL_CB_CLOSE입니다. 즉, SQL ODBC 드라이버는 트랜잭션을 커밋할 때 커서를 닫습니다.<br/>SQL_CB_PRESERVE = **커밋** 작업 전후와 동일한 위치에 있는 커서를 유지 합니다. 응용 프로그램은 계속 해 서 데이터를 페치 하거나, 커서를 닫고 다시 준비 하지 않고 문을 다시 실행할 수 있습니다.|
|SQL_CURSOR_ROLLBACK_BEHAVIOR|1.0|**롤백** 작업이 데이터 원본의 커서 및 준비 된 문에 영향을 주는 방법을 나타내는 SQLUSMALLINT 값입니다.<br/>SQL_CB_DELETE = 커서를 닫고 준비 된 문을 삭제 합니다. 커서를 다시 사용 하려면 응용 프로그램에서 문을 다시 준비 하 고 다시 실행 해야 합니다.<br/>SQL_CB_CLOSE = 커서를 닫습니다. 준비 된 문의 경우 응용 프로그램은 **Sqlexecute** 를 다시 호출 하지 않고 문에서 **sqlexecute** 를 호출할 수 있습니다.<br/>SQL_CB_PRESERVE = **롤백** 작업 전후와 동일한 위치에 있는 커서를 유지 합니다. 응용 프로그램은 계속 해 서 데이터를 페치 하거나, 커서를 닫고 다시 준비 하지 않고 문을 다시 실행할 수 있습니다.|
|SQL_CURSOR_SENSITIVITY|3.0|커서 민감도에 대 한 지원을 나타내는 SQLUINTEGER 값입니다.<br/>SQL_INSENSITIVE = 문 핸들의 모든 커서는 동일한 트랜잭션 내의 다른 커서에의 한 변경 내용을 반영 하지 않고 결과 집합을 표시 합니다.<br/>SQL_UNSPECIFIED = 문 핸들의 커서가 동일한 트랜잭션 내의 다른 커서에의 한 결과 집합의 변경 내용을 볼 수 있는지 여부를 지정 하지 않습니다. 문 핸들의 커서는 표시 되지 않거나, 일부 또는 모든 변경 내용을 볼 수 있습니다.<br/>SQL_SENSITIVE = 커서는 동일한 트랜잭션 내에서 다른 커서에 의해 수행 된 변경 내용을 인식 합니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 SQL_UNSPECIFIED 옵션을 반환 합니다.<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 SQL_INSENSITIVE 옵션을 반환 합니다.|
|SQL_DATA_SOURCE_NAME|1.0|연결 중에 사용 된 데이터 소스 이름을 가진 문자열입니다. 응용 프로그램이 **SQLConnect**이라고 하는 경우이 값은 *szdsn* 인수의 값입니다. 응용 프로그램이 **SQLDriverConnect** 또는 **SQLBrowseConnect**이라고 하는 경우이 값은 드라이버에 전달 된 연결 문자열의 DSN 키워드 값입니다. 연결 문자열에 **DSN** 키워드 (예: **DRIVER** 키워드를 포함 하는 경우)가 포함 되지 않은 경우 빈 문자열입니다.|
|SQL_DATA_SOURCE_READ_ONLY|1.0|문자열입니다. 데이터 원본이 읽기 전용 모드로 설정 된 경우 "Y"이 고, 그렇지 않으면 "N"입니다.<br/><br/>이 특성은 데이터 원본 자체에만 관련 됩니다. 데이터 원본에 대 한 액세스를 활성화 하는 드라이버의 특성이 아닙니다. 읽기/쓰기 인 드라이버는 읽기 전용 데이터 소스와 함께 사용할 수 있습니다. 드라이버가 읽기 전용 이면 모든 데이터 원본은 읽기 전용 이어야 하 고 SQL_DATA_SOURCE_READ_ONLY을 반환 해야 합니다.|
|SQL_DATABASE_NAME|1.0|데이터 소스가 "database" 라는 명명 된 개체를 정의 하는 경우 사용 중인 현재 데이터베이스의 이름이 포함 된 문자열입니다.<br/><br/>ODBC 3.x에서는 SQL_ATTR_CURRENT_CATALOG *특성* 인수를 사용 하 여 **SQLGetConnectAttr** 를 호출 하 여이 *InfoType* 에 대해 반환 된 값을 반환할 수도 있습니다.|
|SQL_DATETIME_LITERALS|3.0|데이터 원본에서 지 원하는 SQL-92 datetime 리터럴을 열거 하는 SQLUINTEGER 비트 마스크입니다. 이러한 리터럴은 SQL-92 사양에 나와 있으며 ODBC에서 정의한 datetime 리터럴 이스케이프 절과는 별개입니다. ODBC datetime 리터럴 이스케이프 절에 대 한 자세한 내용은 [날짜, 시간 및 타임 스탬프 리터럴](../develop-app/date-time-and-timestamp-literals.md)을 참조 하세요.<br/><br/> FIPS 전환 수준 규격 드라이버는 항상 다음 목록에 있는 비트의 비트 마스크에서 "1" 값을 반환 합니다. 값이 "0" 이면 SQL-92 datetime 리터럴이 지원 되지 않음을 의미 합니다.<br/><br/>다음 비트 마스크는 지원 되는 리터럴을 결정 하는 데 사용 됩니다.<br/>SQL_DL_SQL92_DATE<br/>SQL_DL_SQL92_TIME<br/>SQL_DL_SQL92_TIMESTAMP<br/>SQL_DL_SQL92_INTERVAL_YEAR<br/>SQL_DL_SQL92_INTERVAL_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY<br/>SQL_DL_SQL92_INTERVAL_HOUR<br/>SQL_DL_SQL92_INTERVAL_MINUTE<br/>SQL_DL_SQL92_INTERVAL_SECOND<br/>SQL_DL_SQL92_INTERVAL_YEAR_TO_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_HOUR<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND|
|SQL_DBMS_NAME|1.0|드라이버에서 액세스 하는 DBMS 제품의 이름을 포함 하는 문자열입니다.|
|SQL_DBMS_VER|1.0|드라이버에서 액세스 하는 DBMS 제품의 버전을 나타내는 문자열입니다. 버전은 # #. # #. # # # # 형식입니다. 여기서 처음 두 자리는 주 버전, 다음 두 자리는 부 버전, 마지막 4 자리는 릴리스 버전입니다. 드라이버는이 양식에서 DBMS 제품 버전을 렌더링 해야 하지만 DBMS 제품별 버전을 추가할 수도 있습니다. 예를 들면 "04.01.0000 Rdb 4.1"입니다.|
|SQL_DDL_INDEX|3.0|인덱스 생성 및 삭제에 대 한 지원을 나타내는 SQLUINTEGER 값입니다.<br/>SQL_DI_CREATE_INDEX<br/>SQL_DI_DROP_INDEX|
|SQL_DEFAULT_TXN_ISOLATION|1.0|드라이버 또는 데이터 원본에서 지원 되는 기본 트랜잭션 격리 수준을 나타내는 SQLUINTEGER 값 또는 데이터 원본이 트랜잭션을 지원 하지 않는 경우 0입니다. 트랜잭션 격리 수준을 정의 하는 데 사용 되는 용어는 다음과 같습니다.<br/>**커밋되지 않은 읽기** 트랜잭션 1은 행을 변경 합니다. 트랜잭션 1이 변경 내용을 커밋하기 전에 트랜잭션 2는 변경 된 행을 읽습니다. 트랜잭션 1이 변경 내용을 롤백하는 경우 트랜잭션 2는 존재 하지 않는 것으로 간주 되는 행을 읽습니다.<br/>**반복 불가능 읽기** 트랜잭션 1은 행을 읽습니다. 트랜잭션 2가 해당 행을 업데이트 하거나 삭제 하 고이 변경 내용을 커밋합니다. 트랜잭션 1이 행을 다시 읽을 경우 다른 행 값을 받거나 행이 삭제 되었음을 검색 합니다.<br/>**가상** 트랜잭션 1은 일부 검색 조건을 충족 하는 행 집합을 읽습니다. 트랜잭션 2는 검색 조건과 일치 하는 하나 이상의 행 (삽입 또는 업데이트를 통해)을 생성 합니다. 트랜잭션 1에서 행을 읽는 문을 다시 실행 하면 다른 행 집합을 받습니다.<br/><br/>데이터 원본에서 트랜잭션을 지 원하는 경우 드라이버는 다음 비트 마스크 중 하나를 반환 합니다.<br/>SQL_TXN_READ_UNCOMMITTED = 더티 읽기, 반복 불가능 읽기 및 phantoms 가능 합니다.<br/>SQL_TXN_READ_COMMITTED = 더티 읽기는 불가능 합니다. 반복 불가능 읽기 및 phantoms 가능 합니다.<br/>SQL_TXN_REPEATABLE_READ = 커밋되지 않은 읽기 및 반복 되지 않는 읽기는 불가능 합니다. Phantoms를 사용할 수 있습니다.<br/>SQL_TXN_SERIALIZABLE = 트랜잭션을 직렬화 할 수 있습니다. 직렬화 가능 트랜잭션은 커밋되지 않은 읽기, 반복 불가능 읽기 또는 phantoms을 허용 하지 않습니다.|
|SQL_DESCRIBE_PARAMETER|3.0|문자열은 "Y" (매개 변수를 설명할 수 있는 경우)입니다. "N", 그렇지 않으면입니다.<br/><br/>SQL-92 전체 수준 규격 드라이버는 **설명 입력** 문을 지원 하므로 일반적으로 "Y"를 반환 합니다. 그러나이는 기본 SQL 지원을 직접 지정 하지 않으므로 매개 변수를 설명 하는 것은 SQL-92 전체 수준 호환 드라이버 에서도 지원 되지 않을 수 있습니다.|
|SQL_DM_VER|3.0|드라이버 관리자의 버전이 포함 된 문자열입니다. 버전은 # #. # #. # # # #. # # # # 형식입니다. 여기서:<br/>두 숫자의 첫 번째 집합은 상수 SQL_SPEC_MAJOR에 지정 된 대로 주 ODBC 버전입니다.<br/>두 숫자의 두 번째 집합은 상수 SQL_SPEC_MINOR에 지정 된 대로 부 ODBC 버전입니다.<br/>네 자리 숫자의 세 번째 집합은 드라이버 관리자의 주 빌드 번호입니다.<br/>네 자리 숫자의 마지막 집합은 드라이버 관리자 부 빌드 번호입니다.<br/>Windows 7 드라이버 관리자 버전은 03.80입니다. Windows 8 드라이버 관리자 버전은 03.81입니다.|
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|3.8|드라이버가 드라이버 인식 풀링을 지원 하는지 여부를 나타내는 SQLUINTEGER 값입니다. 자세한 내용은 [드라이버 인식 연결 풀링](../develop-app/driver-aware-connection-pooling.md)을 참조 하세요.<br/><br/>SQL_DRIVER_AWARE_POOLING_CAPABLE 드라이버에서 드라이버 인식 풀링 메커니즘을 지원할 수 있음을 나타냅니다.<br/>SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 드라이버에서 드라이버 인식 풀링 메커니즘을 지원할 수 없음을 나타냅니다.<br/><br/>드라이버는 SQL_DRIVER_AWARE_POOLING_SUPPORTED를 구현할 필요가 없으며 드라이버 관리자는 드라이버의 반환 값을 인식 하지 못합니다.|
|SQL_DRIVER_HDBCSQL_DRIVER_HENV|1.0|*InfoType*인수에 의해 결정 되는, 운전 환경 핸들 또는 연결 핸들을 나타내는 SQLULEN 값입니다.<br/><br/>이러한 정보 유형은 드라이버 관리자에 의해 구현 됩니다.|
|SQL_DRIVER_HDESC|3.0|SQLULEN 값으로, 드라이버 관리자의 설명자 핸들에 의해 결정 되는 드라이버 설명자 핸들은 \* 응용 프로그램에서 *infovalueptr* 의 입력에 전달 되어야 합니다. 이 경우 *Infovalueptr* 은 모두 입력 및 출력 인수입니다. \* *Infovalueptr* 에 전달 된 입력 설명자 핸들은 *ConnectionHandle*에 명시적 또는 암시적으로 할당 되어야 합니다.<br/><br/>응용 프로그램은이 정보 형식으로 **SQLGetInfo** 를 호출 하기 전에 드라이버 관리자의 설명자 핸들의 복사본을 만들어 출력에서 핸들을 덮어쓰지 않도록 해야 합니다.<br/><br/>이 정보 유형은 드라이버 관리자에 의해 구현 됩니다.|
|SQL_DRIVER_HLIB|2.0|Microsoft Windows 운영 체제 또는 다른 운영 체제에서 드라이버 DLL이 로드 될 때 드라이버 관리자로 반환 되는 로드 라이브러리의 *hinst* 값입니다. 핸들은 **SQLGetInfo**호출에 지정 된 연결 핸들에 대해서만 유효 합니다.<br/><br/>이 정보 유형은 드라이버 관리자에 의해 구현 됩니다.|
|SQL_DRIVER_HSTMT|1.0|\*응용 프로그램에서 *infovalueptr* 의 입력을 전달 해야 하는 드라이버 관리자 문 핸들에 의해 결정 되는 sqlulen 값입니다. 이 경우 *Infovalueptr* 은 모두 입력 및 출력 인수입니다. \* *Infovalueptr* 에 전달 된 입력 문 핸들은 *ConnectionHandle*인수에 할당 되어야 합니다.<br/><br/>응용 프로그램은이 정보 형식으로 **SQLGetInfo** 를 호출 하기 전에 드라이버 관리자의 문 핸들 복사본을 만들어 출력에서 핸들을 덮어쓰지 않도록 해야 합니다.<br/><br/>이 정보 유형은 드라이버 관리자에 의해 구현 됩니다.|
|SQL_DRIVER_NAME|1.0|데이터 원본에 액세스 하는 데 사용 되는 드라이버의 파일 이름이 포함 된 문자열입니다.|
|SQL_DRIVER_ODBC_VER|2.0|드라이버가 지 원하는 ODBC 버전을 포함 하는 문자열입니다. 버전은 # #. # # 형식입니다. 여기서 처음 두 자리는 주 버전이 고 다음 두 자리는 부 버전입니다. 주 버전 번호와 부 버전 번호를 SQL_SPEC_MAJOR 및 SQL_SPEC_MINOR 정의 합니다. 이 설명서에 설명 된 ODBC 버전의 경우 3 및 0 이며 드라이버는 "03.00"를 반환 해야 합니다.<br/><br/>ODBC 드라이버 관리자는 기존 응용 프로그램에 대해 이전 버전과의 호환성을 유지 하기 위해 SQLGetInfo (SQL_DRIVER_ODBC_VER)의 반환 값을 수정 하지 않습니다. 드라이버에서 반환 되는 값을 지정 합니다. 그러나 C 데이터 형식 확장성을 지 원하는 드라이버는 응용 프로그램에서 **SQLSetEnvAttr** 를 호출 하 여 SQL_ATTR_ODBC_VERSION를 3.8로 설정 하는 경우 3.8 이상을 반환 해야 합니다. 자세한 내용은 [ODBC의 C 데이터 형식](../develop-app/c-data-types-in-odbc.md)을 참조 하세요.|
|SQL_DRIVER_VER|1.0|드라이버 버전 및 드라이버에 대 한 설명 (선택 사항)이 포함 된 문자열입니다. 버전의 버전은 # #. # #. # # # # 형식입니다. 여기서 처음 두 자리는 주 버전이 고 다음 두 자리는 부 버전이 며 마지막 4 자리는 릴리스 버전입니다.|
|SQL_DROP_ASSERTION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP ASSERTION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DA_DROP_ASSERTION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.|
|SQL_DROP_CHARACTER_SET|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP CHARACTER SET** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DCS_DROP_CHARACTER_SET<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.|
|SQL_DROP_COLLATION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP COLLATION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DC_DROP_COLLATION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.|
|SQL_DROP_DOMAIN|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP DOMAIN** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DD_DROP_DOMAIN<br/>SQL_DD_CASCADE<br/>SQL_DD_RESTRICT<br/><br/>SQL-92 중간 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_DROP_SCHEMA|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP SCHEMA** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DS_DROP_SCHEMA<br/>SQL_DS_CASCADE<br/>SQL_DS_RESTRICT<br/><br/>SQL-92 중간 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_DROP_TABLE|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP TABLE** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DT_DROP_TABLE<br/>SQL_DT_CASCADE<br/>SQL_DT_RESTRICT<br/><br/>FIPS 전환 수준 준수 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_DROP_TRANSLATION|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **DROP TRANSLATION** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DTR_DROP_TRANSLATION<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.|
|SQL_DROP_VIEW|3.0|데이터 원본에서 지 원하는 SQL-92에 정의 된 대로 **DROP VIEW** 문의 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_DV_DROP_VIEW<br/>SQL_DV_CASCADE<br/>SQL_DV_RESTRICT<br/><br/>FIPS 전환 수준 준수 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|3.0|드라이버에서 지원 되는 동적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 첫 번째 하위 집합을 포함 합니다. 두 번째 하위 집합은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA1_NEXT = 커서가 동적 커서 인 경우 **Sqlfetchscroll** 에 대 한 호출에서 SQL_FETCH_NEXT의 *fetchorientation* 인수가 지원 됩니다.<br/>SQL_CA1_ABSOLUTE = SQL_FETCH_FIRST, SQL_FETCH_LAST 및 SQL_FETCH_ABSOLUTE의 *Fetchorientation* 인수는 커서가 동적 커서 일 때 **sqlfetchscroll** 에 대 한 호출에서 지원 됩니다. 인출 되는 행 집합은 현재 커서 위치와는 독립적입니다.<br/>SQL_CA1_RELATIVE = SQL_FETCH_PRIOR 및 SQL_FETCH_RELATIVE의 *Fetchorientation* 인수는 커서가 동적 커서 일 때 **sqlfetchscroll** 에 대 한 호출에서 지원 됩니다. 인출 되는 행 집합은 현재 커서 위치에 따라 달라 집니다. 앞 으로만 이동 가능한 커서에는 SQL_FETCH_NEXT만 지원 되기 때문에 SQL_FETCH_NEXT와 구분 됩니다.<br/>SQL_CA1_BOOKMARK = 커서가 동적 커서 인 경우 **Sqlfetchscroll** 에 대 한 호출에서 SQL_FETCH_BOOKMARK의 *fetchorientation* 인수가 지원 됩니다.<br/>SQL_CA1_LOCK_EXCLUSIVE = SQL_LOCK_EXCLUSIVE의 *LockType* 인수는 커서가 동적 커서 이면 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_LOCK_NO_CHANGE = SQL_LOCK_NO_CHANGE의 *LockType* 인수는 커서가 동적 커서 이면 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_LOCK_UNLOCK = SQL_LOCK_UNLOCK의 *LockType* 인수는 커서가 동적 커서 이면 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_POS_POSITION = SQL_POSITION의 *작업* 인수는 커서가 동적 커서 일 때 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_POS_UPDATE = SQL_UPDATE의 *작업* 인수는 커서가 동적 커서 일 때 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_POS_DELETE = SQL_DELETE의 *작업* 인수는 커서가 동적 커서 일 때 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_POS_REFRESH = SQL_REFRESH의 *작업* 인수는 커서가 동적 커서 일 때 **SQLSetPos** 호출에서 지원 됩니다.<br/>SQL_CA1_POSITIONED_UPDATE = 커서가 동적 커서 일 때 현재 SQL 문이 지원 되는 업데이트입니다. SQL-92 항목 수준 호환 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.<br/>SQL_CA1_POSITIONED_DELETE = 커서가 동적 커서 일 때 현재 SQL 문이 지원 되는 DELETE입니다. SQL-92 항목 수준 호환 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.<br/>SQL_CA1_SELECT_FOR_UPDATE = 커서가 동적 커서 이면 SELECT FOR UPDATE SQL 문이 지원 됩니다. SQL-92 항목 수준 호환 드라이버는 항상이 옵션을 지원 되는 것으로 반환 합니다.<br/>SQL_CA1_BULK_ADD = SQL_ADD의 *작업* 인수는 커서가 동적 커서 일 때 **SQLBulkOperations** 에 대 한 호출에서 지원 됩니다.<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK = SQL_UPDATE_BY_BOOKMARK의 *작업* 인수는 커서가 동적 커서 일 때 **SQLBulkOperations** 에 대 한 호출에서 지원 됩니다.<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK = SQL_DELETE_BY_BOOKMARK의 *작업* 인수는 커서가 동적 커서 일 때 **SQLBulkOperations** 에 대 한 호출에서 지원 됩니다.<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK = SQL_FETCH_BY_BOOKMARK의 *작업* 인수는 커서가 동적 커서 일 때 **SQLBulkOperations** 에 대 한 호출에서 지원 됩니다.<br/><br/>SQL-92 중간 수준 규격 드라이버는 포함 된 SQL FETCH 문을 통해 스크롤 가능 커서를 지원 하기 때문에 일반적으로 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 지원 되는 것으로 반환 합니다. 이는 기본 SQL 지원을 직접 확인 하지 않으므로 스크롤 가능 커서는 SQL-92 중간 수준 규격 드라이버에 대해서도 지원 되지 않을 수 있습니다.|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|3.0|드라이버에서 지원 되는 동적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 두 번째 하위 집합을 포함 합니다. 첫 번째 하위 집합은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA2_READ_ONLY_CONCURRENCY = 업데이트가 허용 되지 않는 읽기 전용 동적 커서를 지원 합니다. SQL_ATTR_CONCURRENCY statement 특성은 동적 커서에 대해 SQL_CONCUR_READ_ONLY 수 있습니다.<br/>SQL_CA2_LOCK_CONCURRENCY = 행이 업데이트 될 수 있도록 충분히 낮은 수준의 잠금을 사용 하는 동적 커서입니다. SQL_ATTR_CONCURRENCY statement 특성은 동적 커서에 대해 SQL_CONCUR_LOCK 수 있습니다. 이러한 잠금은 SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정 된 트랜잭션 격리 수준과 일치 해야 합니다.<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY = 행 버전을 비교 하는 낙관적 동시성 제어를 사용 하는 동적 커서가 지원 됩니다. SQL_ATTR_CONCURRENCY statement 특성은 동적 커서에 대해 SQL_CONCUR_ROWVER 수 있습니다.<br/>SQL_CA2_OPT_VALUES_CONCURRENCY = 값을 비교 하는 낙관적 동시성 제어를 사용 하는 동적 커서가 지원 됩니다. SQL_ATTR_CONCURRENCY statement 특성은 동적 커서에 대해 SQL_CONCUR_VALUES 수 있습니다.<br/>SQL_CA2_SENSITIVITY_ADDITIONS = 추가 된 행이 동적 커서에 표시 됩니다. 커서는 이러한 행으로 스크롤할 수 있습니다. 이러한 행은 커서에 추가 되는 드라이버에 종속 됩니다.<br/>SQL_CA2_SENSITIVITY_DELETIONS = 삭제 된 행을 동적 커서에서 더 이상 사용할 수 없으며 결과 집합에 "hole"을 두지 않습니다. 동적 커서가 삭제 된 행에서 스크롤하면 해당 행으로 돌아갈 수 없습니다.<br/>SQL_CA2_SENSITIVITY_UPDATES = 행 업데이트가 동적 커서에 표시 됩니다. 동적 커서가에서 업데이트 된 행으로 스크롤되고 반환 되는 경우 커서가 반환 하는 데이터는 원래 데이터가 아닌 업데이트 된 데이터입니다.<br/>SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서 일 때 **SELECT** 문에 영향을 줍니다.<br/>SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서 인 경우 **INSERT** 문에 영향을 줍니다.<br/>SQL_CA2_MAX_ROWS_DELETE = 커서가 동적 커서 인 경우 SQL_ATTR_MAX_ROWS 문 특성은 **DELETE** 문에 영향을 줍니다.<br/>SQL_CA2_MAX_ROWS_UPDATE = 커서가 동적 커서 인 경우 SQL_ATTR_MAX_ROWS statement 특성은 **UPDATE** 문에 영향을 줍니다.<br/>SQL_CA2_MAX_ROWS_CATALOG = 커서가 동적 커서 인 경우 SQL_ATTR_MAX_ROWS statement 특성은 **카탈로그** 결과 집합에 영향을 줍니다.<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS 문 특성은 커서가 동적 커서 일 때 **SELECT**, **INSERT**, **DELETE**및 **UPDATE** 문과 **카탈로그** 결과 집합에 영향을 줍니다.<br/>SQL_CA2_CRC_EXACT = 커서가 동적 커서 이면 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드에서 정확한 행 수를 사용할 수 있습니다.<br/>SQL_CA2_CRC_APPROXIMATE = 커서가 동적 커서 이면 SQL_DIAG_CURSOR_ROW_COUNT 진단 필드에서 대략적인 행 수를 사용할 수 있습니다.<br/>SQL_CA2_SIMULATE_NON_UNIQUE =이 드라이버는 커서가 동적 커서 일 때 시뮬레이션 된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 주는지 보장 하지 않습니다. 이를 보장 하는 것은 응용 프로그램의 책임입니다. 문이 두 개 이상의 행에 영향을 주는 경우 **Sqlexecute** 또는 **SQLEXECDIRECT** 는 SQLSTATE 01001 [커서 작업 충돌]을 반환 합니다. 이 동작을 설정 하기 위해 응용 프로그램은 SQL_ATTR_SIMULATE_CURSOR 특성이 SQL_SC_NON_UNIQUE로 설정 된 **SQLSetStmtAttr** 를 호출 합니다.<br/>SQL_CA2_SIMULATE_TRY_UNIQUE = 드라이버가 커서가 동적 커서 일 때 시뮬레이션 된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 주는지 보장 하려고 합니다. 드라이버는 고유 키가 없는 경우와 같이 둘 이상의 행에 영향을 줄 수 있는 경우에도 이러한 문을 항상 실행 합니다. 문이 두 개 이상의 행에 영향을 주는 경우 **Sqlexecute** 또는 **SQLEXECDIRECT** 는 SQLSTATE 01001 [커서 작업 충돌]을 반환 합니다. 이 동작을 설정 하기 위해 응용 프로그램은 SQL_ATTR_SIMULATE_CURSOR 특성이 SQL_SC_TRY_UNIQUE로 설정 된 **SQLSetStmtAttr** 를 호출 합니다.<br/>SQL_CA2_SIMULATE_UNIQUE = 드라이버는 커서가 동적 커서 일 때 시뮬레이션 된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 줍니다. 드라이버가 지정 된 문에 대해이를 보장할 수 없는 경우 **Sqlexecdirect** 또는 **SQLPREPARE** 는 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다. 이 동작을 설정 하기 위해 응용 프로그램은 SQL_ATTR_SIMULATE_CURSOR 특성이 SQL_SC_UNIQUE로 설정 된 **SQLSetStmtAttr** 를 호출 합니다.|
|SQL_EXPRESSIONS_IN_ORDERBY|1.0|문자열: 데이터 원본이 **ORDER by** 목록에서 식을 지 원하는 경우에는 "Y"입니다. 그렇지 않으면 "N"입니다.|
|SQL_FILE_USAGE|2.0|단일 계층 드라이버가 데이터 원본에서 파일을 직접 처리 하는 방법을 나타내는 SQLUSMALLINT 값입니다.<br/>SQL_FILE_NOT_SUPPORTED = 드라이버가 단일 계층 드라이버가 아닙니다. 예를 들어 ORACLE 드라이버는 2 계층 드라이버입니다.<br/>SQL_FILE_TABLE = 단일 계층 드라이버는 데이터 원본의 파일을 테이블로 처리 합니다. 예를 들어 Xbase 드라이버는 각 Xbase 파일을 테이블로 처리 합니다.<br/>SQL_FILE_CATALOG = 단일 계층 드라이버는 데이터 원본의 파일을 카탈로그로 처리 합니다. 예를 들어 Microsoft Access 드라이버는 각 Microsoft Access 파일을 전체 데이터베이스로 처리 합니다.<br/><br/>응용 프로그램은이를 사용 하 여 사용자가 데이터를 선택 하는 방법을 결정할 수 있습니다. 예를 들어, Xbase 사용자는 데이터를 파일에 저장 된 것으로 생각 하는 반면, ORACLE 및 Microsoft Access 사용자는 일반적으로 데이터를 테이블에 저장 된 것으로 간주 합니다.<br/><br/>사용자가 Xbase 데이터 소스를 선택 하면 응용 프로그램에서 Windows **파일 열기** 일반 대화 상자를 표시할 수 있습니다. 사용자가 Microsoft Access 또는 ORACLE 데이터 원본을 선택 하면 응용 프로그램에서 사용자 지정 **테이블 선택** 대화 상자를 표시할 수 있습니다.|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|3.0|드라이버에서 지원 되는 앞 으로만 이동 가능한 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 첫 번째 하위 집합을 포함 합니다. 두 번째 하위 집합은 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA1_NEXT<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1를 참조 하 고 "동적 커서"의 경우 "앞 으로만 커서"를 대체 합니다.|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|3.0|드라이버에서 지원 되는 앞 으로만 이동 가능한 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 두 번째 하위 집합을 포함 합니다. 첫 번째 하위 집합은 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2를 참조 하 고 "동적 커서"의 경우 "앞 으로만 커서"를 대체 합니다.|
|SQL_GETDATA_EXTENSIONS|2.0|**SQLGetData**에 확장을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>다음 비트 마스크는 플래그와 함께 드라이버에서 **SQLGetData**에 대해 지 원하는 일반적인 확장을 결정 하는 데 사용 됩니다.<br/>SQL_GD_ANY_COLUMN = **SQLGetData** 는 마지막으로 바인딩된 열 앞에 있는 열을 포함 하 여 바인딩되지 않은 모든 열에 대해 호출 될 수 있습니다. 열이 반환 되는 SQL_GD_ANY_ORDER 경우를 제외 하 고는 열을 오름차순으로 호출 해야 합니다.<br/>SQL_GD_ANY_ORDER = 모든 순서로 바인딩되지 않은 열에 대해 **SQLGetData** 를 호출할 수 있습니다. **SQLGetData** 는 SQL_GD_ANY_COLUMN 반환 되지 않는 한 마지막으로 바인딩된 열 이후의 열에 대해서만 호출할 수 있습니다.<br/>SQL_GD_BLOCK = **SQLSetPos**를 사용 하 여 해당 행에 대 한 위치를 변경한 후 블록 (행 집합 크기가 1 보다 큰)의 모든 행에 있는 바인딩되지 않은 열에 대해 **SQLGetData** 를 호출할 수 있습니다.<br/>바인딩되지 않은 열 외에도 바인딩된 열에 대해서도 SQL_GD_BOUND = **SQLGetData** 를 호출할 수 있습니다. 드라이버는 SQL_GD_ANY_COLUMN 반환 하지 않는 한이 값을 반환할 수 없습니다.<br/>SQL_GD_OUTPUT_PARAMS = **SQLGetData** 를 호출 하 여 출력 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.<br/><br/>**SQLGetData** 는 마지막으로 바인딩된 열 다음에 발생 하는 바인딩되지 않은 열에서 데이터를 반환 하는 데 필요 하며, 열 번호를 오름차순으로 호출 하 고 행 블록의 행에는 표시 되지 않습니다.<br/><br/>드라이버에서 책갈피 (고정 길이 또는 가변 길이)를 지 원하는 경우 0 열에서 **SQLGetData** 호출을 지원 해야 합니다. SQL_GETDATA_EXTENSIONS *InfoType*를 사용 하 여 **SQLGetInfo** 호출에 대해 드라이버가 반환 하는 항목에 관계 없이이 지원이 필요 합니다.|
|SQL_GROUP_BY|2.0|**GROUP by** 절의 열과 select 목록의 집계 되지 않은 열 간의 관계를 지정 하는 SQLUSMALLINT 값입니다.<br/>SQL_GB_COLLATE = 각 그룹화 열 끝에 **COLLATE** 절을 지정할 수 있습니다. (ODBC 3.0)<br/>SQL_GB_NOT_SUPPORTED = **GROUP BY** 절은 지원 되지 않습니다. (ODBC 2.0)<br/>SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP by** 절은 SELECT 목록에서 집계할 때가 아닌 모든 열을 포함 해야 합니다. 다른 열은 포함할 수 없습니다. 예를 들어 **EMPLOYEE GROUP BY DEPT에서 dept, MAX (급여)를 선택**합니다. (ODBC 2.0)<br/>SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP by** 절은 SELECT 목록에서 집계할 때가 아닌 모든 열을 포함 해야 합니다. Select 목록에 없는 열이 포함 될 수 있습니다. 예를 들어 **EMPLOYEE GROUP BY dept, AGE에서 dept, MAX (급여)를 선택**합니다. (ODBC 2.0)<br/>SQL_GB_NO_RELATION = **GROUP by** 절의 열과 select 목록의 열은 관련이 없습니다. Select 목록에서 그룹화 되지 않은 비 집계 열의 의미는 데이터 원본에 따라 달라 집니다. 예를 들어 **부서, 직원 그룹 별 급여, 연령를 선택**합니다. (ODBC 2.0)<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 SQL_GB_GROUP_BY_EQUALS_SELECT 옵션을 반환 합니다. SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 SQL_GB_COLLATE 옵션을 반환 합니다. 지원 되는 옵션이 없는 경우 데이터 원본에서 **GROUP by** 절을 지원 하지 않습니다.|
|SQL_IDENTIFIER_CASE|1.0|SQLUSMALLINT 값은 다음과 같습니다.<br/>SQL_IC_UPPER = SQL의 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에 대문자로 저장 됩니다.<br/>SQL_IC_LOWER = SQL의 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에 소문자로 저장 됩니다.<br/>SQL_IC_SENSITIVE = SQL의 식별자는 대/소문자를 구분 하며 시스템 카탈로그에 혼합 된 대/소문자를 저장 합니다.<br/>SQL_IC_MIXED = SQL의 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에 혼합 된 대/소문자를 저장 합니다.<br/><br/>SQL-92의 식별자는 대/소문자를 구분 하지 않으므로 SQL-92 (모든 수준)를 엄격히 준수 하는 드라이버는 SQL_IC_SENSITIVE 옵션을 지원 되는 것으로 반환 하지 않습니다.|
|SQL_IDENTIFIER_QUOTE_CHAR|1.0|SQL 문에서 따옴표 붙은 (구분 된) 식별자의 시작 및 끝 구분 기호로 사용 되는 문자열입니다. ODBC 함수에 인수로 전달 되는 식별자는 따옴표로 묶을 필요가 없습니다. 데이터 소스에서 따옴표 붙은 식별자를 지원 하지 않는 경우 빈가 반환 됩니다.<br/><br/>연결 특성 SQL_ATTR_METADATA_ID SQL_TRUE으로 설정 된 경우이 문자열을 사용 하 여 카탈로그 함수 인수를 따옴표로 묶을 수도 있습니다.<br/><br/>SQL-92의 식별자 따옴표 문자가 큰따옴표 (") 이기 때문에 SQL-92를 엄격 하 게 준수 하는 드라이버는 항상 큰따옴표 문자를 반환 합니다.|
|SQL_INDEX_KEYWORDS|3.0|드라이버에서 지원 되는 CREATE INDEX 문의 키워드를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/>SQL_IK_NONE = 모든 키워드가 지원 되지 않습니다.<br/>SQL_IK_ASC = ASC 키워드가 지원 됩니다.<br/>SQL_IK_DESC = DESC 키워드가 지원 됩니다.<br/>SQL_IK_ALL = 모든 키워드가 지원 됩니다.<br/><br/>CREATE INDEX 문이 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_DLL_INDEX 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다.|
|SQL_INFO_SCHEMA_VIEWS|3.0|드라이버에서 지 원하는 INFORMATION_SCHEMA의 뷰를 열거 하는 SQLUINTEGER 비트 마스크입니다. 의 뷰와 INFORMATION_SCHEMA 내용은 SQL-92에 정의 되어 있습니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>지원 되는 뷰를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_ISV_ASSERTIONS = 지정 된 사용자가 소유 하 고 있는 카탈로그의 어설션을 식별 합니다. (전체 수준)<br/>SQL_ISV_CHARACTER_SETS = 지정 된 사용자가 액세스할 수 있는 카탈로그의 문자 집합을 식별 합니다. (중간 수준)<br/>SQL_ISV_CHECK_CONSTRAINTS = 지정 된 사용자가 소유 하는 CHECK 제약 조건을 식별 합니다. (중간 수준)<br/>SQL_ISV_COLLATIONS = 지정 된 사용자가 액세스할 수 있는 카탈로그의 문자 데이터 정렬을 식별 합니다. (전체 수준)<br/>SQL_ISV_COLUMN_DOMAIN_USAGE = 카탈로그에 정의 되어 있고 지정 된 사용자가 소유 하는 도메인에 종속 된 카탈로그의 열을 식별 합니다. (중간 수준)<br/>SQL_ISV_COLUMN_PRIVILEGES = 지정 된 사용자가 사용 하거나 허용 하는 영구 테이블의 열에 대 한 권한을 식별 합니다. (FIPS 전환 수준)<br/>SQL_ISV_COLUMNS = 지정 된 사용자가 액세스할 수 있는 영구 테이블의 열을 식별 합니다. (FIPS 전환 수준)<br/>SQL_ISV_CONSTRAINT_COLUMN_USAGE = CONSTRAINT_TABLE_USAGE 뷰와 비슷하며 지정 된 사용자가 소유 하는 다양 한 제약 조건에 대해 열이 식별 됩니다. (중간 수준)<br/>SQL_ISV_CONSTRAINT_TABLE_USAGE = 제약 조건에 사용 되는 테이블 (참조, 고유 및 어설션)을 식별 하 고 지정 된 사용자가 소유 합니다. (중간 수준)<br/>SQL_ISV_DOMAIN_CONSTRAINTS = 지정 된 사용자가 액세스할 수 있는 도메인 제약 조건 (카탈로그의 도메인)을 식별 합니다. (중간 수준)<br/>SQL_ISV_DOMAINS = 사용자가 액세스할 수 있는 카탈로그에 정의 된 도메인을 식별 합니다. (중간 수준)<br/>SQL_ISV_KEY_COLUMN_USAGE = 지정 된 사용자가 키로 제한 하는 카탈로그에 정의 된 열을 식별 합니다. (중간 수준)<br/>SQL_ISV_REFERENTIAL_CONSTRAINTS = 지정 된 사용자가 소유 하 고 있는 참조 제약 조건을 식별 합니다. (중간 수준)<br/>SQL_ISV_SCHEMATA = 지정 된 사용자가 소유 하는 스키마를 식별 합니다. (중간 수준)<br/>SQL_ISV_SQL_LANGUAGES = SQL 구현에서 지원 되는 SQL 규칙 수준, 옵션 및 언어를 식별 합니다. (중간 수준)<br/>SQL_ISV_TABLE_CONSTRAINTS = 지정 된 사용자가 소유 하는 테이블 제약 조건을 식별 합니다. (중간 수준)<br/>SQL_ISV_TABLE_PRIVILEGES = 지정 된 사용자가 사용 하거나 허용 하는 영구 테이블에 대 한 권한을 식별 합니다. (FIPS 전환 수준)<br/>SQL_ISV_TABLES = 지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 영구 테이블을 식별 합니다. (FIPS 전환 수준)<br/>SQL_ISV_TRANSLATIONS = 지정 된 사용자가 액세스할 수 있는 카탈로그의 문자 변환을 식별 합니다. (전체 수준)<br/>SQL_ISV_USAGE_PRIVILEGES = 지정 된 사용자가 사용할 수 있거나 소유 하 고 있는 카탈로그 개체에 대 한 사용 권한을 식별 합니다. (FIPS 전환 수준)<br/>SQL_ISV_VIEW_COLUMN_USAGE = 지정 된 사용자가 소유 하는 카탈로그 뷰가 종속 되는 열을 식별 합니다. (중간 수준)<br/>SQL_ISV_VIEW_TABLE_USAGE = 지정 된 사용자가 소유 하 고 있는 카탈로그의 뷰가 종속 된 테이블을 식별 합니다. (중간 수준)<br/>SQL_ISV_VIEWS = 지정 된 사용자가 액세스할 수 있는이 카탈로그에서 정의 된 표시 된 테이블을 식별 합니다. (FIPS 전환 수준)|
|SQL_INSERT_STATEMENT|3.0|**INSERT** 문에 대 한 지원을 나타내는 SQLUINTEGER 비트 마스크입니다.<br/>SQL_IS_INSERT_LITERALS<br/>SQL_IS_INSERT_SEARCHED<br/>SQL_IS_SELECT_INTO<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_INTEGRITY|1.0|문자열: 데이터 원본이 무결성 향상 기능을 지 원하는 경우 "Y"입니다. 그렇지 않으면 "N"입니다.<br/><br/>Odbc 2.0 *InfoType* SQL_ODBC_SQL_OPT_IEF에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_KEYSET_CURSOR_ATTRIBUTES1|3.0|드라이버에서 지원 되는 키 집합 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 첫 번째 하위 집합을 포함 합니다. 두 번째 하위 집합은 SQL_KEYSET_CURSOR_ATTRIBUTES2를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1를 참조 하 고 "동적 커서"의 경우 "동적 커서"로 대체 합니다.<br/><br/>드라이버가 포함 된 SQL FETCH 문을 통해 스크롤 가능 커서를 지원 하기 때문에 SQL-92 중간 수준 규격 드라이버는 일반적으로 지원 되는 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 반환 합니다. 이는 기본 SQL 지원을 직접 확인 하지 않으므로 스크롤 가능 커서는 SQL-92 중간 수준 규격 드라이버에 대해서도 지원 되지 않을 수 있습니다.|
|SQL_KEYSET_CURSOR_ATTRIBUTES2|3.0|드라이버에서 지원 되는 키 집합 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 두 번째 하위 집합을 포함 합니다. 첫 번째 하위 집합은 SQL_KEYSET_CURSOR_ATTRIBUTES1를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1를 참조 하 고 "동적 커서"의 경우 "동적 커서"로 대체 합니다.|
|SQL_KEYWORDS|2.0|모든 데이터 소스 관련 키워드의 쉼표로 구분 된 목록을 포함 하는 문자열입니다. 이 목록에는 데이터 원본 및 ODBC 모두에서 사용 하는 ODBC 또는 키워드에 해당 하는 키워드가 포함 되어 있지 않습니다. 이 목록은 모든 예약 키워드를 나타냅니다. 상호 운용 가능한 응용 프로그램은 개체 이름에 이러한 단어를 사용 하면 안 됩니다.<br/><br/>ODBC 키워드 목록은 [부록 C: SQL 문법](../appendixes/appendix-c-sql-grammar.md)의 [예약 키워드](../appendixes/reserved-keywords.md) 를 참조 하세요. **#Define** 값 SQL_ODBC_KEYWORDS은 쉼표로 구분 된 ODBC 키워드 목록을 포함 합니다.|
|SQL_LIKE_ESCAPE_CLAUSE|2.0|문자열: "Y": 데이터 소스에서 백분율 문자 (%)의 이스케이프 문자를 지 원하는 경우 **like** 조건자의 밑줄 문자 (_) 및 드라이버는 **like** 조건자 이스케이프 문자를 정의 하기 위한 ODBC 구문을 지원 합니다. 그렇지 않으면 "N"입니다.|
|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|3.0|지정 된 연결에서 드라이버가 지원할 수 있는 비동기 모드의 최대 활성 동시 문 수를 지정 하는 SQLUINTEGER 값입니다. 특정 제한이 없거나 제한을 알 수 없으면이 값은 0입니다.|
|SQL_MAX_BINARY_LITERAL_LEN|2.0|SQL 문에서 이진 리터럴의 최대 길이 ( **SQLGetTypeInfo**에서 반환 된 리터럴 접두사 및 접미사 제외)를 지정 하는 SQLUINTEGER 값입니다. 예를 들어 이진 리터럴 0xFFAA의 길이는 4입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.|
|SQL_MAX_CATALOG_NAME_LEN|1.0|데이터 원본에 있는 카탈로그 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.<br/><br/>FIPS 전체 수준 준수 드라이버는 최소 128을 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_MAX_CHAR_LITERAL_LEN|2.0|SQL 문에서 문자 리터럴의 최대 길이 ( **SQLGetTypeInfo**에서 반환 된 리터럴 접두사 및 접미사를 제외한 문자 수)를 지정 하는 SQLUINTEGER 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.|
|SQL_MAX_COLUMN_NAME_LEN|1.0|데이터 원본에 있는 열 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 18 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 128을 반환 합니다.|
|SQL_MAX_COLUMNS_IN_GROUP_BY|2.0|**GROUP by** 절에 허용 되는 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 6 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 15를 반환 합니다.|
|SQL_MAX_COLUMNS_IN_INDEX|2.0|인덱스에 허용 되는 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.|
|SQL_MAX_COLUMNS_IN_ORDER_BY|2.0|**ORDER by** 절에 허용 되는 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 6 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 15를 반환 합니다.|
|SQL_MAX_COLUMNS_IN_SELECT|2.0|Select 목록에 허용 되는 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 100을 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 250을 반환 합니다.|
|SQL_MAX_COLUMNS_IN_TABLE|2.0|테이블에 허용 되는 최대 열 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 100을 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 250을 반환 합니다.|
|SQL_MAX_CONCURRENT_ACTIVITIES|1.0|드라이버가 연결에 대해 지원할 수 있는 최대 활성 문 수를 지정 하는 SQLUSMALLINT 값입니다. 문은 결과가 보류 중인 경우 활성으로 정의 되 고 "결과" 라는 용어는 **삽입**, **업데이트**또는 **삭제** 작업 **의** 영향을 받는 행 (예: 행 개수) 또는 NEED_DATA 상태에 있는 행을 의미 합니다. 이 값은 드라이버 또는 데이터 원본에 의해 적용 되는 제한을 반영할 수 있습니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>Odbc 2.0 *InfoType* SQL_ACTIVE_STATEMENTS에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_MAX_CURSOR_NAME_LEN|1.0|데이터 원본에 있는 커서 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 18 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 128을 반환 합니다.|
|SQL_MAX_DRIVER_CONNECTIONS|1.0|드라이버가 환경에 대해 지원할 수 있는 최대 활성 연결 수를 지정 하는 SQLUSMALLINT 값입니다. 이 값은 드라이버 또는 데이터 원본에 의해 적용 되는 제한을 반영할 수 있습니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>Odbc 2.0 *InfoType* SQL_ACTIVE_CONNECTIONS에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_MAX_IDENTIFIER_LEN|3.0|데이터 원본이 사용자 정의 이름에 대해 지 원하는 최대 크기 (문자 수)를 나타내는 SQLUSMALLINT입니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 18 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 128을 반환 합니다.|
|SQL_MAX_INDEX_SIZE|2.0|인덱스의 결합 된 필드에 허용 되는 최대 바이트 수를 지정 하는 SQLUINTEGER 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.|
|SQL_MAX_PROCEDURE_NAME_LEN|1.0|데이터 원본에서 프로시저 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.|
|SQL_MAX_ROW_SIZE|2.0|테이블의 단일 행에 대 한 최대 길이를 지정 하는 SQLUINTEGER 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 2000을 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 8000을 반환 합니다.|
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|3.0|문자열: "Y" SQL_MAX_ROW_SIZE 정보 형식에 대해 반환 되는 최대 행 크기가 행에 있는 모든 SQL_LONGVARCHAR 및 SQL_LONGVARBINARY 열의 길이를 포함 하는 경우 그렇지 않으면 "N"입니다.|
|SQL_MAX_SCHEMA_NAME_LEN|1.0|데이터 원본에서 스키마 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 18 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 128을 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_MAX_OWNER_NAME_LEN에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_MAX_STATEMENT_LEN|2.0|SQL 문의 최대 길이 (공백 포함)를 지정 하는 SQLUINTEGER 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.|
|SQL_MAX_TABLE_NAME_LEN|1.0|데이터 원본에 있는 테이블 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 18 개를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 128을 반환 합니다.|
|SQL_MAX_TABLES_IN_SELECT|2.0|**SELECT** 문의 **FROM** 절에 허용 되는 최대 테이블 수를 지정 하는 SQLUSMALLINT 값입니다. 지정 된 제한이 없거나 제한을 알 수 없으면이 값은 0으로 설정 됩니다.<br/><br/>FIPS 항목 수준 준수 드라이버는 최소 15를 반환 합니다. FIPS 중간 수준 규격 드라이버는 최소 50을 반환 합니다.|
|SQL_MAX_USER_NAME_LEN|2.0|데이터 원본에 있는 사용자 이름의 최대 길이를 지정 하는 SQLUSMALLINT 값입니다. 최대 길이가 없거나 길이를 알 수 없는 경우이 값은 0으로 설정 됩니다.|
|SQL_MULT_RESULT_SETS|1.0|문자열은 "Y" (데이터 원본이 여러 결과 집합을 지 원하는 경우)이 고, 그렇지 않으면 "N"입니다.<br/><br/>여러 결과 집합에 대 한 자세한 내용은 [여러 결과](../develop-app/multiple-results.md)를 참조 하세요.|
|SQL_MULTIPLE_ACTIVE_TXN|1.0|문자열이 한 번에 둘 이상의 활성 트랜잭션을 지원 하는 경우 "Y", "N"은 한 번에 하나의 트랜잭션만 활성화할 수 있습니다.<br/><br/>이 정보 형식에 대해 반환 되는 정보는 분산 트랜잭션의 경우에는 적용 되지 않습니다.|
|SQL_NEED_LONG_DATA_LEN|2.0|문자열은 "Y"로, 데이터 원본에 값이 데이터 원본에 전송 되기 전에 데이터 형식에 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 관련 데이터 형식)가 필요한 경우 해당 값이 데이터 원본에 전송 되기 전에 "N"입니다. 자세한 내용은 [SQLBindParameter 함수](sqlbindparameter-function.md) 및 [SQLSetPos 함수](sqlsetpos-function.md)를 참조 하세요.|
|SQL_NON_NULLABLE_COLUMNS|1.0|데이터 원본이 열에서 NOT NULL을 지원 하는지 여부를 지정 하는 SQLUSMALLINT 값입니다.<br/>SQL_NNC_NULL = 모든 열은 null을 허용 해야 합니다.<br/>SQL_NNC_NON_NULL = 열은 null을 허용 하지 않습니다. 데이터 원본은 **CREATE TABLE** 문에서 **not NULL** 열 제약 조건을 지원 합니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 SQL_NNC_NON_NULL 반환 합니다.|
|SQL_NULL_COLLATION|2.0|결과 집합에서 Null이 정렬 되는 위치를 지정 하는 SQLUSMALLINT 값입니다.<br/>SQL_NC_END = Null은 ASC 또는 DESC 키워드에 관계 없이 결과 집합의 끝에 정렬 됩니다.<br/>SQL_NC_HIGH = Null은 ASC 또는 DESC 키워드에 따라 결과 집합의 상위 쪽에서 정렬 됩니다.<br/>SQL_NC_LOW = Null은 ASC 또는 DESC 키워드에 따라 결과 집합의 하위 끝에 정렬 됩니다.<br/>SQL_NC_START = Null은 ASC 또는 DESC 키워드에 관계 없이 결과 집합의 시작 부분에서 정렬 됩니다.|
|SQL_NUMERIC_FUNCTIONS|1.0|참고: 정보 형식은 ODBC 1.0에서 도입 되었습니다. 각 비트 마스크는 도입 된 버전으로 레이블이 지정 됩니다.<br/><br/>드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 숫자 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 숫자 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_NUM_ABS (ODBC 1.0)<br/>SQL_FN_NUM_ACOS (ODBC 1.0)<br/>SQL_FN_NUM_ASIN (ODBC 1.0)<br/>SQL_FN_NUM_ATAN (ODBC 1.0)<br/>SQL_FN_NUM_ATAN2 (ODBC 1.0)<br/>SQL_FN_NUM_CEILING (ODBC 1.0)<br/>SQL_FN_NUM_COS (ODBC 1.0)<br/>SQL_FN_NUM_COT (ODBC 1.0)<br/>SQL_FN_NUM_DEGREES (ODBC 2.0)<br/>SQL_FN_NUM_EXP (ODBC 1.0)<br/>SQL_FN_NUM_FLOOR (ODBC 1.0)<br/>SQL_FN_NUM_LOG (ODBC 1.0)<br/>SQL_FN_NUM_LOG10 (ODBC 2.0)<br/>SQL_FN_NUM_MOD (ODBC 1.0)<br/>SQL_FN_NUM_PI (ODBC 1.0)<br/>SQL_FN_NUM_POWER (ODBC 2.0)<br/>SQL_FN_NUM_RADIANS (ODBC 2.0)<br/>SQL_FN_NUM_RAND (ODBC 1.0)<br/>SQL_FN_NUM_ROUND (ODBC 2.0)<br/>SQL_FN_NUM_SIGN (ODBC 1.0)<br/>SQL_FN_NUM_SIN (ODBC 1.0)<br/>SQL_FN_NUM_SQRT (ODBC 1.0)<br/>SQL_FN_NUM_TAN (ODBC 1.0)<br/>SQL_FN_NUM_TRUNCATE (ODBC 2.0)|
|SQL_ODBC_INTERFACE_CONFORMANCE|3.0|드라이버가 준수 하는 ODBC*3.x 인터페이스의* 수준을 나타내는 SQLUINTEGER 값입니다.<br/><br/>SQL_OIC_CORE: 모든 ODBC 드라이버가 준수 해야 하는 최소 수준입니다. 이 수준에는 연결 함수, SQL 문 준비 및 실행을 위한 함수, 기본 결과 집합 메타 데이터 함수, 기본 카탈로그 함수 등의 기본 인터페이스 요소가 포함 됩니다.<br/>SQL_OIC_LEVEL1: 코어 표준 준수 수준 기능과 스크롤 가능 커서, 책갈피, 위치 지정 업데이트 및 삭제 등을 비롯 한 수준입니다.<br/>SQL_OIC_LEVEL2: 수준 1 표준 준수 수준 기능 및 중요 한 커서와 같은 고급 기능을 포함 한 수준입니다. 책갈피를 통해 업데이트, 삭제 및 새로 고침 저장 프로시저 지원 기본 키 및 외래 키에 대 한 카탈로그 함수 다중 카탈로그 지원; 합니다.<br/><br/>자세한 내용은 [인터페이스 규칙 수준](../develop-app/interface-conformance-levels.md)을 참조 하세요.|
|SQL_ODBC_VER|1.0|드라이버 관리자가 준수 하는 ODBC 버전을 포함 하는 문자열입니다. 버전은 # #. # #. 0000 형식입니다. 여기서 처음 두 자리는 주 버전이 고 다음 두 자리는 부 버전입니다. 이는 드라이버 관리자 에서만 구현 됩니다.|
|SQL_OJ_CAPABILITIES|2.01|드라이버 및 데이터 원본에서 지 원하는 외부 조인 유형을 열거 하는 SQLUINTEGER 비트 마스크입니다. 지원 되는 형식을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_OJ_LEFT = 왼쪽 우선 외부 조인이 지원 됩니다.<br/>SQL_OJ_RIGHT = 오른쪽 우선 외부 조인이 지원 됩니다.<br/>SQL_OJ_FULL = 완전 외부 조인이 지원 됩니다.<br/>SQL_OJ_NESTED = 중첩 된 외부 조인이 지원 됩니다.<br/>SQL_OJ_NOT_ORDERED = outer join의 ON 절에 있는 열 이름은 **OUTER join** 절의 각 테이블 이름과 순서가 같을 필요가 없습니다.<br/>SQL_OJ_INNER = 내부 테이블 (왼쪽 우선 외부 조인의 오른쪽 테이블 또는 오른쪽 우선 외부 조인의 왼쪽 테이블)도 내부 조인에 사용할 수 있습니다. 이는 내부 테이블이 없는 완전 외부 조인에는 적용 되지 않습니다.<br/>SQL_OJ_ALL_COMPARISON_OPS = ON 절의 비교 연산자는 ODBC 비교 연산자 중 하나일 수 있습니다. 이 비트가 설정 되지 않은 경우에는 outer join에 equals (=) 비교 연산자만 사용할 수 있습니다.<br/><br/>이러한 옵션이 지원 되지 않는 것으로 반환 되 면 outer join 절은 지원 되지 않습니다.<br/><br/>SELECT 92 문에서 관계형 조인 연산자를 지 원하는 방법에 대 한 자세한 내용은 SQL_SQL92_RELATIONAL_JOIN_OPERATORS를 참조 하십시오.|
|SQL_ORDER_BY_COLUMNS_IN_SELECT|2.0|문자열은 **ORDER BY** 절의 열이 select 목록에 있어야 하는 경우 "Y"입니다. 그렇지 않으면 "N"입니다.|
|SQL_PARAM_ARRAY_ROW_COUNTS|3.0|매개 변수가 있는 실행에서 행 개수에 대 한 사용 가능 여부와 관련 된 드라이버의 속성을 열거 하는 SQLUINTEGER입니다. 에는 다음 값이 있습니다.<br/>SQL_PARC_BATCH = 각 매개 변수 집합에 대해 개별 행 개수를 사용할 수 있습니다. 이는 배열의 각 매개 변수에 설정 된 SQL 문의 일괄 처리를 생성 하는 드라이버와 개념적으로 동일 합니다. SQL_PARAM_STATUS_PTR 설명자 필드를 사용 하 여 확장 오류 정보를 검색할 수 있습니다.<br/>SQL_PARC_NO_BATCH = 전체 매개 변수 배열에 대해 문을 실행 하 여 생성 되는 누적 행 수 인 행 개수는 하나만 사용할 수 있습니다. 이는 문을 전체 매개 변수 배열과 함께 하나의 원자 단위로 처리 하는 것과 개념적으로 동일 합니다. 오류는 한 문이 실행 된 것과 동일 하 게 처리 됩니다.|
|SQL_PARAM_ARRAY_SELECTS|3.0|매개 변수가 있는 실행에서 결과 집합의 가용성과 관련 된 드라이버의 속성을 열거 하는 SQLUINTEGER입니다. 에는 다음 값이 있습니다.<br/>SQL_PAS_BATCH = 매개 변수 집합 마다 하나의 결과 집합을 사용할 수 있습니다. 이는 배열의 각 매개 변수에 설정 된 SQL 문의 일괄 처리를 생성 하는 드라이버와 개념적으로 동일 합니다.<br/>SQL_PAS_NO_BATCH = 전체 매개 변수 배열에 대해 문을 실행 하 여 생성 되는 누적 결과 집합을 나타내는 하나의 결과 집합만 사용할 수 있습니다. 이는 문을 전체 매개 변수 배열과 함께 하나의 원자 단위로 처리 하는 것과 개념적으로 동일 합니다.<br/>SQL_PAS_NO_SELECT = 드라이버는 매개 변수 배열을 사용 하 여 결과 집합을 생성 하는 문을 실행할 수 없습니다.|
|SQL_POS_OPERATIONS|2.0|**SQLSetPos**의 지원 작업을 열거 하는 sqlinteger 비트 마스크입니다.<br/><br/>다음 비트 마스크는 플래그와 함께 사용 되어 지원 되는 옵션을 결정 합니다.<br/>SQL_POS_POSITION (ODBC 2.0)<br/>SQL_POS_REFRESH (ODBC 2.0)<br/>SQL_POS_UPDATE (ODBC 2.0)<br/>SQL_POS_DELETE (ODBC 2.0)<br/>SQL_POS_ADD (ODBC 2.0)|
|SQL_PROCEDURE_TERM|1.0|프로시저에 대 한 데이터 원본 공급 업체의 이름을 포함 하는 문자열입니다. 예: "데이터베이스 프로시저", "저장 프로시저", "프로시저", "패키지" 또는 "저장 된 쿼리"|
|SQL_PROCEDURES|1.0|문자열: "Y": 데이터 원본이 프로시저를 지원 하 고 드라이버에서 ODBC 프로시저 호출 구문을 지 원하는 경우 그렇지 않으면 "N"입니다.|
|SQL_QUOTED_IDENTIFIER_CASE|2.0|SQLUSMALLINT 값은 다음과 같습니다.<br/>SQL_IC_UPPER = SQL의 따옴표 붙은 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에 대문자로 저장 됩니다.<br/>SQL_IC_LOWER = SQL의 따옴표 붙은 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에 소문자로 저장 됩니다.<br/>SQL_IC_SENSITIVE = SQL의 따옴표 붙은 식별자는 대/소문자를 구분 하며 시스템 카탈로그에서 대/소문자를 구분 하 여 저장 됩니다. (SQL-92 호환 데이터베이스에서는 따옴표 붙은 식별자는 항상 대/소문자를 구분 합니다.)<br/>SQL_IC_MIXED = SQL의 따옴표 붙은 식별자는 대/소문자를 구분 하지 않으며 시스템 카탈로그에서 대/소문자를 구분 하 여 저장 됩니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 SQL_IC_SENSITIVE 반환 합니다.|
|SQL_ROW_UPDATES|1.0|문자열: "Y"는 키 집합 또는 혼합 된 모든 행에 대해 행 버전이 나 값을 유지 관리 하므로 행이 마지막으로 인출 된 이후에 사용자가 행에 적용 한 모든 업데이트를 검색할 수 있습니다. 이는 업데이트에만 적용 되 고 삭제 나 삽입에는 적용 되지 않습니다. **Sqlfetchscroll** 을 호출 하면 드라이버에서 행 상태 배열에 SQL_ROW_UPDATED 플래그를 반환할 수 있습니다. 그렇지 않으면 "N"입니다.|
|SQL_SCHEMA_TERM|1.0|스키마에 대 한 데이터 원본 공급 업체의 이름을 포함 하는 문자열입니다. 예를 들면 "owner", "Authorization ID" 또는 "Schema"입니다.<br/><br/>문자열은 대문자, 소문자 또는 대/소문자를 구분 하 여 반환할 수 있습니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 "schema"를 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_OWNER_TERM에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_SCHEMA_USAGE|2.0|스키마를 사용할 수 있는 문을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/>SQL_SU_DML_STATEMENTS = 모든 데이터 조작 언어 문에서 스키마가 지원 됩니다. **select**, **INSERT**, **UPDATE**, DELETE, 지원 되는 경우 update 및 DELETE 문에 **대해 select** , INSERT, update, **delete**및 select를 선택 합니다.<br/>SQL_SU_PROCEDURE_INVOCATION = 스키마는 ODBC 프로시저 호출 문에서 지원 됩니다.<br/>SQL_SU_TABLE_DEFINITION = 스키마는 **CREATE TABLE**, **CREATE VIEW**, **ALTER Table**, **drop table**및 **drop view**와 같은 모든 테이블 정의 문에서 지원 됩니다.<br/>SQL_SU_INDEX_DEFINITION = 모든 인덱스 정의 문에서 **CREATE INDEX** 및 **DROP INDEX**스키마가 지원 됩니다.<br/>SQL_SU_PRIVILEGE_DEFINITION = 스키마는 **GRANT** 및 **REVOKE**의 모든 권한 정의 문에서 지원 됩니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION 및 SQL_SU_PRIVILEGE_DEFINITION 옵션을 반환 합니다.<br/><br/>Odbc 2.0 *InfoType* SQL_OWNER_USAGE에서 odbc 3.0에 대 한이 *InfoType* 이름이 변경 되었습니다.|
|SQL_SCROLL_OPTIONS|1.0|참고: 정보 형식은 ODBC 1.0에서 도입 되었습니다. 각 비트 마스크는 도입 된 버전으로 레이블이 지정 됩니다.<br/><br/>스크롤할 때 커서에 대해 지원 되는 스크롤 옵션을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 옵션을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_SO_FORWARD_ONLY = 커서는 앞 으로만 스크롤됩니다. (ODBC 1.0)<br/>SQL_SO_STATIC = 결과 집합의 데이터가 정적입니다. (ODBC 2.0)<br/>SQL_SO_KEYSET_DRIVEN = 드라이버는 결과 집합의 모든 행에 대 한 키를 저장 하 고 사용 합니다. (ODBC 1.0)<br/>SQL_SO_DYNAMIC = 드라이버는 행 집합의 모든 행에 대 한 키를 유지 합니다. 키 집합 크기는 행 집합 크기와 같습니다. (ODBC 1.0)<br/>SQL_SO_MIXED = 드라이버는 키 집합의 모든 행에 대 한 키를 유지 하 고 키 집합 크기는 행 집합 크기 보다 큽니다. 커서는 키 집합 내에서 키 집합을 기반으로 하 고 키 집합 외부에서 동적입니다. (ODBC 1.0)<br/><br/>스크롤할 때 커서에 대 한 자세한 내용은 [스크롤 가능 커서](../develop-app/scrollable-cursors.md)를 참조 하세요.|
|SQL_SEARCH_PATTERN_ESCAPE|1.0|드라이버가 지 원하는 문자를 지정 하는 문자열입니다 .이 문자열은 패턴 일치 문자 (_) 및 백분율 기호 (%)를 사용할 수 있습니다. 검색 패턴에서 유효한 문자로 이 이스케이프 문자는 검색 문자열을 지 원하는 카탈로그 함수 인수에 대해서만 적용 됩니다. 이 문자열이 비어 있으면 드라이버에서 검색 패턴 이스케이프 문자를 지원 하지 않습니다.<br/><br/>이 정보 유형은 **LIKE** 조건자의 이스케이프 문자에 대 한 일반 지원을 나타내지 않으므로 SQL-92에는이 문자열에 대 한 요구 사항이 포함 되지 않습니다.<br/><br/>이 *InfoType* 카탈로그 함수로 제한 됩니다. 검색 패턴 문자열에 이스케이프 문자를 사용 하는 방법에 대 한 설명은 [패턴 값 인수](../develop-app/pattern-value-arguments.md)를 참조 하세요.|
|SQL_SERVER_NAME|1.0|실제 데이터 원본 관련 서버 이름을 포함 하는 문자열입니다. **SQLConnect**, **SQLDriverConnect**및 **SQLBrowseConnect**중에 데이터 소스 이름을 사용 하는 경우에 유용 합니다.|
|SQL_SPECIAL_CHARACTERS|2.0|데이터 원본에서 테이블 이름, 열 이름, 인덱스 이름 등의 식별자 이름에 사용할 수 있는 모든 특수 문자 (즉, a-z, a-z, 0 ~ 9 및 밑줄을 제외한 모든 문자)를 포함 하는 문자열입니다. 예를 들면 "# $ ^"입니다. 식별자에 이러한 문자를 하나 이상 포함 하는 경우 식별자는 구분 식별자 여야 합니다.|
|SQL_SQL_CONFORMANCE|3.0|드라이버에서 지원 되는 SQL-92의 수준을 나타내는 SQLUINTEGER 값입니다.<br/>SQL_SC_SQL92_ENTRY = 92 규격 항목 수준입니다.<br/>SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 전환 수준 규격.<br/>SQL_SC_SQL92_FULL = 전체 수준 SQL-92 규격.<br/>SQL_SC_ SQL92_INTERMEDIATE = 중간 수준 SQL-92 호환|
|SQL_SQL92_DATETIME_FUNCTIONS|3.0|92에 정의 된 대로 드라이버 및 연결 된 데이터 원본에서 지원 되는 datetime 스칼라 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 datetime 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_SDF_CURRENT_DATE<br/>SQL_SDF_CURRENT_TIME<br/>SQL_SDF_CURRENT_TIMESTAMP|
|SQL_SQL92_FOREIGN_KEY_DELETE_RULE|3.0|SQLUINTEGER 92에 정의 된 대로 **DELETE** 문에서 외래 키에 대해 지원 되는 규칙을 열거 하는 비트 마스크입니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 절을 확인 하는 데 사용 됩니다.<br/>SQL_SFKD_CASCADE<br/>SQL_SFKD_NO_ACTION<br/>SQL_SFKD_SET_DEFAULT<br/>SQL_SFKD_SET_NULL<br/><br/>FIPS 전환 수준 준수 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_SQL92_FOREIGN_KEY_UPDATE_RULE|3.0|SQL-92에 정의 된 대로 **UPDATE** 문에서 외래 키에 대해 지원 되는 규칙을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 절을 확인 하는 데 사용 됩니다.<br/>SQL_SFKU_CASCADE<br/>SQL_SFKU_NO_ACTION<br/>SQL_SFKU_SET_DEFAULT<br/>SQL_SFKU_SET_NULL<br/><br/>SQL-92 전체 수준 규격 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_SQL92_GRANT|3.0|SQL-92에 정의 된 것 처럼 **GRANT** 문에서 지원 되는 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 절을 확인 하는 데 사용 됩니다.<br/>SQL_SG_DELETE_TABLE (항목 수준)<br/>SQL_SG_INSERT_COLUMN (중간 수준)<br/>SQL_SG_INSERT_TABLE (항목 수준)<br/>SQL_SG_REFERENCES_TABLE (항목 수준)<br/>SQL_SG_REFERENCES_COLUMN (항목 수준)<br/>SQL_SG_SELECT_TABLE (항목 수준)<br/>SQL_SG_UPDATE_COLUMN (항목 수준)<br/>SQL_SG_UPDATE_TABLE (항목 수준)<br/>SQL_SG_USAGE_ON_DOMAIN (FIPS 전환 수준)<br/>SQL_SG_USAGE_ON_CHARACTER_SET (FIPS 전환 수준)<br/>SQL_SG_USAGE_ON_COLLATION (FIPS 전환 수준)<br/>SQL_SG_USAGE_ON_TRANSLATION (FIPS 전환 수준)<br/>SQL_SG_WITH_GRANT_OPTION (항목 수준)|
|SQL_SQL92_NUMERIC_VALUE_FUNCTIONS|3.0|92에 정의 된 대로 드라이버 및 연결 된 데이터 원본에서 지원 되는 숫자 값 스칼라 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 숫자 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_SNVF_BIT_LENGTH<br/>SQL_SNVF_CHAR_LENGTH<br/>SQL_SNVF_CHARACTER_LENGTH<br/>SQL_SNVF_EXTRACT<br/>SQL_SNVF_OCTET_LENGTH<br/>SQL_SNVF_POSITION|
|SQL_SQL92_PREDICATES|3.0|SQL-92에 정의 된 대로 **SELECT** 문에서 지원 되는 조건자를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 옵션을 확인 하는 데 사용 됩니다.<br/>SQL_SP_BETWEEN (항목 수준)<br/>SQL_SP_COMPARISON (항목 수준)<br/>SQL_SP_EXISTS (항목 수준)<br/>SQL_SP_IN (항목 수준)<br/>SQL_SP_ISNOTNULL (항목 수준)<br/>SQL_SP_ISNULL (항목 수준)<br/>SQL_SP_LIKE (항목 수준)<br/>SQL_SP_MATCH_FULL (전체 수준)<br/>SQL_SP_MATCH_PARTIAL (전체 수준)<br/>SQL_SP_MATCH_UNIQUE_FULL (전체 수준)<br/>SQL_SP_MATCH_UNIQUE_PARTIAL (전체 수준)<br/>SQL_SP_OVERLAPS (FIPS 전환 수준)<br/>SQL_SP_QUANTIFIED_COMPARISON (항목 수준)<br/>SQL_SP_UNIQUE (항목 수준)|
|SQL_SQL92_RELATIONAL_JOIN_OPERATORS|3.0|SQL-92에 정의 된 대로 **SELECT** 문에서 지원 되는 관계형 조인 연산자를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 옵션을 확인 하는 데 사용 됩니다.<br/>SQL_SRJO_CORRESPONDING_CLAUSE (중간 수준)<br/>SQL_SRJO_CROSS_JOIN (전체 수준)<br/>SQL_SRJO_EXCEPT_JOIN (중간 수준)<br/>SQL_SRJO_FULL_OUTER_JOIN (중간 수준)<br/>SQL_SRJO_INNER_JOIN (FIPS 전환 수준)<br/>SQL_SRJO_INTERSECT_JOIN (중간 수준)<br/>SQL_SRJO_LEFT_OUTER_JOIN (FIPS 전환 수준)<br/>SQL_SRJO_NATURAL_JOIN (FIPS 전환 수준)<br/>SQL_SRJO_RIGHT_OUTER_JOIN (FIPS 전환 수준)<br/>SQL_SRJO_UNION_JOIN (전체 수준)<br/><br/>SQL_SRJO_INNER_JOIN는 내부 조인 기능이 아니라 **내부 조인** 구문에 대 한 지원을 나타냅니다. **내부 조인** 구문은 FIPS 전환 이지만 내부 조인 기능에 대 한 지원은 **항목**입니다.|
|SQL_SQL92_REVOKE|3.0|데이터 원본에서 지원 되는 SQL-92에 정의 된 대로 **REVOKE** 문에서 지원 되는 절을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 절을 확인 하는 데 사용 됩니다.<br/>SQL_SR_CASCADE (FIPS 전환 수준)<br/>SQL_SR_DELETE_TABLE (항목 수준)<br/>SQL_SR_GRANT_OPTION_FOR (중간 수준)<br/>SQL_SR_INSERT_COLUMN (중간 수준)<br/>SQL_SR_INSERT_TABLE (항목 수준)<br/>SQL_SR_REFERENCES_COLUMN (항목 수준)<br/>SQL_SR_REFERENCES_TABLE (항목 수준)<br/>SQL_SR_RESTRICT (FIPS 전환 수준)<br/>SQL_SR_SELECT_TABLE (항목 수준)<br/>SQL_SR_UPDATE_COLUMN (항목 수준)<br/>SQL_SR_UPDATE_TABLE (항목 수준)<br/>SQL_SR_USAGE_ON_DOMAIN (FIPS 전환 수준)<br/>SQL_SR_USAGE_ON_CHARACTER_SET (FIPS 전환 수준)<br/>SQL_SR_USAGE_ON_COLLATION (FIPS 전환 수준)<br/>SQL_SR_USAGE_ON_TRANSLATION (FIPS 전환 수준)|
|SQL_SQL92_ROW_VALUE_CONSTRUCTOR|3.0|SQL-92에 정의 된 대로 **SELECT** 문에서 지원 되는 행 값 생성자 식을 열거 하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 데이터 원본에서 지원 되는 옵션을 확인 하는 데 사용 됩니다.<br/>SQL_SRVC_VALUE_EXPRESSION<br/>SQL_SRVC_NULL<br/>SQL_SRVC_DEFAULT<br/>SQL_SRVC_ROW_SUBQUERY|
|SQL_SQL92_STRING_FUNCTIONS|3.0|92에 정의 된 대로 드라이버 및 연결 된 데이터 원본에서 지원 되는 문자열 스칼라 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 문자열 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_SSF_CONVERT<br/>SQL_SSF_LOWERSQL_SSF_UPPER<br/>SQL_SSF_SUBSTRING<br/>SQL_SSF_TRANSLATE<br/>SQL_SSF_TRIM_BOTH<br/>SQL_SSF_TRIM_LEADING<br/>SQL_SSF_TRIM_TRAILING|
|SQL_SQL92_VALUE_EXPRESSIONS|3.0|SQL-92에 정의 된 대로 지원 되는 값 식을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>이 기능이 지원 되어야 하는 SQL-92 또는 FIPS 규칙 수준은 각 비트 마스크 옆의 괄호 안에 표시 됩니다.<br/><br/>다음 비트 마스크는 데이터 원본에서 지원 되는 옵션을 확인 하는 데 사용 됩니다.<br/>SQL_SVE_CASE (중간 수준)<br/>SQL_SVE_CAST (FIPS 전환 수준)<br/>SQL_SVE_COALESCE (중간 수준)<br/>SQL_SVE_NULLIF (중간 수준)|
|SQL_STANDARD_CLI_CONFORMANCE|3.0|드라이버가 준수 하는 CLI 표준 또는 표준을 열거 하는 SQLUINTEGER 비트 마스크입니다. 다음 비트 마스크는 드라이버가 준수 하는 수준을 결정 하는 데 사용 됩니다.<br/>SQL_SCC_XOPEN_CLI_VERSION1: 드라이버가 오픈 그룹 CLI 버전 1을 준수 합니다.<br/>SQL_SCC_ISO92_CLI: 드라이버가 ISO 92 CLI를 준수 합니다.|
|SQL_STATIC_CURSOR_ATTRIBUTES1|3.0|드라이버에서 지 원하는 정적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 첫 번째 하위 집합을 포함 합니다. 두 번째 하위 집합은 SQL_STATIC_CURSOR_ATTRIBUTES2를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 ()을 참조 하 고 "동적 커서"를 "동적 커서"로 대체 합니다.<br/><br/>드라이버가 포함 된 SQL FETCH 문을 통해 스크롤 가능 커서를 지원 하기 때문에 SQL-92 중간 수준 규격 드라이버는 일반적으로 지원 되는 SQL_CA1_NEXT, SQL_CA1_ABSOLUTE 및 SQL_CA1_RELATIVE 옵션을 반환 합니다. 이는 기본 SQL 지원을 직접 확인 하지 않으므로 스크롤 가능 커서는 SQL-92 중간 수준 규격 드라이버에 대해서도 지원 되지 않을 수 있습니다.|
|SQL_STATIC_CURSOR_ATTRIBUTES2|3.0|드라이버에서 지 원하는 정적 커서의 특성을 설명 하는 SQLUINTEGER 비트 마스크입니다. 이 비트 마스크는 특성의 두 번째 하위 집합을 포함 합니다. 첫 번째 하위 집합은 SQL_STATIC_CURSOR_ATTRIBUTES1를 참조 하세요.<br/><br/>지원 되는 특성을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>이러한 비트 마스크에 대 한 설명은 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 ()을 참조 하 고 "동적 커서"를 "동적 커서"로 대체 합니다.|
|SQL_STRING_FUNCTIONS|1.0|참고: 정보 형식은 ODBC 1.0에서 도입 되었습니다. 각 비트 마스크는 도입 된 버전으로 레이블이 지정 됩니다.<br/><br/>드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 문자열 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 문자열 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_STR_ASCII (ODBC 1.0)<br/>SQL_FN_STR_BIT_LENGTH (ODBC 3.0)<br/>SQL_FN_STR_CHAR (ODBC 1.0)<br/>SQL_FN_STR_CHAR_LENGTH (ODBC 3.0)<br/>SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0)<br/>SQL_FN_STR_CONCAT (ODBC 1.0)<br/>SQL_FN_STR_DIFFERENCE (ODBC 2.0)<br/>SQL_FN_STR_INSERT (ODBC 1.0)<br/>SQL_FN_STR_LCASE (ODBC 1.0)<br/>SQL_FN_STR_LEFT (ODBC 1.0)<br/>SQL_FN_STR_LENGTH (ODBC 1.0)<br/>SQL_FN_STR_LOCATE (ODBC 1.0)<br/>SQL_FN_STR_LTRIM (ODBC 1.0)<br/>SQL_FN_STR_OCTET_LENGTH (ODBC 3.0)<br/>SQL_FN_STR_POSITION (ODBC 3.0)<br/>SQL_FN_STR_REPEAT (ODBC 1.0)<br/>SQL_FN_STR_REPLACE (ODBC 1.0)<br/>SQL_FN_STR_RIGHT (ODBC 1.0)<br/>SQL_FN_STR_RTRIM (ODBC 1.0)<br/>SQL_FN_STR_SOUNDEX (ODBC 2.0)<br/>SQL_FN_STR_SPACE (ODBC 2.0)<br/>SQL_FN_STR_SUBSTRING (ODBC 1.0)<br/>SQL_FN_STR_UCASE (ODBC 1.0)<br/><br/>응용 프로그램에서 *string_exp1*, *string_exp2*및 *시작* 인수를 사용 하 여 **찾기** 스칼라 함수를 호출할 수 있는 경우 드라이버는 SQL_FN_STR_LOCATE 비트 마스크를 반환 합니다. 응용 프로그램에서 *string_exp1* 및 *string_exp2* 인수만 사용 하 여 찾기 스칼라 함수를 호출할 수 있는 경우 드라이버는 SQL_FN_STR_LOCATE_2 비트 마스크를 반환 합니다. **찾기** 스칼라 함수를 완전히 지 원하는 드라이버는 두 비트 마스크를 모두 반환 합니다.<br/><br/>자세한 내용은 부록 E의 [문자열 함수](../appendixes/string-functions.md) , "스칼라 함수"를 참조 하십시오.|
|SQL_SUBQUERIES|2.0|하위 쿼리를 지 원하는 조건자를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/>SQL_SQ_CORRELATED_SUBQUERIES<br/>SQL_SQ_COMPARISON<br/>SQL_SQ_EXISTS<br/>SQL_SQ_INSQL_SQ_QUANTIFIED<br/><br/>SQL_SQ_CORRELATED_SUBQUERIES 비트 마스크는 하위 쿼리를 지 원하는 모든 조건자가 상관 관계 하위 쿼리를 지원 함을 나타냅니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 이러한 모든 비트가 설정 된 비트 마스크를 반환 합니다.|
|SQL_SYSTEM_FUNCTIONS|1.0|드라이버 및 연결 된 데이터 원본에서 지원 되는 스칼라 시스템 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 시스템 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_SYS_DBNAME<br/>SQL_FN_SYS_IFNULL<br/>SQL_FN_SYS_USERNAME|
|SQL_TABLE_TERM|1.0|테이블에 대 한 데이터 원본 공급 업체의 이름을 포함 하는 문자열입니다. 예를 들면 "table" 또는 "file"입니다.<br/><br/>이 문자열은 대문자, 소문자 또는 혼합 일 수 있습니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 "table"을 반환 합니다.|
|SQL_TIMEDATE_ADD_INTERVALS|2.0|TIMESTAMPADD 스칼라 함수에 대 한 드라이버 및 연결 된 데이터 원본에서 지원 되는 타임 스탬프 간격을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 간격을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>FIPS 전환 수준 규격 드라이버는 항상 이러한 모든 비트가 설정 된 비트 마스크를 반환 합니다.|
|SQL_TIMEDATE_DIFF_INTERVALS|2.0|TIMESTAMPDIFF 스칼라 함수에 대 한 드라이버 및 연결 된 데이터 원본에서 지원 되는 타임 스탬프 간격을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 간격을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>FIPS 전환 수준 규격 드라이버는 항상 이러한 모든 비트가 설정 된 비트 마스크를 반환 합니다.|
|SQL_TIMEDATE_FUNCTIONS|1.0|참고: 정보 형식은 ODBC 1.0에서 도입 되었습니다. 각 비트 마스크는 도입 된 버전으로 레이블이 지정 됩니다.<br/><br/>드라이버 및 연결 된 데이터 원본에서 지 원하는 스칼라 날짜 및 시간 함수를 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>지원 되는 날짜 및 시간 함수를 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br/>SQL_FN_TD_CURRENT_DATE (ODBC 3.0)<br/>SQL_FN_TD_CURRENT_TIME (ODBC 3.0)<br/>SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0)<br/>SQL_FN_TD_CURDATE (ODBC 1.0)<br/>SQL_FN_TD_CURTIME (ODBC 1.0)<br/>SQL_FN_TD_DAYNAME (ODBC 2.0)<br/>SQL_FN_TD_DAYOFMONTH (ODBC 1.0)<br/>SQL_FN_TD_DAYOFWEEK (ODBC 1.0)<br/>SQL_FN_TD_DAYOFYEAR (ODBC 1.0)<br/>SQL_FN_TD_EXTRACT (ODBC 3.0)<br/>SQL_FN_TD_HOUR (ODBC 1.0)<br/>SQL_FN_TD_MINUTE (ODBC 1.0)<br/>SQL_FN_TD_MONTH (ODBC 1.0)<br/>SQL_FN_TD_MONTHNAME (ODBC 2.0)<br/>SQL_FN_TD_NOW (ODBC 1.0)<br/>SQL_FN_TD_QUARTER (ODBC 1.0)<br/>SQL_FN_TD_SECOND (ODBC 1.0)<br/>SQL_FN_TD_TIMESTAMPADD (ODBC 2.0)<br/>SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0)<br/>SQL_FN_TD_WEEK (ODBC 1.0)<br/>SQL_FN_TD_YEAR (ODBC 1.0)|
|SQL_TXN_CAPABLE|1.0|참고: 정보 형식은 ODBC 1.0에서 도입 되었습니다. 각 반환 값에는 해당 값이 도입 된 버전으로 레이블이 지정 됩니다.<br/><br/>드라이버 또는 데이터 원본의 트랜잭션 지원을 설명 하는 SQLUSMALLINT 값입니다.<br/>SQL_TC_NONE = 지원 되지 않는 트랜잭션입니다. (ODBC 1.0)<br/>SQL_TC_DML = 트랜잭션은 DML (데이터 조작 언어) 문 (**SELECT**, **INSERT**, **UPDATE**, **DELETE**)만 포함할 수 있습니다. 트랜잭션에서 DDL (데이터 정의 언어) 문을 실행할 때 오류가 발생 했습니다. (ODBC 1.0)<br/>SQL_TC_DDL_COMMIT = 트랜잭션에는 DML 문만 포함 될 수 있습니다. 트랜잭션에서 DDL 문 (**CREATE TABLE**, **DROP INDEX**등)이 발생 하면 트랜잭션이 커밋됩니다. (ODBC 2.0)<br/>SQL_TC_DDL_IGNORE = 트랜잭션에는 DML 문만 포함 될 수 있습니다. 트랜잭션에서 발생 한 DDL 문은 무시 됩니다. (ODBC 2.0)<br/>SQL_TC_ALL = 트랜잭션은 모든 순서로 DDL 문 및 DML 문을 포함할 수 있습니다. (ODBC 1.0)<br/><br/>트랜잭션 지원은 SQL-92에서 필수 이며, SQL-92 준수 드라이버 [모든 수준]은 SQL_TC_NONE를 반환 하지 않습니다.)|
|SQL_TXN_ISOLATION_OPTION|1.0|드라이버 또는 데이터 원본에서 사용할 수 있는 트랜잭션 격리 수준을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/><br/>다음 비트 마스크는 플래그와 함께 사용 되어 지원 되는 옵션을 결정 합니다.<br/>SQL_TXN_READ_UNCOMMITTED<br/>SQL_TXN_READ_COMMITTED<br/>SQL_TXN_REPEATABLE_READ<br/>SQL_TXN_SERIALIZABLE<br/><br/>이러한 격리 수준에 대 한 설명은 SQL_DEFAULT_TXN_ISOLATION 설명을 참조 하세요.<br/><br/>트랜잭션 격리 수준을 설정 하기 위해 응용 프로그램은 **SQLSetConnectAttr** 를 호출 하 여 SQL_ATTR_TXN_ISOLATION 특성을 설정 합니다. 자세한 내용은 [SQLSetConnectAttr 함수](sqlsetconnectattr-function.md)를 참조 하세요.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 SQL_TXN_SERIALIZABLE 반환 합니다. FIPS 전환 수준 준수 드라이버는 항상 지원 되는 모든 옵션을 반환 합니다.|
|SQL_UNION|2.0|**UNION** 절에 대 한 지원을 열거 하는 SQLUINTEGER 비트 마스크입니다.<br/>SQL_U_UNION = 데이터 원본은 **UNION** 절을 지원 합니다.<br/>SQL_U_UNION_ALL = 데이터 원본은 **UNION** 절의 **ALL** 키워드를 지원 합니다. **SQLGetInfo** 는 SQL_U_UNION와 SQL_U_UNION_ALL를 모두 반환 합니다.<br/><br/>SQL-92 항목 수준 호환 드라이버는 항상 지원 되는 옵션을 모두 반환 합니다.|
|SQL_USER_NAME|1.0|특정 데이터베이스에 사용 되는 이름의 문자열로, 로그인 이름과 다를 수 있습니다.|
|SQL_XOPEN_CLI_YEAR|3.0|ODBC 드라이버 관리자의 버전이 완전히 준수 하는 개방형 그룹 사양의 게시 연도를 나타내는 문자열입니다.|
  
## <a name="example"></a>예제  

 **SQLGetInfo** 는 지원 되는 옵션 목록을 **InfoSQLUINTEGER EPTR*의 비트 마스크로 반환 합니다. 각 옵션에 대 한 비트 마스크는 플래그와 함께 사용 되어 옵션이 지원 되는지 여부를 결정 합니다.  
  
 예를 들어 응용 프로그램에서 다음 코드를 사용 하 여 연결에 연결 된 드라이버에서 SUBSTRING 스칼라 함수가 지원 되는지 여부를 확인할 수 있습니다.  
  
 **SQLGetInfo**를 사용 하는 또 다른 예는 [sqltables 함수](sqltables-function.md)를 참조 하세요.  
  
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
 [SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](sqlgetconnectattr-function.md)  
  
 드라이버에서 함수를 지원 하는지 여부 확인  
 [SQLGetFunctions 함수](sqlgetfunctions-function.md)  
  
 문 특성의 설정 반환  
 [SQLGetStmtAttr 함수](sqlgetstmtattr-function.md)  
  
 데이터 원본의 데이터 형식에 대 한 정보 반환  
 [SQLGetTypeInfo 함수](sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>참고 항목  

 [ODBC API 참조](odbc-api-reference.md)  
 [ODBC 헤더 파일](../install/odbc-header-files.md)
