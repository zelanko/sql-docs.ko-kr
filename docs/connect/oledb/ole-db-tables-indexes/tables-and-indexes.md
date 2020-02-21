---
title: 테이블 및 인덱스 | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 테이블 및 인덱스 만들기, 변경 및 삭제
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- OLE DB Driver for SQL Server, tables
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0fc8aeed348f64c17894fa3432a7a81274ffbea4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015243"
---
# <a name="tables-and-indexes"></a>테이블 및 인덱스
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버는 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블과 인덱스를 생성, 변경 및 삭제할 수 있도록 **IIndexDefinition** 및 **ITableDefinition** 인터페이스를 노출합니다. 올바른 테이블 및 인덱스 정의는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다.  
  
 테이블과 인덱스를 만들거나 삭제하는 기능은 소비자 애플리케이션 사용자의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 액세스 권한에 따라 달라집니다. 테이블 삭제는 선언적 참조 무결성 제약 조건이나 다른 요인이 있는지 여부에 따라 더욱 제한할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 대상으로 하는 대부분의 애플리케이션은 이 OLE DB Driver for SQL Server 인터페이스 대신 SQL-DMO를 사용합니다. SQL-DMO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 모든 관리 기능을 지원하는 OLE Automation 개체 컬렉션입니다. 여러 OLE DB 공급자를 대상으로 하는 애플리케이션은 다양한 OLE DB 공급자가 지원하는 일반 OLE DB 인터페이스를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 공급자별 속성 집합 DBPROPSET_SQLSERVERCOLUMN에 다음과 같은 속성을 정의합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|유형: VT_BSTR<br /><br /> R/W: 쓰기<br /><br /> Default: Null<br /><br /> 설명: 이 속성은 **ITableDefinition**에서만 사용됩니다. 이 속성에 지정된 문자열은 [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)을 생성할 때 사용됨<br /><br /> 문을 만들 때 사용됩니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 테이블 만들기](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [SQL Server 테이블에 열 추가](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [SQL Server 테이블에서 열 제거](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [SQL Server 테이블 삭제](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [SQL Server 인덱스 만들기](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [SQL Server 인덱스 삭제](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
