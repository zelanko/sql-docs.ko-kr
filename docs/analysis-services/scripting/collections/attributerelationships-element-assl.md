---
title: "AttributeRelationships 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AttributeRelationships Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MemberProperties
helpviewer_keywords: AttributeRelationships element
ms.assetid: f2ff82f6-6a7f-481a-a1ef-014bef38face
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edc04660f5b991256d1d4cdbfd0b0c5f4d10201d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="attributerelationships-element-assl"></a>AttributeRelationships 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]컬렉션을 포함 [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) 특성에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <AttributeRelationships>  
      <AttributeRelationship>...</AttributeRelationship>  
   </AttributeRelationships>  
   ...  
</Attribute>  
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
|부모 요소|[특성](../../../analysis-services/scripting/objects/attribute-element-assl.md) 형식의 [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AttributeRelationshipCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
