---
title: AttributeHierarchyVisible 요소 (ASSL) | Microsoft Docs
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
- AttributeHierarchyVisible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeHierarchyVisible
helpviewer_keywords:
- AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5b5ec37036d23c8e1c70e9fe7ba333a8e4c370bb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184584"
---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 요소(ASSL)
  클라이언트 응용 프로그램에서 특성 계층을 볼 수 있는지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|`True`|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeAttribute](../data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `AttributeHierarchyVisible` 요소는 클라이언트 응용 프로그램에서 특성과 연결된 특성 계층을 볼 수 있는지 여부를 결정합니다. 이 요소가 `False`로 설정된 경우 특성 계층을 사용하여 사용자 정의 계층을 만들고 MDX(Multidimensional Expressions) 문에서 이 계층을 참조할 수 있습니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `AttributeHierarchyVisible`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CubeAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute> 및 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [AttributeHierarchyEnabled 요소 &#40;ASSL&#41;](enabled-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  