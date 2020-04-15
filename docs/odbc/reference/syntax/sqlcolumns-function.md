---
title: SQLColumns 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301259"
---
# <a name="sqlcolumns-function"></a>SQLColumns 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: 개방형 그룹  
  
 **요약**  
 **SQLColumns는** 지정된 테이블의 열 이름 목록을 반환합니다. 드라이버는 지정된 *StatementHandle*에 설정된 결과로 이 정보를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *CatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] **카탈로그 이름의*문자 길이 .  
  
 *스키마 이름*  
 [입력] 스키마 이름에 대한 문자열 검색 패턴입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *SchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *스키마Name은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이2*  
 [입력] **스키마 이름의*문자 길이입니다.  
  
 *Tablename*  
 [입력] 테이블 이름에 대한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *TableName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *TableName은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이3*  
 [입력] **테이블 네임의*문자 길이 .  
  
 *ColumnName*  
 [입력] 열 이름에 대한 문자열 검색 패턴입니다.  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *ColumnName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *ColumnName은* 패턴 값 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이4*  
 [입력] **열 이름의*문자 길이 .  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 핸들 *SQL_HANDLE_STMT* 핸들 *핸들* *Handle* 핸들을 호출 하 여 **SQLGetDiagRec를** 가져올 수 있습니다. 다음 표에서는 **SQLColumns에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서* 커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션의 리소스 교착 상태 때문에 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *스키마Name*, *TableName*또는 *ColumnName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLColumns** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 카탈로그 또는 이름의 최대 길이 값을 초과했습니다. 각 카탈로그 또는 이름의 최대 *길이는 InfoType* 값으로 **SQLGetInfo를** 호출하여 가져올 수 있습니다. ("댓글"참조))|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|카탈로그 이름이 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 스키마 이름이 지정되었으며 드라이버 또는 데이터 원본은 스키마를 지원하지 않습니다.<br /><br /> 스키마 이름, 테이블 이름 또는 열 이름에 대해 문자열 검색 패턴이 지정되었으며 데이터 원본은 이러한 인수 중 하나 이상에 대한 검색 패턴을 지원하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 일반적으로 문 실행 전에 데이터 원본 카탈로그에서 테이블 또는 테이블에 대한 열에 대한 정보를 검색하는 데 사용됩니다. **SQLColumns는** SQLTables 에서 반환되는 모든 유형의 항목에 대한 데이터를 검색하는 데 사용할 수 **있습니다.** 기본 테이블 외에도 보기, 동의어, 시스템 테이블 등이 포함될 수 있습니다(이에 국한되지 않음). 반대로 **SQLColAttribute** 및 **SQLDescribeCol** 함수는 결과 집합의 열을 설명하고 **SQLNumResultCols** 함수는 결과 집합의 열 수를 반환합니다. 자세한 내용은 [카탈로그 데이터 사용을](../../../odbc/reference/develop-app/uses-of-catalog-data.md)참조하십시오.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 **SQLColumns는** TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 ORDINAL_POSITION 따라 정렬된 표준 결과 집합으로 결과를 반환합니다.  
  
> [!NOTE]  
>  응용 프로그램이 ODBC 2와 함께 작동하는 경우. *결과* 집합에서 ORDINAL_POSITION 열이 반환되지 않습니다. 그 결과, ODBC 2로 작업할 때. *x* 드라이버, **SQLColumns에** 의해 반환 된 열 목록의 열 순서는 응용 프로그램이 해당 테이블의 모든 열에 SELECT 문을 수행할 때 반환 된 열의 순서와 반드시 동일 하지 않습니다.  
  
> [!NOTE]  
>  **SQLColumns가** 모든 열을 반환하지 않을 수 있습니다. 예를 들어 드라이버는 Oracle ROWID와 같은 의사 열에 대한 정보를 반환하지 않을 수 있습니다. 응용 프로그램은 **SQLColumns**에서 반환되는지 여부에 관계없이 유효한 열을 사용할 수 있습니다.  
>   
>  **SQLStatistics에서** 반환할 수 있는 일부 열은 **SQLColumns**에서 반환되지 않습니다. 예를 들어 **SQLColumns는** 급여 + 혜택 또는 DEPT = 0012와 같은 식 또는 필터를 통해 만든 인덱스의 열을 반환하지 않습니다.  
  
 VARCHAR 열의 길이는 표에 표시되지 않습니다. 실제 길이는 데이터 원본에 따라 다릅니다. TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.  
  
 ODBC 3의 경우 다음 열의 이름이 변경되었습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 ODBC 3에 대해 **SQLColumns에서** 반환된 결과 집합에 다음 열이 추가되었습니다. *x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 18(IS_NULLABLE)을 초과하는 추가 열은 드라이버에 의해 정의될 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 대한 액세스 권한을 얻어야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열<br /><br /> number|데이터 형식|주석|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|카탈로그 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에는 지원하지 않는 경우 카탈로그가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|스키마 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 스키마가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_NAME (ODBC 1.0)|3|바르카르 는 NULL이 아닙니다.|테이블 이름입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|바르카르 는 NULL이 아닙니다.|열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|5|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. datetime 및 간격 데이터 형식의 경우 이 열은 간결한 데이터 형식(예: SQL_DATETIME 또는 SQL_INTERVAL 같은 간결한 데이터 형식 대신 SQL_TYPE_DATE 또는 SQL_INTERVAL_YEAR_TO_MONTH)을 반환합니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 [형식의 SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md) 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.<br /><br /> ODBC 3에 대해 반환된 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램이 다를 수 있습니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.|  
|TYPE_NAME (ODBC 1.0)|6|바르카르 는 NULL이 아닙니다.|데이터 원본 종속 데이터 형식 이름; 예를 들어 , "CHAR", "VARCHAR", "돈", "긴 VARBINAR", 또는 "CHAR () 비트 데이터".|  
|COLUMN_SIZE (ODBC 1.0)|7|정수|DATA_TYPE SQL_CHAR 또는 SQL_VARCHAR 경우 이 열에는 열문자의 최대 길이가 포함됩니다. datetime 데이터 형식의 경우 문자로 변환될 때 값을 표시하는 데 필요한 총 문자 수입니다. 숫자 데이터 형식의 경우 NUM_PREC_RADIX 열에 따라 총 자릿수 또는 열에 허용되는 총 비트 수입니다. 간격 데이터 형식의 경우 간격 리터럴의 문자 표현에 있는 문자 수입니다(정밀도를 선도하는 간격으로 정의된 대로 부록 D: 데이터 형식의 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md) 참조). 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|BUFFER_LENGTH (ODBC 1.0)|8|정수|SQL_C_DEFAULT 지정된 경우 SQLGetData, SQLFetch 또는 SQLFetch스크롤 작업에서 전송되는 데이터의 바이트 길이입니다. 숫자 데이터의 경우 이 크기는 데이터 원본에 저장된 데이터의 크기와 다를 수 있습니다. 이 값은 문자 데이터에 대한 COLUMN_SIZE 열과 다를 수 있습니다. 길이에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|소수점 오른쪽에 있는 중요한 자릿수입니다. SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP 경우 이 열에는 소수 초 구성 요소의 숫자 수가 포함됩니다. 다른 데이터 형식의 경우 데이터 원본에 있는 열의 소수 자릿수입니다. 시간 구성 요소가 포함된 간격 데이터 형식의 경우 이 열에는 소수점 오른쪽에 있는 숫자 수(소수점 초)가 포함됩니다. 시간 구성 요소가 포함되지 않은 간격 데이터 형식의 경우 이 열은 0입니다. 소수 자릿수에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오. DECIMAL_DIGITS 적용되지 않는 데이터 형식에 대해 NULL이 반환됩니다.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|숫자 데이터 형식의 경우 10 또는 2입니다. 10이면 COLUMN_SIZE DECIMAL_DIGITS 값은 열에 허용되는 소수 자릿수를 지정합니다. 예를 들어 DECIMAL(12,5) 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 12, DECIMAL_DIGITS 반환합니다. FLOAT 열은 NUM_PREC_RADIX 10, COLUMN_SIZE 15 및 null DECIMAL_DIGITS 반환할 수 있습니다.<br /><br /> 2이면 COLUMN_SIZE 및 DECIMAL_DIGITS 값은 열에 허용되는 비트 수를 지정합니다. 예를 들어 FLOAT 열은 RADIX 2, COLUMN_SIZE 53 및 null DECIMAL_DIGITS 반환할 수 있습니다.<br /><br /> null은 NUM_PREC_RADIX 적용할 수 없는 데이터 형식에 대해 반환됩니다.|  
|널수(ODBC 1.0)|11|NULL이 아닌 Smallint|열에 NULL 값을 포함할 수 없는 경우 SQL_NO_NULLS.<br /><br /> 열이 NULL 값을 허용하는지 SQL_NULLABLE.<br /><br /> 열이 NULL 값을 허용하는지 여부를 알 수 없는 경우 SQL_NULLABLE_UNKNOWN.<br /><br /> 이 열에 대해 반환된 값은 IS_NULLABLE 열에 대해 반환된 값과 다릅니다. NULLABLE 열은 열이 NUL을 수락할 수 있지만 열이 NUL을 허용하지 않음을 확실하게 나타낼 수 없음을 나타냅니다. IS_NULLABLE 열은 열이 NUL을 수락할 수 없지만 열이 NUL을 수락한다는 것을 확실하게 나타낼 수 없음을 나타냅니다.|  
|비고(ODBC 1.0)|12|Varchar|열에 대한 설명입니다.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|열의 기본값입니다. 이 열의 값은 따옴표로 둘러싸인 경우 문자열로 해석되어야 합니다.<br /><br /> NULL을 기본값으로 지정한 경우 이 열은 따옴표로 묶이지 않는 NULL이라는 단어입니다. 기본값을 잘리지 않고 나타낼 수 없는 경우 이 열에는 단일 따옴표를 포함하지 않고 TRUNCATED가 포함됩니다. 기본값을 지정하지 않은 경우 이 열은 NULL입니다.<br /><br /> COLUMN_DEF 값은 TRUNCATED 값을 포함하는 경우를 제외하고 새 열 정의를 생성하는 데 사용할 수 있습니다.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|NULL이 아닌 Smallint|SQL 데이터 형식은 IRD의 SQL_DESC_TYPE 레코드 필드에 나타납니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. 이 열은 날짜 시간 및 간격 데이터 형식을 제외한 DATA_TYPE 열과 동일합니다. 이 열은 날짜 시간 및 간격 데이터 형식에 대한 간결한 데이터 형식(예: SQL_TYPE_DATE 또는 SQL_INTERVAL_YEAR_TO_MONTH)대신 간결하지 않은 데이터 형식(예: SQL_DATETIME 또는 SQL_INTERVAL)을 반환합니다. 이 열이 SQL_DATETIME 또는 SQL_INTERVAL 반환하는 경우 SQL_DATETIME_SUB 열에서 특정 데이터 형식을 확인할 수 있습니다. 유효한 ODBC SQL 데이터 형식 목록은 부록 D: 데이터 [형식의 SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md) 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.<br /><br /> ODBC 3에 대해 반환된 데이터 형식입니다. *x* 및 ODBC 2. *x* 응용 프로그램이 다를 수 있습니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|datetime 및 간격 데이터 형식에 대한 하위 유형 코드입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다. 날짜 시간 및 간격 하위 코드에 대한 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)"SQL_DESC_DATETIME_INTERVAL_CODE"을 참조하십시오.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|정수|문자 또는 이진 데이터 형식 열의 바이트별 최대 길이입니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다.|  
|ORDINAL_POSITION (ODBC 3.0)|17|NULL이 아닌 Integer|테이블에 있는 열의 서수 위치입니다. 테이블의 첫 번째 열은 숫자 1입니다.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|열에 NULL이 포함되어 있지 않은 경우 "NO"입니다.<br /><br /> 열에 눌루를 포함할 수 있는 경우 "YES"입니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> 이 열에 대해 반환된 값은 NULLABLE 열에 대해 반환된 값과 다릅니다. NULLABLE 열에 대한 설명을 참조하십시오.|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 SQLColumns에서 반환하는 결과 집합에 대한 **버퍼를 선언합니다.** EMPLOYEE 테이블의 각 열을 설명하는 결과 집합을 반환하기 위해 **SQLColumns를 호출합니다.** 그런 다음 **SQLBindCol을** 호출하여 결과 집합의 열을 버퍼에 바인딩합니다. 마지막으로 응용 프로그램은 **SQLFetch를** 사용하여 데이터의 각 행을 가져와 처리합니다.  
  
```cpp  
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
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|열 또는 열에 대한 권한 반환|[SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|행을 고유하게 식별하는 열 또는 트랜잭션에 의해 자동으로 업데이트되는 열 반환|[SQLSpecialColumns 함수](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|데이터 원본의 테이블 목록 반환|[SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)|  
|테이블 또는 테이블에 대한 권한 반환|[SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
