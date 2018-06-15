---
title: OverrideBehavior 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 60cb7a9abaa65e01321adff12376d2fe82de1c3c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045987"
---
# <a name="overridebehavior-element-assl"></a>OverrideBehavior 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  설명 되는 관계의 재정의 동작을 나타냅니다는 [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*강력한*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **OverrideBehavior** 요소는 관련 특성의 위치 지정이 특성의 위치 지정에 영향을 주는 방식을 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*강력한*|AttributeRelationship 요소로 설명되는 관계의 재정의 동작을 나타냅니다. 한 특성의 위치 지정이 다른 특성의 위치에 영향을 주는 방식을 나타냅니다.|  
|*없음*|아무런 영향이 없습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **OverrideBehavior** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.OverrideBehavior>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [특성 및 특성 계층](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
