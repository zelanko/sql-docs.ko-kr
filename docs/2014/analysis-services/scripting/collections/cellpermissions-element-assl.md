---
title: CellPermissions 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellPermissions
helpviewer_keywords:
- CellPermissions element
ms.assetid: 4a604f2f-f4c3-42bd-a42b-951263942cc6
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dafcaf786d58fd8c1441c0f1df50aa5a7d47be31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176460"
---
# <a name="cellpermissions-element-assl"></a>CellPermissions 요소(ASSL)
  연결 된 셀에 대 한 사용 권한의 컬렉션을 포함 [큐브](../objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubePermission>  
   ...  
   <CellPermissions>  
      <CellPermission>...</CellPermission>  
   </CellPermissions>  
   ...  
</CubePermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubePermission](../objects/cubepermission-element-assl.md)|  
|자식 요소|[CellPermission](../objects/cellpermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 컬렉션 하나를 포함할 수 있습니다 `CellPermission` 허용 된 각 값에 대 한 개체를 [액세스](../properties/access-element-assl.md) 요소입니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CellPermissionCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Permission 데이터 형식 &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
