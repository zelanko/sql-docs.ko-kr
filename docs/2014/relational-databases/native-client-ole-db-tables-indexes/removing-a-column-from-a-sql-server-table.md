---
title: SQL Server 테이블에서 열 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7b5173ad5f617eccf41f8e8d60a81305ff1ca48
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409932"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>SQL Server 테이블에서 열 제거
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **ITableDefinition::DropColumn** 함수입니다. 이렇게 하면에서 열을 제거 하려면 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 소비자에서 유니코드 문자열로 테이블 이름을 지정 합니다 *pwszName*의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수입니다. 합니다 *eKind*소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 소비자의 열 이름을 나타냅니다 합니다 *pwszName*의 멤버는 *uName* 공용 구조체의 *pColumnID* 매개 변수입니다. 열 이름은 유니코드 문자열입니다. 합니다 *eKind* 소속 *pColumnID* DBKIND_NAME 이어야 합니다.  
  
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
 [테이블 및 인덱스](tables-and-indexes.md)  
  
  
