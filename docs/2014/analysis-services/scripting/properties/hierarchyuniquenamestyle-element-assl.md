---
title: HierarchyUniqueNameStyle 요소 (ASSL) | Microsoft Docs
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
- HierarchyUniqueNameStyle Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- HierarchyUniqueNameStyle element
ms.assetid: 2ac57825-e9e5-4ec4-9856-fa2326d2c43f
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d19fa53581241686d68179162762a0909fcc69f5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304293"
---
# <a name="hierarchyuniquenamestyle-element-assl"></a>HierarchyUniqueNameStyle 요소(ASSL)
  어떻게 고유한 이름을 결정에 포함 된 계층에 대해 생성 되는 [CubeDimension](../data-type/dimension-data-type-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
   ...  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*IncludeDimensionName*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IncludeDimensionName*|차원 이름이 계층 이름의 일부로 포함됩니다.|  
|*ExcludeDimensionName*|차원 이름이 계층 이름의 일부로 포함되지 않습니다.|  
  
 부모에 해당 하는 요소가 `HierarchyUniqueNameStyle` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
