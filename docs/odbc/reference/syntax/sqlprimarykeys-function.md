---
title: SQL프라이어 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrimaryKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrimaryKeys
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC]
ms.assetid: 3f809b09-3c1b-415e-80c5-a603e8e25d5b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24407670ab9f1489a14bec19d910060b49d4bda0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306868"
---
# <a name="sqlprimarykeys-function"></a>SQLPrimaryKeys 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLPrimaryKeys는** 테이블의 기본 키를 구성하는 열 이름을 반환합니다. 드라이버는 결과 집합으로 정보를 반환합니다. 이 함수는 단일 호출에서 여러 테이블에서 기본 키를 반환하는 것을 지원하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPrimaryKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *카탈로그 이름*  
 [입력] 카탈로그 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에 는 지원하지 않는 경우 빈 문자열("")은 카탈로그가 없는 테이블을 나타냅니다. *카탈로그Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *CatalogName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE 경우 *CatalogName은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요합니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 *NameLength1*  
 [입력] **카탈로그 이름의*문자 길이 .  
  
 *스키마 이름*  
 [입력] 스키마 이름입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 빈 문자열("")은 스키마가 없는 테이블을 나타냅니다. *스키마Name* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *SchemaName은* 식별자로 처리되고 해당 경우는 중요하지 않습니다. SQL_FALSE 경우 *스키마이름은* 일반적인 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요하지 않습니다.  
  
 *이름 길이2*  
 [입력] **스키마 이름의*문자 길이입니다.  
  
 *Tablename*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터가 될 수 없습니다. *TableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 *TableName은* 식별자로 처리되고 해당 사례는 중요하지 않습니다. SQL_FALSE *경우 TableName은* 일반 인수입니다. 그것은 문자 그대로 처리되며, 그 경우는 중요하지 않습니다.  
  
 *이름 길이3*  
 [입력] **테이블 네임의*문자 길이 .  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLPrimaryKeys가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLPrimaryKeys에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|(DM) *명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll가** 호출되었습니다.<br /><br /> *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) *TableName* 인수는 null 포인터였습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성은 SQL_TRUE *설정되었으며, CatalogName* 인수는 null 포인터이고, **sqlGetInfo는** SQL_CATALOG_NAME 정보 형식이 카탈로그 이름이 지원되는 반환을 반환합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정되었으며 *SchemaName* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLPrimaryKeys** 함수가 호출될 때 이 비동기 함수가 계속 실행되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 이름 길이 인수 중 하나의 값은 0보다 작지만 SQL_NTS 같지 않으며 연결된 이름 인수는 null 포인터가 아닙니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 이름의 최대 길이 값을 초과했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|카탈로그가 지정되었으며 드라이버 또는 데이터 원본은 카탈로그를 지원하지 않습니다.<br /><br /> 스키마가 지정되었으며 드라이버 또는 데이터 원본이 스키마를 지원하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 요청된 결과 집합을 반환하기 전에 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLPrimaryKeys는** TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 KEY_SEQ 따라 정렬된 표준 결과 집합으로 결과를 반환합니다. 이 정보를 사용하는 방법에 대한 자세한 내용은 [카탈로그 데이터 사용을](../../../odbc/reference/develop-app/uses-of-catalog-data.md)참조하십시오.  
  
 ODBC 3의 경우 다음 열의 이름이 변경되었습니다. *x*. 열 이름 변경은 응용 프로그램이 열 번호로 바인딩되므로 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3. *x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 확인하려면 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용하여 **SQLGetInfo를** 호출합니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환된 데이터에 대한 자세한 내용은 [카탈로그 함수 를](../../../odbc/reference/develop-app/catalog-functions.md)참조하십시오.  
  
 다음 표에는 결과 집합의 열이 나열됩니다. 열 6(PK_NAME)을 초과하는 추가 열은 드라이버가 정의할 수 있습니다. 응용 프로그램은 명시적 서수 위치를 지정하는 대신 결과 집합의 끝에서 카운트다운하여 드라이버 별 열에 액세스해야 합니다. 자세한 내용은 [카탈로그 함수에서 반환되는 데이터를](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)참조하십시오.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|기본 키 테이블 카탈로그 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 카탈로그를 지원하지만 다른 테이블에는 지원하지 않는 경우 카탈로그가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|기본 키 테이블 스키마 이름; 데이터 원본에 적용되지 않는 경우 NULL입니다. 드라이버가 다른 DBMS에서 데이터를 검색할 때와 같이 일부 테이블에 대한 스키마를 지원하지만 다른 테이블에는 지원하지 않는 경우 스키마가 없는 테이블에 대해 빈 문자열("")을 반환합니다.|  
|TABLE_NAME (ODBC 1.0)|3|바르카르 는 NULL이 아닙니다.|기본 키 테이블 이름입니다.|  
|COLUMN_NAME (ODBC 1.0)|4|바르카르 는 NULL이 아닙니다.|기본 키 열 이름입니다. 드라이버는 이름이 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|KEY_SEQ (ODBC 1.0)|5|NULL이 아닌 Smallint|키의 열 시퀀스 번호(1로 시작).|  
|PK_NAME (ODBC 2.0)|6|Varchar|기본 키 이름입니다. 데이터 원본에 적용되지 않는 경우 NULL입니다.|  
  
## <a name="code-example"></a>코드 예  
 [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|외래 키의 열 반환|[SQLForeignKeys 함수](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
