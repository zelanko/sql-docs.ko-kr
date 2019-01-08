---
title: SQLSpecialColumns 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f44ae90a82e778bf8e8564b719aa6b9f0157a05a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204372"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. 그룹 열기  
  
 **요약**  
 **SQLSpecialColumns** 지정된 된 테이블 내의 열에 대 한 다음 정보를 검색 합니다.  
  
-   테이블의 행을 고유 하 게 식별 하는 열의 최적 집합.  
  
-   행의 모든 값은 트랜잭션에 의해 업데이트 될 때 자동으로 업데이트 되는 열입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *IdentifierType*  
 [입력] 반환할 열의 형식입니다. 다음 값 중 하나 여야 합니다.  
  
 SQL_BEST_ROWID: 최적 열 또는 열 또는 열에서 값을 검색 하 여 고유 하 게 식별 하는에 지정된 된 테이블에 행을 허용 하는 열 집합을 반환 합니다. 열에는이 용도 (예: Oracle ROWID 또는 Ingres TID) 열 또는 테이블의 모든 고유 인덱스의 열에 대 한 설계 의사 (pseudo) 열 수 있습니다.  
  
 SQL_ROWVER: 행의 모든 값 (예: SQLBase ROWID 또는 Sybase 타임 스탬프) 트랜잭션에 의해 업데이트 될 때 데이터 원본에서 자동으로 업데이트 되는 경우 지정된 된 테이블의 열을 반환 합니다.  
  
 *카탈로그 이름*  
 [입력] 테이블에 대 한 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *CatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *CatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *CatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 테이블의 스키마 이름입니다. 드라이버를 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 테이블을 나타냅니다. *SchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *SchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *SchemaName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *TableName*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터 일 수 없습니다. *TableName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *TableName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *TableName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
 *범위*  
 [입력] 범위는 rowid에 필요한 최소입니다. 반환 된 rowid 더 넓은 범위의 될 수 있습니다. 다음 중 하나여야 합니다.  
  
 SQL_SCOPE_CURROW: Rowid 해당 행에 있는 동안에 유효 하도록 보장 됩니다. Rowid를 사용 하 여 나중에 다시 선택 행 업데이트 되거나 다른 트랜잭션에 의해 삭제 된 경우 행을 반환 하지 않을 수 있습니다.  
  
 SQL_SCOPE_TRANSACTION: Rowid 현재 트랜잭션 기간 동안 유효 하도록 보장 됩니다.  
  
 SQL_SCOPE_SESSION: Rowid가 유효 하도록 보장 세션 기간 (트랜잭션이 바뀌어도).  
  
 *Null 허용*  
 [입력] NULL 값을 가질 수 있는 특수 열을 반환할 것인지를 결정 합니다. 다음 중 하나여야 합니다.  
  
 SQL_NO_NULLS: NULL 값을 가질 수 있는 특별 한 열을 제외 합니다. 일부 드라이버 SQL_NO_NULLS를 지원할 수 없습니다 하 고 이러한 드라이버 SQL_NO_NULLS 지정 된 경우 설정 하는 빈 결과 반환 합니다. 반드시 필요한 경우에 대/소문자 및 요청 SQL_NO_NULLS이 응용 프로그램 준비 해야 합니다.  
  
 SQL_NULLABLE: NULL 값을 가질 수 있습니다 하는 경우에 특별 한 열을 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSpecialColumns** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSpecialColumns** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** sql_no_data가 반환 되지 않은 및 드라이버에 의해 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|합니다 *TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *CatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목* 반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 하며 *SchemaName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 함수가 계속 실행 될 때 **SQLSpecialColumns** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.<br /><br /> 해당 이름의 최대 길이 값을 초과 하는 길이 인수 중 하나의 값입니다. 호출 하 여 각 이름의 최대 길이 가져올 수 있습니다 **SQLGetInfo** 사용 하 여 합니다 *정보 항목* 값: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, 또는 SQL_MAX_TABLE_NAME_LEN 합니다.|  
|HY097|열 유형 범위를 벗어났습니다|(DM)는 잘못 *IdentifierType* 값이 지정 되었습니다.|  
|HY098|범위 유형 범위를 벗어났습니다.|(DM)는 잘못 *범위* 값이 지정 되었습니다.|  
|HY099|Nullable 형식 범위를 벗어났습니다.|(DM)는 잘못 *Nullable* 값이 지정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그를 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마를 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 경우는 *IdentifierType* SQL_BEST_ROWID, 인수가 **SQLSpecialColumns** 표의 각 행을 고유 하 게 식별 하는 열을 반환 합니다. 이러한 열에 항상 사용할 수 있습니다는 *선택 목록* 하거나 **여기서** 절. **SQLColumns**, 테이블의 열에 다양 한 정보를 반환 하는 데 사용 되는 반환 하지 않는 반드시 각 행을 고유 하 게 식별 하는 열 또는 값이 행 하는 경우 자동으로 업데이트 되는 열에 의해 업데이트 될를 트랜잭션입니다. 예를 들어 **SQLColumns** Oracle 의사 (pseudo) 열 ROWID를 반환할 수 있습니다. 이 인해 **SQLSpecialColumns** 이러한 열이 반환 하는 데 사용 됩니다. 자세한 내용은 [카탈로그 데이터의 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 테이블의 각 행을 고유 하 게 식별 하는 열이 없는 경우 **SQLSpecialColumns** 행이 없는 사용 하 여 행 집합 반환;에 대 한 후속 호출 **SQLFetch** 또는 **SQLFetchScroll**문에서 SQL_NO_DATA를 반환 합니다.  
  
 경우는 *IdentifierType*를 *범위*, 또는 *Nullable* 데이터 원본에서 지원 되지 않는 특성을 지정 하는 인수 **SQLSpecialColumns**  빈 결과 집합을 반환 합니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우는 *CatalogName*, *SchemaName*, 및 *TableName* 인수 이므로 식별자로 처리 되는 특정 상황에서 null 포인터를 설정할 수 없습니다. (자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** 범위에 따라 순서가 지정 된 표준 결과 집합으로 결과 반환 합니다.  
  
 ODBC 3에 대 한 다음과 같은 열 이름이 바뀌었습니다 *.x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC 3 *.x* 열|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_MAX_COLUMN_NAME_LEN 옵션을 사용 합니다.  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 8 (PSEUDO_COLUMN) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 것이 아니라 결과 집합의 끝에서 카운트다운 여 드라이버별 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|범위 (ODBC 1.0)|1|Smallint|Rowid의 실제 범위입니다. 다음 값 중 하나가 포함 되어 있습니다.<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL이 반환 됩니다 *IdentifierType* SQL_ROWVER 됩니다. 각 값에 대 한 참조에 대 한 설명을 *범위* 이 섹션 앞부분의 "구문 에서"입니다.|  
|COLUMN_NAME (ODBC 1.0)|2|NULL이 아닌 Varchar|열 이름입니다. 드라이버 이름 없는 열에 대 한 빈 문자열을 반환 합니다.|  
|DATA_TYPE (ODBC 1.0)|3|NULL이 아닌 Smallint|SQL 데이터 형식입니다. 이 ODBC SQL 데이터 형식 또는 드라이버별 SQL 데이터 형식 수 있습니다. 유효한 ODBC SQL 데이터 형식의 목록을 참조 하세요 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)합니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.|  
|TYPE_NAME (ODBC 1.0)|4|NULL이 아닌 Varchar|데이터 원본에 종속적인 데이터 형식 이름입니다. 예를 들어, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.|  
|COLUMN_SIZE (ODBC 1.0)|5|정수|데이터 원본에서 열의 크기를 지정 합니다. 열 크기에 관한 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.|  
|BUFFER_LENGTH (ODBC 1.0)|6|정수|전송 되는 데이터의 바이트 길이 **SQLGetData** 하거나 **SQLFetch** SQL_C_DEFAULT를 지정 하는 경우 작업 합니다. 숫자 데이터에 대 한이 크기는 데이터 원본에 저장 된 데이터의 크기 보다 다 수 있습니다. 이 값은 문자 또는 이진 데이터에 대 한 COLUMN_SIZE 열과 동일 합니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|데이터 원본에 열 10 진수 숫자입니다. NULL이 반환 됩니다 데이터 형식의 소수 자릿수가 적용 되지 않습니다. 10 진수 숫자와 관련 된 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|의사 (pseudo) 열을 Oracle ROWID 같은 열인지 여부를 나타냅니다.<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **참고 합니다.**  최대 상호 운용성에 대 한 의사 (pseudo) 열은 따옴표로 묶어서는 안 반환한 식별자 따옴표 문자를 사용 하 여 **SQLGetInfo**합니다.|  
  
 SQL_BEST_ROWID에 대 한 값을 검색 하는 응용 프로그램, 후 응용 프로그램 정의 된 범위 내에서 해당 행을 다시 선택 하려면 이러한 값을 사용할 수 있습니다. 합니다 **선택** 문에 행 또는 행이 하나씩 반환 하도록 보장 합니다.  
  
 응용 프로그램 reselects rowid 열 또는 열을 기반으로 행을 행이 없는 경우 응용 프로그램에는 행이 삭제 또는 수정 된 rowid 열 가정할 수 있습니다. 반대로 해당 되지 않습니다: 행의 다른 열 rowid 변경 되지 않은 경우에 변경 될 수 있습니다.  
  
 앞으로 스크롤해야 하는 응용 프로그램 및 결과 행 집합에서 가장 최근 데이터를 검색 하려면 집합 내에서 다시 SQL_BEST_ROWID 유용 열 유형에 대해 반환 된 열입니다. 열 또는 열의 rowid 해당 행에 있는 동안 변경 하지 않도록 보장 됩니다.  
  
 Rowid의 열 수 있습니다 유효 커서가 된 행에 배치 되지 경우에 응용 프로그램의 범위 열에 결과 집합을 확인 하 여이 확인할 수 있습니다.  
  
 SQL_ROWVER 행 rowid를 사용 하 여 다시 선택 하는 동안 지정된 된 행의 열 업데이트 여부를 확인 하는 기능을 필요로 하는 응용 프로그램에 유용 하는 열 유형에 대해 반환 된 열입니다. 예를 들어 rowid를 사용 하 여 행을 충분히 후 응용 프로그램 SQL_ROWVER 열만 가져온 것을 이전 값을 비교 수 있습니다. SQL_ROWVER 열의 값은 이전 값을 다를 경우 응용 프로그램에 사용자 표시에는 데이터가 변경 되었음을 경고할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제를 참조 하세요 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|테이블 또는 테이블에 열을 반환합니다.|[SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|기본 키의 열을 반환합니다.|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
