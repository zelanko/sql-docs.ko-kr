---
title: 테이블 및 인덱스 | Microsoft Docs
description: 생성, 변경 및 droping 테이블 및 OLE DB 드라이버를 사용 하 여 SQL Server에 대 한 인덱스
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79fe84a1a8e741a29f8796a84a63a5d7b7466d8f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="tables-and-indexes"></a>테이블 및 인덱스
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server 노출 된 **IIndexDefinition** 및 **ITableDefinition** 인터페이스를 만들려면 소비자가 변경 하 고 삭제할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 및 인덱스입니다. 올바른 테이블 및 인덱스 정의는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다.  
  
 테이블과 인덱스를 만들거나 삭제하는 기능은 소비자 응용 프로그램 사용자의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 액세스 권한에 따라 달라집니다. 테이블 삭제는 선언적 참조 무결성 제약 조건이나 다른 요인이 있는지 여부에 따라 더욱 제한할 수 있습니다.  
  
 대부분의 응용 프로그램을 대상으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server 인터페이스에 대 한 이러한 OLE DB Driver 대신 SQL-DMO를 사용 합니다. SQL-DMO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 모든 관리 기능을 지원하는 OLE Automation 개체 컬렉션입니다. 여러 OLE DB 공급자를 대상으로 하는 응용 프로그램은 다양한 OLE DB 공급자가 지원하는 일반 OLE DB 인터페이스를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 공급자별 속성 집합 DBPROPSET_SQLSERVERCOLUMN에 다음과 같은 속성을 정의합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|유형: VT_BSTR<br /><br /> R/W: 쓰기<br /><br /> 기본값: Null<br /><br /> 설명:이 속성은 사용에 **ITableDefinition**합니다. 이 속성에 지정 된 문자열은 만들 때 사용 되는 [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> 문을 만들 때 사용됩니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 테이블 만들기](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [SQL Server 테이블에 열 추가](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [SQL Server 테이블에서 열 제거](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [SQL Server 테이블 삭제](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [SQL Server 인덱스 만들기](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [SQL Server 인덱스 삭제](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)   
 [DROP table& #40; Transact SQL & #41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
