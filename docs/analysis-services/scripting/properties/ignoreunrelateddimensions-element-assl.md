---
title: IgnoreUnrelatedDimensions 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 42dbcb7a41eec2d620b0a0c098503ff2aa8d2fec
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="ignoreunrelateddimensions-element-assl"></a>IgnoreUnrelatedDimensions 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  측정값 그룹과 관련이 없는 차원의 멤버가 쿼리에 포함될 때 관련이 없는 차원이 최상위로 강제되는지 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|True|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값 그룹](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **IgnoreUnrelatedDimensions** 가 **true**이면 관련이 없는 차원이 최상위로 강제되고 **false**이면 최상위로 강제되지 않습니다. 이 속성은 유사 하는 MDX (Multidimensional Expressions) [ValidMeasure](../../../mdx/validmeasure-mdx.md) 함수입니다.  
  
 부모에 해당 하는 요소 **IgnoreUnrelatedDimensions** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroup>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
