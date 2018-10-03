---
title: SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e5bb94b8b99881784dba458969ba4b24789ee85
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839811"
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLTables는 정적 서버 커서에 대해 실행할 수 있습니다. SQLTables 업데이트 가능한 (동적 또는 키 집합) 커서에서 실행 하려고 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 SQLTables의 모든 테이블을 보고 될 때 데이터베이스를 *CatalogName* 매개 변수가 sql_all_catalogs이 고 다른 모든 매개 변수가 기본값 (NULL 포인터)을 포함 합니다.  
  
 사용 가능한 카탈로그, 스키마 및 테이블 형식 보고서를 SQLTables는 특수 한 빈 문자열 (길이가 0 인 바이트 포인터) 사용 합니다. 빈 문자열은 기본값(NULL 포인터)이 아닙니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 그대로 사용 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
 SQLTables 반환에 대 한 정보가 테이블 이름이 일치 *TableName* 고 현재 사용자가 소유 합니다.  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 및 테이블 반환 매개 변수  
 문 특성 SQL_SOPT_SS_NAME_SCOPE에 기본값인 SQL_SS_NAME_SCOPE_TABLE이 아니라 SQL_SS_NAME_SCOPE_TABLE_TYPE 값이 있으면 SQLTables 테이블 형식에 대 한 정보를 반환 합니다. SQLTables 반환한 결과 집합의 열 4에서에서 테이블 형식에 대해 반환 되는 TABLE_TYPE 값은 테이블 형식입니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 하세요. [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 테이블, 뷰 및 동의어는 테이블 형식에 사용되는 네임스페이스와 다른 공용 네임스페이스를 공유합니다. 따라서 테이블과 뷰를 같은 이름으로 만들 수는 없지만 동일한 카탈로그 및 스키마에서 테이블과 테이블 형식을 같은 이름으로 만드는 것은 가능합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="example"></a>예제  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQLTables 함수](http://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
