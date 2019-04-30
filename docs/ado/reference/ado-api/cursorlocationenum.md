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
manager: craigg
ms.openlocfilehash: 832372ee3f8e80a9da4a758c759d9b5399a20a57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309715"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
커서 서비스의 위치를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|로컬 커서 라이브러리에서 제공 하는 클라이언트 쪽 커서를 사용 합니다. 로컬 커서 서비스 드라이버 제공 커서 않을 많은 기능이 허용는 종종이 설정을 사용 하 여 사용할 수 있는 기능에 대해이 점으로 손꼽을 제공할 수 있도록 합니다. 이전 버전과 호환성을 위해 동의어 **adUseClientBatch** 도 지원 됩니다.|  
|**adUseNone**|1|커서 서비스를 사용 하지 않습니다. (이 상수는 사용 되지 않습니다 및 이전 버전과 호환성을 위해서만 나타납니다.)|  
|**adUseServer**|2|기본. 데이터 공급자 또는 드라이버에서 제공 하는 커서를 사용 합니다. 이러한 커서는 매우 유연 하 고 데이터 원본에 허용 되는 다른 변경 작업에 대 한 추가 민감도 대 한 허용 합니다. 그러나 일부 기능의 합니다 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)분리와 같은<br /><br /> [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 서버 쪽 커서를 사용 하 여 개체를 시뮬레이션할 수 없습니다 및 이러한 기능에이 설정을 사용 하 여 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>적용 대상  
 [CursorLocation 속성(ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
