---
description: 카탈로그 함수 사용
title: 카탈로그 함수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5047e64eed31c1b6853cbe23fc2008d61015fbca
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467614"
---
# <a name="using-catalog-functions"></a>카탈로그 함수 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  모든 데이터베이스에는 데이터베이스에 저장된 데이터를 포함하는 구조가 있습니다. 이 구조의 정의는 데이터 사전이라고도 하는 시스템 테이블의 집합으로 구현된 카탈로그에 사용 권한과 같은 다른 정보와 함께 저장됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버를 사용 하면 응용 프로그램에서 odbc 카탈로그 함수를 호출 하 여 데이터베이스 구조를 확인할 수 있습니다. 카탈로그 함수는 결과 집합에 정보를 반환하며 카탈로그의 시스템 테이블을 쿼리하는 카탈로그 저장 프로시저를 사용하여 구현됩니다. 예를 들어 애플리케이션은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다. 표준 ODBC 카탈로그 함수는 애플리케이션이 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 카탈로그 정보를 가져오는 데 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 단일 쿼리를 통해 여러 다른 유형의 OLE DB 데이터 원본에 있는 데이터에 액세스하는 분산 쿼리를 지원합니다. 원격 OLE DB 데이터 원본에 액세스하는 방법 중 하나는 데이터 원본을 연결된 서버로 정의하는 것입니다. [Sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용 하 여이 작업을 수행할 수 있습니다. 연결된 서버를 정의하면 Transact-SQL 문에서 네 부분으로 된 이름을 사용하여 해당 서버의 개체를 참조할 수 있습니다.  
  
 *linked_server_name. object_name*.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결된 서버에서 카탈로그 정보를 얻는 데 도움이 되는 두 가지 드라이버별 함수를 지원합니다.  
  
-   **SQLLinkedServers**  
  
     로컬 서버에 대해 정의되어 있는 연결된 서버 목록을 반환합니다.  
  
-   **SQLLinkedCatalogs**  
  
     연결된 서버에 포함되어 있는 카탈로그 목록을 반환합니다.  
  
 연결 된 서버 이름과 카탈로그 이름이 있으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 _linked_server_name_ 의 두 부분으로 된 이름을 사용 하 여 카탈로그에서 정보 가져오기를 지원 합니다 **.** 다음 ODBC 카탈로그 함수에서 *CatalogName* 에 대 한 _카탈로그_ :  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 두 부분으로 구성 된 _linked_server_name_**입니다.** _카탈로그_ 는 [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md)의 *FKCatalogName* 및 *PKCatalogName* 에 대해서도 지원 됩니다.  
  
 SQLLinkedServers 및 SQLLinkedCatalogs를 사용하려면 다음 파일이 필요합니다.  
  
-   sqlncli.h  
  
     연결된 서버 카탈로그 함수를 위한 함수 프로토타입 및 상수 정의를 포함합니다. sqlncli.h는 ODBC 애플리케이션에 포함되어야 하며 애플리케이션을 컴파일할 때 포함 경로에 있어야 합니다.  
  
-   sqlncli11.lib  
  
     링커의 라이브러리 경로에 있어야 하며 링크할 파일로 지정해야 합니다. sqlncli11.lib는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
-   sqlncli11.dll  
  
     실행 단계에 있어야 합니다. sqlncli11.dll은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../../relational-databases/native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../../relational-databases/native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
  
