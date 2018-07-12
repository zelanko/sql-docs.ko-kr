---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71999899b70c8eab76e26dba22f09884618277d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413611"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
  OLE DB 표준 사양을 통해 공급자가 `DBPROPINFO::vValues`에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB는 항상 VT_EMPTY를 반환를 호출할 때 `IDBProperties::GetPropertyInfo` 사용 하 여 `DBPROPSET_ROWSETALL` 행 집합 속성을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
