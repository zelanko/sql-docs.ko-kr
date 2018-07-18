---
title: OrderByAttributeID 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e6ab7a00961d4e5b925556d107eec32b7ddb9c9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38018217"
---
# <a name="orderbyattributeid-element-assl"></a>OrderByAttributeID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Dimension](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 특성의 멤버를 정렬하는 기준인 다른 특성을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderByAttributeID>...</OrderByAttributeID>  
   ...  
</DimensionAttribute>  
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
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **OrderByAttributeID** 요소인 경우에만 사용된 값을 [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md) 요소에 대 한 합니다 **DimensionAttribute** 로 설정 되어 *AttributeKey* 나 *AttributeName*합니다.  
  
 부모에 해당 하는 요소가 **OrderByAttributeID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
