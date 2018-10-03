---
title: DefaultMember 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c90abe48fc1d3bfa099e39234d22df822a03782
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055303"
---
# <a name="defaultmember-element-assl"></a>DefaultMember 요소(ASSL)
  부모 요소의 기본 멤버를 식별하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
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
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributePermission](../objects/attributepermission-element-assl.md)하십시오 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)하십시오 [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md), [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `DefaultMember` 요소는 부모 요소의 기본 멤버를 정의합니다. 하는 경우 `DefaultMember` 지정 되지 않았거나 빈 문자열로 설정 됩니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 기본 멤버로 사용할 멤버를 선택 합니다.  
  
 `ManyToManyMeasureGroupDimension` 요소의 경우 `DefaultMember` 요소는 `CubeDimensionID`의 `ManyToManyMeasureGroupDimension` 요소에서 식별되는 차원 멤버를 지정하는 MDX 식을 포함합니다. MDX 식은 비슷합니다는 [StrToMember](/sql/mdx/strtomember-mdx) MDX 함수와 CONSTRAINED 키워드를 사용 하 여에 MDX 또는 사용자 정의 함수를 포함할 수 없습니다.  
  
 기본 멤버에 대한 자세한 내용은 [기본 멤버 정의](../../multidimensional-models/attribute-properties-define-a-default-member.md)를 참조하세요.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `DefaultMember`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute> 및 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
