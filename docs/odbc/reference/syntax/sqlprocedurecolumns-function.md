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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa5998d240b447b4204528af6c89e9c202e5963e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766541"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 함수(SQLProcedureColumns Function)
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLProcedureColumns** 결과 지정 된 프로시저에 대 한 집합을 구성 하는 열 뿐만 아니라 입력 및 출력 매개 변수 목록을 반환 합니다. 드라이버는 결과 집합으로 지정 된 문에 대 한 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 프로시저 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 프로시저의 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 해당 프로시저를 나타냅니다. *CatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *CatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *CatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 프로시저 스키마 이름에 대 한 검색 패턴을 문자열입니다. 드라이버를 일부 프로시저의 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 해당 프로시저를 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *SchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *SchemaName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *ProcName*  
 [입력] 프로시저 이름에 대 한 검색 패턴을 문자열입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *ProcName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *ProcName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **ProcName*합니다.  
  
 *ColumnName*  
 [입력] 열 이름에 대 한 검색 패턴을 문자열입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *ColumnName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *ColumnName* 패턴 값 인수를 사용 하는 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength4*  
 [입력] 문자 길이 **ColumnName*합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLProcedureColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLProcedureColumns** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 앞 드라이버에서 반환 된 Sqlstate 설명은 관리자입니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 하지 않은 한 경우 드라이버에서 반환 됩니다 **SQLFetch** 또는**SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLError** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *CatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목* 반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 하며 *SchemaName*를 *ProcName*, 또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. SQLProcedureColumns 함수 호출 되었을 때이 aynschronous 함수가 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.<br /><br /> 이름 길이 인수 중 하나의 값을는 해당 카탈로그, 스키마, 프로시저 또는 열 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|프로시저 카탈로그를 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 프로시저 스키마를 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.<br /><br /> 프로시저 스키마, 프로시저 이름 또는 열 이름에 대 한 지정 된 문자열 검색 패턴 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 대개 프로시저 매개 변수 및 있으면 프로시저에서 반환 된 집합을 결과 집합을 구성 하는 열에 대 한 정보를 검색할 문 실행 하기 전에 사용 됩니다. 자세한 내용은 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)합니다.  
  
> [!NOTE]  
>  **SQLProcedureColumns** 프로시저를 사용 하는 모든 열을 반환 하지 않을 수 있습니다. 예를 들어, 드라이버는 프로시저를 생성 하는 결과 집합의 열으로 사용 된 매개 변수에 대 한 유일한 정보를 반환할 수 있습니다.  
  
 합니다 *SchemaName*를 *ProcName*, 및 *ColumnName* 인수 검색 패턴을 허용 합니다. 올바른 검색 패턴에 대 한 자세한 내용은 참조 하세요. [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 **SQLProcedureColumns** PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME, 및 COLUMN_TYPE 정렬할 표준 결과 집합으로 결과 반환 합니다. 다음 순서 대로 각 프로시저에 대 한 열 이름을 반환 하는: 반환 값의 이름을, (호출 순서) 대로 프로시저 호출에서 각 매개 변수의 이름 및 열 순서 대로 프로시저가 반환한 결과 집합의 각 열 이름입니다.  
  
 응용 프로그램에는 결과 집합의 끝을 기준으로 드라이버 관련 열 바인딩해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME, 및 COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_를 사용 하 여 PROCEDURE_NAME_LEN, 및 SQL_MAX_COLUMN_NAME_LEN 옵션입니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다. *x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3입니다. *x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|프로시저 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 다음 열이 반환한 결과 집합에 추가 되었습니다 **SQLProcedureColumns** ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 19 (IS_NULLABLE) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 것이 아니라 결과 집합의 끝에서 카운트다운 여 드라이버별 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|프로시저 카탈로그 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 프로시저의 아니라 다른 다양 한 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 프로시저의 아니라 다른 다양 한 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|NULL이 아닌 Varchar|프로시저 이름입니다. 프로시저의 경우 이름 없는 빈 문자열이 반환 됩니다.|  
|COLUMN_NAME (ODBC 2.0)|4|NULL이 아닌 Varchar|프로시저 열 이름입니다. 드라이버 이름 없는 프로시저 열에 대해 빈 문자열을 반환 합니다.|  
|COLUMN_TYPE (ODBC 2.0)|5|NULL이 아닌 Smallint|매개 변수로 프로시저 열 또는 결과 집합 열을 정의합니다.<br /><br /> SQL_PARAM_TYPE_UNKNOWN: 프로시저 열은 형식이 알려지지 않은 매개 변수입니다. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT: 프로시저 열 입력된 매개 변수입니다. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: 프로시저 열 입/출력 매개 변수입니다. ODBC (1.0)<br /><br /> SQL_PARAM_OUTPUT: 프로시저 열을 출력 매개 변수입니다. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: 프로시저 열이 프로시저의 반환 값입니다. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: 프로시저 열은 결과 집합 열. ODBC (1.0)|  
|DATA_TYPE (ODBC 2.0)|6|NULL이 아닌 Smallint|SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식 수 있습니다. 날짜/시간 및 간격 데이터 형식에 대해이 열에는 간결한 데이터 형식 (예: SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH) 반환합니다. 유효한 ODBC SQL 데이터 형식의 목록을 참조 하세요 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.|  
|TYPE_NAME (ODBC 2.0)|7|NULL이 아닌 Varchar|데이터 소스에 따라 다릅니다 데이터 형식 이름입니다. 예를 들어, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 2.0)|8|정수|데이터 원본에 프로시저 열의 열 크기를 지정 합니다. NULL 열 크기 적용할 수 없는 데이터 형식에 대해 반환 됩니다. 전체 자릿수와 관련 된 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|BUFFER_LENGTH (ODBC 2.0)|9|정수|전송 되는 데이터의 바이트 길이 **SQLGetData** 하거나 **SQLFetch** SQL_C_DEFAULT를 지정 하는 경우 작업 합니다. 숫자 데이터에 대 한이 크기는 데이터 원본에 저장 된 데이터의 크기 보다 다 수 있습니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), 부록 d: 데이터 형식에서입니다.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|프로시저 열 데이터 원본에서의 10 진수입니다. NULL이 반환 됩니다 데이터 형식의 소수 자릿수가 적용 되지 않습니다. 10 진수 숫자와 관련 된 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), 부록 d: 데이터 형식에서입니다.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|숫자 데이터 형식에 대 한 10 또는 2입니다.<br /><br /> 10 일 경우 COLUMN_SIZE 및 DECIMAL_DIGITS 값 열에 대해 허용 된 10 진수 자릿수를 제공 합니다. 예를 들어 DECIMAL(12,5) 열 10, 12, COLUMN_SIZE 및 5; DECIMAL_DIGITS NUM_PREC_RADIX 반환 FLOAT 열에는 10, 15, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL의 NUM_PREC_RADIX 반환할 수 있습니다.<br /><br /> 2 인 경우에 있는 값 COLUMN_SIZE 및 DECIMAL_DIGITS 열의 허용 하는 비트 수를 제공 합니다. 예를 들어, FLOAT 열에는 2, 53, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL NUM_PREC_RADIX 반환할 수 있습니다.<br /><br /> NULL은 NUM_PREC_RADIX 적용할 수 없는 데이터 형식에 대해 반환 됩니다.|  
|NULL을 허용 (ODBC 2.0)|12|NULL이 아닌 Smallint|여부 프로시저 열에 NULL 값을 허용 합니다.<br /><br /> SQL_NO_NULLS: 프로시저 열 NULL 값을 허용 하지 않습니다.<br /><br /> SQL_NULLABLE: 프로시저 열에 NULL 값 허용합니다.<br /><br /> SQL_NULLABLE_UNKNOWN: 프로시저 열에 NULL 값을 사용할 경우 알려지지 않습니다.|  
|설명 (ODBC 2.0)|13|Varchar|프로시저 열에 대 한 설명|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|열의 기본값입니다.<br /><br /> NULL 값을 기본값으로 지정 된 경우이 열은 NULL 이라는 단어를 따옴표로 묶여 있지. 기본값을 잘림 없이 표현할 수 없는 경우이 열 잘림, 없습니다 바깥쪽 작은따옴표를 사용 하 여 포함 합니다. 기본값이 지정 된 경우이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값 잘림 값이 포함 된 경우 제외 하 고 새 열 정의 생성할 때 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|NULL이 아닌 Smallint|설명자의 SQL_DESC_TYPE 필드에는 SQL 데이터 형식으로 값 표시 됩니다. 이 열은 datetime 및 interval 데이터 형식 제외 하 고는 DATA_TYPE 열과 동일 합니다.<br /><br /> 날짜/시간 및 간격 데이터 형식에 대 한 결과 집합의 SQL_DATA_TYPE 필드, SQL_DATETIME 또는 sql_interval 인 반환 하 고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜/시간 데이터 형식에 대 한 하위 코드를 반환 합니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|날짜/시간 및 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|정수|문자 또는 이진 데이터의 최대 길이 (바이트)에서 열을 입력 합니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|18|NULL이 아닌 Integer|입력 및 출력 매개 변수의 순서로 증가 매개 변수를 1부터 프로시저 정의에서 매개 변수의 서 수 위치입니다. 반환 값 (있는 경우), 0이 반환 됩니다. 결과 집합 열에 대 한 결과에서 열의 서 수 위치 설정, 결과 집합 중 첫 번째 열을 사용 하 여 번호가 1입니다. 여러 결과 집합의 경우 열 서 수 위치는 드라이버별 방식으로 반환 됩니다.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"아니요" 열에 Null이 포함 되어 있지 않으면입니다.<br /><br /> 면 "YES" 열이 Null을 포함할 수 있습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS는 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 반환되는 값은 NULLABLE 열에 반환되는 값과 다릅니다. (Null 허용 열에 대 한 설명을 참조).|  
  
## <a name="code-example"></a>코드 예  
 참조 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터 원본에서 프로시저의 목록 반환|[SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
