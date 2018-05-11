---
title: AggregationDesignID 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a947676c65929b3844d1bd8a982818aea2f0d5e9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationdesignid-element-assl"></a>AggregationDesignID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  식별 된 [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) 요소와 연관 된는 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Partition>  
      ...  
   <AggregationDesignID>...</AggregationDesignID>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **AggregationDesignID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Partition>합니다. 참고 항목 <xref:Microsoft.AnalysisServices.AggregationDesign>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AggregationDesign 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
