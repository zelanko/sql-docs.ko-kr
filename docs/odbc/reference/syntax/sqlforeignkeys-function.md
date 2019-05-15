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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1aeaef9b120a0bd4be008adafe8e9a24724279a0
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537252"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLForeignKeys** 반환할 수 있습니다.  
  
-   목록에서 지정된 된 테이블 (열 지정된 된 테이블의 다른 테이블의 기본 키를 참조 하는) 외래 키입니다.  
  
-   지정된 된 테이블의 기본 키를 참조 하는 다른 테이블의 외래 키의 목록입니다.  
  
 드라이버에는 결과 집합으로 지정 된 문에서 각 목록을 반환 합니다.  
  
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
 [입력] 문 핸들입니다.  
  
 *PKCatalogName*  
 [입력] 기본 키 테이블 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *PKCatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *PKCatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *PKCatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 길이 **PKCatalogName*, 문자에서입니다.  
  
 *PKSchemaName*  
 [입력] 기본 키 테이블 스키마 이름입니다. 드라이버를 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 테이블을 나타냅니다. *PKSchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *PKSchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *PKSchemaName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 길이 **PKSchemaName*, 문자에서입니다.  
  
 *PKTableName*  
 [입력] 기본 키 테이블 이름입니다. *PKTableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *PKTableName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *PKTableName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 길이 **PKTableName*, 문자에서입니다.  
  
 *FKCatalogName*  
 [입력] 외래 키 테이블 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *FKCatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *FKCatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *FKCatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength4*  
 [입력] 길이 **FKCatalogName*, 문자에서입니다.  
  
 *FKSchemaName*  
 [입력] 외래 키 테이블 스키마 이름입니다. 드라이버를 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 테이블을 나타냅니다. *FKSchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *FKSchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *FKSchemaName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength5*  
 [입력] 길이 **FKSchemaName*, 문자에서입니다.  
  
 *FKTableName*  
 [입력] 외래 키 테이블 이름입니다. *FKTableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *FKTableName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *FKTableName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength6*  
 [입력] 길이 **FKTableName*, 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLForeignKeys** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* sql _HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLForeignKeys** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 하지 않은 한 경우 드라이버에서 반환 됩니다 **SQLFetch** 또는**SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle*, 및 함수를 호출한 다음 다시 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *PKTableName* 하 고 *FKTableName* 모두 null 포인터인 되었습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *FKCatalogName* 하거나 *PKCatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목*반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 및 *FKSchemaName*, *PKSchemaName*하십시오 *FKTableName*, 또는 *PKTableName*  인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수 SQLForeignKeys 함수가 호출 되었을 때 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.|  
|||이름 길이 인수 중 하나의 값을 해당 이름에 대 한 최대 길이 값을 초과 했습니다. ("주석입니다." 참조)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그 이름을 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마 이름을 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.|  
|||SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 이 함수에서 반환 된 정보를 사용할 수 있는 방법에 대 한 자세한 내용은 [카탈로그 데이터의 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
 하는 경우 \* *PKTableName* 는 테이블 이름이 포함 됩니다 **SQLForeignKeys** 지정된 된 테이블의 기본 키 및 참조 하는 모든 외래 키를 포함 하는 결과 집합을 반환 합니다. 다른 테이블의 외래 키 목록이 지정된 된 테이블에서 unique 제약 조건을 가리키는 외래 키를 포함 되지 않습니다.  
  
 하는 경우 \* *FKTableName* 는 테이블 이름이 포함 됩니다 **SQLForeignKeys** 다른 테이블의 기본 키를 가리키는 지정된 된 테이블의 외래 키를 모두 포함 된 결과 집합을 반환 하며 참조 하는 다른 테이블의 기본 키입니다. 지정된 된 테이블의 외래 키의 목록에 다른 테이블에서 unique 제약 조건을 참조 하는 외래 키를 없습니다.  
  
 둘 다 \* *PKTableName* 하 고 \* *FKTableName* 테이블 이름이 포함 되어 **SQLForeignKeys** 지정한 테이블의 외래 키를 반환 합니다. \* *FKTableName* 에서 지정한 테이블의 기본 키를 참조 하는 **PKTableName*합니다. 최대 하나의 키 여야 합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 **SQLForeignKeys** 표준 결과 집합으로 결과 반환 합니다. 기본 키와 연결 된 외래 키를 요청 하는 경우 결과 집합 FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME 및 KEY_SEQ 정렬 되어 있습니다. 외래 키와 연결 된 기본 키를 요청 하는 경우 결과 집합 PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME, 및 KEY_SEQ 정렬 되어 있습니다. 다음 표에서 결과 집합의 열을 나열합니다.  
  
 테이블에 VARCHAR 열 길이가 표시 되지 않습니다. 실제 길이 데이터 원본에 따라 달라 집니다. PKTABLE_CAT 또는 FKTABLE_CAT, PKTABLE_SCHEM FKTABLE_SCHEM의 실제 길이 확인 하려면 PKTABLE_NAME FKTABLE_NAME 및 PKCOLUMN_NAME 또는 FKCOLUMN_NAME 열 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** 는 SQL_MAX_를 사용 하 여 CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, 및 SQL_MAX_COLUMN_NAME_LEN 옵션입니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다 *. x입니다.* 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 14 (설명) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|기본 키 테이블 카탈로그 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 테이블에 대 한 합니다.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|기본 키 테이블 스키마 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 테이블에 대 한 합니다.|  
|PKTABLE_NAME (ODBC 1.0)|3|NULL이 아닌 Varchar|기본 키 테이블 이름입니다.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|NULL이 아닌 Varchar|기본 키 열 이름입니다. 드라이버 이름 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|외래 키 테이블 카탈로그 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 테이블에 대 한 합니다.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|외래 키 테이블 스키마 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 테이블에 대 한 합니다.|  
|FKTABLE_NAME (ODBC 1.0)|7|NULL이 아닌 Varchar|외래 키 테이블 이름입니다.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|NULL이 아닌 Varchar|외래 키 열 이름입니다. 드라이버 이름 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|KEY_SEQ (ODBC 1.0)|9|NULL이 아닌 Smallint|시퀀스 번호 (1부터 시작) 키 열입니다.|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL 작업이 일 때 외래 키에 적용할 동작 **업데이트**합니다. 다음 값 중 하나일 수 있습니다. (참조 테이블은 기본 키가 있는 테이블; 참조 테이블은 외래 키가 있는 테이블입니다.)<br /><br /> SQL_CASCADE: 참조 되는 테이블의 기본 키 업데이트 되 면 참조 테이블의 외래 키도 업데이트 됩니다.<br /><br /> SQL_NO_ACTION: 참조 되는 테이블의 기본 키를 업데이트 하는 참조 테이블 에서도 "현 수 참조"로 인해 경우 (즉, 참조 테이블의 행은가 없는 해당 참조 되는 테이블에서) 업데이트가 거부 되었습니다. 참조 하는 테이블의 외래 키 업데이트는 참조 되는 테이블의 기본 키의 값으로 존재 하지 않는 값에 도입 업데이트 거부 됩니다. (이 작업은 ODBC 2 SQL_RESTRICT 동작 동일 *.x*.)<br /><br /> SQL_SET_NULL: 기본 키의 변경 된 구성 요소에 해당 하는 참조 테이블의 외래 키의 구성 요소 참조 테이블에 하나 이상의 행은 기본 키의 하나 이상의 구성 요소가 변경 되는 방식으로 업데이트 하는 경우 모든 NULL로 설정 됩니다. 참조 테이블의 일치 하는 행입니다.<br /><br /> SQL_SET_DEFAULT: 참조 테이블에 하나 이상의 행이 기본 키의 하나 이상의 구성 요소가 변경 되는 방식으로 업데이트 되, 기본 키의 변경 된 구성 요소에 해당 하는 참조 테이블의 외래 키의 구성 요소는 applicab 설정 됩니다. le 참조 테이블의 모든 일치 하는 행의 기본 값입니다.<br /><br /> 데이터 원본에 해당 하지 않는 경우 NULL입니다.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL 작업이 일 때 외래 키에 적용할 동작 **삭제**합니다. 다음 값 중 하나일 수 있습니다. (참조 테이블은 기본 키가 있는 테이블; 참조 테이블은 외래 키가 있는 테이블입니다.)<br /><br /> SQL_CASCADE: 참조 되는 테이블의 행이 삭제 되 면 참조 테이블에 일치 하는 모든 행도 삭제 됩니다.<br /><br /> SQL_NO_ACTION: 참조 되는 테이블의 행을 삭제 하는 참조 테이블 에서도 "현 수 참조"를 야기 하는 경우 (즉, 참조 테이블의 행은가 없는 해당 참조 되는 테이블에서) 업데이트가 거부 되었습니다. (이 작업은 ODBC 2 SQL_RESTRICT 동작 동일 *.x*.)<br /><br /> SQL_SET_NULL: 참조 된 테이블에서 하나 이상의 행이 삭제 되는 경우 참조 하는 테이블의 외래 키의 각 구성 요소 참조 테이블의 모든 일치 하는 행의 NULL로 설정 됩니다.<br /><br /> SQL_SET_DEFAULT: 참조 테이블에 하나 이상의 행이 삭제 되는 경우 참조 하는 테이블의 외래 키의 각 구성 요소 참조 테이블의 모든 일치 하는 행의 해당 기본값으로 설정 됩니다.<br /><br /> 데이터 원본에 해당 하지 않는 경우 NULL입니다.|  
|FK_NAME (ODBC 2.0)|12|Varchar|외래 키 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다.|  
|PK_NAME (ODBC 2.0)|13|Varchar|기본 키 이름입니다. 데이터 원본에 해당 하지 않는 경우 NULL입니다.|  
|연기 (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>코드 예  
 다음 표에서 볼 수 있듯이,이 예제에서는 세 개의 테이블, 주문, 선 및 고객에 게 명명 된를 사용 합니다.  
  
|ORDERS|줄|고객은|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|줄|NAME|  
|개장 날짜|PARTID|주소|  
|판매 직원|수량|전화|  
|STATUS|||  
  
 ORDERS 테이블을 CUSTID 판매 수행 된 고객을 식별 합니다. 가리키는 CUSTID CUSTOMERS 테이블의 외래 키 임  
  
 줄 테이블의 ORDERID 판매 주문의 품목와 관련 된 식별 합니다. ORDERS 테이블의 ORDERID 가리키는 외래 키 임  
  
 이 예제에서는 호출 **SQLPrimaryKeys** ORDERS 테이블의 기본 키를 가져옵니다. 결과 집합에 하나의 행; 해야 합니다. 중요 한 열은 다음 표에 표시 됩니다.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|ORDERID|1|  
  
 다음으로 호출 하 여 **SQLForeignKeys** ORDERS 테이블의 기본 키를 참조 하는 다른 테이블의 외래 키를 가져오려고 합니다. 결과 집합에 하나의 행; 해야 합니다. 중요 한 열은 다음 표에 표시 됩니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|줄|CUSTID|1|  
  
 마지막으로 호출 하 여 **SQLForeignKeys** 다른 테이블의 기본 키를 참조 하는 ORDERS 테이블의 외래 키를 가져오려고 합니다. 결과 집합에 하나의 행; 해야 합니다. 중요 한 열은 다음 표에 표시 됩니다.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|고객은|CUSTID|ORDERS|CUSTID|1|  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키의 열을 반환합니다.|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|테이블 통계 및 인덱스를 반환합니다.|[SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
