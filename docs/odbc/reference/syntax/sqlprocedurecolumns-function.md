---
title: SQL절차열 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306854"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 함수(SQLProcedureColumns Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLProcedureColumns는** 지정된 프로시저에 대한 결과 집합을 구성하는 열뿐만 아니라 입력 및 출력 매개 변수 목록을 반환합니다. 드라이버는 지정된 문에 설정된 결과로 정보를 반환합니다.  
  
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
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 프로시저 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 프로시저의 카탈로그를 지원하지만 다른 프로시저에 대한 카탈로그를 지원하는 경우 빈 문자열("")은 카탈로그가 없는 프로시저를 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *CatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] **카탈로그 이름의*문자 길이 .  
  
 *스키마 이름*  
 [입력] 프로시저 스키마 이름에 대한 문자열 검색 패턴입니다. 드라이버가 다른 DBMS에서 데이터를 검색하는 경우와 같이 일부 프로시저에 대한 스키마를 지원하지만 다른 프로시저에 대한 스키마를 지원하는 경우 빈 문자열("")은 스키마가 없는 프로시저를 나타냅니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *SchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *스키마Name은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이2*  
 [입력] **스키마 이름의*문자 길이입니다.  
  
 *프록시 이름*  
 [입력] 프로시저 이름에 대한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *ProcName은* 식별자로 처리되고 해당 케이스는 중요하지 않습니다. SQL_FALSE 경우 *ProcName은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이3*  
 [입력] **ProcName의*문자 길이.  
  
 *ColumnName*  
 [입력] 열 이름에 대한 문자열 검색 패턴입니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *ColumnName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *ColumnName은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이4*  
 [입력] **열 이름의*문자 길이 .  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLProcedureColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *문 핸들* *핸들을* 호출 하는 **SQLGetDiagRec를** 호출 하 여 관련 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLProcedureColumns에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLError에서** 반환된 오류 메시지는 오류와 그 원인을 설명합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *스키마Name,* *ProcName*또는 *ColumnName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. SQLProcedureColumns 함수가 호출될 때 이 aynschronous 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 카탈로그, 스키마, 프로시저 또는 열 이름의 최대 길이 값을 초과했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|프로시저 카탈로그가 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 프로시저 스키마가 지정되었으며 드라이버 또는 데이터 원본은 스키마를 지원하지 않습니다.<br /><br /> 프로시저 스키마, 프로시저 이름 또는 열 이름에 대해 문자열 검색 패턴이 지정되었으며 데이터 원본은 이러한 인수 중 하나 이상에 대한 검색 패턴을 지원하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 일반적으로 명령문 실행 전에 프로시저 매개 변수 및 프로시저에서 반환되는 결과 집합 또는 집합을 구성하는 열(있는 경우)에 대한 정보를 검색하는 데 사용됩니다. 자세한 내용은 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)를 참조하세요.  
  
> [!NOTE]  
>  **SQLProcedureColumns프로시저에서** 사용하는 모든 열을 반환하지 않을 수 있습니다. 예를 들어 드라이버는 프로시저가 생성하는 결과 집합의 열이 아닌 프로시저에서 사용되는 매개 변수에 대한 정보만 반환할 수 있습니다.  
  
 *스키마 이름,* *ProcName*및 *ColumnName* 인수는 검색 패턴을 허용합니다. 유효한 검색 패턴에 대한 자세한 내용은 [패턴 값 인수를](../../../odbc/reference/develop-app/pattern-value-arguments.md)참조하십시오.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 **SQLProcedureColumns는** PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME 및 COLUMN_TYPE 따라 정렬된 표준 결과 집합으로 결과를 반환합니다. 열 이름은 반환 값의 이름, 프로시저 호출의 각 매개 변수 이름(호출 순서) 및 프로시저에서 반환되는 결과 집합의 각 열 이름(열 순서)으로 각 프로시저에 대해 반환됩니다.  
  
 응용 프로그램은 결과 집합의 끝을 기준으로 드라이버 관련 열을 바인딩해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME 및 COLUMN_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.  
  
 ODBC 3의 경우 다음 열의 이름이 변경되었습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|절차 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 ODBC 3에 대해 **SQLProcedureColumns에서** 반환된 결과 집합에 다음 열이 추가되었습니다. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 19(IS_NULLABLE)를 초과하는 추가 열은 드라이버에 의해 정의될 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|프로시저 카탈로그 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 프로시저의 카탈로그를 지원하지만 다른 프로시저에 대한 카탈로그는 지원하지 않는 경우 카탈로그가 없는 프로시저에 대해 빈 문자열("")을 반환합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 프로시저에 대한 스키마를 지원하지만 다른 프로시저에는 지원하지 않는 경우 스키마가 없는 프로시저에 대해 빈 문자열("")을 반환합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|바르카르 는 NULL이 아닙니다.|프로시저 이름입니다. 이름이 없는 프로시저에 대해 빈 문자열이 반환됩니다.|  
|COLUMN_NAME (ODBC 2.0)|4|바르카르 는 NULL이 아닙니다.|프로시저 열 이름입니다. 드라이버는 이름이 없는 프로시저 열에 대해 빈 문자열을 반환합니다.|  
|COLUMN_TYPE (ODBC 2.0)|5|NULL이 아닌 Smallint|프로시저 열을 매개 변수 또는 결과 집합 열로 정의합니다.<br /><br /> SQL_PARAM_TYPE_UNKNOWN: 프로시저 열은 형식을 알 수 없는 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: 프로시저 열은 입력 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: 프로시저 열은 입력/출력 매개 변수입니다. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: 프로시저 열은 출력 매개 변수입니다. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: 프로시저 열은 프로시저의 반환 값입니다. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: 프로시저 열은 결과 집합 열입니다. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. datetime 및 간격 데이터 형식의 경우 이 열은 간결한 데이터 형식(예: SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH)을 반환합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 [형식의 SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md) 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.|  
|TYPE_NAME (ODBC 2.0)|7|바르카르 는 NULL이 아닙니다.|데이터 원본 종속 데이터 형식 이름; 예를 들어 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR ()에 대한 비트 데이터"를 예로 들 수 있습니다.|  
|COLUMN_SIZE (ODBC 2.0)|8|정수|데이터 원본의 프로시저 열의 열 크기입니다. 열 크기를 적용할 수 없는 데이터 형식에 대해 NULL이 반환됩니다. 정밀도에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|BUFFER_LENGTH (ODBC 2.0)|9|정수|SQL_C_DEFAULT 지정된 경우 **SQLGetData** 또는 **SQLFetch** 작업에서 전송되는 데이터의 바이트 길이입니다. 숫자 데이터의 경우 이 크기는 데이터 원본에 저장된 데이터의 크기와 다를 수 있습니다. 자세한 내용은 부록 D: 데이터 유형의 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|데이터 원본의 프로시저 열의 소수 자릿수입니다. 소수 자릿수를 적용할 수 없는 데이터 형식에 대해 NULL이 반환됩니다. 소수 자릿수에 대한 자세한 내용은 부록 D: 데이터 유형의 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|숫자 데이터 형식의 경우 10 또는 2입니다.<br /><br /> 10이면 COLUMN_SIZE 및 DECIMAL_DIGITS 값은 열에 허용되는 소수 자릿수를 지정합니다. 예를 들어 DECIMAL(12,5) 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 12, DECIMAL_DIGITS 반환합니다. FLOAT 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 15 및 null DECIMAL_DIGITS 반환할 수 있습니다.<br /><br /> 2이면 COLUMN_SIZE 및 DECIMAL_DIGITS 값은 열에 허용되는 비트 수를 지정합니다. 예를 들어 FLOAT 열은 NUM_PREC_RADIX 2, COLUMN_SIZE 53 및 null DECIMAL_DIGITS 반환할 수 있습니다.<br /><br /> null은 NUM_PREC_RADIX 적용할 수 없는 데이터 형식에 대해 반환됩니다.|  
|널수(ODBC 2.0)|12|NULL이 아닌 Smallint|프로시저 열이 NULL 값을 허용하는지 여부:<br /><br /> SQL_NO_NULLS: 프로시저 열이 NULL 값을 허용하지 않습니다.<br /><br /> SQL_NULLABLE: 프로시저 열은 NULL 값을 허용합니다.<br /><br /> SQL_NULLABLE_UNKNOWN: 프로시저 열이 NULL 값을 허용하는지 알 수 없습니다.|  
|비고(ODBC 2.0)|13|Varchar|프로시저 열에 대한 설명입니다.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|열의 기본값입니다.<br /><br /> NULL을 기본값으로 지정한 경우 이 열은 따옴표로 묶이지 않는 NULL이라는 단어입니다. 기본값을 잘리지 않고 나타낼 수 없는 경우 이 열에는 단일 따옴표를 둘러싸지 않고 TRUNCATED가 포함됩니다. 기본값을 지정하지 않은 경우 이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값은 TRUNCATED 값을 포함하는 경우를 제외하고 새 열 정의를 생성하는 데 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|NULL이 아닌 Smallint|설명자의 SQL_DESC_TYPE 필드에 나타나는 SQL 데이터 형식의 값입니다. 이 열은 날짜 시간 및 간격 데이터 형식을 제외한 DATA_TYPE 열과 동일합니다.<br /><br /> datetime 및 간격 데이터 형식의 경우 결과 집합의 SQL_DATA_TYPE 필드는 SQL_INTERVAL 또는 SQL_DATETIME 반환하고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜 시간 데이터 형식에 대한 하위 코드를 반환합니다. [(부록 D: 데이터 유형](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조))|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|datetime 및 간격 데이터 형식에 대한 하위 유형 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|정수|문자 또는 이진 데이터 형식 열의 바이트별 최대 길이입니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|18|NULL이 아닌 Integer|입력 및 출력 매개변수의 경우 프로시저 정의에서 매개 변수의 서수 위치(매개 변수 순서 증가, 1부터 시작). 반환 값(있는 경우)의 경우 0이 반환됩니다. 결과 집합 열의 경우 결과 집합의 열의 서수 위치가 결과 집합의 첫 번째 열이 숫자 1입니다. 여러 결과 집합이 있는 경우 열 서수 위치는 드라이버별 방식으로 반환됩니다.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|열에 NULL이 포함되어 있지 않은 경우 "NO"입니다.<br /><br /> 열에 NULL을 포함할 수 있는 경우 "YES"입니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 반환되는 값은 NULLABLE 열에 반환되는 값과 다릅니다. NULLABLE 열에 대한 설명을 참조하십시오.|  
  
## <a name="code-example"></a>코드 예  
 [프로시저 호출을](../../../odbc/reference/develop-app/procedure-calls.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터 원본의 프로시저 목록 반환|[SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
