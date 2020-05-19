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
manager: craigg
ms.openlocfilehash: 7598f1c865395f2a43eba8f67c86a68bd46d586b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707359"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
  OLE DB 표준 사양을 통해 공급자가 `DBPROPINFO::vValues`에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 하 여 `IDBProperties::GetPropertyInfo` `DBPROPSET_ROWSETALL` 행 집합 속성을 검색 하는 경우 Native Client OLE DB는 항상 VT_EMPTY를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
