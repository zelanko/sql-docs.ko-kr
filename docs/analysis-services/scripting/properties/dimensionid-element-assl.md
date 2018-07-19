---
title: DimensionID 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 340225d519cb119daaae4628033e67a9f007d830
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052711"
---
# <a name="dimensionid-element-assl"></a>DimensionID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  차원의 ID(식별자)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension> <!-- or DimensionBinding, DimensionAttributeBinding -- >  
   ...  
   <DimensionID>...</DimensionID>  
      ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)하십시오 [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 **DimensionID** Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.CubeDimension> 고 <xref:Microsoft.AnalysisServices.DimensionBinding>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
