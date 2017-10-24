---
title: "Hierarchies 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Hierarchies Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Hierarchies
helpviewer_keywords:
- Hierarchies element
ms.assetid: dc844eea-869c-4217-b9be-e543a76f5e92
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b4ba62d1a41b224dc75e77ddddda208bc8e46bb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchies-element-assl"></a>Hierarchies 요소(ASSL)
  컬렉션을 포함 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 부모 요소와 관련 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension> <!-- or CubeDimension, PerspectiveDimension -->  
   ...  
   <Hierarchies>  
            <Hierarchy>...</Hierarchy> <!-- parent: Dimension -->  
      <!-- or -->  
      <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- parent: CubeDimension -->  
     <!-- or -->  
      <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- parent: PerspectiveDimension -->  
   <Hierarchies>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|[계층 구조](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 형식의 [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|[계층 구조](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 형식의 [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
  
## <a name="remarks"></a>주의  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.HierarchyCollection>, <xref:Microsoft.AnalysisServices.CubeHierarchyCollection> 및 <xref:Microsoft.AnalysisServices.PerspectiveHierarchyCollection>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

