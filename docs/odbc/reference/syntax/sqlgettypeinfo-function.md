---
title: SQLGetTypeInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1690e8c9f4f0e8c491bedac1a27faf65cde747
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809922"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 함수(SQLGetTypeInfo Function)
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수 합니다: ISO 92  
  
 **요약**  
 **SQLGetTypeInfo** 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 형태로 정보를 반환합니다. 데이터 형식은 데이터 정의 언어 (DDL) 문에서 사용이 됩니다.  
  
> [!IMPORTANT]  
>  응용 프로그램의 TYPE_NAME 열에서 반환 된 형식 이름을 사용 해야 합니다는 **SQLGetTypeInfo** 결과 집합 **ALTER TABLE** 하 고 **CREATE TABLE** 문. **SQLGetTypeInfo** DATA_TYPE 열에 동일한 값을 가진 둘 이상의 행을 반환할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 결과 집합에 대 한 문의 핸들입니다.  
  
 *데이터 형식*  
 [입력] SQL 데이터 형식입니다. 값 중 하나 이어야 합니다는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식 또는 드라이버별 SQL 데이터 형식에 대 한 부분입니다. SQL_ALL_TYPES 모든 데이터 형식에 대 한 정보 반환 되어야 함을 지정 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetTypeInfo** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* sql _HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetTypeInfo** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|지정 된 문 특성을 일시적으로 유사한 값에 대체 되므로 구현 작업 조건으로 인해 잘못 되었습니다. (호출 **SQLGetStmtAttr** 일시적으로 대체 값을 결정 합니다.) 대체 값이 적합 합니다 *StatementHandle* 커서를 닫을 때까지 합니다. 변경할 수 있는 문 특성은: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT, 및 SQL_ATTR_SIMULATE_CURSOR 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle,* 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 하지 않은 한 경우 드라이버에서 반환 됩니다 **SQLFetch** 또는**SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 결과 집합에 열려 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY004|잘못 된 SQL 데이터 형식|인수에 지정 된 값 *DataType* 유효한 ODBC SQL 데이터 형식 식별자도 아니고 드라이버에서 지 원하는 드라이버별 데이터 형식 식별자를 했습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*오른쪽 다음 함수가 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 되었습니다 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 이 함수가 호출 하 고 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLGetTypeInfo** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetTypeInfo** DATA_TYPE 한 후 얼마나 밀접 하 게 데이터 형식이 해당 ODBC SQL 데이터 형식에 매핑되는 여 순서가 지정 된 표준 결과 집합으로 결과 반환 합니다. 데이터 원본에서 정의한 데이터 유형을 사용자 정의 데이터 형식 보다 우선 합니다. 결과적으로 정렬 순서 반드시 일치 하지 않습니다 하지만 수 수 먼저 DATA_TYPE로 일반화, TYPE_NAME, 모두 오름차순 뒤에. 예를 들어 데이터 원본이 카운터가 있는 자동 증분 정수와 카운터 데이터 형식을 정의 하 고 사용자 정의 데이터 형식을 WHOLENUM도 정의 되었다고 가정 합니다. 이러한 정수 WHOLENUM 순서 대로 반환 됩니다 및 카운터를 ODBC SQL 데이터에 가깝게 WHOLENUM 맵 형식 SQL_INTEGER, 자동 증분 데이터를 입력 하는 동안 데이터 원본에서 지 원하는 경우에 매핑되지 않는 경우 밀접 하 게 하는 ODBC SQL 데이터 형식입니다. 이 정보를 어떻게 사용할 수 있는지에 대 한 자세한 내용은 [DDL 문은](../../../odbc/reference/develop-app/ddl-statements.md)합니다.  
  
 경우는 *DataType* 인수 드라이버에서 지 원하는 ODBC의 버전에 대 한 유효한 데이터 형식을 지정 하지만 드라이버에서 지원 되지 않는 다음 빈 결과 집합을 반환 합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다. *x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3입니다. *x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 다음 열이 반환한 결과 집합에 추가 되었습니다 **SQLGetTypeInfo** ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 19 (INTERVAL_PRECISION) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 것이 아니라 결과 집합의 끝에서 카운트다운 여 드라이버별 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 모든 데이터 형식을 반환 하지 않을 수 있습니다. 예를 들어, 드라이버를 사용자 정의 데이터 형식을 반환 하지 않을 수 있습니다. 응용 프로그램에서 반환 되는지 여부에 관계 없이 모든 유효한 데이터 형식에 따르면 **SQLGetTypeInfo**합니다. 반환 되는 데이터 형식 **SQLGetTypeInfo** 데이터 원본에서 지원 되는 합니다. 이러한 데이터 정의 언어 (DDL) 문에서 사용이 됩니다. 드라이버에서 반환한 형식 이외의 데이터 형식을 사용 하 여 결과 집합 데이터를 반환할 수 있습니다 **SQLGetTypeInfo**합니다. 드라이버의 결과 집합 카탈로그 함수에 대 한 만들기, 데이터 원본에서 지원 되지 않는 데이터 형식을 사용할 수 있습니다.  
  
|열 이름|Column<br /><br /> number|데이터 형식|주석|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|NULL이 아닌 Varchar|데이터 소스에 따라 다릅니다 데이터 형식 이름입니다. 예를 들어, "char ()", "VARCHAR()", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다. 응용 프로그램에서이 이름을 사용 해야 합니다 **CREATE TABLE** 하 고 **ALTER TABLE** 문입니다.|  
|DATA_TYPE (ODBC 2.0)|2|NULL이 아닌 Smallint|SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식 수 있습니다. 이 열 데이터 형식 datetime 또는 간격에 대 한 간결한 데이터 형식 (예: SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH)를 반환합니다. 유효한 ODBC SQL 데이터 형식의 목록을 참조 하세요 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.|  
|COLUMN_SIZE (ODBC 2.0)|3|정수|서버에서이 데이터 형식에 대 한 지 최대 열 크기입니다. 숫자 데이터의 최대 전체 자릿수입니다. 문자열 데이터의 문자 길이입니다. Datetime 데이터 형식의 경우 문자 (최대 허용된 전체 자릿수 소수 자릿수 초 구성 요소를 가정) 문자열 표현의 길이입니다. NULL 열 크기 적용할 수 없는 데이터 형식에 대해 반환 됩니다. 간격 데이터 형식에 대 한 리터럴 간격의 문자 표현에 있는 문자의 수입니다 (선행 정밀도; 간격에 따라 정의 된 대로 참조 하세요 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md) 부록 d: 데이터 형식에서).<br /><br /> 열 크기에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|문자 또는 문자 리터럴을; 접두사를 지정 하는 데 사용 예를 들어, 작은따옴표 (') 문자 데이터 형식 또는 이진 데이터 형식에 대 한 0x NULL 리터럴 접두사를 적용할 수 없는 데이터 형식에 대해 반환 됩니다.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|문자 또는 문자 리터럴을;를 종료 하는 데 사용 예를 들어, 작은따옴표 ('); 문자 데이터 형식에 대 한 NULL 리터럴 접미사를 적용할 수 없는 데이터 형식에 대해 반환 됩니다.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|목록 TYPE_NAME 필드에서 반환 되는 이름을 사용 하는 경우 응용 프로그램 괄호 안에 지정할 수 있는 각 매개 변수에 해당 하는 쉼표로 구분 하 여 키워드입니다. 키워드 목록에는 다음 중 하나일 수 있습니다: 길이, 전체 자릿수 또는 소수입니다. 구문을 사용할 해야 하는 순서에 표시 됩니다. 예를 들어, 소수의 CREATE_PARAMS 것 "precision, scale"; Varchar CREATE_PARAMS "길이입니다."와 같습니다. 데이터 형식 정의;에 대 한 매개 변수가 없는 경우 NULL이 반환 됩니다. 예를 들어 정수입니다.<br /><br /> 드라이버는 사용 된 국가/지역의 언어로 CREATE_PARAMS 텍스트를 제공 합니다.|  
|NULL을 허용 (ODBC 2.0)|7|NULL이 아닌 Smallint|NULL 값 허용 여부는 데이터 형식:<br /><br /> 데이터 형식이 NULL 값을 허용 하지 않는 경우 SQL_NO_NULLS 합니다.<br /><br /> SQL_NULLABLE 데이터 형식이 NULL 값을 허용 하는 경우입니다.<br /><br /> SQL_NULLABLE_UNKNOWN 경우 열에 NULL 값 허용 하는지 여부를 알 수 없습니다.|  
|CASE_SENSITIVE (ODBC 2.0)|8|NULL이 아닌 Smallint|문자 데이터 형식 인지 데이터 정렬 및 비교에서 대/소문자 구분:<br /><br /> Sql_true는 해당 데이터 형식이 문자 데이터 형식이 며 대/소문자 구분 하는 경우.<br /><br /> 데이터 형식이 문자 데이터 형식이 아니거나 대/소문자 구분 없는 경우 SQL_FALSE입니다.|  
|검색 가능한 (ODBC 2.0)|9|NULL이 아닌 Smallint|데이터 형식에서 어떻게 사용 되는 **여기서** 절:<br /><br /> SQL_PRED_NONE 열에서 사용할 수 없는 경우는 **여기서** 절. (이 / ODBC 2에서 SQL_UNSEARCHABLE 값과 동일 합니다. *x*.)<br /><br /> SQL_PRED_CHAR 열에서 사용할 수 있는 경우는 **위치** 절만 합니다 **같은** 조건자입니다. (이 / ODBC 2에서 SQL_LIKE_ONLY 값과 동일 합니다. *x*.)<br /><br /> SQL_PRED_BASIC 열에서 사용할 수 있는 경우는 **여기서** 제외한 모든 비교 연산자를 사용 하 여 절 **와 같은** (비교, 정량화 된 비교 **BETWEEN**를  **DISTINCT**, **IN**를 **일치**, 및 **UNIQUE**). (이 / ODBC 2에서 SQL_ALL_EXCEPT_LIKE 값과 동일 합니다. *x*.)<br /><br /> SQL_SEARCHABLE 열에서 사용할 수 있는 경우는 **여기서** 임의의 비교 연산자를 사용 하 여 절.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|여부는 데이터 형식은 부호가 없습니다.<br /><br /> Sql_true는 해당 데이터 형식이 서명 되어 있지 않으면입니다.<br /><br /> 데이터 형식에 부호가 경우 SQL_FALSE입니다.<br /><br /> 특성 데이터 형식에 적용할 수 없거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환 됩니다.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|NULL이 아닌 Smallint|전체 자릿수 및 소수 (임, 데이터 소스 관련), money 데이터 형식과 같은 데이터 형식에 미리 정의 된 여부 수정 됨:<br /><br /> SQL_TRUE는 미리 정의 하는 경우에 전체 자릿수 및 소수 수정 되었습니다.<br /><br /> 미리 정의 된 정밀도 배율이 고정 되지 않은 경우 SQL_FALSE입니다.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|데이터 형식이 자동 증가 인지 여부.<br /><br /> Sql_true는 해당 데이터 형식이 자동 증가 합니다.<br /><br /> 데이터 형식이 자동 증가 하는 경우 SQL_FALSE입니다.<br /><br /> 특성 데이터 형식에 적용할 수 없거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환 됩니다.<br /><br /> 응용 프로그램 값이이 특성을 가진 열을 삽입할 수 있지만 일반적으로 열에 값을 업데이트할 수 없습니다.<br /><br /> 자동 증가 열에 삽입 수행 되 면 삽입 시 고유 값 열에 삽입 됩니다. Increment를 정의 하지 않은 이지만 데이터 소스 관련 있습니다. 응용 프로그램 특정 값으로 자동 증분 열을 증가 나 특정 지점에서 시작 하는 것을 가정 하지 않아야 합니다.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|데이터 형식의 데이터 소스에 따라 다릅니다 이름의 지역화 된 버전입니다. 데이터 원본이 지역화된 이름을 지원하지 않는 경우에는 NULL이 반환됩니다. 이 이름은 표시 대화 상자와 같이 등만 위한 것입니다.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|데이터 원본에서 데이터 형식의 최소 소수 자릿수입니다. 데이터 형식이 고정 소수 자릿수인 경우에는 MINIMUM_SCALE 및 MAXIMUM_SCALE 열 모두 이 값을 포함합니다. 예를 들어는 SQL_TYPE_TIMESTAMP 열 소수 자릿수 초에 대 한 고정된 소수가 있을 수 있습니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|데이터 원본에서 데이터 형식의 최대 소수 자릿수입니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 최대 소수 자릿수에 정의 되어 있지 별도로 데이터 원본에 정의 됩니다. 대신 최대 자릿수와 동일 하지만이 열에는 동일한 COLUMN_SIZE 열의 값을 포함 합니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint NOT NULL|설명자의 SQL_DESC_TYPE 필드에는 SQL 데이터 형식으로 값 표시 됩니다. 이 열은 간격 및 datetime 데이터 형식 제외 하 고는 DATA_TYPE 열과 동일 합니다.<br /><br /> 간격 및 datetime 데이터 형식에 대 한 결과 집합의 SQL_DATA_TYPE 필드, SQL_DATETIME 또는 sql_interval 인 반환 하 고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜/시간 데이터 형식에 대 한 하위 코드를 반환 합니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATA_TYPE 값 SQL_DATETIME 또는 sql_interval 인 경우이 열에 날짜/시간/간격 하위 코드를 포함 합니다. 날짜/시간 및 간격 이외 데이터 형식의 경우이 필드는 NULL입니다.<br /><br /> 간격 또는 날짜/시간 데이터 형식에 대 한 결과 집합의 SQL_DATA_TYPE 필드, SQL_DATETIME 또는 sql_interval 인 반환 하 고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜/시간 데이터 형식에 대 한 하위 코드를 반환 합니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|정수|데이터 형식이 근사치 숫자 형식, COLUMN_SIZE 지정 된 비트 수를 표시 하는 2 값이이 열에 포함 됩니다. 정확한 숫자 형식인 경우이 열 값 COLUMN_SIZE 소수 자릿수를 지정 하는지 표시 하는 10을 포함 합니다. 그렇지 않은 경우 이 열은 NULL입니다.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|데이터 형식이 간격 데이터 유형을 이면이 열이 선행 간격 정밀도 값을 포함 합니다. (참조 [간격 데이터 형식 전체 자릿수](../../../odbc/reference/appendixes/interval-data-type-precision.md) 부록 d: 데이터 형식에서입니다.) 그렇지 않은 경우 이 열은 NULL입니다.|  
  
 특성 정보 또는 결과 집합의 특정 열 데이터 형식에 적용할 수 있습니다. **SQLGetTypeInfo** ; 데이터 형식과 연결 된 특성에 대 한 정보를 반환 합니다. **SQLColAttribute** 결과 집합의 열과 연결 된 특성에 대 한 정보를 반환 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLColAttribute 함수](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보를 반환합니다.|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
