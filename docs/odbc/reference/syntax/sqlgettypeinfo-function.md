---
title: SQLGetTypeInfo 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303264"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 함수(SQLGetTypeInfo Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetTypeInfo** 는 데이터 원본에서 지원하는 데이터 형식에 대한 정보를 반환합니다. 드라이버는 SQL 결과 집합의 형태로 정보를 반환합니다. 데이터 형식은 DDL(데이터 정의 언어) 문에서 사용하기 위한 것입니다.  
  
> [!IMPORTANT]  
>  응용 프로그램은 **ALTER TABLE** 및 **CREATE TABLE** 문에서 설정된 **SQLGetTypeInfo** 결과의 TYPE_NAME 열에 반환된 형식 이름을 사용해야 합니다. **SQLGetTypeInfo** DATA_TYPE 열에서 동일한 값을 가진 두 개 이상의 행을 반환할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 결과 집합에 대한 명령문 핸들입니다.  
  
 *DataType*  
 [입력] SQL 데이터 형식입니다. 이 값은 부록 D: 데이터 형식 또는 드라이버 별 SQL 데이터 형식의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션의 값 중 하나여야 합니다. SQL_ALL_TYPES 모든 데이터 형식에 대한 정보를 반환해야 한다고 지정합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetTypeInfo** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *문 핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLGetTypeInfo에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|구현 작업 조건으로 인해 지정된 문 특성이 잘못되었기 때문에 유사한 값이 일시적으로 대체되었습니다. **(SQLGetStmtAttr에** 전화하여 일시적으로 대체된 값을 결정합니다.) 대체 값은 커서가 닫혀있을 때까지 *StatementHandle에* 대해 유효합니다. 변경할 수 있는 명령문 특성은 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT 및 SQL_ATTR_SIMULATE_CURSOR. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서* 커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> 명령문 *핸들에서*결과 집합이 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY004|잘못된 SQL 데이터 형식|인수 *DataType에* 대해 지정된 값은 유효한 ODBC SQL 데이터 형식 식별자도 아니고 드라이버에서 지원하는 드라이버 별 데이터 형식 식별자가 아닙니다.|  
|HY08|작업 취소됨|비동기 처리는 *StatementHandle에*대해 활성화되었으며 함수가 호출되고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLGetTypeInfo** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle에* 해당하는 드라이버는 기능을 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetTypeInfo는** DATA_TYPE 의해 정렬된 다음 데이터 형식이 해당 ODBC SQL 데이터 형식에 얼마나 가깝게 매핑되는지에 따라 결과를 표준 결과 집합으로 반환합니다. 데이터 원본에 의해 정의된 데이터 형식이 사용자 정의 데이터 형식보다 우선합니다. 따라서 정렬 순서가 반드시 일치하지는 않지만 먼저 DATA_TYPE 일반화한 다음 TYPE_NAME 오름차순으로 정렬할 수 있습니다. 예를 들어, 데이터 원본이 정수 및 COUNTER 데이터 형식을 정의하고, 여기서 COUNTER가 자동으로 증분되고 사용자 정의 데이터 형식 WHOLENUM도 정의되었다고 가정합니다. WHOLENUM이 ODBC SQL 데이터 형식SQL_INTEGER 밀접하게 매핑하는 반면, 데이터 원본에서 지원되더라도 자동 증분 데이터 형식은 ODBC SQL 데이터 형식에 밀접하게 매핑되지 않으므로 정수, WHOLENUM 및 COUNTER 순서로 반환됩니다. 이 정보를 사용하는 방법에 대한 자세한 내용은 [DDL 문을](../../../odbc/reference/develop-app/ddl-statements.md)참조하십시오.  
  
 *DataType* 인수가 드라이버에서 지원하는 ODBC 버전에 대해 유효하지만 드라이버에서 지원되지 않는 데이터 형식을 지정하면 빈 결과 집합이 반환됩니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 ODBC 3의 경우 다음 열의 이름이 변경되었습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 ODBC 3에 대해 **SQLGetTypeInfo에서** 반환된 결과 집합에 다음 열이 추가되었습니다. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 19(INTERVAL_PRECISION)를 초과하는 추가 열은 드라이버에 의해 정의될 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
> [!NOTE]  
>  **SQLGetTypeInfo는** 모든 데이터 형식을 반환하지 않을 수 있습니다. 예를 들어 드라이버가 사용자 정의 데이터 형식을 반환하지 않을 수 있습니다. 응용 프로그램은 **SQLGetTypeInfo**에 의해 반환되는지 여부에 관계없이 유효한 데이터 형식을 사용할 수 있습니다. **SQLGetTypeInfo에서** 반환하는 데이터 형식은 데이터 원본에서 지원하는 데이터 형식입니다. DDL(데이터 정의 언어) 명령문에 사용하기 위한 것입니다. 드라이버는 **SQLGetTypeInfo에서**반환하는 형식 이외의 데이터 형식을 사용하여 결과 집합 데이터를 반환할 수 있습니다. 카탈로그 함수에 대한 결과 집합을 만들 때 드라이버는 데이터 원본에서 지원하지 않는 데이터 형식을 사용할 수 있습니다.  
  
|열 이름|열<br /><br /> number|데이터 형식|주석|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|바르카르 는 NULL이 아닙니다.|데이터 원본 종속 데이터 형식 이름; 예를 들어 , "CHAR()", "VARCHAR()", "돈", "긴 VARBINARY" 또는 "CHAR (CHAR) 비트 데이터"를 예로 들 수 있습니다. 응용 프로그램은 **테이블 만들기** 및 **테이블 문 변경에서** 이 이름을 사용해야 합니다.|  
|DATA_TYPE (ODBC 2.0)|2|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. datetime 또는 간격 데이터 형식의 경우 이 열은 간결한 데이터 형식(예: SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH)을 반환합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 [형식의 SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md) 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.|  
|COLUMN_SIZE (ODBC 2.0)|3|정수|서버가 이 데이터 형식에 대해 지원하는 최대 열 크기입니다. 숫자 데이터의 경우 최대 정밀도입니다. 문자열 데이터의 경우 이 값은 문자의 길이입니다. datetime 데이터 형식의 경우 이 길이는 문자열 표현의 문자 길이입니다(소수 초 구성 요소의 최대 허용 정밀도가정). 열 크기를 적용할 수 없는 데이터 형식에 대해 NULL이 반환됩니다. 간격 데이터 형식의 경우 간격 리터럴의 문자 표현에 있는 문자 수입니다(정밀도를 선도하는 간격으로 정의된 대로 부록 D: 데이터 형식의 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md) 참조).<br /><br /> 열 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|리터럴 을 접두사로 사용하는 문자 또는 문자; 예를 들어 문자 데이터 형식에 대한 단일 따옴표(')이거나 이진 데이터 형식의 경우 0x입니다. 리터럴 접두사를 적용할 수 없는 데이터 형식에 대해 NULL이 반환됩니다.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|리터럴을 종료하는 데 사용되는 문자 또는 문자; 예를 들어 문자 데이터 형식에 대한 단일 따옴표(')입니다. NULL은 리터럴 접미사를 적용할 수 없는 데이터 형식에 대해 반환됩니다.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|TYPE_NAME 필드에 반환되는 이름을 사용할 때 응용 프로그램이 괄호안에 지정할 수 있는 각 매개 변수에 해당하는 쉼표로 구분된 키워드 목록입니다. 목록의 키워드는 길이, 정밀도 또는 배율 중 어느 정도일 수 있습니다. 구문을 사용해야 하는 순서대로 나타납니다. 예를 들어, deciMAL에 대한 CREATE_PARAMS "정밀도, 배율"입니다. VARCHAR에 대한 CREATE_PARAMS "길이"와 같습니다. 데이터 형식 정의에 대한 매개 변수가 없는 경우 NULL이 반환됩니다. 예를 들어 정수입니다.<br /><br /> 드라이버는 CREATE_PARAMS 텍스트가 사용되는 국가/지역의 언어로 제공됩니다.|  
|널수(ODBC 2.0)|7|NULL이 아닌 Smallint|데이터 형식이 NULL 값을 허용하는지 여부:<br /><br /> 데이터 형식이 NULL 값을 허용하지 않는 경우 SQL_NO_NULLS.<br /><br /> 데이터 형식이 NULL 값을 허용하는지 SQL_NULLABLE.<br /><br /> 열이 NULL 값을 허용하는지 여부를 알 수 없는 경우 SQL_NULLABLE_UNKNOWN.|  
|CASE_SENSITIVE (ODBC 2.0)|8|NULL이 아닌 Smallint|문자 데이터 형식이 데이터 정렬 및 비교에서 대/소문자 구분인지 여부:<br /><br /> 데이터 형식이 문자 데이터 형식이고 대/소문자를 구분하는 경우 SQL_TRUE.<br /><br /> 데이터 형식이 문자 데이터 형식이 아니거나 대/소문자를 구분하지 않는 경우 SQL_FALSE.|  
|검색 가능 (ODBC 2.0)|9|NULL이 아닌 Smallint|**WHERE** 절에서 데이터 형식을 사용하는 방법:<br /><br /> **WHERE** 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE. ODBC 2의 SQL_UNSEARCHABLE 값과 동일합니다. *x*.)<br /><br /> SQL_PRED_CHAR **WHERE** 절에서 열을 사용할 수 있지만 **LIKE** 조건자만 사용할 수 있는지 를 지정합니다. ODBC 2의 SQL_LIKE_ONLY 값과 동일합니다. *x*.)<br /><br /> SQL_PRED_BASIC 열을 **LIKE를** 제외한 모든 비교 연산자와 **WHERE** 절에서 사용할 수 있는 경우(비교, 정량화 **비교,** **구별**, **IN,** **MATCH**및 **UNIQUE).** ODBC 2의 SQL_ALL_EXCEPT_LIKE 값과 동일합니다. *x*.)<br /><br /> SQL_SEARCHABLE 비교 연산자가 있는 **WHERE** 절에서 열을 사용할 수 있는지 를 지정합니다.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|데이터 형식이 서명되지 않았는지 여부:<br /><br /> 데이터 형식이 서명되지 않은 경우 SQL_TRUE.<br /><br /> 데이터 형식이 서명되었는지 SQL_FALSE.<br /><br /> 특성이 데이터 형식에 적용되지 않거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환됩니다.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|NULL이 아닌 Smallint|데이터 형식에 미리 정의된 고정 정밀도 및 배율(데이터 원본별)이 있는지 여부(예: money 데이터 형식)<br /><br /> 미리 정의된 정밀도와 배율이 있는지 SQL_TRUE.<br /><br /> 미리 정의된 고정 정밀도와 배율이 없는 경우 SQL_FALSE.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|데이터 형식이 자동 증분인지 여부:<br /><br /> 데이터 형식이 자동 증분인지 SQL_TRUE.<br /><br /> 데이터 형식이 자동 증가되지 않는지 SQL_FALSE.<br /><br /> 특성이 데이터 형식에 적용되지 않거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환됩니다.<br /><br /> 응용 프로그램은 이 특성을 갖는 열을 열에 삽입할 수 있지만 일반적으로 열의 값을 업데이트할 수는 없습니다.<br /><br /> 인서트가 자동 증분 열로 만들어지면 삽입 시 고유한 값이 열에 삽입됩니다. 증분은 정의되지 않지만 데이터 원본에 따라 다릅니다. 응용 프로그램은 자동 증분 열이 특정 지점에서 시작하거나 특정 값으로 증분한다고 가정해서는 안 됩니다.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|데이터 원본에 종속적인 데이터 형식 이름의 지역화된 버전입니다. 데이터 원본이 지역화된 이름을 지원하지 않는 경우에는 NULL이 반환됩니다. 이 이름은 대화 상자와 같이 표시하기 위한 것입니다.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|데이터 원본의 데이터 형식의 최소 배율입니다. 데이터 형식이 고정 소수 자릿수인 경우에는 MINIMUM_SCALE 및 MAXIMUM_SCALE 열 모두 이 값을 포함합니다. 예를 들어 SQL_TYPE_TIMESTAMP 열에는 소수 초 동안 고정된 축척이 있을 수 있습니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|데이터 원본의 데이터 형식의 최대 배율입니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 최대 축척이 데이터 원본에서 별도로 정의되지 않고 대신 최대 정밀도와 동일하도록 정의된 경우 이 열에는 COLUMN_SIZE 열과 동일한 값이 포함됩니다. 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|NULL이 아닌 Smallint|설명자의 SQL_DESC_TYPE 필드에 나타나는 SQL 데이터 형식의 값입니다. 이 열은 간격 및 날짜 시간 데이터 형식을 제외한 DATA_TYPE 열과 동일합니다.<br /><br /> 간격 및 날짜 시간 데이터 형식의 경우 결과 집합의 SQL_DATA_TYPE 필드는 SQL_INTERVAL 또는 SQL_DATETIME 반환하고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜 시간 데이터 형식에 대한 하위 코드를 반환합니다. [(부록 D: 데이터 유형](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조))|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATA_TYPE 값이 SQL_DATETIME 또는 SQL_INTERVAL 경우 이 열에는 datetime/interval 하위 코드가 포함됩니다. 날짜 및 간격 이외의 데이터 형식의 경우 이 필드는 NULL입니다.<br /><br /> 간격 또는 datetime 데이터 형식의 경우 결과 집합의 SQL_DATA_TYPE 필드는 SQL_INTERVAL 또는 SQL_DATETIME 반환하고 SQL_DATETIME_SUB 필드는 특정 간격 또는 날짜 시간 데이터 형식에 대한 하위 코드를 반환합니다. [(부록 D: 데이터 유형](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조))|  
|NUM_PREC_RADIX (ODBC 3.0)|18|정수|데이터 형식이 대략적인 숫자 형식인 경우 이 열에는 COLUMN_SIZE 여러 비트를 지정함을 나타내는 값 2가 포함되어 있습니다. 정확한 숫자 형식의 경우 이 열에는 COLUMN_SIZE 소수자릿수를 지정함을 나타내는 값 10이 포함되어 있습니다. 그렇지 않은 경우 이 열은 NULL입니다.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|데이터 형식이 간격 데이터 형식인 경우 이 열에는 정밀도를 선도하는 간격 값이 포함됩니다. (부록 D: 데이터 형식의 [간격 데이터 형식 정밀도](../../../odbc/reference/appendixes/interval-data-type-precision.md) 를 참조하십시오.) 그렇지 않으면 이 열은 NULL입니다.|  
  
 특성 정보는 데이터 형식 또는 결과 집합의 특정 열에 적용할 수 있습니다. **SQLGetTypeInfo는** 데이터 형식과 관련된 특성에 대한 정보를 반환합니다. **SQLColAttribute는** 결과 집합의 열과 연결된 특성에 대한 정보를 반환합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLColAttribute 함수](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|드라이버 또는 데이터 원본에 대한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
