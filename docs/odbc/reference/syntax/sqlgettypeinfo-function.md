---
description: SQLGetTypeInfo 함수(SQLGetTypeInfo Function)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47ff65a1c7912aef196c79b9b26c8286fb05fef2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421197"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 함수(SQLGetTypeInfo Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetTypeInfo** 는 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합 형식으로 정보를 반환 합니다. 데이터 형식은 DDL (데이터 정의 언어) 문에서 사용 하기 위한 것입니다.  
  
> [!IMPORTANT]  
>  응용 프로그램은 **ALTER TABLE** 및 **CREATE TABLE** 문에서 **SQLGetTypeInfo** result 집합의 TYPE_NAME 열에 반환 된 형식 이름을 사용 해야 합니다. **SQLGetTypeInfo** 는 DATA_TYPE 열에 동일한 값을 가진 행을 두 개 이상 반환할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 결과 집합에 대 한 문 핸들입니다.  
  
 *DataType*  
 입력 SQL 데이터 형식입니다. 부록 D: 데이터 형식 또는 드라이버별 SQL 데이터 형식의 [Sql 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션에 있는 값 중 하나 여야 합니다. SQL_ALL_TYPES는 모든 데이터 형식에 대 한 정보를 반환 하도록 지정 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetTypeInfo** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetTypeInfo** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|구현 작업 조건 때문에 지정 된 문 특성이 잘못 되었습니다. 따라서 유사한 값이 일시적으로 대체 되었습니다. ( **SQLGetStmtAttr** 를 호출 하 여 임시로 대체 된 값을 확인 합니다.) 대체 값은 커서가 닫힐 때까지 *StatementHandle* 에 대해 유효 합니다. 변경할 수 있는 문 특성은 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT, SQL_ATTR_SIMULATE_CURSOR입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고, **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에 대 한 결과 집합이 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY004|잘못 된 SQL 데이터 형식|인수 *데이터* 형식에 지정 된 값이 올바른 ODBC SQL 데이터 형식 식별자 또는 드라이버에서 지 원하는 드라이버별 데이터 형식 식별자가 아닙니다.|  
|HY008|작업 취소됨|비동기 처리가 *StatementHandle*에 대해 사용 하도록 설정 된 다음 함수를 호출 하 고 실행을 완료 하기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **sqlcancelhandle** 이 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetTypeInfo** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetTypeInfo** 는 결과를 DATA_TYPE 정렬 된 표준 결과 집합으로 반환 하 고 그 다음에 데이터 형식이 해당 ODBC SQL 데이터 형식으로 매핑되는 정도를 기준으로 결과를 반환 합니다. 데이터 원본에 의해 정의 되는 데이터 형식은 사용자 정의 데이터 형식 보다 우선적으로 적용 됩니다. 따라서 정렬 순서가 반드시 일치 하는 것은 아니지만 DATA_TYPE first로 일반화 한 다음 TYPE_NAME (오름차순)를 사용할 수 있습니다. 예를 들어, 데이터 원본에서 정수 및 카운터 데이터 형식을 정의 하는 경우 카운터가 자동으로 증가 하 고 사용자 정의 데이터 형식 WHOLENUM도 정의 되어 있다고 가정 합니다. WHOLENUM는 ODBC SQL 데이터 형식 SQL_INTEGER와 긴밀 하 게 매핑되며, 데이터 원본에서 지 원하는 경우에도 자동 증분 데이터 형식은 ODBC SQL 데이터 형식에 긴밀 하 게 매핑되지 않기 때문에 이러한 값은 order WHOLENUM 및 COUNTER로 반환 됩니다. 이 정보를 사용 하는 방법에 대 한 자세한 내용은 [DDL 문](../../../odbc/reference/develop-app/ddl-statements.md)을 참조 하십시오.  
  
 *DataType* 인수가 드라이버에서 지원 되는 ODBC 버전에 유효한 데이터 형식을 지정 하지만 드라이버에서 지원 하지 않는 경우 빈 결과 집합을 반환 합니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 ODBC 3의 열 이름은 다음과 같습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 다음 열이 ODBC 3 용 **SQLGetTypeInfo** 에서 반환 된 결과 집합에 추가 되었습니다. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 19 (INTERVAL_PRECISION) 외의 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 액세스할 수 있어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 일부 데이터 형식을 반환 하지 않을 수 있습니다. 예를 들어 드라이버가 사용자 정의 데이터 형식을 반환 하지 않을 수 있습니다. 응용 프로그램은 **SQLGetTypeInfo**에 의해 반환 되는지 여부와 관계 없이 모든 유효한 데이터 형식을 사용할 수 있습니다. **SQLGetTypeInfo** 에서 반환 되는 데이터 형식은 데이터 원본에서 지 원하는 데이터 형식입니다. DDL (데이터 정의 언어) 문에서 사용 하기 위한 것입니다. 드라이버는 **SQLGetTypeInfo**에서 반환 하는 형식 이외의 데이터 형식을 사용 하 여 결과 집합 데이터를 반환할 수 있습니다. 카탈로그 함수에 대 한 결과 집합을 만들 때 드라이버는 데이터 원본에서 지원 하지 않는 데이터 형식을 사용할 수 있습니다.  
  
|열 이름|열<br /><br /> number|데이터 형식|주석|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar not NULL|데이터 원본에 종속 된 데이터 형식 이름입니다. 예를 들면 "CHAR ()", "VARCHAR ()", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다. 응용 프로그램은 **CREATE TABLE** 및 **ALTER TABLE** 문에서이 이름을 사용 해야 합니다.|  
|DATA_TYPE (ODBC 2.0)|2|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. Datetime 또는 interval 데이터 형식의 경우이 열은 SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR_TO_MONTH 같은 간결한 데이터 형식을 반환 합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 형식에서 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.|  
|COLUMN_SIZE (ODBC 2.0)|3|정수|서버에서이 데이터 형식에 대해 지 원하는 최대 열 크기입니다. 숫자 데이터의 경우 최대 전체 자릿수입니다. 문자열 데이터의 경우 문자 길이입니다. Datetime 데이터 형식의 경우 문자열 표현의 문자 길이입니다 (소수 자릿수 초 구성 요소의 최대 허용 전체 자릿수 라고 가정). 열 크기를 적용할 수 없는 데이터 형식에 대해서는 NULL이 반환 됩니다. Interval 데이터 형식의 경우 interval 리터럴의 문자 표현에 있는 문자 수입니다 (간격 선행 전체 자릿수에 정의 됨). 자세한 내용은 부록 D: 데이터 형식의 [Interval 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md) 를 참조 하세요.<br /><br /> 열 크기에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|리터럴 접두사에 사용 되는 문자 예를 들어 문자 데이터 형식에 대 한 작은따옴표 (') 또는 이진 데이터 형식에 대 한 0x가 있습니다. 리터럴 접두사가 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|리터럴을 종료 하는 데 사용 되는 문자 예를 들어 문자 데이터 형식에 대 한 작은따옴표 (')가 있습니다. 리터럴 접미사가 적용 되지 않는 데이터 형식에 대해서는 NULL이 반환 됩니다.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|TYPE_NAME 필드에 반환 되는 이름을 사용할 때 응용 프로그램이 괄호 안에 지정할 수 있는 각 매개 변수에 해당 하는 키워드 목록 (쉼표로 구분)입니다. 목록의 키워드는 길이, 전체 자릿수 또는 소수 자릿수 중 하나일 수 있습니다. 구문에서 사용 해야 하는 순서 대로 표시 됩니다. 예를 들어 10 진수에 대 한 CREATE_PARAMS는 "전체 자릿수, 소수 자릿수"와 같습니다. VARCHAR의 CREATE_PARAMS는 "length"와 같습니다. 데이터 형식 정의에 대 한 매개 변수가 없는 경우 NULL이 반환 됩니다. 예를 들면 INTEGER입니다.<br /><br /> 드라이버는 사용 되는 국가/지역 언어로 CREATE_PARAMS 텍스트를 제공 합니다.|  
|NULLABLE (ODBC 2.0)|7|NULL이 아닌 Smallint|데이터 형식이 NULL 값을 허용 하는지 여부를 나타냅니다.<br /><br /> 데이터 형식이 NULL 값을 허용 하지 않는 경우 SQL_NO_NULLS 합니다.<br /><br /> 데이터 형식이 NULL 값을 허용 하는지 여부를 SQL_NULLABLE 합니다.<br /><br /> 열이 NULL 값을 허용 하는지 여부를 알 수 없는 경우에 SQL_NULLABLE_UNKNOWN 합니다.|  
|CASE_SENSITIVE (ODBC 2.0)|8|NULL이 아닌 Smallint|문자 데이터 형식이 데이터 정렬과 비교에서 대/소문자를 구분 하는지 여부입니다.<br /><br /> 데이터 형식이 문자 데이터 형식이 고 대/소문자를 구분 하는지 여부를 SQL_TRUE 합니다.<br /><br /> 데이터 형식이 문자 데이터 형식이 아니거나 대/소문자를 구분 하지 않는 경우 SQL_FALSE 합니다.|  
|검색 가능 (ODBC 2.0)|9|NULL이 아닌 Smallint|**WHERE** 절에서 데이터 형식을 사용 하는 방법:<br /><br /> **WHERE** 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE 합니다. 이 값은 ODBC 2의 SQL_UNSEARCHABLE 값과 동일 합니다. *x*.)<br /><br /> **WHERE** 절에서 열을 사용할 수 있지만 **LIKE** 조건자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_PRED_CHAR 합니다. 이 값은 ODBC 2의 SQL_LIKE_ONLY 값과 동일 합니다. *x*.)<br /><br /> **LIKE** (comparison, 정량화 된 Comparison, **BETWEEN**, **DISTINCT**, **in**, **MATCH**및 **UNIQUE**)를 제외한 모든 비교 연산자를 사용 하 여 **WHERE** 절에서 열을 사용할 수 있는지 여부를 SQL_PRED_BASIC 합니다. 이 값은 ODBC 2의 SQL_ALL_EXCEPT_LIKE 값과 동일 합니다. *x*.)<br /><br /> **WHERE** 절에서 비교 연산자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_SEARCHABLE 합니다.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|데이터 형식이 부호 없는 형식 인지 여부를 나타냅니다.<br /><br /> 데이터 형식이 unsigned 인 경우 SQL_TRUE 합니다.<br /><br /> 데이터 형식이 서명 된 경우에는 SQL_FALSE 합니다.<br /><br /> 특성을 데이터 형식에 적용할 수 없거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환 됩니다.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|NULL이 아닌 Smallint|데이터 형식이 다음과 같이 money 데이터 형식과 같이 고정 전체 자릿수와 소수 자릿수 (데이터 원본에 따라 달라 지는)를 미리 정의 했는지 여부입니다.<br /><br /> 고정 전체 자릿수와 소수 자릿수가 미리 정의 되어 있는 경우 SQL_TRUE 합니다.<br /><br /> 미리 정의 된 고정 전체 자릿수 및 소수 자릿수가 없는 경우 SQL_FALSE 합니다.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|데이터 형식이 자동 증가 여부를 나타냅니다.<br /><br /> 데이터 형식이 자동 증가 하는지 여부를 SQL_TRUE 합니다.<br /><br /> 데이터 형식이 자동 증가 하지 않을 경우 SQL_FALSE 합니다.<br /><br /> 특성을 데이터 형식에 적용할 수 없거나 데이터 형식이 숫자가 아닌 경우 NULL이 반환 됩니다.<br /><br /> 응용 프로그램은이 특성이 있는 열에 값을 삽입할 수 있지만 일반적으로 열의 값을 업데이트할 수 없습니다.<br /><br /> 자동 증분 열에 삽입을 수행 하는 경우 삽입 시 열에 고유한 값이 삽입 됩니다. 증가값은 정의 되지 않지만 데이터 원본에만 해당 됩니다. 응용 프로그램에서는 자동 증분 열이 특정 지점에서 시작 되거나 특정 값으로 증가 한다고 가정 하지 않아야 합니다.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|데이터 원본에 종속적인 데이터 형식 이름의 지역화된 버전입니다. 데이터 원본이 지역화된 이름을 지원하지 않는 경우에는 NULL이 반환됩니다. 이 이름은 대화 상자에 표시 되는 것과 같은 용도로만 사용 됩니다.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|데이터 원본에 있는 데이터 형식의 최소 소수 자릿수입니다. 데이터 형식이 고정 소수 자릿수인 경우에는 MINIMUM_SCALE 및 MAXIMUM_SCALE 열 모두 이 값을 포함합니다. 예를 들어 SQL_TYPE_TIMESTAMP 열에는 소수 자릿수 초에 대 한 고정 된 눈금이 있을 수 있습니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|데이터 원본에 있는 데이터 형식의 최대 소수 자릿수입니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다. 최대 소수 자릿수가 데이터 원본에서 별도로 정의 되지 않고 최대 전체 자릿수와 동일 하 게 정의 된 경우이 열은 COLUMN_SIZE 열과 동일한 값을 포함 합니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|NULL이 아닌 Smallint|설명자의 SQL_DESC_TYPE 필드에 표시 되는 SQL 데이터 형식의 값입니다. 이 열은 interval 및 datetime 데이터 형식을 제외 하 고는 DATA_TYPE 열과 동일 합니다.<br /><br /> Interval 및 datetime 데이터 형식의 경우 결과 집합의 SQL_DATA_TYPE 필드는 SQL_INTERVAL 또는 SQL_DATETIME를 반환 하 고, SQL_DATETIME_SUB 필드는 특정 interval 또는 datetime 데이터 형식에 대 한 하위 코드를 반환 합니다. [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATA_TYPE 값이 SQL_DATETIME 되거나 SQL_INTERVAL 경우이 열에는 DATETIME/INTERVAL 하위 코드가 포함 됩니다. Datetime 및 interval 이외의 데이터 형식의 경우이 필드는 NULL입니다.<br /><br /> Interval 또는 datetime 데이터 형식의 경우에는 결과 집합의 SQL_DATA_TYPE 필드가 SQL_INTERVAL 또는 SQL_DATETIME를 반환 하 고 SQL_DATETIME_SUB 필드는 특정 interval 또는 datetime 데이터 형식에 대 한 하위 코드를 반환 합니다. [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.|  
|NUM_PREC_RADIX (ODBC 3.0)|18|정수|데이터 형식이 근사 숫자 형식인 경우이 열에는 COLUMN_SIZE에서 비트 수를 지정 하는 값 2가 포함 됩니다. 정확한 숫자 형식의 경우이 열에는 COLUMN_SIZE 10 진수 수를 지정 하는 값 10이 포함 됩니다. 그렇지 않은 경우 이 열은 NULL입니다.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|데이터 형식이 interval 데이터 형식인 경우이 열에는 간격의 선행 전체 자릿수 값이 포함 됩니다. 자세한 내용은 부록 D: 데이터 형식의 [간격 데이터 형식 전체 자릿수](../../../odbc/reference/appendixes/interval-data-type-precision.md) 를 참조 하세요. 그렇지 않으면이 열은 NULL입니다.|  
  
 특성 정보는 데이터 형식이 나 결과 집합의 특정 열에 적용 될 수 있습니다. **SQLGetTypeInfo** 는 데이터 형식과 연결 된 특성에 대 한 정보를 반환 합니다. **Sqlcolattribute** 는 결과 집합의 열과 관련 된 특성에 대 한 정보를 반환 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLColAttribute 함수](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
