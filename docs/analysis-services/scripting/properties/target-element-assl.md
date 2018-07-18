---
title: Target 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 98ec5c729f5735343f5eaa87e5232fcfb138cf38
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045781"
---
# <a name="target-element-assl"></a>Target 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  대상을 식별 합니다 [동작](../../../analysis-services/scripting/objects/action-element-assl.md) 요소입니다.  
  
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
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 필요한 값의 값에 따라 달라 집니다 합니다 [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) 부모 요소 **동작**합니다. 다음 표에서는 **Target** 의 값을 기반으로 **TargetType**의 필요한 값을 설명합니다.  
  
|TargetType 값|필요한 값|  
|----------------------|--------------------|  
|*Cube*|큐브의 이름입니다.|  
|*셀*|하위 큐브 식입니다.|  
|*설정*|집합 식 또는 명명된 집합의 이름입니다.<br /><br /> 참고: 하위 select 문에서 사용할 수 없습니다.|  
|*HierarchyMembers 계층*|계층의 이름입니다.|  
|*차원에 DimensionMembers*|차원의 이름입니다.|  
|*LevelMembers 수준*|수준의 이름입니다.|  
|*AttributeMembers 특성*|특성의 이름입니다.|  
  
 부모에 해당 하는 요소가 **대상** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
