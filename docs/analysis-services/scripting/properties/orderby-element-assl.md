---
title: "OrderBy 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- OrderBy Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- OrderBy
helpviewer_keywords:
- OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35479ebb898200c9082a7e08369a3ae5d4c57ac3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="orderby-element-assl"></a>OrderBy 요소(ASSL)
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
|*키*|멤버 키별로 정렬합니다.|  
|*AttributeKey*|에 지정 된 특성의 멤버 키별로 정렬는 [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md) 요소의 **DimensionAttribute**합니다.|  
|*AttributeName*|**OrderByAttributeID** 의 **DimensionAttribute**요소에 지정된 특성의 멤버 이름별로 정렬합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **OrderBy** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.OrderBy>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

