---
title: AttributePermission 요소 (ASSL) | Microsoft Docs
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
- AttributePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributePermission
helpviewer_keywords:
- AttributePermission element
ms.assetid: efc8aa63-3959-4b2e-98f8-2a9c424298c2
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c39047b1f63f0abbab109e2d1e8f82ca2a4c863
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277879"
---
# <a name="attributepermission-element-assl"></a>AttributePermission 요소(ASSL)
  사용 권한을 해당 멤버의 정의 [역할](role-element-assl.md) 요소의 개별 차원 특성에는 [큐브](cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributePermissions>  
   <AttributePermission>  
      <AttributeID>...</AttributeID>  
      <Description>...</Description>  
      <DefaultMember>...</DefaultMember>  
            <VisualTotals>...</VisualTotals>  
      <AllowedSet>...</AllowedSet>  
            <DeniedSet>...</DeniedSet>  
      <Annotations>...</Annotations>  
   </AttributePermission>  
</AttributePermissions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributePermissions](../collections/attributepermissions-element-assl.md)|  
|자식 요소|[AllowedSet](../properties/allowedset-element-assl.md), [주석을](../collections/annotations-element-assl.md)를 [AttributeID](../properties/id-element-assl.md)를 [DefaultMember](member-element-assl.md)를 [DeniedSet](../properties/deniedset-element-assl.md), [설명 ](../properties/description-element-assl.md), [VisualTotals](../properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AttributePermission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CubeDimensionPermission 데이터 형식 &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
