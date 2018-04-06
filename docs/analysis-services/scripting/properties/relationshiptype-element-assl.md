---
title: RelationshipType 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- RelationshipType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ac893cc0b06cfa4f5f0925e94672b8da5de885e0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]나타냅니다 여부에 대 한 멤버 관계는 [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) 변경할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*유연한*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*고정 된 관계로*|특성 및 관련 특성 사이의 멤버 관계를 변경할 수 없습니다.|  
|*유연한*|특성 및 관련 특성 사이의 멤버 관계를 변경할 수 있습니다.|  
  
 예를 들어 **ZipCode** 의 **City** 를 다른 값으로 변경할 수 없는 경우 **ZipCode** 와 **City** 의 관계는 *Rigid*로 표시됩니다.  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **RelationshipType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.RelationshipType>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [특성 및 특성 계층](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
