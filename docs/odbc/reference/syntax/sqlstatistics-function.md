---
title: SQLStatistics 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302947"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLStatistics** 는 단일 테이블 및 테이블과 연결 된 인덱스에 대 한 통계 목록을 검색 합니다. 드라이버는 정보를 결과 집합으로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *CatalogName*  
 입력 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서는 카탈로그를 지원 하지 않는 경우 빈 문자열 ("")에는 카탈로그가 없는 테이블이 표시 됩니다. *CatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *CatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *CatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **CatalogName*의 문자 길이입니다.  
  
 *SchemaName*  
 입력 스키마 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")에는 스키마가 없는 테이블이 표시 됩니다. *SchemaName* 에는 문자열 검색 패턴을 사용할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *SchemaName* 은 식별자로 처리 되 고 대/소문자는 중요 하지 않습니다. SQL_FALSE 되는 경우 *SchemaName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **SchemaName*의 문자 길이입니다.  
  
 *TableName*  
 입력 테이블 이름입니다. 이 인수는 null 포인터 일 수 없습니다. *SchemaName* 에는 문자열 검색 패턴을 사용할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *TableName* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *TableName* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **TableName*의 문자 길이입니다.  
  
 *고유*  
 입력 인덱스 유형: SQL_INDEX_UNIQUE 또는 SQL_INDEX_ALL.  
  
 *Reserved*  
 입력 결과 집합에서 카디널리티 및 페이지 열의 중요도를 나타냅니다. 다음 옵션은 카디널리티 및 페이지 열을 반환 하는 경우에만 영향을 줍니다. 카디널리티 및 페이지가 반환 되지 않은 경우에도 인덱스 정보가 반환 됩니다.  
  
 SQL_ENSURE는 드라이버가 통계를 무조건 검색 하도록 요청 합니다. Open Group standard만 준수 하 고 ODBC 확장을 지원 하지 않는 드라이버는 SQL_ENSURE를 지원할 수 없습니다.  
  
 SQL_QUICK은 드라이버가 서버에서 쉽게 사용할 수 있는 경우에만 카디널리티 및 페이지를 검색 하도록 요청 합니다. 이 경우 드라이버는 값이 최신 값인지 확인하지 않습니다. Open Group standard에 작성 된 응용 프로그램은 항상 ODBC *3. x*호환 드라이버에서 SQL_QUICK 동작을 가져옵니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLStatistics** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLStatistics** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch 또는** **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고 **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|*TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *CatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 에서 해당 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *SchemaName* 인수가 null 포인터 였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLStatistics** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> 이름 길이 인수 중 하나의 값이 해당 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY100|고유성 옵션 형식이 범위를 벗어났습니다.|(DM) 잘못 된 *고유* 값이 지정 되었습니다.|  
|HY101|정확도 옵션 유형 범위를 벗어났습니다.|(DM) 잘못 된 *예약* 값이 지정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그가 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마가 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLStatistics** 는 단일 테이블에 대 한 정보를 NON_UNIQUE, 형식, INDEX_QUALIFIER, INDEX_NAME 및 ORDINAL_POSITION 기준으로 정렬 된 표준 결과 집합으로 반환 합니다. 결과 집합은 각 인덱스에 대 한 정보를 포함 하 여 테이블에 대 한 통계 정보 (결과 집합의 카디널리티 및 페이지 열)를 결합 합니다. 이 정보를 사용 하는 방법에 대 한 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
 TABLE_CAT, TABLE_SCHEM, TABLE_NAME 및 COLUMN_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 ODBC 3.x에 대해 다음 열의 이름이 바뀌었습니다 *.* 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC *3.x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 13 (FILTER_CONDITION)을 초과 하는 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 대 한 액세스 권한을 얻어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|통계 또는 인덱스가 적용 되는 테이블의 카탈로그 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|통계 또는 인덱스가 적용 되는 테이블의 스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|통계 또는 인덱스가 적용 되는 테이블의 이름입니다.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|인덱스에서 중복 값을 허용 하지 않는지 여부를 나타냅니다.<br /><br /> 인덱스 값이 고유 하지 않을 수 있는 경우 SQL_TRUE 합니다.<br /><br /> 인덱스 값이 고유 해야 하는 경우 SQL_FALSE 합니다.<br /><br /> 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|**DROP INDEX**를 수행 하는 인덱스 이름을 정규화 하는 데 사용 되는 식별자입니다. 인덱스 한정자가 데이터 소스에서 지원 되지 않거나 형식이 SQL_TABLE_STAT 경우 NULL이 반환 됩니다. 이 열에 null이 아닌 값이 반환 되는 경우이 값을 사용 하 여 **DROP INDEX** 문에서 인덱스 이름을 한정 해야 합니다. 그렇지 않으면 TABLE_SCHEM를 사용 하 여 인덱스 이름을 한정 해야 합니다.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|인덱스 이름 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|형식 (ODBC 1.0)|7|NULL이 아닌 Smallint|반환 되는 정보의 유형입니다.<br /><br /> SQL_TABLE_STAT는 카디널리티 또는 페이지 열에서 테이블에 대 한 통계를 나타냅니다.<br /><br /> SQL_INDEX_BTREE는 B-트리 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_CLUSTERED는 클러스터형 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_CONTENT 콘텐츠 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_HASHED는 해시 된 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_OTHER는 다른 인덱스 유형을 나타냅니다.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|인덱스의 열 시퀀스 번호 (1부터 시작) 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|열 이름입니다. 열이 급여 + 이점과 같은 식을 기반으로 하는 경우 식이 반환 됩니다. 식을 확인할 수 없으면 빈 문자열이 반환 됩니다. 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|열에 대 한 정렬 순서: "A" (오름차순) 내림차순의 경우 "D"입니다. 데이터 원본에서 열 정렬 시퀀스를 지원 하지 않거나 형식이 SQL_TABLE_STAT 경우 NULL이 반환 됩니다.|  
|카디널리티 (ODBC 1.0)|11|정수|테이블 또는 인덱스의 카디널리티입니다. 형식이 SQL_TABLE_STAT 경우 테이블의 행 수입니다. 형식이 SQL_TABLE_STAT 아닌 경우 인덱스에 있는 고유 값의 수입니다. 데이터 원본에서 값을 사용할 수 없으면 NULL이 반환 됩니다.|  
|페이지 (ODBC 1.0)|12|정수|인덱스 또는 테이블을 저장 하는 데 사용 되는 페이지 수입니다. 형식이 SQL_TABLE_STAT 경우 테이블에 대 한 페이지 수 형식이 SQL_TABLE_STAT 되지 않은 경우 인덱스의 페이지 수입니다. 데이터 원본에서 값을 사용할 수 없거나 데이터 원본에 적용할 수 없는 경우 NULL이 반환 됩니다.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|인덱스가 필터링 된 인덱스인 경우 급여 > 3만 등의 필터 조건입니다. 필터 조건을 확인할 수 없으면 빈 문자열입니다.<br /><br /> 인덱스가 필터링 된 인덱스가 아닌 경우 인덱스는 필터링 된 인덱스 인지 또는 형식이 SQL_TABLE_STAT 인지 여부를 확인할 수 없습니다.|  
  
 결과 집합의 행이 테이블에 해당 하는 경우 드라이버는 유형을 SQL_TABLE_STAT 설정 하 고 NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME 및 ASC_OR_DESC을 NULL로 설정 합니다. 데이터 원본에서 카디널리티 또는 페이지를 사용할 수 없는 경우 드라이버는이를 NULL로 설정 합니다.  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제는 [Sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록을 인출 합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|외래 키 열 반환|[SQLForeignKeys 함수](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|기본 키 열 반환|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
