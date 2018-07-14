---
title: Action 요소 (ASSL) | Microsoft Docs
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
- Action Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Action
helpviewer_keywords:
- Action element
ms.assetid: aaee06a2-91c6-4007-b787-79cb08d63c77
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bfc51d797852e80cf7bf501cf3f1d93f2f52c9d9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196013"
---
# <a name="action-element-assl"></a>Action 요소(ASSL)
  사용 가능한 동작에 대 한 정보를 포함 한 [큐브](cube-element-assl.md) 요소 또는 [관점](perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Actions>  
   <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
   <!-- or -->  
   <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
</Actions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[큐브](../data-type/action-data-type-assl.md)하십시오 [ReportAction](../data-type/reportaction-data-type-assl.md), [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|[큐브 뷰](../data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../collections/actions-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](cube-element-assl.md)   
 [Perspective 요소의 &#40;ASSL&#41;](perspective-element-assl.md)   
 [PerspectiveAction 데이터 형식 &#40;ASSL&#41;](../data-type/perspectiveaction-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
