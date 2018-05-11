---
title: 대상 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 796d81ddb3c2d56f8efd25b9df194a2e4d942be5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="target-element-assl"></a>Target 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  대상을 식별 하는 [동작](../../../analysis-services/scripting/objects/action-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 필요한 값의 값에 따라는 [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) 부모에 대 한 요소 **동작**합니다. 다음 표에서는 **Target** 의 값을 기반으로 **TargetType**의 필요한 값을 설명합니다.  
  
|TargetType 값|필요한 값|  
|----------------------|--------------------|  
|*Cube*|큐브의 이름입니다.|  
|*셀*|하위 큐브 식입니다.|  
|*설정*|집합 식 또는 명명된 집합의 이름입니다.<br /><br /> 참고:는 하위 select 문에서 사용할 수 없습니다.|  
|*HierarchyMembers 계층 구조*|계층의 이름입니다.|  
|*차원, DimensionMembers*|차원의 이름입니다.|  
|*LevelMembers 수준*|수준의 이름입니다.|  
|*특성을 AttributeMembers*|특성의 이름입니다.|  
  
 부모에 해당 하는 요소 **대상** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
