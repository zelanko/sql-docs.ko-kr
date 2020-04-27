---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3af18120af91fe06da48c2e3636bf8a7c572161
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919298"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
커서 서비스의 위치를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|로컬 커서 라이브러리에서 제공 하는 클라이언트 쪽 커서를 사용 합니다. 로컬 커서 서비스를 사용 하면 드라이버에서 제공 하는 커서의 많은 기능을 사용할 수 있으므로이 설정을 사용 하면 사용할 수 있는 기능과 관련 된 이점을 얻을 수 있습니다. 이전 버전과의 호환성을 위해 동의어 **adUseClientBatch** 지원 됩니다.|  
|**adUseNone**|1|는 커서 서비스를 사용 하지 않습니다. 이 상수는 사용 되지 않으며 이전 버전과의 호환성을 위해서만 표시 됩니다.|  
|**adUseServer**|2|기본값 데이터 공급자나 드라이버에서 제공 하는 커서를 사용 합니다. 이러한 커서는 때때로 매우 유연 하며 다른 사용자가 데이터 원본에 대 한 변경 내용에 대 한 추가 민감도를 허용 합니다. 그러나 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)의 일부 기능 (예: 연결이 끊어졌습니다.<br /><br /> [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 서버 쪽 커서를 사용 하 여 시뮬레이션할 수 없으며이 설정에서는 이러한 기능을 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. CursorLocation|  
|AdoEnums. CursorLocation|  
|AdoEnums. CursorLocation|  
  
## <a name="applies-to"></a>적용 대상  
 [CursorLocation 속성(ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
