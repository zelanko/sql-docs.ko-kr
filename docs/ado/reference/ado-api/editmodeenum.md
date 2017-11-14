---
title: EditModeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b59850d8b04854ee74f94664b53dc22242c6913
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="editmodeenum"></a>EditModeEnum
레코드의 편집 상태를 지정합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|편집 작업이 진행에서 중인지를 나타냅니다.|  
|**adEditInProgress**|1.|현재 레코드의 데이터가 수정 되었지만 저장 안 됨을 나타냅니다.|  
|**adEditAdd**|2|나타냅니다는 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드를 호출 하 고 복사 버퍼의 현재 레코드는 데이터베이스에 저장 되지 않은 새 레코드입니다.|  
|**adEditDelete**|4|현재 레코드 삭제 했을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>적용 대상  
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)

