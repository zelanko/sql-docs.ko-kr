---
title: IDBProperties(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: rothja
ms.author: jroth
ms.openlocfilehash: f42ab47de2471fc413e4c6acf0d6c61cb2b6d77c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056193"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
  OLE DB 표준 사양을 통해 공급자가 `DBPROPINFO::vValues`에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 하 여 `IDBProperties::GetPropertyInfo` `DBPROPSET_ROWSETALL` 행 집합 속성을 검색 하는 경우 Native Client OLE DB는 항상 VT_EMPTY를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
