---
title: AttributeHierarchyVisible 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f66395c1d2f673d2bf1d068bc22bc6ba68384f9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [AttributeHierarchyEnabled 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
