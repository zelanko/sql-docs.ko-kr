---
title: OrderBy 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2d2c8caf392e5d80d82b06a7d7fd9b5cd724a35e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="orderby-element-assl"></a>OrderBy 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  특성에 포함된 멤버의 정렬 방식을 설명합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*이름*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*이름*|멤버 이름별로 정렬합니다.|  
|*Key*|멤버 키별로 정렬합니다.|  
|*AttributeKey*|에 지정 된 특성의 멤버 키별로 정렬는 [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md) 요소의 **DimensionAttribute**합니다.|  
|*AttributeName*|**OrderByAttributeID** 의 **DimensionAttribute**요소에 지정된 특성의 멤버 이름별로 정렬합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **OrderBy** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.OrderBy>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
