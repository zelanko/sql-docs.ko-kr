---
title: SQLForeignKeys 함수 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285863"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLForeignKeys** 는 다음을 반환할 수 있습니다.  
  
-   지정 된 테이블의 외래 키 목록 (다른 테이블의 기본 키를 참조 하는 지정 된 테이블의 열)입니다.  
  
-   지정 된 테이블의 기본 키를 참조 하는 다른 테이블의 외래 키 목록입니다.  
  
 드라이버는 지정 된 문의 결과 집합으로 각 목록을 반환 합니다.  
  
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
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *PKCatalogName*  
 입력 기본 키 테이블 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지 원하는 경우 빈 문자열 ("")은 카탈로그가 없는 테이블을 나타냅니다. *PKCatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *PKCatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *PKCatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다. 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 *NameLength1*  
 입력 **PKCatalogName*의 길이 (문자)입니다.  
  
 *PKSchemaName*  
 입력 기본 키 테이블 스키마 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")은 스키마가 없는 테이블을 나타냅니다. *Pkschemaname* 은 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *Pkschemaname* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 되는 경우 *Pkschemaname* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength2*  
 입력 **Pkschemaname*의 길이 (문자)입니다.  
  
 *PKTableName*  
 입력 기본 키 테이블 이름입니다. *Pktablename* 은 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *Pktablename* 은 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 되는 경우 *Pktablename* 은 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength3*  
 입력 **Pktablename*의 길이 (문자)입니다.  
  
 *FKCatalogName*  
 입력 외래 키 테이블 카탈로그 이름입니다. 드라이버가 여러 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지 원하는 경우 빈 문자열 ("")은 카탈로그가 없는 테이블을 나타냅니다. *FKCatalogName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *FKCatalogName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *FKCatalogName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength4*  
 입력 **FKCatalogName*의 길이 (문자)입니다.  
  
 *FKSchemaName*  
 입력 외래 키 테이블 스키마 이름입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하 고 다른 Dbms에서 데이터를 검색 하는 경우 빈 문자열 ("")은 스키마가 없는 테이블을 나타냅니다. *FKSchemaName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *FKSchemaName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *FKSchemaName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength5*  
 입력 **FKSchemaName*의 길이 (문자)입니다.  
  
 *FKTableName*  
 입력 외래 키 테이블 이름입니다. *FKTableName* 는 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 된 경우 *FKTableName* 는 식별자로 처리 되 고 해당 사례는 중요 하지 않습니다. SQL_FALSE 경우 *FKTableName* 는 일반 인수입니다. 이는 문자 그대로 처리 되며, 해당 사례는 중요 합니다.  
  
 *NameLength6*  
 입력 **FKTableName*의 길이 (문자)입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLForeignKeys** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLForeignKeys** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle*에서 커서가 열려 있고 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다. 이 오류는 **sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에 의해 반환 되 고, **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서 반환 됩니다.<br /><br /> *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) *Pktablename* 및 *FKTableName* 인수가 모두 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되 고, *FKCatalogName* 또는 *PKCatalogName* 인수가 null 포인터이 고, SQL_CATALOG_NAME *InfoType* 는 카탈로그 이름이 지원 됨을 반환 합니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE로 설정 되었고 *FKSchemaName*, *pkschemaname*, *FKTableName*또는 *pkschemaname* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. SQLForeignKeys 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|||이름 길이 인수 중 하나의 값이 해당 이름에 대 한 최대 길이 값을 초과 했습니다. "설명"을 참조 하십시오.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|카탈로그 이름이 지정 되었으며 드라이버 또는 데이터 원본이 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름이 지정 되었으며 드라이버 또는 데이터 원본이 스키마를 지원 하지 않습니다.|  
|||SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE statement 특성의 현재 설정 조합이 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 되 고 SQL_ATTR_CURSOR_TYPE statement 특성이 해당 드라이버가 책갈피를 지원 하지 않는 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수에서 반환 되는 정보를 사용할 수 있는 방법에 대 한 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
 \* *Pktablename* 에 테이블 이름이 포함 된 경우 **SQLForeignKeys** 은 지정 된 테이블의 기본 키와이를 참조 하는 모든 외래 키를 포함 하는 결과 집합을 반환 합니다. 다른 테이블의 외래 키 목록에는 지정 된 테이블의 unique 제약 조건을 가리키는 외래 키가 포함 되지 않습니다.  
  
 \* *FKTableName* 에 테이블 이름이 포함 된 경우 **SQLForeignKeys** 는 지정 된 테이블에서 다른 테이블의 기본 키를 가리키는 모든 외래 키와 해당 키가 참조 하는 다른 테이블의 기본 키를 포함 하는 결과 집합을 반환 합니다. 지정 된 테이블의 외래 키 목록에 다른 테이블의 unique 제약 조건을 참조 하는 외래 키가 포함 되어 있지 않습니다.  
  
 \* *Pktablename* 과 \* *FKTableName* 에 모두 테이블 이름이 포함 된 경우 **SQLForeignKeys** 는 \* *FKTableName* 에 지정 된 테이블에서 **pktablename*에 지정 된 테이블의 기본 키를 참조 하는 외래 키를 반환 합니다. 이는 하나의 키 여야 합니다.  
  
> [!NOTE]  
>  ODBC 카탈로그 함수의 일반 사용, 인수 및 반환 데이터에 대 한 자세한 내용은 [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)를 참조 하세요.  
  
 **SQLForeignKeys** 는 결과를 표준 결과 집합으로 반환 합니다. 기본 키와 연결 된 외래 키가 요청 된 경우 결과 집합은 FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME 및 KEY_SEQ를 기준으로 정렬 됩니다. 외래 키와 연결 된 기본 키가 요청 된 경우 결과 집합은 PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME 및 KEY_SEQ를 기준으로 정렬 됩니다. 다음 표에서는 결과 집합의 열을 나열 합니다.  
  
 VARCHAR 열의 길이는 테이블에 표시 되지 않습니다. 실제 길이는 데이터 원본에 따라 달라 집니다. PKTABLE_CAT 또는 FKTABLE_CAT, PKTABLE_SCHEM 또는 FKTABLE_SCHEM, PKTABLE_NAME 또는 FKTABLE_NAME 열의 실제 길이를 확인 하기 위해 응용 프로그램은 PKCOLUMN_NAME, FKCOLUMN_NAME, SQL_MAX_CATALOG_NAME_LEN 및 SQL_MAX_SCHEMA_NAME_LEN 옵션을 사용 하 여 **SQLGetInfo** 를 호출할 수 있습니다.  
  
 ODBC 3.x에 대해 다음 열의 이름이 바뀌었습니다 *.* 열 이름 변경은 응용 프로그램이 열 번호를 기준으로 바인딩하기 때문에 이전 버전과의 호환성에 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3.x*열*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 다음 표에서는 결과 집합의 열을 나열 합니다. 열 14 (설명)를 초과 하는 추가 열은 드라이버에서 정의할 수 있습니다. 응용 프로그램은 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝에서 계산 하 여 드라이버별 열에 대 한 액세스 권한을 얻어야 합니다. 자세한 내용은 [Catalog 함수에서 반환 된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)를 참조 하세요.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|기본 키 테이블 카탈로그 이름 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|기본 키 테이블 스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar not NULL|기본 키 테이블 이름입니다.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|기본 키 열 이름입니다. 드라이버는 이름이 없는 열에 대해 빈 문자열을 반환 합니다.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|외래 키 테이블 카탈로그 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 카탈로그를 지원 하면 카탈로그가 없는 테이블에 대해 빈 문자열 ("")이 반환 됩니다.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|외래 키 테이블 스키마 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. 드라이버가 다른 Dbms에서 데이터를 검색 하는 경우와 같이 드라이버가 일부 테이블에 대해서만 스키마를 지원 하지만 스키마가 없는 테이블에 대해 빈 문자열 ("")을 반환 합니다.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar not NULL|외래 키 테이블 이름입니다.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar not NULL|외래 키 열 이름입니다. 드라이버는 이름이 없는 열에 대해 빈 문자열을 반환 합니다.|  
|KEY_SEQ (ODBC 1.0)|9|NULL이 아닌 Smallint|키의 열 시퀀스 번호 (1부터 시작)입니다.|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL 작업이 **업데이트**될 때 외래 키에 적용 되는 동작입니다. 다음 값 중 하나를 사용할 수 있습니다. 참조 되는 테이블은 기본 키가 있는 테이블입니다. 참조 테이블은 외래 키가 있는 테이블입니다.<br /><br /> SQL_CASCADE: 참조 된 테이블의 기본 키가 업데이트 되 면 참조 테이블의 외래 키도 업데이트 됩니다.<br /><br /> SQL_NO_ACTION: 참조 된 테이블의 기본 키를 업데이트 하 여 참조 테이블에 "현 수 참조"가 발생 하는 경우 (즉, 참조 하는 테이블의 행이 참조 테이블에 해당 하는 항목이 없는 경우) 업데이트가 거부 됩니다. 참조 하는 테이블의 외래 키에 대 한 업데이트에서 참조 된 테이블의 기본 키 값으로 존재 하지 않는 값을 도입 하는 경우 업데이트가 거부 됩니다. 이 동작은 ODBC 2.x의 SQL_RESTRICT 작업과 동일*합니다.*<br /><br /> SQL_SET_NULL: 기본 키의 하나 이상의 구성 요소가 변경 되는 방식으로 참조 된 테이블에서 하나 이상의 행이 업데이트 되는 경우 참조 하는 테이블의 변경 된 구성 요소에 해당 하는 참조 테이블의 외래 키 구성 요소는 참조 하는 테이블의 모든 일치 하는 행에서 NULL로 설정 됩니다.<br /><br /> SQL_SET_DEFAULT: 기본 키의 하나 이상의 구성 요소가 변경 되는 방식으로 참조 된 테이블에서 하나 이상의 행이 업데이트 되는 경우 기본 키의 변경 된 구성 요소에 해당 하는 참조 테이블의 외래 키 구성 요소는 참조 하는 테이블의 모든 일치 하는 행에서 적용 가능한 기본값으로 설정 됩니다.<br /><br /> 데이터 원본에 적용할 수 없는 경우 NULL입니다.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL 작업이 **삭제**될 때 외래 키에 적용 되는 동작입니다. 다음 값 중 하나를 사용할 수 있습니다. 참조 되는 테이블은 기본 키가 있는 테이블입니다. 참조 테이블은 외래 키가 있는 테이블입니다.<br /><br /> SQL_CASCADE: 참조 된 테이블의 행이 삭제 되 면 참조 하는 테이블의 모든 일치 하는 행도 삭제 됩니다.<br /><br /> SQL_NO_ACTION: 참조 된 테이블에서 행을 삭제 하면 참조 하는 테이블에 "현 수 참조"가 발생 하는 경우 (즉, 참조 하는 테이블의 행이 참조 테이블에 해당 하는 항목이 없는 경우) 업데이트가 거부 됩니다. 이 동작은 ODBC 2.x의 SQL_RESTRICT 작업과 동일*합니다.*<br /><br /> SQL_SET_NULL: 참조 된 테이블에서 하나 이상의 행이 삭제 되는 경우 참조 하는 테이블의 외래 키에 있는 각 구성 요소는 참조 하는 테이블의 모든 일치 하는 행에서 NULL로 설정 됩니다.<br /><br /> SQL_SET_DEFAULT: 참조 된 테이블에서 하나 이상의 행이 삭제 되는 경우 참조 하는 테이블의 외래 키에 있는 각 구성 요소는 참조 하는 테이블의 모든 일치 하는 행에서 해당 기본값으로 설정 됩니다.<br /><br /> 데이터 원본에 적용할 수 없는 경우 NULL입니다.|  
|FK_NAME (ODBC 2.0)|12|Varchar|외래 키 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다.|  
|PK_NAME (ODBC 2.0)|13|Varchar|기본 키 이름입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다.|  
|연기 (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>코드 예  
 다음 표에서 설명 하는 것 처럼이 예에서는 ORDERS, LINES 및 CUSTOMERS 라는 세 개의 테이블을 사용 합니다.  
  
|ORDERS|가로줄|통해|  
|------------|-----------|---------------|  
|주문|주문|CUSTID|  
|CUSTID|가로줄|NAME|  
|OPENDATE|PARTID|위치|  
|일하고|판매량|전화|  
|상태|||  
  
 ORDERS 테이블에서 CUSTID는 판매가 발생 한 고객을 식별 합니다. CUSTOMERS 테이블의 CUSTID를 참조 하는 외래 키입니다.  
  
 줄 테이블에서 ORDERID는 선 항목이 연결 된 판매 주문을 식별 합니다. ORDERS 테이블의 ORDERID를 참조 하는 외래 키입니다.  
  
 이 예에서는 **Sqlprimarykeys** 를 호출 하 여 ORDERS 테이블의 기본 키를 가져옵니다. 결과 집합에는 하나의 행이 포함 됩니다. 다음 표에서는 중요 한 열을 보여 줍니다.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|주문|1|  
  
 그런 다음이 예에서는 **SQLForeignKeys** 를 호출 하 여 ORDERS 테이블의 기본 키를 참조 하는 다른 테이블의 외래 키를 가져옵니다. 결과 집합에는 하나의 행이 포함 됩니다. 다음 표에서는 중요 한 열을 보여 줍니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|가로줄|CUSTID|1|  
  
 마지막으로,이 예에서는 **SQLForeignKeys** 를 호출 하 여 ORDERS 테이블에서 다른 테이블의 기본 키를 참조 하는 외래 키를 가져옵니다. 결과 집합에는 하나의 행이 포함 됩니다. 다음 표에서는 중요 한 열을 보여 줍니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|통해|CUSTID|ORDERS|CUSTID|1|  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키 열 반환|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|테이블 통계 및 인덱스 반환|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
