---
title: "AttributeHierarchyEnabled 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
apiname: AttributeHierarchyEnabled Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeHierarchyEnabled
helpviewer_keywords: AttributeHierarchyEnabled element
ms.assetid: 1e95307f-530e-4e98-a0e1-2b0462d330a3
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5581a7b280eb2ba93144afbabad6e5e9e181d7d9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="attributehierarchyenabled-element-assl"></a>AttributeHierarchyEnabled 요소(ASSL)
  특성에 대한 특성 계층을 설정할지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute><!-- or CubeAttribute -->  
   ...  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
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
|부모 요소|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **AttributeHierarchyEnabled** 요소는 특성 계층을 생성할지 여부를 결정 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 특성에 대 한 합니다. 특성 계층이 설정되지 않으면 사용자 정의 계층에서 해당 특성을 사용할 수 없으며 MDX(Multidimensional Expressions) 문에서 특성 계층을 참조할 수도 없습니다.  
  
 부모에 해당 하는 요소 **AttributeHierarchyEnabled** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeAttribute> 및 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AttributeHierarchyVisible 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
