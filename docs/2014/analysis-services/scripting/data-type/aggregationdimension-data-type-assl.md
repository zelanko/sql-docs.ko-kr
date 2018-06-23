---
title: AggregationDimension 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AggregationDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDimension
helpviewer_keywords:
- AggregationDimension data type
ms.assetid: 697e0e09-3210-4a56-882f-80726abc4c68
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a2e289e1ea6f5c91fc362f309eb73cf5586d6295
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182111"
---
# <a name="aggregationdimension-data-type-assl"></a>AggregationDimension 데이터 형식(ASSL)
  차원 관계를 나타내는 기본 데이터 형식을 정의 및 [집계](../objects/aggregation-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDimension>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석](../collections/annotations-element-assl.md), [특성](../collections/attributes-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md)|  
|파생 요소|[차원](../objects/dimension-element-assl.md) ([차원](../collections/dimensions-element-assl.md) 컬렉션 [집계](../objects/aggregation-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 [AggregationDimension](dimension-data-type-assl.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  