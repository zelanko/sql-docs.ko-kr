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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f3fa2b053c41facba7d608b2352772abd3ff103
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291772"
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLTables는 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 SQLTables를 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 SQLTables는 *CatalogName* 매개 변수가 SQL_ALL_CATALOGS 되 고 다른 모든 매개 변수에 기본값 (NULL 포인터)이 포함 된 경우 모든 데이터베이스의 테이블을 보고 합니다.  
  
 SQLTables는 사용 가능한 카탈로그, 스키마 및 테이블 형식을 보고 하기 위해 빈 문자열 (길이가 0 인 바이트 포인터)을 특별 하 게 사용 합니다. 빈 문자열은 기본값(NULL 포인터)이 아닙니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
 SQLTables는 이름이 *TableName* 과 일치 하 고 현재 사용자가 소유 하 고 있는 모든 테이블에 대 한 정보를 반환 합니다.  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 및 테이블 반환 매개 변수  
 Statement 특성 SQL_SOPT_SS_NAME_SCOPE의 기본값 SQL_SS_NAME_SCOPE_TABLE이 아닌 SQL_SS_NAME_SCOPE_TABLE_TYPE 값이 있으면 SQLTables는 테이블 형식에 대 한 정보를 반환 합니다. SQLTables에서 반환 된 결과 집합의 열 4에서 테이블 형식에 대해 반환 되는 TABLE_TYPE 값은 테이블 형식입니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.  
  
 테이블, 뷰 및 동의어는 테이블 형식에 사용되는 네임스페이스와 다른 공용 네임스페이스를 공유합니다. 따라서 테이블과 뷰를 같은 이름으로 만들 수는 없지만 동일한 카탈로그 및 스키마에서 테이블과 테이블 형식을 같은 이름으로 만드는 것은 가능합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLTables 함수](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
