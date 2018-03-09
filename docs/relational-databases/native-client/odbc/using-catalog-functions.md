---
title: "카탈로그 함수를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77d2f7de5e43df5cfc559b12bb88dcdd4412af6e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="using-catalog-functions"></a>카탈로그 함수 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  모든 데이터베이스에는 데이터베이스에 저장된 데이터를 포함하는 구조가 있습니다. 이 구조의 정의는 데이터 사전이라고도 하는 시스템 테이블의 집합으로 구현된 카탈로그에 사용 권한과 같은 다른 정보와 함께 저장됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용 하면 응용 프로그램을 ODBC 카탈로그 함수 호출을 통해 데이터베이스 구조를 확인 합니다. 카탈로그 함수는 결과 집합에 정보를 반환하며 카탈로그의 시스템 테이블을 쿼리하는 카탈로그 저장 프로시저를 사용하여 구현됩니다. 예를 들어 응용 프로그램은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다. 표준 ODBC 카탈로그 함수는 응용 프로그램이 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 카탈로그 정보를 가져오는 데 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 단일 쿼리를 통해 여러 다른 유형의 OLE DB 데이터 원본에 있는 데이터에 액세스하는 분산 쿼리를 지원합니다. 원격 OLE DB 데이터 원본에 액세스하는 방법 중 하나는 데이터 원본을 연결된 서버로 정의하는 것입니다. 사용 하 여이 작업을 수행할 수 있습니다 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)합니다. 연결된 서버를 정의하면 Transact-SQL 문에서 네 부분으로 된 이름을 사용하여 해당 서버의 개체를 참조할 수 있습니다.  
  
 *linked_server_name.catalog.schema.object_name*.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결된 서버에서 카탈로그 정보를 얻는 데 도움이 되는 두 가지 드라이버별 함수를 지원합니다.  
  
-   **SQLLinkedServers**  
  
     로컬 서버에 대해 정의되어 있는 연결된 서버 목록을 반환합니다.  
  
-   **SQLLinkedCatalogs**  
  
     연결된 서버에 포함되어 있는 카탈로그 목록을 반환합니다.  
  
 연결 된 서버 이름 및 카탈로그 이름을 구성한 후의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 두 부분으로 이루어진 이름을 사용 하 여 카탈로그에서 정보를 가져오지 지원 *linked_server_name과***.*** 카탈로그* 에 대 한 *CatalogName* 다음 odbc 카탈로그 함수:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 두 부분 *linked_server_name과***.*** 카탈로그* 에 지원 됩니다 *FKCatalogName* 및 *PKCatalogName* 에 [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md)합니다.  
  
 SQLLinkedServers 및 SQLLinkedCatalogs를 사용하려면 다음 파일이 필요합니다.  
  
-   sqlncli.h  
  
     연결된 서버 카탈로그 함수를 위한 함수 프로토타입 및 상수 정의를 포함합니다. sqlncli.h는 ODBC 응용 프로그램에 포함되어야 하며 응용 프로그램을 컴파일할 때 포함 경로에 있어야 합니다.  
  
-   sqlncli11.lib  
  
     링커의 라이브러리 경로에 있어야 하며 링크할 파일로 지정해야 합니다. sqlncli11.lib는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
-   sqlncli11.dll  
  
     실행 단계에 있어야 합니다. sqlncli11.dll은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../../relational-databases/native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../../relational-databases/native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
  
