---
title: Aggregation 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Aggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregation
helpviewer_keywords:
- Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0780a8c81cf80871eed925471fd0ea7e6103e9b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167803"
---
# <a name="aggregation-element-assl"></a>Aggregation 요소(ASSL)
  에 대 한 단일 집계를 정의 된 [파티션](partition-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[집계](../collections/aggregations-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [설명을](../properties/description-element-assl.md)를 [차원](../collections/dimensions-element-assl.md)를 [ID](../properties/id-element-assl.md), [이름](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Aggregation>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 파티션 &#40;ASSL&#41;](partition-element-assl.md)   
 [AggregationDesign 요소 &#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [MeasureGroup 요소 &#40;ASSL&#41;](group-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
