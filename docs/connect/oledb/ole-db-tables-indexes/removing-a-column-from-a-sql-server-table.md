---
title: SQL Server 테이블에서 열 제거 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 SQL Server 테이블에서 열을 제거 합니다.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- OLE DB Driver for SQL Server, columns
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4047c464ac1f2a27222f8d15160cbeaf75ba37c6
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="removing-a-column-from-a-sql-server-table"></a>SQL Server 테이블에서 열 제거
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server 노출 된 **ITableDefinition::DropColumn** 함수입니다. 이렇게 하면 열을 제거 하는 소비자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 소비자의 유니코드 문자열에서 테이블 이름을 지정는 *pwszName*의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind*소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 소비자의 열 이름을 나타냅니다는 *pwszName*의 멤버는 *uName* 공용 구조체는 *pColumnID* 매개 변수입니다. 열 이름은 유니코드 문자열입니다. *eKind* 소속 *pColumnID* DBKIND_NAME 이어야 합니다.  
  
## <a name="example"></a>예제  
  
### <a name="code"></a>코드  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
