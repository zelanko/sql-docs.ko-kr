---
title: SQL절차 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4c8b8a9f22f6005d1af811e56485299bad3a425
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306844"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQL프로시저는** 특정 데이터 원본에 저장된 프로시저 이름 목록을 반환합니다. *프로시저는* *실행 가능한 개체*또는 입력 및 출력 매개 변수를 사용하여 호출할 수 있는 명명된 엔터티를 설명하는 데 사용되는 일반 용어입니다. 절차에 대한 자세한 내용은 [절차를](../../../odbc/reference/develop-app/procedures-odbc.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 프로시저 카탈로그. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
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
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQL프로시서가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLProcedures에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *스키마Name* 또는 *ProcName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 이 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 이름의 최대 길이 값을 초과했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|프로시저 카탈로그가 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 프로시저 스키마가 지정되었으며 드라이버 또는 데이터 원본은 스키마를 지원하지 않습니다.<br /><br /> 프로시저 스키마 또는 프로시저 이름에 대해 문자열 검색 패턴이 지정되었으며 데이터 원본은 하나 이상의 인수에 대한 검색 패턴을 지원하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 요청된 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 이 기능을 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQL프로시서에는** 요청된 범위의 모든 프로시저가 나열됩니다. 사용자는 이러한 프로시저를 실행할 수 있는 권한이 있거나 없을 수도 있습니다. 접근성을 확인하려면 응용 프로그램에서 **SQLGetInfo를** 호출하고 SQL_ACCESSIBLE_PROCEDURES 정보 값을 확인할 수 있습니다. 그렇지 않으면 응용 프로그램은 사용자가 실행할 수 없는 프로시저를 선택하는 상황을 처리할 수 있어야 합니다. 이 정보를 사용하는 방법에 대한 자세한 내용은 [절차 를](../../../odbc/reference/develop-app/procedures-odbc.md)참조하십시오.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 **SQLProcedures는** PROCEDURE_CAT, PROCEDURE_SCHEMA 및 PROCEDURE_NAME 따라 정렬된 표준 결과 집합으로 결과를 반환합니다.  
  
> [!NOTE]  
>  **SQL프로시저는** 모든 프로시저를 반환하지 않을 수 있습니다. 응용 프로그램은 **SQLProcedures**에서 반환되는지 여부에 관계없이 유효한 프로시저를 사용할 수 있습니다.  
  
 ODBC 3 *.x에*대해 다음 열의 이름이 변경되었습니다. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|절차 _OWNER|절차 _SCHEM|  
  
 PROCEDURE_CAT, PROCEDURE_SCHEM 및 PROCEDURE_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN 및 SQL_MAX_PROCEDURE_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 드라이버가 열 8(PROCEDURE_TYPE)을 초과하는 추가 열을 정의할 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|프로시저 카탈로그 식별자; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 프로시저의 카탈로그를 지원하지만 다른 프로시저에 대한 카탈로그는 지원하지 않는 경우 카탈로그가 없는 프로시저에 대해 빈 문자열("")을 반환합니다.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|프로시저 스키마 식별자; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 프로시저에 대한 스키마를 지원하지만 다른 프로시저에는 지원하지 않는 경우 스키마가 없는 프로시저에 대해 빈 문자열("")을 반환합니다.|  
|PROCEDURE_NAME (ODBC 2.0)|3|바르카르 는 NULL이 아닙니다.|프로시저 식별자입니다.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|해당 없음|다음에 사용하도록 예약됩니다. 응용 프로그램은 이러한 결과 열에서 반환되는 데이터에 의존해서는 안 됩니다.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|해당 없음|다음에 사용하도록 예약됩니다. 응용 프로그램은 이러한 결과 열에서 반환되는 데이터에 의존해서는 안 됩니다.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|해당 없음|다음에 사용하도록 예약됩니다. 응용 프로그램은 이러한 결과 열에서 반환되는 데이터에 의존해서는 안 됩니다.|  
|비고(ODBC 2.0)|7|Varchar|절차에 대한 설명입니다.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|프로시저 유형을 정의합니다.<br /><br /> SQL_PT_UNKNOWN: 프로시저가 값을 반환하는지 여부를 확인할 수 없습니다.<br /><br /> SQL_PT_PROCEDURE: 반환된 개체는 프로시저입니다. 즉, 반환 값이 없습니다.<br /><br /> SQL_PT_FUNCTION: 반환된 개체는 함수입니다. 즉, 반환 값을 가합니다.|  
  
 *스키마 이름* 및 *ProcName* 인수는 검색 패턴을 허용합니다. 유효한 검색 패턴에 대한 자세한 내용은 [패턴 값 인수를](../../../odbc/reference/develop-app/pattern-value-arguments.md)참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 [프로시저 호출을](../../../odbc/reference/develop-app/procedure-calls.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|드라이버 또는 데이터 원본에 대한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|프로시저의 매개 변수 및 결과 집합 열 반환|[SQLProcedureColumns 함수](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|저장 프로시저 호출구문|[명령문 실행](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
