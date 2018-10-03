---
title: OrderBy 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OrderBy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OrderBy
helpviewer_keywords:
- OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95ed1ce8e5b9df8340b41b8ec24e713dae9739ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168733"
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*이름*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*이름*|멤버 이름별로 정렬합니다.|  
|*키*|멤버 키별로 정렬합니다.|  
|*AttributeKey*|에 지정 된 특성의 멤버 키별로 정렬 합니다 [OrderByAttributeID](id-element-assl.md) 요소의 `DimensionAttribute`합니다.|  
|*AttributeName*|`OrderByAttributeID`의 `DimensionAttribute` 요소에 지정된 특성의 멤버 이름별로 정렬합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `OrderBy`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.OrderBy>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
