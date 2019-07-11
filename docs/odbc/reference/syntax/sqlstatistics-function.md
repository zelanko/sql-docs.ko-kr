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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc0c1d981180c61452f97a01bc0aba6fdc2d81e3
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793729"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLStatistics** 단일 테이블 및 테이블에 연결 된 인덱스에 대 한 통계 목록을 검색 합니다. 드라이버 정보 결과 집합으로 반환 합니다.  
  
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
 [입력] 문 핸들입니다.  
  
 *CatalogName*  
 [입력] 카탈로그 이름입니다. 드라이버 카탈로그에서 지 원하는 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 경우 ("")는 카탈로그에 있지 않은 테이블을 나타냅니다. *CatalogName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *CatalogName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *CatalogName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 *NameLength1*  
 [입력] 문자 길이 **CatalogName*합니다.  
  
 *SchemaName*  
 [입력] 스키마 이름입니다. 드라이버를 일부 테이블에 대 한 아니라 드라이버가 다른 Dbms를 빈 문자열에서 데이터를 검색 하는 경우 등의 다른 스키마를 지 원하는 경우 ("") 스키마에 있지 않은 테이블을 나타냅니다. *SchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *SchemaName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *SchemaName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength2*  
 [입력] 문자 길이 **SchemaName*합니다.  
  
 *TableName*  
 [입력] 테이블 이름입니다. 이 인수는 null 포인터 일 수 없습니다. *SchemaName* 문자열 검색 패턴을 포함할 수 없습니다.  
  
 SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 경우 *TableName* 식별자로 처리 됩니다 및 대 소문자는 중요 하지 않습니다. SQL_FALSE, 있으면 *TableName* 은 일반 인수로 리터럴로 처리 됩니다 하 고 해당 대/소문자는 중요 합니다.  
  
 *NameLength3*  
 [입력] 문자 길이 **TableName*합니다.  
  
 *고유*  
 [입력] 인덱스의 유형: SQL_INDEX_UNIQUE 또는 SQL_INDEX_ALL 합니다.  
  
 *Reserved*  
 [입력] 결과 집합의 카디널리티 및 페이지 열의 중요도 나타냅니다. 카디널리티 및 페이지 열만 반환 하는 다음 옵션에 영향을 줄합니다 카디널리티 및 페이지는 반환 되지 않습니다 하는 경우에 인덱스 정보가 반환 됩니다.  
  
 SQL_ENSURE는 드라이버 통계를 무조건 검색 하는 것을 요청 합니다. (만 표준을 준수 하는 Open Group 및 ODBC 확장을 지원 하지 않는 드라이버 됩니다 SQL_ENSURE를 지원할 수 있습니다.)  
  
 SQL_QUICK 요청는 드라이버가 서버에서 쉽게 사용할 수 있는 경우에 카디널리티 및 페이지를 검색 합니다. 이 경우 드라이버는 값이 최신 값인지 확인하지 않습니다. (Open Group 표준으로 작성 된 응용 프로그램이 ODBC에서 SQL_QUICK 동작을 얻을 항상 *3.x*-규격 드라이버입니다.)  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLStatistics** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLStatistics** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|커서가에서 열린 합니다 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 호출 되었지만 합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** sql_no_data가 반환 되지 않은 및 드라이버에 의해 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 열린 합니다 *StatementHandle*, 있지만 **SQLFetch** 또는 **SQLFetchScroll** 호출한 되었습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle*, 및 함수를 호출한 다음 다시 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|합니다 *TableName* 인수가 null 포인터입니다.<br /><br /> SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 합니다 *CatalogName* 인수가 null 포인터인 경우 및는 SQL_CATALOG_NAME *정보 항목* 반환 이름을 카탈로그는 지원 됩니다.<br /><br /> (DM) SQL_ATTR_METADATA_ID 문 특성을 SQL_TRUE로 설정 된 하며 *SchemaName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLStatistics** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 이름 길이 인수 중 하나의 값이 0 보다 작은 있지만 SQL_NTS 다음과 같지 않은 경우.<br /><br /> 이름 길이 인수 중 하나의 값을 해당 이름에 대 한 최대 길이 값을 초과 했습니다.|  
|HY100|고유 옵션 유형 범위를 벗어났습니다.|(DM)는 잘못 *Unique* 값이 지정 되었습니다.|  
|HY101|정확도 옵션 유형 범위를 벗어났습니다.|(DM)는 잘못 *예약* 값이 지정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|카탈로그를 지정 하 고 데이터 소스를 드라이버 카탈로그를 지원 하지 않습니다.<br /><br /> 스키마를 지정 하 고 드라이버 또는 데이터 원본 스키마를 지원 하지 않습니다.<br /><br /> SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본 요청 된 결과 집합을 반환 하기 전에 쿼리 제한 시간 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLStatistics** NON_UNIQUE, 형식, INDEX_QUALIFIER, INDEX_NAME, 및 ORDINAL_POSITION 순으로 정렬 하는 표준 결과 집합을 단일 테이블에 대 한 정보를 반환 합니다. 결과 집합에 있는 통계 정보 (결과 집합의 카디널리티 및 페이지 열)을 테이블에 대 한 각 인덱스에 대 한 정보를 사용 하 여 결합합니다. 이 정보를 어떻게 사용할 수 있는지에 대 한 자세한 내용은 [카탈로그 데이터의 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
 TABLE_CAT table_schem 순, TABLE_NAME, COLUMN_NAME 열의 실제 길이 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN를 사용 하 여 및 SQL_MAX_COLUMN_NAME_LEN 옵션을 지정 합니다.  
  
> [!NOTE]  
>  범용, 인수 및 반환 된 데이터의 ODBC 카탈로그 함수에 대 한 자세한 내용은 참조 하세요. [카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
 ODBC에 대 한 다음과 같은 열 이름이 바뀌었습니다 *3.x*합니다. 열 이름 변경을 응용 프로그램 열 번호로 바인딩할 수 있으므로 이전 버전과 호환성 영향을 주지 않습니다.  
  
|ODBC 2.0 열|ODBC *3.x* 열|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 다음 표에서 결과 집합의 열을 나열합니다. 드라이버에서 열 13 (FILTER_CONDITION) 이후의 추가 열을 정의할 수 있습니다. 응용 프로그램 명시적 서 수 위치를 지정 하는 대신 결과 집합의 끝부터 계산 하 여 드라이버 관련 열에 액세스 해야 합니다. 자세한 내용은 [데이터 카탈로그 함수에서 반환한](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)합니다.  
  
|열 이름|열 번호|데이터 형식|주석|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|통계 또는 인덱스에 적용 되는; 테이블의 카탈로그 이름 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 카탈로그 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 카탈로그에 있지 않은 테이블에 대 한 합니다.|  
|TABLE_SCHEM 순 (ODBC 1.0)|2|Varchar|통계 또는 인덱스에 적용 되는; 테이블의 스키마 이름 데이터 원본에 해당 하지 않는 경우 NULL입니다. 드라이버에서 지 원하는 경우 스키마 일부 테이블에 대해서만, 다른 Dbms에서 데이터를 검색 하는 드라이버, 빈 문자열을 반환 하는 등 ("") 스키마에 있지 않은 테이블에 대 한 합니다.|  
|TABLE_NAME (ODBC 1.0)|3|NULL이 아닌 Varchar|테이블 통계 또는 인덱스에 적용 되는 테이블의 이름입니다.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|인덱스에 중복 값을 허용 하지 여부를 나타냅니다.<br /><br /> SQL_TRUE 경우 인덱스 값이 고유 하지 않은 수 있습니다.<br /><br /> 인덱스 값이 고유 해야 하는 경우 SQL_FALSE입니다.<br /><br /> 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|인덱스를 정하는 데 사용 되는 식별자 이름을 수행 하는 **DROP INDEX**; 형식이 SQL_TABLE_STAT 인지 또는 데이터 원본에서 인덱스의 한정자를 지원 하지 않는 경우 NULL이 반환 됩니다. Null이 아닌 값이이 열에 반환 되 면에서 인덱스 이름을 한 정하는 데 사용 되어야 합니다는 **DROP INDEX** 문과 인덱스 이름을 정규화 하는 table_schem 순 사용할지이 고, 그렇지 합니다.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|인덱스 이름입니다. 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|형식 (ODBC 1.0)|7|NULL이 아닌 Smallint|반환 되는 정보의 유형:<br /><br /> SQL_TABLE_STAT (카디널리티 또는 페이지 열)의 테이블에 대 한 통계를 나타냅니다.<br /><br /> SQL_INDEX_BTREE B-트리 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_CLUSTERED 클러스터형된 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_CONTENT 콘텐츠 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_HASHED 해시 인덱스를 나타냅니다.<br /><br /> SQL_INDEX_OTHER 또 다른 유형의 인덱스를 나타냅니다.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|(1부터 시작); 인덱스의 열 시퀀스 번호 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|열 이름입니다. 식 기반 열 경우 급여 + 혜택, 같은 식이 반환 됩니다. 식을 확인할 수 없는 경우 빈 문자열이 반환 됩니다. 형식이 SQL_TABLE_STAT 이면 NULL이 반환 됩니다.|  
|ASC_OR_DESC (ODBC 1.0)|10|char(1)|열의 정렬 순서: "A" 오름차순을 선택 합니다. "D" 내림차순; 형식이 SQL_TABLE_STAT 인지 또는 데이터 원본에서 열 정렬 순서를 지원 하지 않는 경우 NULL이 반환 됩니다.|  
|카디널리티 (ODBC 1.0)|11|정수|테이블 또는 인덱스 카디널리티입니다. 형식은 SQL_TABLE_STAT; 경우 테이블의 행 수 형식이 지원 되지 않으면 SQL_TABLE_STAT; 인덱스의 고유 값 수 데이터 원본에서 값을 사용할 수 없는 경우 NULL이 반환 됩니다.|  
|페이지 (ODBC 1.0)|12|정수|인덱스 또는 테이블을 저장 하는 데 사용 되는 페이지 수 형식은 SQL_TABLE_STAT; 경우 테이블에 대 한 페이지 수 형식이 지원 되지 않으면 SQL_TABLE_STAT; 인덱스에 대 한 페이지 수 데이터 원본에서 값을 사용할 수 없는 경우 또는 데이터 원본에 해당 하지 않는 경우 NULL이 반환 됩니다.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|이 급여와 같은 필터 조건을 인덱스 필터링 된 인덱스인 경우 > 30000; 필터 조건을 확인할 수 없는 경우 빈 문자열입니다.<br /><br /> 인덱스가 필터링된 된 인덱스가 없는 경우 NULL를 확인할 수 없는 형식 SQL_TABLE_STAT 중인지 여부는 필터링 된 인덱스입니다.|  
  
 결과 집합의 행을 테이블에 해당 하는 경우 드라이버는 형식을 SQL_TABLE_STAT로 설정 하 고 NULL로 NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME 및 ASC_OR_DESC를 설정 합니다. 카디널리티 또는 페이지를 사용할 수 없는 데이터 원본의 경우 드라이버가 NULL로 설정 합니다.  
  
## <a name="code-example"></a>코드 예  
 유사한 함수의 코드 예제를 참조 하세요 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 인출 합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|외래 키의 열을 반환합니다.|[SQLForeignKeys 함수](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|기본 키의 열을 반환합니다.|[SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
