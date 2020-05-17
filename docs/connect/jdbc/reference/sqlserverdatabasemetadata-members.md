---
title: SQLServerDatabaseMetaData 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 327ba0bc-438a-494c-b119-1cd4a096bb58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a250cac94cdba3c4f71ce359b964ed5ef50e895f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971553"
---
# <a name="sqlserverdatabasemetadata-members"></a>SQLServerDatabaseMetaData 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|속성|Description|  
|----------|-----------------|  
|java.sql.DatabaseMetaData|attributeNoNulls, attributeNullable, attributeNullableUnknown, bestRowNotPseudo, bestRowPseudo, bestRowSession, bestRowTemporary, bestRowTransaction, bestRowUnknown, columnNoNulls, columnNullable, columnNullableUnknown, importedKeyCascade, importedKeyInitiallyDeferred, importedKeyInitiallyImmediate, importedKeyNoAction, importedKeyNotDeferrable, importedKeyRestrict, importedKeySetDefault, importedKeySetNull, procedureColumnIn, procedureColumnInOut, procedureColumnOut, procedureColumnResult, procedureColumnReturn, procedureColumnUnknown, procedureNoNulls, procedureNoResult, procedureNullable, procedureNullableUnknown, procedureResultUnknown, procedureReturnsResult, sqlStateSQL, sqlStateSQL99, sqlStateXOpen, tableIndexClustered, tableIndexHashed, tableIndexOther, tableIndexStatistic, typeNoNulls, typeNullable, typeNullableUnknown, typePredBasic, typePredChar, typePredNone, typeSearchable, versionColumnNotPseudo, versionColumnPseudo, versionColumnUnknown|  
  
## <a name="methods"></a>메서드  
  
|속성|Description|  
|----------|-----------------|  
|[allProceduresAreCallable](../../../connect/jdbc/reference/allproceduresarecallable-method-sqlserverdatabasemetadata.md)|[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md) 메서드에서 반환된 모든 프로시저를 호출할 수 있는 권한이 현재 사용자에게 있는지 여부를 검색합니다.|  
|[allTablesAreSelectable](../../../connect/jdbc/reference/alltablesareselectable-method-sqlserverdatabasemetadata.md)|SELECT 문의 [getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) 메서드에서 반환된 모든 테이블을 사용할 수 있는 권한이 현재 사용자에게 있는지 여부를 검색합니다.|  
|[autoCommitFailureClosesAllResultSets](../../../connect/jdbc/reference/autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata.md)|자동 커밋이 사용되며 예외가 발생할 때 JDBC 드라이버에서 유지 가능한 결과 집합을 포함하여 열려 있는 모든 결과 집합을 닫는지 여부를 나타냅니다.|  
|[dataDefinitionCausesTransactionCommit](../../../connect/jdbc/reference/datadefinitioncausestransactioncommit-method-sqlserverdatabasemetadata.md)|트랜잭션 내의 데이터 정의 문이 트랜잭션을 강제로 커밋하는지 여부를 검색합니다.|  
|[dataDefinitionIgnoredInTransactions](../../../connect/jdbc/reference/datadefinitionignoredintransactions-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 트랜잭션 내의 데이터 정의 문을 무시하는지 여부를 검색합니다.|  
|[deletesAreDetected](../../../connect/jdbc/reference/deletesaredetected-method-sqlserverdatabasemetadata.md)|[SQLServerResultSet](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 클래스의 [rowDeleted](../../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 호출하여 표시된 행 삭제를 검색할 수 있는지 여부를 검색합니다.|  
|[doesMaxRowSizeIncludeBlobs](../../../connect/jdbc/reference/doesmaxrowsizeincludeblobs-method-sqlserverdatabasemetadata.md)|[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md) 메서드의 반환 값에 SQL 데이터 형식 LONGVARCHAR 및 LONGVARBINARY가 포함되는지 여부를 검색합니다.|  
|[getAttributes](../../../connect/jdbc/reference/getattributes-method-sqlserverdatabasemetadata.md)|지정된 스키마 및 카탈로그에서 사용할 수 있는 사용자 정의 형식에 대해 지정된 형식의 지정된 특성에 대한 설명을 검색합니다.|  
|[getBestRowIdentifier](../../../connect/jdbc/reference/getbestrowidentifier-method-sqlserverdatabasemetadata.md)|테이블의 열 중 행을 고유하게 식별하는 최적의 열 집합에 대한 설명을 검색합니다.|  
|[getCatalogs](../../../connect/jdbc/reference/getcatalogs-method-sqlserverdatabasemetadata.md)|연결된 서버에서 사용할 수 있는 카탈로그 이름을 검색합니다.|  
|[getCatalogSeparator](../../../connect/jdbc/reference/getcatalogseparator-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 카탈로그 및 테이블 이름 사이에 구분 기호로 사용하는 **문자열**을 검색합니다.|  
|[getCatalogTerm](../../../connect/jdbc/reference/getcatalogterm-method-sqlserverdatabasemetadata.md)|데이터베이스 공급업체에서 "카탈로그"에 사용하는 기본 용어를 검색합니다.|  
|[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)|드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색합니다.|  
|[getColumnPrivileges](../../../connect/jdbc/reference/getcolumnprivileges-method-sqlserverdatabasemetadata.md)|테이블의 열에 대한 액세스 권한 설명을 검색합니다.|  
|[getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)|지정된 카탈로그에서 사용할 수 있는 테이블 열에 대한 설명을 검색합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatabasemetadata.md)|이 메타데이터 개체를 생성한 연결을 검색합니다.|  
|[getCrossReference](../../../connect/jdbc/reference/getcrossreference-method-sqlserverdatabasemetadata.md)|지정된 외래 키 테이블에서 지정된 기본 키 테이블의 기본 키 열을 참조하는 외래 키 열에 대한 설명을 검색합니다.|  
|[getDatabaseMajorVersion](../../../connect/jdbc/reference/getdatabasemajorversion-method-sqlserverdatabasemetadata.md)|기본 데이터베이스의 주 버전 번호를 검색합니다.|  
|[getDatabaseMinorVersion](../../../connect/jdbc/reference/getdatabaseminorversion-method-sqlserverdatabasemetadata.md)|기본 데이터베이스의 부 버전 번호를 검색합니다.|  
|[getDatabaseProductName](../../../connect/jdbc/reference/getdatabaseproductname-method-sqlserverdatabasemetadata.md)|이 데이터베이스 제품의 이름을 검색합니다.|  
|[getDatabaseProductVersion](../../../connect/jdbc/reference/getdatabaseproductversion-method-sqlserverdatabasemetadata.md)|이 데이터베이스 제품의 버전 번호를 검색합니다.|  
|[getDefaultTransactionIsolation](../../../connect/jdbc/reference/getdefaulttransactionisolation-method-sqlserverdatabasemetadata.md)|이 데이터베이스에 대한 기본 트랜잭션 격리 수준을 검색합니다.|  
|[getDriverMajorVersion](../../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)|이 JDBC 드라이버의 주 버전 번호를 검색합니다.|  
|[getDriverMinorVersion](../../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)|이 JDBC 드라이버의 부 버전 번호를 검색합니다.|  
|[getDriverName](../../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md)|이 JDBC 드라이버의 이름을 검색합니다.|  
|[getDriverVersion](../../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)|이 JDBC 드라이버의 버전 번호를 검색합니다.|  
|[getExportedKeys](../../../connect/jdbc/reference/getexportedkeys-method-sqlserverdatabasemetadata.md)|지정된 테이블의 기본 키 열을 참조하는 외래 키 열에 대한 설명을 검색합니다.|  
|[getExtraNameCharacters](../../../connect/jdbc/reference/getextranamecharacters-method-sqlserverdatabasemetadata.md)|따옴표가 없는 식별자 이름에서 사용할 수 있는 모든 추가 문자(예: a-z, A-Z, 0-9 및 _ 이외의 문자)를 검색합니다.|  
|[getFunctions](../../../connect/jdbc/reference/getfunctions-method-sqlserverdatabasemetadata.md)|시스템 및 사용자 함수에 대한 설명을 검색합니다.|  
|[getFunctionColumns](../../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)|지정된 카탈로그의 시스템 또는 사용자 함수 매개 변수와 반환 형식에 대한 설명을 검색합니다.|  
|[getIdentifierQuoteString](../../../connect/jdbc/reference/getidentifierquotestring-method-sqlserverdatabasemetadata.md)|SQL 식별자를 쿼리하는 데 사용되는 **문자열**을 검색합니다.|  
|[getImportedKeys](../../../connect/jdbc/reference/getimportedkeys-method-sqlserverdatabasemetadata.md)|테이블의 외래 키 열에서 참조하는 기본 키 열에 대한 설명을 검색합니다.|  
|[getIndexInfo](../../../connect/jdbc/reference/getindexinfo-method-sqlserverdatabasemetadata.md)|지정된 테이블의 인덱스 및 통계에 대한 설명을 검색합니다.|  
|[getJDBCMajorVersion](../../../connect/jdbc/reference/getjdbcmajorversion-method-sqlserverdatabasemetadata.md)|이 드라이버의 주 JDBC 버전 번호를 검색합니다.|  
|[getJDBCMinorVersion](../../../connect/jdbc/reference/getjdbcminorversion-method-sqlserverdatabasemetadata.md)|이 드라이버의 부 JDBC 버전 번호를 검색합니다.|  
|[getMaxBinaryLiteralLength](../../../connect/jdbc/reference/getmaxbinaryliterallength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 인라인 이진 리터럴에 허용하는 최대 16진수 문자 수를 검색합니다.|  
|[getMaxCatalogNameLength](../../../connect/jdbc/reference/getmaxcatalognamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 카탈로그 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxCharLiteralLength](../../../connect/jdbc/reference/getmaxcharliterallength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 문자 리터럴에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxColumnNameLength](../../../connect/jdbc/reference/getmaxcolumnnamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 열 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxColumnsInGroupBy](../../../connect/jdbc/reference/getmaxcolumnsingroupby-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 GROUP BY 절에 허용하는 최대 열 수를 검색합니다.|  
|[getMaxColumnsInIndex](../../../connect/jdbc/reference/getmaxcolumnsinindex-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 인덱스에 허용하는 최대 열 수를 검색합니다.|  
|[getMaxColumnsInOrderBy](../../../connect/jdbc/reference/getmaxcolumnsinorderby-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 ORDER BY 절에 허용하는 최대 열 수를 검색합니다.|  
|[getMaxColumnsInSelect](../../../connect/jdbc/reference/getmaxcolumnsinselect-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 SELECT 목록에 허용하는 최대 열 수를 검색합니다.|  
|[getMaxColumnsInTable](../../../connect/jdbc/reference/getmaxcolumnsintable-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 테이블에 허용하는 최대 열 수를 검색합니다.|  
|[getMaxConnections](../../../connect/jdbc/reference/getmaxconnections-method-sqlserverdatabasemetadata.md)|이 데이터베이스에 대해 가능한 최대 동시 연결 수를 검색합니다.|  
|[getMaxCursorNameLength](../../../connect/jdbc/reference/getmaxcursornamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 커서 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxIndexLength](../../../connect/jdbc/reference/getmaxindexlength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 인덱스(인덱스의 모든 부분 포함)에 허용하는 최대 바이트 수를 검색합니다.|  
|[getMaxProcedureNameLength](../../../connect/jdbc/reference/getmaxprocedurenamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 프로시저 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 단일 행에 허용하는 최대 바이트 수를 검색합니다.|  
|[getMaxSchemaNameLength](../../../connect/jdbc/reference/getmaxschemanamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 스키마 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxStatementLength](../../../connect/jdbc/reference/getmaxstatementlength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 SQL 문에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxStatements](../../../connect/jdbc/reference/getmaxstatements-method-sqlserverdatabasemetadata.md)|이 데이터베이스에 대해 동시에 열릴 수 있는 최대 활성 문 수를 검색합니다.|  
|[getMaxTableNameLength](../../../connect/jdbc/reference/getmaxtablenamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 테이블 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getMaxTablesInSelect](../../../connect/jdbc/reference/getmaxtablesinselect-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 SELECT 문에 허용하는 최대 테이블 수를 검색합니다.|  
|[getMaxUserNameLength](../../../connect/jdbc/reference/getmaxusernamelength-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 사용자 이름에 허용하는 최대 문자 수를 검색합니다.|  
|[getNumericFunctions](../../../connect/jdbc/reference/getnumericfunctions-method-sqlserverdatabasemetadata.md)|이 데이터베이스와 함께 사용할 수 있는 수치 연산 함수의 쉼표로 구분된 목록을 검색합니다.|  
|[getPrimaryKeys](../../../connect/jdbc/reference/getprimarykeys-method-sqlserverdatabasemetadata.md)|지정된 테이블의 기본 키 열에 대한 설명을 검색합니다.|  
|[getProcedureColumns](../../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md)|저장 프로시저 매개 변수 및 결과 열에 대한 설명을 검색합니다.|  
|[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md)|지정된 카탈로그, 스키마 또는 저장 프로시저 이름 패턴에 사용할 수 있는 저장 프로시저에 대한 설명을 검색합니다.|  
|[getProcedureTerm](../../../connect/jdbc/reference/getprocedureterm-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 "프로시저"에 사용하는 기본 용어를 검색합니다.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverdatabasemetadata.md)|이 데이터베이스에 대한 결과 집합의 기본 유지 기능을 검색합니다.|  
|[getRowIdLifetime](../../../connect/jdbc/reference/getrowidlifetime-method-sqlserverdatabasemetadata.md)|SQL RowId 데이터 형식이 지원되는지 여부를 나타내는 상태를 반환합니다. 이 데이터 형식이 지원되는 경우 이 메서드는 RowId 개체가 유효한 상태로 있는 수명을 반환합니다.|  
|[getSchemas](../../../connect/jdbc/reference/getschemas-method.md)|현재 데이터베이스에서 사용할 수 있는 스키마 이름을 검색합니다.|  
|[getSchemaTerm](../../../connect/jdbc/reference/getschematerm-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 "스키마"에 사용하는 기본 용어를 검색합니다.|  
|[getSearchStringEscape](../../../connect/jdbc/reference/getsearchstringescape-method-sqlserverdatabasemetadata.md)|와일드카드 문자를 이스케이프하는 데 사용할 수 있는 **문자열**을 검색합니다.|  
|[getSQLKeywords](../../../connect/jdbc/reference/getsqlkeywords-method-sqlserverdatabasemetadata.md)|이 데이터베이스의 SQL 키워드 중 SQL92 키워드와 중복되지 않는 모든 키워드의 쉼표로 구분된 목록을 검색합니다.|  
|[getSQLStateType](../../../connect/jdbc/reference/getsqlstatetype-method-sqlserverdatabasemetadata.md)|SQLException.getSQLState 메서드에서 반환된 SQLSTATE가 X/Open(현재는 Open Group이라고 함), SQL CLI, SQL99(JDBC 3.0) 또는 SQL:2003(JDBC 4.0) 중 무엇인지를 나타냅니다.|  
|[getStringFunctions](../../../connect/jdbc/reference/getstringfunctions-method-sqlserverdatabasemetadata.md)|이 데이터베이스와 함께 사용할 수 있는 **String** 함수의 쉼표로 구분된 목록을 검색합니다.|  
|[getSuperTables](../../../connect/jdbc/reference/getsupertables-method-sqlserverdatabasemetadata.md)|이 데이터베이스의 특정 스키마에 정의된 테이블 계층 구조에 대한 설명을 검색합니다.|  
|[getSuperTypes](../../../connect/jdbc/reference/getsupertypes-method-sqlserverdatabasemetadata.md)|이 데이터베이스의 특정 스키마에 정의된 사용자 정의 형식 계층 구조에 대한 설명을 검색합니다.|  
|[getSystemFunctions](../../../connect/jdbc/reference/getsystemfunctions-method-sqlserverdatabasemetadata.md)|이 데이터베이스와 함께 사용할 수 있는 시스템 함수의 쉼표로 구분된 목록을 검색합니다.|  
|[getTablePrivileges](../../../connect/jdbc/reference/gettableprivileges-method-sqlserverdatabasemetadata.md)|지정된 카탈로그, 스키마 또는 테이블 이름 패턴에 사용할 수 있는 각 테이블에 대한 액세스 권한 설명을 검색합니다.|  
|[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md)|지정된 카탈로그, 스키마 또는 테이블 이름 패턴에 사용할 수 있는 테이블에 대한 설명을 검색합니다.|  
|[getTableTypes](../../../connect/jdbc/reference/gettabletypes-method-sqlserverdatabasemetadata.md)|현재 데이터베이스에서 사용할 수 있는 테이블 형식을 검색합니다.|  
|[getTimeDateFunctions](../../../connect/jdbc/reference/gettimedatefunctions-method-sqlserverdatabasemetadata.md)|이 데이터베이스와 함께 사용할 수 있는 시간 및 날짜 함수의 쉼표로 구분된 목록을 검색합니다.|  
|[getTypeInfo](../../../connect/jdbc/reference/gettypeinfo-method-sqlserverdatabasemetadata.md)|현재 데이터베이스에서 지원하는 모든 표준 SQL 형식에 대한 설명을 검색합니다.|  
|[getUDTs](../../../connect/jdbc/reference/getudts-method-sqlserverdatabasemetadata.md)|특정 스키마에 정의된 사용자 정의 형식에 대한 설명을 검색합니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatabasemetadata.md)|이 데이터베이스의 URL을 검색합니다.|  
|[getUserName](../../../connect/jdbc/reference/getusername-method-sqlserverdatabasemetadata.md)|이 데이터베이스에 알려진 사용자 이름을 검색합니다.|  
|[getVersionColumns](../../../connect/jdbc/reference/getversioncolumns-method-sqlserverdatabasemetadata.md)|테이블에서 행 값이 업데이트될 때 자동으로 업데이트되는 열에 대한 설명을 검색합니다.|  
|[insertsAreDetected](../../../connect/jdbc/reference/insertsaredetected-method-sqlserverdatabasemetadata.md)|[SQLServerResultSet](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md) 클래스의 [rowInserted](../../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 호출하여 표시된 행 삽입을 검색할 수 있는지 여부를 검색합니다.|  
|[isCatalogAtStart](../../../connect/jdbc/reference/iscatalogatstart-method-sqlserverdatabasemetadata.md)|카탈로그가 정규화된 테이블 이름의 처음에 나타나는지 여부를 검색합니다.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverdatabasemetadata.md)|이 데이터베이스가 읽기 전용 모드에 있는지 여부를 검색합니다.|  
|[locatorsUpdateCopy](../../../connect/jdbc/reference/locatorsupdatecopy-method-sqlserverdatabasemetadata.md)|LOB에 대한 업데이트가 복사본에서 수행되는지 아니면 LOB에 직접 수행되는지를 나타냅니다.|  
|[nullPlusNonNullIsNull](../../../connect/jdbc/reference/nullplusnonnullisnull-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 NULL 값과 NULL이 아닌 값 사이의 연결이 NULL이 될 수 있는지 여부를 나타냅니다.|  
|[nullsAreSortedAtEnd](../../../connect/jdbc/reference/nullsaresortedatend-method-sqlserverdatabasemetadata.md)|정렬 순서에 관계없이 NULL 값이 끝에 정렬되는지 여부를 검색합니다.|  
|[nullsAreSortedAtStart](../../../connect/jdbc/reference/nullsaresortedatstart-method-sqlserverdatabasemetadata.md)|정렬 순서에 관계없이 NULL 값이 처음에 정렬되는지 여부를 검색합니다.|  
|[nullsAreSortedHigh](../../../connect/jdbc/reference/nullsaresortedhigh-method-sqlserverdatabasemetadata.md)|NULL 값이 상위에 정렬되는지 여부를 검색합니다.|  
|[nullsAreSortedLow](../../../connect/jdbc/reference/nullsaresortedlow-method-sqlserverdatabasemetadata.md)|NULL 값이 하위에 정렬되는지 여부를 검색합니다.|  
|[othersDeletesAreVisible](../../../connect/jdbc/reference/othersdeletesarevisible-method-sqlserverdatabasemetadata.md)|다른 사람이 수행한 삭제 내용이 표시되는지 여부를 검색합니다.|  
|[othersInsertsAreVisible](../../../connect/jdbc/reference/othersinsertsarevisible-method-sqlserverdatabasemetadata.md)|다른 사람이 수행한 삽입 내용이 표시되는지 여부를 검색합니다.|  
|[othersUpdatesAreVisible](../../../connect/jdbc/reference/othersupdatesarevisible-method-sqlserverdatabasemetadata.md)|다른 사람이 수행한 업데이트 내용이 표시되는지 여부를 검색합니다.|  
|[ownDeletesAreVisible](../../../connect/jdbc/reference/owndeletesarevisible-method-sqlserverdatabasemetadata.md)|결과 집합 자체의 삭제 내용이 표시되는지 여부를 검색합니다.|  
|[ownInsertsAreVisible](../../../connect/jdbc/reference/owninsertsarevisible-method-sqlserverdatabasemetadata.md)|결과 집합 자체의 삽입 내용이 표시되는지 여부를 검색합니다.|  
|[ownUpdatesAreVisible](../../../connect/jdbc/reference/ownupdatesarevisible-method-sqlserverdatabasemetadata.md)|결과 집합 자체의 업데이트 내용이 표시되는지 여부를 검색합니다.|  
|[storesLowerCaseIdentifiers](../../../connect/jdbc/reference/storeslowercaseidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이지 않고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 소문자로 저장하는지 여부를 검색합니다.|  
|[storesLowerCaseQuotedIdentifiers](../../../connect/jdbc/reference/storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 소문자로 저장하는지 여부를 검색합니다.|  
|[storesMixedCaseIdentifiers](../../../connect/jdbc/reference/storesmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이지 않고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대/소문자가 혼합된 형식으로 저장하는지 여부를 검색합니다.|  
|[storesMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대/소문자가 혼합된 형식으로 저장하는지 여부를 검색합니다.|  
|[storesUpperCaseIdentifiers](../../../connect/jdbc/reference/storesuppercaseidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이지 않고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대문자로 저장하는지 여부를 검색합니다.|  
|[storesUpperCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대문자로 저장하는지 여부를 검색합니다.|  
|[supportsAlterTableWithAddColumn](../../../connect/jdbc/reference/supportsaltertablewithaddcolumn-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 열 추가를 통한 ALTER TABLE을 지원하는지 여부를 검색합니다.|  
|[supportsAlterTableWithDropColumn](../../../connect/jdbc/reference/supportsaltertablewithdropcolumn-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 열 삭제를 통한 ALTER TABLE을 지원하는지 여부를 검색합니다.|  
|[supportsANSI92EntryLevelSQL](../../../connect/jdbc/reference/supportsansi92entrylevelsql-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ANSI92 초급 단계 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsANSI92FullSQL](../../../connect/jdbc/reference/supportsansi92fullsql-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ANSI92 전체 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsANSI92IntermediateSQL](../../../connect/jdbc/reference/supportsansi92intermediatesql-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ANSI92 중간 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsBatchUpdates](../../../connect/jdbc/reference/supportsbatchupdates-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 일괄 처리 업데이트를 지원하는지 여부를 검색합니다.|  
|[supportsCatalogsInDataManipulation](../../../connect/jdbc/reference/supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata.md)|데이터 조작 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsCatalogsInIndexDefinitions](../../../connect/jdbc/reference/supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata.md)|인덱스 정의 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsCatalogsInPrivilegeDefinitions](../../../connect/jdbc/reference/supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|권한 정의 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsCatalogsInProcedureCalls](../../../connect/jdbc/reference/supportscatalogsinprocedurecalls-method-sqlserverdatabasemetadata.md)|프로시저 호출 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsCatalogsInTableDefinitions](../../../connect/jdbc/reference/supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata.md)|테이블 정의 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsColumnAliasing](../../../connect/jdbc/reference/supportscolumnaliasing-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 열 별칭 지정을 지원하는지 여부를 검색합니다.|  
|[supportsConvert](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SQL 형식 간의 CONVERT 기능을 지원하는지 여부를 검색합니다.|  
|[supportsCoreSQLGrammar](../../../connect/jdbc/reference/supportscoresqlgrammar-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ODBC 핵심 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsCorrelatedSubqueries](../../../connect/jdbc/reference/supportscorrelatedsubqueries-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 상관 하위 쿼리를 지원하는지 여부를 검색합니다.|  
|[supportsDataDefinitionAndDataManipulationTransactions](../../../connect/jdbc/reference/supportsdatadefinitionanddatamanipulationtransactions-method.md)|이 데이터베이스에서 트랜잭션 내의 데이터 정의 및 데이터 조작 문을 지원하는지 여부를 검색합니다.|  
|[supportsDataManipulationTransactionsOnly](../../../connect/jdbc/reference/supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 트랜잭션 내의 데이터 정의 및 데이터 조작 문만 지원하는지 여부를 검색합니다.|  
|[supportsDifferentTableCorrelationNames](../../../connect/jdbc/reference/supportsdifferenttablecorrelationnames-method-sqlserverdatabasemetadata.md)|테이블 상관 관계 이름이 지원되는 경우 이 이름이 테이블 이름과는 다르도록 제한되는지 여부를 검색합니다.|  
|[supportsExpressionsInOrderBy](../../../connect/jdbc/reference/supportsexpressionsinorderby-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ORDER BY 목록의 식을 지원하는지 여부를 검색합니다.|  
|[supportsExtendedSQLGrammar](../../../connect/jdbc/reference/supportsextendedsqlgrammar-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ODBC 확장 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsFullOuterJoins](../../../connect/jdbc/reference/supportsfullouterjoins-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 중첩된 외부 조인을 모두 지원하는지 여부를 검색합니다.|  
|[supportsGetGeneratedKeys](../../../connect/jdbc/reference/supportsgetgeneratedkeys-method-sqlserverdatabasemetadata.md)|문이 실행된 후 자동 생성된 키를 검색할 수 있는지 여부를 검색합니다.|  
|[supportsGroupBy](../../../connect/jdbc/reference/supportsgroupby-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 일부 형식의 GROUP BY 절을 지원하는지 여부를 검색합니다.|  
|[supportsGroupByBeyondSelect](../../../connect/jdbc/reference/supportsgroupbybeyondselect-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SELECT 문의 모든 열이 GROUP BY 절에 포함된 경우 SELECT 문에 포함되지 않은 열을 GROUP BY 절에 사용할 수 있는지 여부를 검색합니다.|  
|[supportsGroupByUnrelated](../../../connect/jdbc/reference/supportsgroupbyunrelated-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SELECT 문에 포함되지 않은 열을 GROUP BY 절에 사용할 수 있는지 여부를 검색합니다.|  
|[supportsIntegrityEnhancementFacility](../../../connect/jdbc/reference/supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SQL 무결성 향상 기능을 지원하는지 여부를 검색합니다.|  
|[supportsLikeEscapeClause](../../../connect/jdbc/reference/supportslikeescapeclause-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 LIKE 이스케이프 절을 지정할 수 있는지 여부를 검색합니다.|  
|[supportsLimitedOuterJoins](../../../connect/jdbc/reference/supportslimitedouterjoins-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 외부 조인을 제한적으로 지원하는지 여부를 검색합니다.|  
|[supportsMinimumSQLGrammar](../../../connect/jdbc/reference/supportsminimumsqlgrammar-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 ODBC 최소 SQL 문법을 지원하는지 여부를 검색합니다.|  
|[supportsMixedCaseIdentifiers](../../../connect/jdbc/reference/supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이지 않고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대/소문자가 혼합된 형식으로 저장하는지 여부를 검색합니다.|  
|[supportsMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 따옴표로 묶이고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 대/소문자가 혼합된 형식으로 저장하는지 여부를 검색합니다.|  
|[supportsMultipleOpenResults](../../../connect/jdbc/reference/supportsmultipleopenresults-method-sqlserverdatabasemetadata.md)|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에서 동시에 여러 개의 [SQLServerResultSet](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체가 반환될 수 있는지 여부를 검색합니다.|  
|[supportsMultipleResultSets](../../../connect/jdbc/reference/supportsmultipleresultsets-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 [execute](../../../connect/jdbc/reference/execute-method.md) 메서드를 한 번 호출하여 여러 개의 [SQLServerResultSet](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체를 가져올 수 있는지 여부를 검색합니다.|  
|[supportsMultipleTransactions](../../../connect/jdbc/reference/supportsmultipletransactions-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 여러 개의 트랜잭션이 서로 다른 연결에서 동시에 열려 있을 수 있는지 여부를 검색합니다.|  
|[supportsNamedParameters](../../../connect/jdbc/reference/supportsnamedparameters-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 호출 가능한 문의 명명된 매개 변수를 지원하는지 여부를 검색합니다.|  
|[supportsNonNullableColumns](../../../connect/jdbc/reference/supportsnonnullablecolumns-method-sqlserverdatabasemetadata.md)|이 데이터베이스의 열을 Null을 허용하지 않는 열로 정의할 수 있는지 여부를 검색합니다.|  
|[supportsOpenCursorsAcrossCommit](../../../connect/jdbc/reference/supportsopencursorsacrosscommit-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 여러 번 커밋하는 동안 커서를 열어 둘 수 있는지 여부를 검색합니다.|  
|[supportsOpenCursorsAcrossRollback](../../../connect/jdbc/reference/supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 여러 번 롤백하는 동안 커서를 열어 둘 수 있는지 여부를 검색합니다.|  
|[supportsOpenStatementsAcrossCommit](../../../connect/jdbc/reference/supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 여러 번 커밋하는 동안 문을 열어 둘 수 있는지 여부를 검색합니다.|  
|[supportsOpenStatementsAcrossRollback](../../../connect/jdbc/reference/supportsopenstatementsacrossrollback-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 여러 번 롤백하는 동안 문을 열어 둘 수 있는지 여부를 검색합니다.|  
|[supportsOrderByUnrelated](../../../connect/jdbc/reference/supportsorderbyunrelated-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SELECT 문에 포함되지 않은 열을 ORDER BY 절에 사용할 수 있는지 여부를 검색합니다.|  
|[supportsOuterJoins](../../../connect/jdbc/reference/supportsouterjoins-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 일부 형식의 외부 조인을 지원하는지 여부를 검색합니다.|  
|[supportsPositionedDelete](../../../connect/jdbc/reference/supportspositioneddelete-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 위치 지정된 DELETE 문을 지원하는지 여부를 검색합니다.|  
|[supportsPositionedUpdate](../../../connect/jdbc/reference/supportspositionedupdate-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 위치 지정된 UPDATE 문을 지원하는지 여부를 검색합니다.|  
|[supportsResultSetConcurrency](../../../connect/jdbc/reference/supportsresultsetconcurrency-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 지정된 결과 집합 유형과 함께 지정된 동시성 유형을 지원하는지 여부를 검색합니다.|  
|[supportsResultSetHoldability](../../../connect/jdbc/reference/supportsresultsetholdability-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 지정된 결과 집합 유지 기능을 지원하는지 여부를 검색합니다.|  
|[supportsResultSetType](../../../connect/jdbc/reference/supportsresultsettype-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 지정된 결과 집합 유형을 지원하는지 여부를 검색합니다.|  
|[supportsSavepoints](../../../connect/jdbc/reference/supportssavepoints-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 저장점을 지원하는지 여부를 검색합니다.|  
|[supportsSchemasInDataManipulation](../../../connect/jdbc/reference/supportsschemasindatamanipulation-method-sqlserverdatabasemetadata.md)|데이터 조작 문에 스키마 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsSchemasInIndexDefinitions](../../../connect/jdbc/reference/supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata.md)|인덱스 정의 문에 스키마 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsSchemasInPrivilegeDefinitions](../../../connect/jdbc/reference/supportsschemasinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|권한 정의 문에 스키마 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsSchemasInProcedureCalls](../../../connect/jdbc/reference/supportsschemasinprocedurecalls-method-sqlserverdatabasemetadata.md)|프로시저 호출 문에 스키마 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsSchemasInTableDefinitions](../../../connect/jdbc/reference/supportsschemasintabledefinitions-method-sqlserverdatabasemetadata.md)|테이블 정의 문에 스키마 이름을 사용할 수 있는지 여부를 검색합니다.|  
|[supportsSelectForUpdate](../../../connect/jdbc/reference/supportsselectforupdate-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SELECT FOR UPDATE 문을 지원하는지 여부를 검색합니다.|  
|[supportsStatementPooling](../../../connect/jdbc/reference/supportsstatementpooling-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 문 풀링을 지원하는지 여부를 검색합니다.|  
|[supportsStoredFunctionsUsingCallSyntax](../../../connect/jdbc/reference/supportsstoredfunctionsusingcallsyntax-method-sqlserverdatabasemetadata.md)|현재 데이터베이스에서 저장 프로시저 이스케이프 구문을 사용하여 사용자 정의 또는 공급업체 정의 함수를 호출할 수 있는지 여부를 나타냅니다.|  
|[supportsStoredProcedures](../../../connect/jdbc/reference/supportsstoredprocedures-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 저장 프로시저 이스케이프 구문을 사용한 저장 프로시저 호출을 지원하는지 여부를 검색합니다.|  
|[supportsSubqueriesInComparisons](../../../connect/jdbc/reference/supportssubqueriesincomparisons-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 비교 식의 하위 쿼리를 지원하는지 여부를 검색합니다.|  
|[supportsSubqueriesInExists](../../../connect/jdbc/reference/supportssubqueriesinexists-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 EXISTS 식의 하위 쿼리를 지원하는지 여부를 검색합니다.|  
|[supportsSubqueriesInIns](../../../connect/jdbc/reference/supportssubqueriesinins-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 IN 식의 하위 쿼리를 지원하는지 여부를 검색합니다.|  
|[supportsSubqueriesInQuantifieds](../../../connect/jdbc/reference/supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 정량화된 식의 하위 쿼리를 지원하는지 여부를 검색합니다.|  
|[supportsTableCorrelationNames](../../../connect/jdbc/reference/supportstablecorrelationnames-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 테이블 상관 관계 이름을 지원하는지 여부를 검색합니다.|  
|[supportsTransactionIsolationLevel](../../../connect/jdbc/reference/supportstransactionisolationlevel-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 지정된 트랜잭션 격리 수준을 지원하는지 여부를 검색합니다.|  
|[supportsTransactions](../../../connect/jdbc/reference/supportstransactions-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 트랜잭션을 지원하는지 여부를 검색합니다.|  
|[supportsUnion](../../../connect/jdbc/reference/supportsunion-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SQL UNION을 지원하는지 여부를 검색합니다.|  
|[supportsUnionAll](../../../connect/jdbc/reference/supportsunionall-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 SQL UNION ALL을 지원하는지 여부를 검색합니다.|  
|[updatesAreDetected](../../../connect/jdbc/reference/updatesaredetected-method-sqlserverdatabasemetadata.md)|[SQLServerResultSet](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) 클래스의 [rowUpdated](../../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 호출하여 표시된 행 업데이트를 검색할 수 있는지 여부를 검색합니다.|  
|[usesLocalFilePerTable](../../../connect/jdbc/reference/useslocalfilepertable-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 각 테이블에 대해 개별 파일을 사용하는지 여부를 검색합니다.|  
|[usesLocalFiles](../../../connect/jdbc/reference/useslocalfiles-method-sqlserverdatabasemetadata.md)|이 데이터베이스에서 테이블을 로컬 파일에 저장하는지 여부를 검색합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
