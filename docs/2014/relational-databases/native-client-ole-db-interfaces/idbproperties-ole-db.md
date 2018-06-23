---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bee573d18bce37685612ab79a715834ca27e5fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093304"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
  OLE DB 표준 사양을 통해 공급자가 `DBPROPINFO::vValues`에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 하는 경우 항상 VT_EMPTY를 반환 Native Client OLE DB `IDBProperties::GetPropertyInfo` 와 `DBPROPSET_ROWSETALL` 행 집합 속성을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  