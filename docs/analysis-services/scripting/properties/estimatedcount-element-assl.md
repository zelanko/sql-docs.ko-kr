---
title: EstimatedCount 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8e3f533bcc9cf1f6ff3c63c1a2b039b5ec942dc1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="estimatedcount-element-assl"></a>EstimatedCount 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  사용자가 정의한 특성의 예상 멤버 수를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDesignAttribute> <!-- or DimensionAttribute -->  
      ...  
   <EstimatedCount>...</EstimatedCount>  
   ...  
</AggregationDesignAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Long|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationDesignAttribute](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 값은 사용자가 할당 됩니다 및에서 사용 되는 [AggregationDesign 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)합니다.  
  
 부모에 해당 하는 요소 **EstimatedCount** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AggregationDesignAttribute> 및 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
