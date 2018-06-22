---
title: SQL Server 테이블에서 열 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a41ffd9ca8791de63f7abcf17e50c2474e6754e2
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699864"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>SQL Server 테이블에서 열 제거
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 된 **ITableDefinition::DropColumn** 함수입니다. 이렇게 하면 열을 제거 하는 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
