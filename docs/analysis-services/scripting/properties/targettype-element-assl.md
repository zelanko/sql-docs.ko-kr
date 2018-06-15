---
title: TargetType 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe1e79254f4daef21634b4e9c5b2144c857bfee0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039397"
---
# <a name="targettype-element-assl"></a>TargetType 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  식별 된 항목의 유형을 식별 된 [대상](../../../analysis-services/scripting/properties/target-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Cube*|동작 대상이 큐브입니다.|  
|*셀*|동작 대상이 하위 큐브입니다.|  
|*설정*|동작 대상이 집합입니다.|  
|*계층 구조*|동작 대상이 계층입니다.|  
|*Level*|동작 대상이 수준입니다.|  
|*DimensionMembers*|동작 대상이 차원의 멤버입니다.|  
|*HierarchyMembers*|동작 대상이 계층의 멤버입니다.|  
|*LevelMembers*|동작 대상이 수준의 멤버입니다.|  
|*AttributeMembers*|동작 대상이 특성의 멤버입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **TargetType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ActionTargetType>합니다.  
  
 부모에 해당 하는 요소 **TargetType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
