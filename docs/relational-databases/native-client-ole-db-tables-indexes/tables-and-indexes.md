---
title: 테이블 및 인덱스 (Native Client OLE DB 공급자)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- SQL Server Native Client OLE DB provider, tables
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: 4217c6d8-8cd2-43dc-b36f-3cfd8a58fabc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3cceffac463294bce24b3573aca6ecdeae2ce599
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332310"
---
# <a name="tables-and-indexes-in-sql-server-native-client"></a>SQL Server Native Client의 테이블 및 인덱스
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 소비자가 테이블과 인덱스를 생성, 변경 및 삭제할 수 있도록 **Iindexdefinition** 및 **itabledefinition** 인터페이스를 제공 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 올바른 테이블 및 인덱스 정의는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다.  
  
 테이블과 인덱스를 만들거나 삭제하는 기능은 소비자 애플리케이션 사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 권한에 따라 달라집니다. 테이블 삭제는 선언적 참조 무결성 제약 조건이나 다른 요인이 있는지 여부에 따라 더욱 제한할 수 있습니다.  
  
 을 대상으로 하는 대부분의 응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 인터페이스 대신 sql-dmo를 사용 합니다. SQL-DMO는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 관리 기능을 지원하는 OLE Automation 개체 컬렉션입니다. 여러 OLE DB 공급자를 대상으로 하는 애플리케이션은 다양한 OLE DB 공급자가 지원하는 일반 OLE DB 인터페이스를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 공급자별 속성 집합 DBPROPSET_SQLSERVERCOLUMN에 다음과 같은 속성을 정의합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|유형: VT_BSTR<br /><br /> R/W: 쓰기<br /><br /> 기본값: Null<br /><br /> 설명: 이 속성은 **ITableDefinition**에서만 사용됩니다. 이 속성에 지정된 문자열은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)을 생성할 때 사용됨<br /><br /> 문을 만들 때 사용됩니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 테이블 만들기](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [SQL Server 테이블에 열 추가](../../relational-databases/native-client-ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [SQL Server 테이블에서 열 제거](../../relational-databases/native-client-ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [SQL Server 테이블 삭제](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [SQL Server 인덱스 만들기](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [SQL Server 인덱스 삭제](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
