---
title: Target 요소 (ASSL) | Microsoft Docs
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
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec2f4a43b8b03e2f28d4bd8c61a9c6e4a9d20eb5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180770"
---
# <a name="target-element-assl"></a>Target 요소(ASSL)
  대상을 식별 합니다 [동작](../objects/action-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 필요한 값의 값에 따라 달라 집니다 합니다 [TargetType](targettype-element-assl.md) 부모 요소 `Action`합니다. 다음 표에서는 `Target`의 값을 기반으로 `TargetType`의 필요한 값을 설명합니다.  
  
|TargetType 값|필요한 값|  
|----------------------|--------------------|  
|*Cube*|큐브의 이름입니다.|  
|*셀*|하위 큐브 식입니다.|  
|*설정*|집합 식 또는 명명된 집합의 이름입니다. **참고:** 하위 select 문을 사용할 수 없습니다.|  
|*HierarchyMembers 계층*|계층의 이름입니다.|  
|*차원에 DimensionMembers*|차원의 이름입니다.|  
|*LevelMembers 수준*|수준의 이름입니다.|  
|*AttributeMembers 특성*|특성의 이름입니다.|  
  
 부모에 해당 하는 요소가 `Target` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
