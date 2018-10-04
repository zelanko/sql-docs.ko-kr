---
title: Type 요소 (MeasureGroupAttribute) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (MeasureGroupAttribute)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 93740504-297a-4a06-ab3e-b598e466eebb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfe3b0cda9061e18b9a275eac98e02ed90453adc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087934"
---
# <a name="type-element-measuregroupattribute-assl"></a>Type 요소(MeasureGroupAttribute)(ASSL)
  형식이 포함 된 [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|일반 특성을 나타냅니다.|  
|*세분성*|세분성 특성을 나타냅니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Type`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>입니다.  
  
 부모에 해당 하는 요소가 `Type` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 특성 &#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 데이터 형식 &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
