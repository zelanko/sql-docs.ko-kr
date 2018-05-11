---
title: OrderByAttributeID 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 08414e3c5ccd3806ba8b77ad8b39fb636c92b775
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="orderbyattributeid-element-assl"></a>OrderByAttributeID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  멤버를 정렬 하는 기준인 다른 특성을 식별 된 [차원](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) 특성입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderByAttributeID>...</OrderByAttributeID>  
   ...  
</DimensionAttribute>  
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
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **OrderByAttributeID** 요소는 경우에만 사용된의 값은 [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md) 에 대 한 요소는 **DimensionAttribute** 로 설정 되어 *AttributeKey* 또는 *AttributeName*합니다.  
  
 부모에 해당 하는 요소 **OrderByAttributeID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
