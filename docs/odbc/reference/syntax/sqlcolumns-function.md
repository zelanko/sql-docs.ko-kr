---
title: SQLColumns 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d48fad8c874a9edda7da1afbe2f006726c39ee5b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923338"
---
# <a name="sqlcolumns-function"></a>SQLColumns 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: Open Group  
  
 **요약**  
 **SQLColumns** 지정 된 테이블의 열 이름 목록을 반환 합니다. 결과 집합으로 지정 된이 정보를 반환 하는 드라이버 *StatementHandle*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 경우 ("") 카탈로그를 갖지 않는 이러한 테이블을 나타냅니다. *CatalogName* string 검색 패턴을 포함할 수 없습니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *CatalogName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *CatalogName* 는 일반 인수 리터럴로 취급 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *schemaName*  
 [입력] 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버 일부 테이블에 대 한 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마가 없는 테이블을 나타냅니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *SchemaName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *SchemaName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *TableName*  
 [입력] 테이블 이름에 대 한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *TableName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *TableName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
 *ColumnName*  
 [입력] 열 이름에 대 한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *ColumnName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *ColumnName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength4*  
 [입력] 문자 길이 **ColumnName*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLColumns** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|에 커서가 열린는 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출한 합니다. 이 오류는 경우 드라이버 관리자에서 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 에 커서가 열린는 *StatementHandle* 하지만 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 합니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된는 *CatalogName* 인수는 null 포인터 되었으며는 SQL_CATALOG_NAME *정보 항목* 카탈로그 이름은 반환 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된 및 *SchemaName*, *TableName*, 또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLColumns** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 하지만 SQL_NTS과 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값을 해당 카탈로그 또는 이름에 대 한 최대 길이 값을 초과 했습니다. 호출 하 여 각 카탈로그 또는 이름의 최대 길이 가져올 수 있습니다 **SQLGetInfo** 와 *정보 항목* 값입니다. ("주석" 참조)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그 이름을 지정 하 고 드라이버 또는 데이터 원본 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름을 지정 하 고 드라이버 또는 데이터 원본의 스키마를 지원 하지 않습니다.<br /><br /> String 검색 패턴 스키마 이름, 테이블 이름 또는 열 이름에 대해 지정 된 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정의 조합 드라이버 또는 데이터 원본에서 지원 되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버 책갈피에 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 이 함수 일반적으로 사용 됩니다 문 실행 하기 전에 데이터 원본 카탈로그에서 테이블 또는 테이블에 대 한 열에 대 한 정보를 검색 합니다. **SQLColumns** 는 모든 유형의에서 반환 된 항목에 대 한 데이터를 검색 하는 데 사용할 수 **SQLTables**합니다. 기본 테이블 외에도이 포함 될 수 있습니다 (그러나에 국한 되지 않음) 뷰, 동의어, 시스템 테이블 및 등입니다. 이와 반대로 함수 **SQLColAttribute** 및 **SQLDescribeCol** 함수 및 결과 집합의 열을 설명 **SQLNumResultCols** 의 수를 반환 합니다. 결과 집합의 열입니다. 자세한 내용은 참조 [카탈로그 데이터의 사용 하 여](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
> [!NOTE]  
>  일반적으로 사용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 **SQLColumns** TABLE_CAT, table_schem 순으로 정렬, TABLE_NAME 및 ORDINAL_POSITION 순으로 정렬 하 여 표준 결과 집합으로 결과 반환 합니다.  
  
> [!NOTE]  
>  ODBC 2 연동 응용 프로그램입니다. *x* 드라이버 ORDINAL_POSITION 열은 결과 집합에 반환 됩니다. 결과적으로 ODBC 2를 사용 합니다. *x* 에서 반환 된 열 목록의 열 순서, 드라이버 **SQLColumns** 반드시 열 순서와 동일 하 게은 응용 프로그램이 모든 SELECT 문을 수행 하는 경우 해당 테이블의 열입니다.  
  
> [!NOTE]  
>  **SQLColumns** 모든 열을 반환할 수 없습니다. 예를 들어, 드라이버는 Oracle ROWID 등의 의사 (pseudo) 열에 대 한 정보를 반환 하지 수도 있습니다. 응용 프로그램에서 반환 되는 여부 유효한 모든 열을 사용할 수 **SQLColumns**합니다.  
>   
>  반환 될 수 있는 일부 열 **SQLStatistics** 는 반환 하지 **SQLColumns**합니다. 예를 들어 **SQLColumns** 식 또는 부서 또는 급여 + 이점 등의 필터를 통해 생성 된 인덱스에 열을 반환 하지 않는 0012 = 합니다.  
  
 VARCHAR 열의 길이; 테이블에 표시 되지 않습니다. 실제 길이 데이터 원본에 따라 달라 집니다. TABLE_CAT 및 table_schem 순으로 정렬, TABLE_NAME, COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 지정 합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다. *x*합니다. 열 이름 변경 응용 프로그램 열 번호에 의해 바인딩될 있기 때문에 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3입니다. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 다음 열에서 반환 된 결과 집합에 추가 된 **SQLColumns** ODBC 3. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 18 (IS_NULLABLE) 열 추가 열을 정의할 수 있습니다. 응용 프로그램 결과 명시적 서 수 위치를 지정 하는 대신 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 참조 [카탈로그 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열<br /><br /> number|데이터 형식|설명|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1.|Varchar|카탈로그 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버 카탈로그 일부 테이블을 지원 하지만 지원만, 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 카탈로그를 갖지 않는 이러한 테이블에 대 한 합니다.|  
|TABLE_SCHEM 순으로 정렬 (ODBC 1.0)|2|Varchar|스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 지 원하는 스키마만, 하지만 일부 테이블에 대 한 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 스키마가 없는 해당 테이블에 대 한 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|NULL이 아닌 Varchar|테이블 이름입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|NULL이 아닌 Varchar|열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|5|NULL이 아닌 Smallint|SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식이 나 드라이버별 SQL 데이터 형식과 수 있습니다. 날짜/시간 및 간격 데이터 형식의 경우이 열 간결 하 게 데이터 형식 (예: SQL_TYPE_DATE 또는 SQL_DATETIME 또는 sql_interval 인 같은 nonconcise 데이터 형식이 아닌 SQL_INTERVAL_YEAR_TO_MONTH)를 반환합니다. 목록이 유효한 ODBC SQL 데이터 형식에 대 한 참조 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.<br /><br /> ODBC 3에 대 한 반환 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램 다를 수 있습니다. 자세한 내용은 참조 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.|  
|TYPE_NAME (ODBC 1.0)|6|NULL이 아닌 Varchar|데이터 소스에 따라 다릅니다 데이터 형식 이름입니다. 예를 들어 "CHAR", "VARCHAR", "MONEY", "긴 VARBINAR" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 1.0)|7|정수|DATA_TYPE SQL_CHAR 또는 SQL_VARCHAR 이면이 열이 문자 열의 최대 길이 포함 합니다. Datetime 데이터 형식에 대 한 문자를 문자로 변환 될 때 값을 표시 하는 데 필요한 총 수입니다. 숫자 데이터 형식에 대 한이 전체 자릿수 또는 총 수는 열에 허용 되는 비트 NUM_PREC_RADIX 열에 따라 합니다. Interval 데이터 형식에 대 한 리터럴 간격의 문자 표시에 있는 문자의 수입니다 (전체 자릿수를 유도 하는 간격에 정의 된 대로 참조 [간격 데이터 형식의 길이가](../../../odbc/reference/appendixes/interval-data-type-length.md) 부록 d: 데이터 형식에). 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|BUFFER_LENGTH (ODBC 1.0)|8|정수|SQL_C_DEFAULT를 지정 하는 경우 데이터의 바이트 길이 SQLGetData, SQLFetch, 또는 SQLFetchScroll 작업에서 전송 합니다. 숫자 데이터에 대 한이 크기는 데이터 원본에 저장 된 데이터의 크기와에서 다를 수 있습니다. 이 값은 문자 데이터에 대 한 COLUMN_SIZE 열의에서 달라질 수 있습니다. 길이 대 한 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|소수점 오른쪽 자릿수의 총 수입니다. 이 열 SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP에 대 한 소수 자릿수 초 구성 요소에는 자릿수를 포함합니다. 다른 데이터 형식 열이 데이터 원본에의 10 진수입니다. 시간 구성 요소를 포함 하는 간격 데이터 형식의 경우이 열 (소수 자릿수 초) 소수점 오른쪽 자릿수를 포함 합니다. 시간 구성 요소를 포함 하지 않는 간격 데이터 형식의 경우이 열은 0입니다. 10 진수 숫자에 대 한 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다. DECIMAL_DIGITS 적용할 수 없는 데이터 형식에 대해 NULL이 반환 됩니다.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|숫자 데이터 형식에 대 한 10 또는 2입니다. 10 이면 COLUMN_SIZE 및 DECIMAL_DIGITS 값 수의 열에 허용 되는 소수 자릿수를 제공 합니다. 예를 들어 DECIMAL(12,5) 열 10, 12, COLUMN_SIZE 및 5; DECIMAL_DIGITS NUM_PREC_RADIX 반환 FLOAT 열에는 10, 15, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL의 NUM_PREC_RADIX 반환할 수 있습니다.<br /><br /> 2 이면에 있는 값 COLUMN_SIZE 및 DECIMAL_DIGITS 열의 허용 하는 비트 수를 제공 합니다. 예를 들어 FLOAT 열 2, 53, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL의 기 수를 반환할 수 있습니다.<br /><br /> NUM_PREC_RADIX 적용할 수 없는 데이터 형식에 대해 NULL이 반환 됩니다.|  
|NULL 허용 (ODBC 1.0)|11|NULL이 아닌 Smallint|열의 NULL 값을 포함 하지 못한 경우 SQL_NO_NULLS 합니다.<br /><br /> 열에 NULL 값을 사용할 경우 SQL_NULLABLE 합니다.<br /><br /> SQL_NULLABLE_UNKNOWN 경우 열이 NULL 값 허용 여부를 알 수 없습니다.<br /><br /> 이 열에 대해 반환 되는 값 IS_NULLABLE 열에 대해 반환 되는 값과에서 다릅니다. Null 허용 열은 열, Null을 허용할 수 있지만 열에서 Null을 허용 하지 않는 확실 하 게 나타낼 수 없습니다 확실 하 게 나타냅니다. IS_NULLABLE 열은 열, Null을 허용할 수 없습니다 있지만 열 Null을 허용 하는 확실 하 게 나타낼 수 없습니다 확실 하 게 나타냅니다.|  
|설명 (ODBC 1.0)|12|Varchar|열에 대 한 설명|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|열의 기본값입니다. 이 열의 값에에서는 따옴표에 포함 되어 있으면 문자열로 해석 해야 합니다.<br /><br /> NULL 값을 기본값으로 지정 된 경우이 열은 단어 NULL, 따옴표에 포함 되지 않습니다. 잘림 없이 기본값을 표현할 수 없는 경우이 열에 작은따옴표를 포함 하지 않고 잘림, 포함 되어 있습니다. 기본값이 사용 되지 않는 지정 된 경우이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값 잘림 값을 포함 하는 경우를 제외 하 고 새 열 정의 생성에 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|NULL이 아닌 Smallint|IRD의 SQL_DESC_TYPE 레코드 필드에 표시 된 대로 SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식이 나 드라이버별 SQL 데이터 형식과 수 있습니다. 이 열은 날짜/시간 및 간격 데이터 형식 제외 하 고는 DATA_TYPE 열과 동일 합니다. 이 열이 datetime에 대해 간결 하 게 데이터 형식 (예: SQL_TYPE_DATE 또는 SQL_INTERVAL_YEAR_TO_MONTH) 및 interval 데이터 형식을 대신 nonconcise 데이터 형식 (예: SQL_DATETIME 또는 sql_interval 인)를 반환합니다. 이 열 SQL_DATETIME 또는 sql_interval 인을 반환 하면 SQL_DATETIME_SUB 열에서 특정 데이터 형식이 확인할 수 있습니다. 목록이 유효한 ODBC SQL 데이터 형식에 대 한 참조 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.<br /><br /> ODBC 3에 대 한 반환 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램 다를 수 있습니다. 자세한 내용은 참조 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|날짜/시간 및 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다. 날짜/시간 및 간격 하위 코드에 대 한 자세한 내용은의 "값을 SQL_DESC_DATETIME_INTERVAL_CODE" 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|정수|문자 또는 이진 데이터의 최대 길이 (바이트)에서 열을 입력 합니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|17|NULL이 아닌 Integer|테이블에 있는 열의 서수 위치입니다. 테이블의 첫 번째 열은 숫자 1입니다.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"NO" 열에 null 값이 포함 되어 있지 않으면입니다.<br /><br /> "YES" 경우 열이 Null을 포함할 수 없습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 대해 반환 되는 값은 NULLABLE 열에 반환 되는 값에서 다릅니다. (Null 허용 열에 대 한 설명을 참조).|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램에서 반환 된 결과 집합에 대 한 버퍼 선언 **SQLColumns**합니다. 호출 **SQLColumns** EMPLOYEE 테이블의 각 열을 설명 하는 결과 집합을 반환 합니다. 그런 다음 연속 호출 **SQLBindCol** 결과 집합을 버퍼에에서 열을 바인딩할 수 있습니다. 응용 프로그램에서 사용 하 여 데이터의 각 행을 인출 하는 마지막으로, **SQLFetch** 를 처리 합니다.  
  
```  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|하나 이상의 열에 대 한 권한을 반환합니다.|[SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|트랜잭션에 의해 자동으로 업데이트 하는 열 또는 행을 고유 하 게 식별 하는 열을 반환 합니다.|[SQLSpecialColumns 함수](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|테이블 통계 및 인덱스를 반환합니다.|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|데이터 원본에서 테이블의 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
|테이블 또는 테이블에 대 한 권한을 반환합니다.|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
