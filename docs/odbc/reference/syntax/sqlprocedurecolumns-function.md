---
title: "SQLProcedureColumns 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db80c3c1fbf8e4d22f09849c95dde4bc4319bedf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 함수(SQLProcedureColumns Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLProcedureColumns** 으로 입력 및 출력 매개 변수는 지정 된 프로시저의 결과 집합은 구성 하는 열 목록을 반환 합니다. 드라이버는 결과 집합으로 지정된 된 문에 대 한 정보를 반환 합니다.  
  
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
 [입력] 프로시저 카탈로그 이름입니다. 일부 프로시저 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 드라이버 카탈로그를 지원 하는 경우 ("")는 카탈로그를 갖지 않는 이러한 프로시저를 나타냅니다. *CatalogName* string 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *CatalogName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *CatalogName* 는 일반 인수 리터럴로 취급 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 프로시저 스키마 이름에 대 한 문자열 검색 패턴입니다. 드라이버는 일부 프로시저 있지만 대 한 드라이버 다른 Dbms, 빈 문자열에서에서 데이터를 검색 하는 경우 등의 다른 스키마에서 지 원하는 경우 ("") 스키마가 없는 이러한 프로시저를 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *SchemaName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *SchemaName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *ProcName*  
 [입력] 프로시저 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *ProcName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *ProcName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **ProcName*합니다.  
  
 *열 이름*  
 [입력] 열 이름에 대 한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성, SQL_TRUE로 설정 되어 있으면 *ColumnName* 식별자로 처리 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 이면 *ColumnName* 패턴 값 인수; 리터럴로 취급 됩니다이 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength4*  
 [입력] 문자 길이 **ColumnName*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLProcedureColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 여의 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLProcedureColumns** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버에 의해 반환 된 Sqlstate 설명 관리자입니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|에 커서가 열린는 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출한 합니다. 이 오류는 경우 드라이버 관리자에서 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 에 커서가 열린는 *StatementHandle*, 하지만 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 합니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLError** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된는 *CatalogName* 인수는 null 포인터 되었으며는 SQL_CATALOG_NAME *정보 항목* 카탈로그 이름은 반환 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이, SQL_TRUE로 설정 된 및 *SchemaName*, *ProcName*, 또는 *ColumnName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. SQLProcedureColumns 함수를 호출할 때이 aynschronous 함수 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서 * StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 하지만 SQL_NTS과 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값을 해당 카탈로그, 스키마, 프로시저 또는 열 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|프로시저 카탈로그를 지정 하 고 드라이버 또는 데이터 원본 카탈로그를 지원 하지 않습니다.<br /><br /> 프로시저 스키마가으로 지정 하 고 드라이버 또는 데이터 원본의 스키마를 지원 하지 않습니다.<br /><br /> String 검색 패턴 프로시저 스키마, 프로시저 이름, 또는 열 이름에 대해 지정 된 및 해당 인수 중 하나 이상에 대 한 데이터 원본 검색 패턴을 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정의 조합 드라이버 또는 데이터 원본에서 지원 되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버 책갈피에 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 소스 결과 집합을 반환 하기 전에 제한 시간을 초과 합니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 이 함수는 대개 프로시저 매개 변수 및 있는 경우 결과 집합 또는 프로시저에서 반환 된 집합을 구성 하는 열에 대 한 정보를 검색할 문 실행 하기 전에 사용 됩니다. 자세한 내용은 참조 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)합니다.  
  
> [!NOTE]  
>  **SQLProcedureColumns** 프로시저에서 사용 되는 모든 열을 반환할 수 없습니다. 예를 들어, 드라이버는 프로시저 및 생성 하는 결과 집합의 열에서 사용 하는 매개 변수에 대 한 유일한 정보를 반환할 수 있습니다.  
  
 *SchemaName*, *ProcName*, 및 *ColumnName* 인수 검색 패턴에 동의 합니다. 올바른 검색 패턴에 대 한 자세한 내용은 참조 [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)합니다.  
  
> [!NOTE]  
>  일반적으로 사용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 **SQLProcedureColumns** PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME, 및 COLUMN_TYPE 순으로 정렬 하 여 표준 결과 집합으로 결과 반환 합니다. 열 이름은 다음과 같은 순서로 각 절차에 대해 반환 됩니다: 반환 값의 이름은 프로시저 호출 (호출 순서)에 있는 각 매개 변수 이름 및 열 순서에 프로시저에서 반환 된 결과 집합에 있는 각 열의 이름입니다.  
  
 응용 프로그램 결과 집합의 끝을 기준으로 드라이버 관련 열을 바인딩해야 합니다. 자세한 내용은 참조 [카탈로그 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME, 및 COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_와 PROCEDURE_NAME_LEN, 및 SQL_MAX_COLUMN_NAME_LEN 옵션입니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다. *x*합니다. 열 이름 변경 응용 프로그램 열 번호에 의해 바인딩될 있기 때문에 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3입니다. *x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|프로시저 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 다음 열에서 반환 된 결과 집합에 추가 된 **SQLProcedureColumns** ODBC 3.* x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 19 (IS_NULLABLE) 열 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적는 서 수 위치를 지정 하지 않고 결과 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 참조 [카탈로그 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|설명|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1.|Varchar|프로시저 카탈로그 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버 카탈로그 일부 절차에 대 한 지원 하지만 지원만, 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 카탈로그를 갖지 않는 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 지 원하는 스키마만, 하지만 몇 가지 절차에 대 한 빈 문자열을 반환 다른 Dbms에서 데이터를 검색 하는 드라이버와 같은 경우 ("") 스키마가 없는 해당 프로시저에 대 한 합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|NULL이 아닌 Varchar|프로시저 이름입니다. 프로시저의 경우 이름 없는 빈 문자열이 반환 됩니다.|  
|COLUMN_NAME (ODBC 2.0)|4|NULL이 아닌 Varchar|프로시저 열 이름입니다. 드라이버는 이름 없는 프로시저 열에 대 한 빈 문자열을 반환 합니다.|  
|COLUMN_TYPE (ODBC 2.0)|5|NULL이 아닌 Smallint|매개 변수로 프로시저 열 또는 결과 집합 열을 정의합니다.<br /><br /> SQL_PARAM_TYPE_UNKNOWN: 프로시저 열은 형식이 알 수 없는 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: 프로시저 열이 입력된 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: 프로시저 열은 입/출력 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: 프로시저 열이 출력 매개 변수입니다. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: 프로시저 열은 프로시저의 반환 값입니다. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: 프로시저 열은 결과 집합 열. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|NULL이 아닌 Smallint|SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식이 나 드라이버별 SQL 데이터 형식과 수 있습니다. 날짜/시간 및 간격 데이터 형식의이 열이 간결 하 게 데이터 형식 (예를 들어 SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH)를 반환합니다. 목록이 유효한 ODBC SQL 데이터 형식에 대 한 참조 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.|  
|TYPE_NAME (ODBC 2.0)|7|NULL이 아닌 Varchar|데이터 소스에 따라 다릅니다 데이터 형식 이름입니다. 예를 들어 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 2.0)|8|정수|데이터 원본에 대해 프로시저 열의 열 크기를 지정 합니다. 열 크기를 적용할 수 없는 데이터 형식에 대해 NULL이 반환 됩니다. 전체 자릿수에 관한 자세한 내용은 참조 하십시오. [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|BUFFER_LENGTH (ODBC 2.0)|9|정수|전송 되는 데이터의 바이트 길이 **SQLGetData** 또는 **SQLFetch** SQL_C_DEFAULT를 지정 하는 경우 작업 합니다. 숫자 데이터에 대 한이 크기는 데이터 원본에 저장 된 데이터의 크기 보다 다 수 있습니다. 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), 부록 d: 데이터 형식에서입니다.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|데이터 원본에 대해 프로시저 열의 10 진수입니다. 10 진수 적용할 수 없는 데이터 형식에 대해 NULL이 반환 됩니다. 10 진수에 관한 자세한 내용은 참조 하십시오. [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), 부록 d: 데이터 형식에서입니다.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|숫자 데이터 형식에 대 한 10 또는 2입니다.<br /><br /> 10, 경우 COLUMN_SIZE 및 DECIMAL_DIGITS 값 수의 열에 허용 되는 소수 자릿수를 제공 합니다. 예를 들어 DECIMAL(12,5) 열 10, 12, COLUMN_SIZE 및 5; DECIMAL_DIGITS NUM_PREC_RADIX 반환 FLOAT 열에는 10, 15, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL의 NUM_PREC_RADIX 반환할 수 있습니다.<br /><br /> 2 인 경우에 있는 값 COLUMN_SIZE 및 DECIMAL_DIGITS 열의 허용 하는 비트 수를 제공 합니다. 예를 들어 FLOAT 열 2, 53, COLUMN_SIZE 및 DECIMAL_DIGITS의 NULL의 NUM_PREC_RADIX 반환할 수 있습니다.<br /><br /> NUM_PREC_RADIX 적용할 수 없는 데이터 형식에 대해 NULL이 반환 됩니다.|  
|NULL 허용 (ODBC 2.0)|12|NULL이 아닌 Smallint|프로시저 열에 NULL 값을 수락할지 여부:<br /><br /> SQL_NO_NULLS: 프로시저 열 NULL 값을 허용 하지 않습니다.<br /><br /> SQL_NULLABLE: 프로시저 열에 NULL 값 허용합니다.<br /><br /> SQL_NULLABLE_UNKNOWN: 프로시저 열에 NULL 값을 사용할 경우 알려지지 않습니다.|  
|설명 (ODBC 2.0)|13|Varchar|프로시저 열에 대 한 설명|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|열의 기본값입니다.<br /><br /> NULL 값을 기본값으로 지정 된 경우이 열은 단어 NULL, 따옴표에 포함 되지 않습니다. 잘림 없이 기본값을 표현할 수 없는 경우이 열 잘림, 바깥쪽 단일 인용 부호를 포함 합니다. 기본값이 사용 되지 않는 지정 된 경우이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값 잘림 값을 포함 하는 경우를 제외 하 고 새 열 정의 생성에 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|NULL이 아닌 Smallint|SQL 데이터 형식으로 값 설명자의 SQL_DESC_TYPE 필드에 나타납니다. 이 열은 날짜/시간 및 간격 데이터 형식 제외 하 고는 DATA_TYPE 열과 동일 합니다.<br /><br /> 날짜/시간 및 간격 데이터 형식의 결과 집합에 SQL_DATA_TYPE 필드, SQL_DATETIME 또는 sql_interval 인 반환 하 고 SQL_DATETIME_SUB 필드는 특정 간격 또는 datetime 데이터 형식에 대 한 하위 코드를 반환 합니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|날짜/시간 및 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|정수|문자 또는 이진 데이터의 최대 길이 (바이트)에서 열을 입력 합니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|18|NULL이 아닌 Integer|입력 및 출력 매개 변수의 순서에 따라 증가 매개 변수를 1부터 시작 하는 프로시저 정의에서 매개 변수의 서 수 위치입니다. 반환 값 (있는 경우), 0이 반환 됩니다. 결과 집합 열에 대 한 결과 열의 서 수 위치 세트에 설정 되는 결과의 첫 번째 열 번호 1입니다. 여러 결과 집합 열 서 수 위치는 드라이버 특정 방식으로 반환 됩니다.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO" 열에 null 값이 포함 되어 있지 않으면입니다.<br /><br /> "YES" 경우 열이 Null을 포함할 수 있습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 반환되는 값은 NULLABLE 열에 반환되는 값과 다릅니다. (Null 허용 열에 대 한 설명을 참조).|  
  
## <a name="code-example"></a>코드 예  
 참조 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터 원본에서 프로시저의 목록 반환|[SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

