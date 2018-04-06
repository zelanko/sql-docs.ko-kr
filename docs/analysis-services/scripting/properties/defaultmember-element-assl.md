---
title: DefaultMember 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- DefaultMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3559aafd4fc5b31b1cfc73bdf7dc75a9d6821b84
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="defaultmember-element-assl"></a>DefaultMember 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]부모 요소의 기본 멤버를 식별 하는 MDX (Multidimensional Expressions) 식을 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
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
|부모 요소|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **DefaultMember** 요소는 부모 요소의 기본 멤버를 정의합니다. 경우 **DefaultMember** 지정 되지 않았거나 빈 문자열로 설정 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 기본 멤버로 사용할 멤버를 선택 합니다.  
  
 **ManyToManyMeasureGroupDimension** 요소의 경우 **DefaultMember** 요소는 **CubeDimensionID** 의 **ManyToManyMeasureGroupDimension**요소에서 식별되는 차원 멤버를 지정하는 MDX 식을 포함합니다. MDX 식을 비슷합니다는 [StrToMember](../../../mdx/strtomember-mdx.md) MDX 또는 사용자 정의 함수를 포함할 수 없습니다 한다는 점에서 MDX 제한 된 키워드와 함께 작동 합니다.  
  
 기본 멤버에 대한 자세한 내용은 [기본 멤버 정의](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)를 참조하세요.  
  
 부모에 해당 하는 요소 **DefaultMember** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, 및 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
