---
title: SQL스페셜칼럼 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287173"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: 개방형 그룹  
  
 **요약**  
 **SQLSpecialColumns는** 지정된 테이블 내의 열에 대한 다음 정보를 검색합니다.  
  
-   테이블의 행을 고유하게 식별하는 최적의 열 집합입니다.  
  
-   행의 값이 트랜잭션에 의해 업데이트될 때 자동으로 업데이트되는 열입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *식별자 유형*  
 [입력] 반환할 열의 유형입니다. 다음 값 중 하나여야 합니다.  
  
 SQL_BEST_ROWID: 열 또는 열에서 값을 검색하여 지정된 테이블의 행을 고유하게 식별할 수 있는 최적의 열 또는 열 집합을 반환합니다. 열은 이러한 목적을 위해 특별히 설계된 의사 열(Oracle ROWID 또는 Ingres TID에서와 같이) 또는 테이블에 대한 고유한 인덱스의 열 또는 열일 수 있습니다.  
  
 SQL_ROWVER: 행의 값이 트랜잭션에 의해 업데이트될 때 데이터 원본에 의해 자동으로 업데이트되는 지정된 테이블(있는 경우)의 열 또는 열을 반환합니다(SQLBase ROWID 또는 Sybase TIMESTAMP).  
  
 *카탈로그 이름*  
 [입력] 테이블의 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *CatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] **카탈로그 이름의*문자 길이 .  
  
 *스키마 이름*  
 [입력] 테이블의 스키마 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다. *스키마Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *SchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *스키마이름은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이2*  
 [입력] **스키마 이름의*문자 길이입니다.  
  
 *Tablename*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터가 될 수 없습니다. *TableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *TableName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE *경우 TableName은* 일반 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이3*  
 [입력] **테이블 네임의*문자 길이 .  
  
 *범위*  
 [입력] rowid의 최소 필수 범위입니다. 반환된 rowid는 더 큰 범위일 수 있습니다. 다음 중 하나여야 합니다.  
  
 SQL_SCOPE_CURROW: rowid는 해당 행에 위치하는 동안에만 유효합니다. rowid를 사용하여 나중에 다시 선택하면 행이 다른 트랜잭션에 의해 업데이트되거나 삭제된 경우 행이 반환되지 않을 수 있습니다.  
  
 SQL_SCOPE_TRANSACTION: rowid는 현재 트랜잭션 의 기간 동안 유효합니다.  
  
 SQL_SCOPE_SESSION: rowid는 세션 기간(트랜잭션 경계를 넘어)에 대해 유효하도록 보장됩니다.  
  
 *Null 허용*  
 [입력] NULL 값을 가질 수 있는 특수 열을 반환할지 여부를 결정합니다. 다음 중 하나여야 합니다.  
  
 SQL_NO_NULLS: NULL 값을 가질 수 있는 특수 열을 제외합니다. 일부 드라이버는 SQL_NO_NULLS 지원할 수 없으며 이러한 드라이버는 SQL_NO_NULLS 지정된 경우 빈 결과 집합을 반환합니다. 응용 프로그램은이 경우에 대비하고 절대적으로 필요한 경우에만 SQL_NO_NULLS 요청해야합니다.  
  
 SQL_NULLABLE: NULL 값을 가질 수 있는 경우에도 특수 열을 반환합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSpecialColumns** SQL_ERROR 반환 하거나 SQL_SUCCESS_WITH_INFO 경우 관련 된 SQLSTATE 값 핸들 SQL_HANDLE_STMT *핸들* *핸들*핸들을 *Handle* 호출 하 여 **SQLGetDiagRec를** 가져올 수 있습니다. 다음 표에서는 **SQLSpecialColumns에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 **및 SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|*TableName* 인수는 null 포인터였습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *SchemaName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLSpecialColumns가** 호출될 때 이 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 는 않습니다.<br /><br /> 길이 인수 중 하나의 값이 해당 이름의 최대 길이 값을 초과했습니다. 각 이름의 최대 길이는 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN 또는 SQL_MAX_TABLE_NAME_LEN *인InfoType* 값으로 **SQLGetInfo를** 호출하여 가져올 수 있습니다.|  
|HY097|범위를 벗어난 열 유형|(DM) 잘못된 *식별자 Type* 값이 지정되었습니다.|  
|HY098|범위를 벗어난 범위 유형|(DM) 잘못된 *범위* 값이 지정되었습니다.|  
|HY099|범위를 벗어난 Null 형식|(DM) 유효하지 않은 *Nullable* 값이 지정되었습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|카탈로그가 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 스키마가 지정되었으며 드라이버 또는 데이터 원본이 스키마를 지원하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 요청된 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 *IdentifierType* 인수가 SQL_BEST_ROWID **SQLSpecialColumns는** 테이블의 각 행을 고유하게 식별하는 열이나 열을 반환합니다. 이러한 열은 항상 선택 *목록* 또는 **WHERE** 절에서 사용할 수 있습니다. 테이블의 열에 대한 다양한 정보를 반환하는 데 사용되는 **SQLColumns는**각 행을 고유하게 식별하는 열이나 트랜잭션에 의해 행의 값이 업데이트될 때 자동으로 업데이트되는 열을 반드시 반환하지는 않습니다. 예를 들어 **SQLColumns는** Oracle 의사 열 ROWID를 반환하지 않을 수 있습니다. **SQLSpecialColumns가** 이러한 열을 반환하는 데 사용되는 이유입니다. 자세한 내용은 [카탈로그 데이터 사용을](../../../odbc/reference/develop-app/uses-of-catalog-data.md)참조하십시오.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 테이블의 각 행을 고유하게 식별하는 열이 없는 경우 **SQLSpecialColumns는** 행이 없는 행 집합을 반환합니다. SQLFetch 또는 **SQLFetch** **SQLFetchScroll에** 대 한 후속 호출 문에 SQL_NO_DATA 반환 합니다.  
  
 *IdentifierType*, *Scope*또는 *Nullable* 인수가 데이터 원본에서 지원되지 않는 특성을 지정하는 경우 **SQLSpecialColumns는** 빈 결과 집합을 반환합니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName*, *SchemaName*및 *TableName* 인수는 식별자로 처리되므로 특정 상황에서는 null 포인터로 설정할 수 없습니다. (자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.)  
  
 **SQLSpecialColumns는** SCOPE에 의해 정렬된 표준 결과 집합으로 결과를 반환합니다.  
  
 ODBC *3.x에*대해 다음 열의 이름이 변경되었습니다. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC *3.x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 COLUMN_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_COLUMN_NAME_LEN 옵션으로 **SQLGetInfo를** 호출할 수 있습니다.  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 8(PSEUDO_COLUMN) 이외의 추가 열은 드라이버가 정의할 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|범위(ODBC 1.0)|1|Smallint|rowid의 실제 범위입니다. 다음 값 중 하나를 포함합니다.<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> *식별자Type이* SQL_ROWVER 때 NULL이 반환됩니다. 각 값에 대한 설명은 이 섹션의 "구문"의 *범위* 설명을 참조하십시오.|  
|COLUMN_NAME (ODBC 1.0)|2|바르카르 는 NULL이 아닙니다.|열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|3|NULL이 아닌 Smallint|SQL 데이터 형식입니다. ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식일 수 있습니다. 유효한 ODBC SQL 데이터 형식 목록은 [SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md)참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.|  
|TYPE_NAME (ODBC 1.0)|4|바르카르 는 NULL이 아닙니다.|데이터 원본 종속 데이터 형식 이름; 예를 들어 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR ()에 대한 비트 데이터"를 예로 들 수 있습니다.|  
|COLUMN_SIZE (ODBC 1.0)|5|정수|데이터 원본의 열 크기입니다. 열 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 옥텟 전사 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.|  
|BUFFER_LENGTH (ODBC 1.0)|6|정수|SQL_C_DEFAULT 지정된 경우 **SQLGetData** 또는 **SQLFetch** 작업에서 전송되는 데이터의 바이트 길이입니다. 숫자 데이터의 경우 이 크기는 데이터 원본에 저장된 데이터의 크기와 다를 수 있습니다. 이 값은 문자 또는 이진 데이터에 대한 COLUMN_SIZE 열과 동일합니다. 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|데이터 원본에 있는 열의 소수 자릿수입니다. 소수 자릿수를 적용할 수 없는 데이터 형식에 대해 NULL이 반환됩니다. 소수 자릿수에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|열이 Oracle ROWID와 같은 의사 열인지 여부를 나타냅니다.<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **참고:** 최대 상호 운용성을 위해 의사 열은 **SQLGetInfo**에서 반환된 식별자 따옴표 문자로 인용해서는 안 됩니다.|  
  
 응용 프로그램이 SQL_BEST_ROWID 대한 값을 검색한 후 응용 프로그램은 이러한 값을 사용하여 정의된 범위 내에서 해당 행을 다시 선택할 수 있습니다. **SELECT** 문은 행이나 행 이 없음또는 하나의 행을 반환하도록 보장됩니다.  
  
 응용 프로그램이 rowid 열 또는 열을 기반으로 행을 다시 선택하고 행을 찾을 수 없는 경우 응용 프로그램은 행이 삭제되었거나 rowid 열이 수정되었다고 가정할 수 있습니다. 그 반대의 경우도 마찬가지입니다: rowid가 변경되지 않은 경우에도 행의 다른 열이 변경되었을 수 있습니다.  
  
 열 유형 SQL_BEST_ROWID 반환되는 열은 행 집합에서 가장 최근 데이터를 검색하기 위해 결과 집합 내에서 앞뒤로 스크롤해야 하는 응용 프로그램에 유용합니다. rowid의 열 또는 열은 해당 행에 위치하는 동안 변경되지 않도록 보장됩니다.  
  
 rowid의 열이나 열은 커서가 행에 배치되지 않은 경우에도 유효할 수 있습니다. 응용 프로그램은 결과 집합에서 SCOPE 열을 확인하여 이를 확인할 수 있습니다.  
  
 열 유형에 대해 반환되는 열 SQL_ROWVER rowid를 사용하여 행을 다시 선택한 동안 지정된 행의 열이 업데이트되었는지 여부를 확인하는 기능이 필요한 응용 프로그램에 유용합니다. 예를 들어 rowid를 사용하여 행을 다시 선택한 후 응용 프로그램은 SQL_ROWVER 열의 이전 값을 방금 가져온 값과 비교할 수 있습니다. SQL_ROWVER 열의 값이 이전 값과 다른 경우 응용 프로그램은 디스플레이의 데이터가 변경되었음을 사용자에게 알릴 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제는 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블 또는 테이블의 열 반환|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키의 열 반환|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
