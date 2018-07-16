---
title: Filter 요소 (바인딩) (ASSL) | Microsoft Docs
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
- Filter Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- filter
helpviewer_keywords:
- Filter element
ms.assetid: 3d4cd169-2903-4266-8541-540ece424b7b
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca1fe43bfe98061065cda1da5b1ff64772a4751d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291309"
---
# <a name="filter-element-binding-assl"></a>Filter 요소(Binding)(ASSL)
  부모 요소의 내용을 필터링하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Filter>...</Filter>  
   ...  
</CubeDimensionBinding>  
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
|부모 요소|[CubeDimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 합니다 `Binding` 테이블을 비롯 한 형식 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ASSL (Scripting Language) 개체를 `Binding` 형식과의 상속 계층 구조 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](../data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 부모에 해당 하는 요소가 `Filter` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.CubeDimensionBinding> 및 <xref:Microsoft.AnalysisServices.MeasureGroupBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Binding 데이터 형식 &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
