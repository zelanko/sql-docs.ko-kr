---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e7752b4c460bccbca1b98d9a95d04df96006ea6
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277422"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
커서 서비스의 위치를 지정합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|로컬 커서 라이브러리에서 제공 하는 클라이언트 쪽 커서를 사용 합니다. 로컬 커서 서비스 종종 하면 드라이버 제공 커서 수 있는 다양 한 기능이 없으므로이 설정을 사용 하 여 사용할 수 있는 기능 관련 하 여 더 뛰어난 이점을 제공 될 수 있습니다. 이전 버전과 호환성을 동의어에 대 한 **adUseClientBatch** 도 지원 합니다.|  
|**adUseNone**|1|커서 서비스를 사용 하지 않습니다. (이 상수가 사용 되지 않으며 이전 버전과 호환성을 위해서만 나타납니다.)|  
|**adUseServer**|2|기본. 데이터 공급자 또는 드라이버에서 제공 하는 커서를 사용 합니다. 이러한 커서 경우가 매우 유연 하며 데이터 원본에 허용 되는 다른 사용자 변경 작업에 대 한 추가 민감도 대 한 허용 합니다. 그러나의 기능 중 일부는 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)연결을 끊을 등<br /><br /> [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 서버 쪽 커서와 함께 개체를 시뮬레이션할 수 없습니다 및 이러한 기능에이 설정을 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>적용 대상  
 [CursorLocation 속성(ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
