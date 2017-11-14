---
title: "AttributeHierarchyVisible 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AttributeHierarchyVisible Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeHierarchyVisible
helpviewer_keywords:
- AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e79ef9a4a3d248f9641bc6aae44c50acb83b56b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|**True**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **AttributeHierarchyVisible** 요소는 클라이언트 응용 프로그램에서 특성과 연결된 특성 계층을 볼 수 있는지 여부를 결정합니다. 이 요소가 **False**로 설정된 경우 특성 계층을 사용하여 사용자 정의 계층을 만들고 MDX(Multidimensional Expressions) 문에서 이 계층을 참조할 수 있습니다.  
  
 부모에 해당 하는 요소 **AttributeHierarchyVisible** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, 및 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AttributeHierarchyEnabled 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

