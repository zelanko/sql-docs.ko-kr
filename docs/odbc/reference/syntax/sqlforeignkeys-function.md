---
title: SQLForeignKeys 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285863"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLForeignKeys는** 다음을 반환할 수 있습니다.  
  
-   지정된 테이블의 외래 키 목록입니다(다른 테이블의 기본 키를 참조하는 지정된 테이블의 열).  
  
-   지정된 테이블의 기본 키를 참조하는 다른 테이블의 외래 키 목록입니다.  
  
 드라이버는 지정된 문에 설정된 결과로 각 목록을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *PK카탈로그 이름*  
 [입력] 기본 키 테이블 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *PKCatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *PKCatalogName은* 식별자로 처리되고 해당 케이스는 중요하지 않습니다. SQL_FALSE *경우 PKCatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] 문자에서 **PKCatalogName의*길이입니다.  
  
 *PKSchemaName*  
 [입력] 기본 키 테이블 스키마 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다. *PKSchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *PKSchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *PKSchemaName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이2*  
 [입력] 길이 **PKSchemaName,* 문자.  
  
 *PK테이블 이름*  
 [입력] 기본 키 테이블 이름입니다. *PKTableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *PKTableName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE *경우 PKTableName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이3*  
 [입력] 문자 **PKTableName의*길이입니다.  
  
 *FK카탈로그 이름*  
 [입력] 외래 키 테이블 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *FKCatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되면 *FKCatalogName은* 식별자로 처리되고 해당 케이스는 중요하지 않습니다. SQL_FALSE 경우 *FKCatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이4*  
 [입력] **FKCatalogName의*길이, 문자.  
  
 *FKSchemaName*  
 [입력] 외래 키 테이블 스키마 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다. *FKSchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *FKSchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *FKSchemaName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름 길이5*  
 [입력] 길이 **FKSchemaName,* 문자.  
  
 *FK테이블 네임*  
 [입력] 외래 키 테이블 이름입니다. *FKTableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *FKTableName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *FKTableName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다.  
  
 *이름길이6*  
 [입력] **FKTableName의*길이, 문자.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLForeignKeys** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLForeignKeys에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll이** 호출되었습니다. **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션의 리소스 교착 상태 때문에 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle에서*호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) 인수 *PKTableName* 및 *FKTableName은* 모두 null 포인터였습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE 설정되었으며, *FKCatalogName* 또는 *PKCatalogName* 인수는 null 포인터이며 SQL_CATALOG_NAME *InfoType은* 카탈로그 이름이 지원되는 것을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *FKSchemaName,* *PKSchemaName,* *FKTableName*또는 *PKTableName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 SQLForeignKeys 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 이름의 최대 길이 값을 초과했습니다. ("댓글"참조))|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|카탈로그 이름이 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 스키마 이름이 지정되었으며 드라이버 또는 데이터 원본은 스키마를 지원하지 않습니다.|  
|||SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수에서 반환되는 정보를 사용하는 방법에 대한 자세한 내용은 [카탈로그 데이터 사용을](../../../odbc/reference/develop-app/uses-of-catalog-data.md)참조하십시오.  
  
 \* *PKTableName* 테이블 이름이 포함 된 경우 **SQLForeignKeys** 지정 된 테이블의 기본 키와 참조 하는 모든 외부 키를 포함 하는 결과 집합을 반환 합니다. 다른 테이블의 외래 키 목록에는 지정된 테이블의 고유한 제약 조건을 가리키는 외래 키가 포함되지 않습니다.  
  
 \* *FKTableName에* 테이블 이름이 포함된 경우 **SQLForeignKeys는** 다른 테이블의 기본 키를 가리키는 지정된 테이블의 모든 외래 키와 참조하는 다른 테이블의 기본 키를 포함하는 결과 집합을 반환합니다. 지정된 테이블의 외래 키 목록에는 다른 테이블의 고유한 제약 조건을 참조하는 외래 키가 포함되어 있지 않습니다.  
  
 \* *PKTableName* 및 \* *FKTableName* 모두 테이블 이름을 포함하는 경우 **SQLForeignKeys는** \***PKTableName에*지정된 테이블의 기본 키를 참조하는 *FKTableName에* 지정된 테이블의 외래 키를 반환합니다. 이것은 하나의 키여야 합니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 **SQLForeignKeys는** 결과를 표준 결과 집합으로 반환합니다. 기본 키와 연결된 외래 키가 요청되면 결과 집합은 FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME 및 KEY_SEQ 의해 정렬됩니다. 외래 키와 연결된 기본 키가 요청되면 결과 집합은 PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME 및 KEY_SEQ 의해 정렬됩니다. 다음 표에는 결과 집합의 열이 나열됩니다.  
  
 VARCHAR 열의 길이는 표에 표시되지 않습니다. 실제 길이는 데이터 원본에 따라 다릅니다. PKTABLE_CAT 또는 FKTABLE_CAT, PKTABLE_SCHEM 또는 FKTABLE_SCHEM, PKTABLE_NAME 또는 FKTABLE_NAME 및 PKCOLUMN_NAME 또는 FKCOLUMN_NAME 열의 실제 길이를 결정하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.  
  
 ODBC 3 *.x의* 경우 다음 열의 이름이 변경되었습니다. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 14(REMARKS)를 초과하는 추가 열은 드라이버가 정의할 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 대한 액세스 권한을 얻어야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|기본 키 테이블 카탈로그 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에는 지원하지 않는 경우 카탈로그가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|기본 키 테이블 스키마 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 스키마가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|PKTABLE_NAME (ODBC 1.0)|3|바르카르 는 NULL이 아닙니다.|기본 키 테이블 이름입니다.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|바르카르 는 NULL이 아닙니다.|기본 키 열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|외래 키 테이블 카탈로그 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에는 지원하지 않는 경우 카탈로그가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|외래 키 테이블 스키마 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 스키마가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|FKTABLE_NAME (ODBC 1.0)|7|바르카르 는 NULL이 아닙니다.|외래 키 테이블 이름입니다.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|바르카르 는 NULL이 아닙니다.|외래 키 열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|KEY_SEQ (ODBC 1.0)|9|NULL이 아닌 Smallint|키의 열 시퀀스 번호(1로 시작).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL 작업이 **UPDATE일**때 외래 키에 적용할 작업입니다. 다음 값 중 하나를 가질 수 있습니다. 참조된 테이블은 기본 키가 있는 테이블이며 참조 테이블은 외래 키가 있는 테이블입니다.<br /><br /> SQL_CASCADE: 참조된 테이블의 기본 키가 업데이트되면 참조 테이블의 외래 키도 업데이트됩니다.<br /><br /> SQL_NO_ACTION: 참조된 테이블의 기본 키를 업데이트하면 참조 테이블에서 "매달려 있는 참조"가 발생하면(즉, 참조 테이블의 행에는 참조 테이블에 해당 테이블이 없는 경우) 업데이트가 거부됩니다. 참조 테이블의 외래 키를 업데이트하면 참조된 테이블의 기본 키 값으로 존재하지 않는 값이 발생하면 업데이트가 거부됩니다. (이 작업은 ODBC 2 *.x.x의*SQL_RESTRICT 동작과 동일합니다.)<br /><br /> SQL_SET_NULL: 참조된 테이블의 하나 이상의 행이 주 키의 하나 이상의 구성 요소를 변경하는 방식으로 업데이트되면 기본 키의 변경된 구성 요소에 해당하는 참조 테이블의 외래 키 구성 요소가 참조 테이블의 모든 일치하는 행에서 NULL로 설정됩니다.<br /><br /> SQL_SET_DEFAULT: 참조된 테이블의 하나 이상의 행이 주 키의 하나 이상의 구성 요소를 변경하는 방식으로 업데이트되는 경우 기본 키의 변경된 구성 요소에 해당하는 참조 테이블의 외래 키 구성 요소는 참조 테이블의 모든 일치하는 행에서 적용 가능한 기본값으로 설정됩니다.<br /><br /> 데이터 원본에 적용되지 않는 경우 NULL입니다.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL 작업이 **DELETE일**때 외래 키에 적용할 작업입니다. 다음 값 중 하나를 가질 수 있습니다. 참조된 테이블은 기본 키가 있는 테이블이며 참조 테이블은 외래 키가 있는 테이블입니다.<br /><br /> SQL_CASCADE: 참조된 테이블의 행이 삭제되면 참조 테이블의 일치하는 모든 행도 삭제됩니다.<br /><br /> SQL_NO_ACTION: 참조된 테이블의 행을 삭제하면 참조 테이블에서 "매달려 있는 참조"가 발생하면(즉, 참조 테이블의 행에는 참조 테이블에 해당 테이블이 없음) 업데이트가 거부됩니다. (이 작업은 ODBC 2 *.x.x의*SQL_RESTRICT 동작과 동일합니다.)<br /><br /> SQL_SET_NULL: 참조된 테이블의 하나 이상의 행이 삭제되면 참조 테이블의 외래 키의 각 구성 요소가 참조 테이블의 일치하는 모든 행에서 NULL로 설정됩니다.<br /><br /> SQL_SET_DEFAULT: 참조된 테이블의 하나 이상의 행이 삭제되면 참조 테이블의 외래 키의 각 구성 요소가 참조 테이블의 모든 일치하는 행에서 적용 가능한 기본값으로 설정됩니다.<br /><br /> 데이터 원본에 적용되지 않는 경우 NULL입니다.|  
|FK_NAME (ODBC 2.0)|12|Varchar|외래 키 이름입니다. 데이터 원본에 적용되지 않는 경우 NULL입니다.|  
|PK_NAME (ODBC 2.0)|13|Varchar|기본 키 이름입니다. 데이터 원본에 적용되지 않는 경우 NULL입니다.|  
|추론성 (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>코드 예  
 다음 표에 설명된 대로 이 예제에서는 ORDERS, LINES 및 CUSTOMERS라는 세 개의 테이블을 사용합니다.  
  
|ORDERS|라인|고객|  
|------------|-----------|---------------|  
|Orderid|Orderid|CUSTID|  
|CUSTID|라인|NAME|  
|오픈 데이트|파르티드 ()파르티드|주소|  
|영업 사원|수량|전화|  
|상태|||  
  
 ORDERS 테이블에서 CUSTID는 판매가 이루어진 고객을 식별합니다. 고객 테이블에서 CUSTID를 참조하는 외래 키입니다.  
  
 LINES 테이블에서 ORDERID는 광고 항목이 연결된 판매 순서를 식별합니다. ORDERS 테이블에서 ORDERID를 참조하는 외부 키입니다.  
  
 이 예제는 ORDERS 테이블의 기본 키를 얻기 위해 **SQLPrimaryKeys를** 호출합니다. 결과 집합에는 하나의 행이 있습니다. 중요한 열은 다음 표에 나와 있습니다.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|Orderid|1|  
  
 그런 다음 이 예제에서는 **SQLForeignKeys를** 호출하여 ORDERS 테이블의 기본 키를 참조하는 다른 테이블의 외래 키를 가져옵니다. 결과 집합에는 하나의 행이 있습니다. 중요한 열은 다음 표에 나와 있습니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|라인|CUSTID|1|  
  
 마지막으로 이 예제에서는 **SQLForeignKeys를** 호출하여 다른 테이블의 기본 키를 참조하는 ORDERS 테이블의 외래 키를 가져옵니다. 결과 집합에는 하나의 행이 있습니다. 중요한 열은 다음 표에 나와 있습니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|고객|CUSTID|ORDERS|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키의 열 반환|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
