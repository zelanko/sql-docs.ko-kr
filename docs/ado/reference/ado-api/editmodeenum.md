---
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d98e6d27de571bc799cc8442fbe6ef9debc0beaa
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695250"
---
# <a name="editmodeenum"></a>EditModeEnum
레코드의 편집 상태를 지정합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|편집 작업이 진행에서 중임을 나타냅니다.|  
|**adEditInProgress**|1|현재 레코드의 데이터가 수정 되었지만 저장 되지 있는지를 나타냅니다.|  
|**adEditAdd**|2|나타내는 합니다 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드를 호출 이며 복사 버퍼에서 현재 레코드가 새 레코드를 데이터베이스에 저장 되지 않았습니다.|  
|**adEditDelete**|4|현재 레코드를 삭제 했을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>적용 대상  
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)
