---
title: SQL Server 테이블에서 열 제거 (Native Client OLE DB 공급자)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0aa472e45dd9e5f1f7ae830684fa9d55f11c53c4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87240469"
---
# <a name="removing-a-column-from-a-sql-server-table-native-client-ole-db-provider"></a>SQL Server 테이블에서 열 제거 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 **Itabledefinition::D ropcolumn** 함수를 노출 합니다. 이 함수를 사용하여 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 열을 제거할 수 있습니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에서 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind*멤버는 DBKIND_NAME이어야 합니다.  
  
 소비자는 *pColumnID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 구성원에 열 이름을 표시합니다. 열 이름은 유니코드 문자열입니다. *pColumnID*의 *eKind*멤버는 DBKIND_NAME이어야 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
