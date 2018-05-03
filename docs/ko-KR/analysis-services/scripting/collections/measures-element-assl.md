---
title: 요소 (ASSL)를 측정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Measures Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Measures
helpviewer_keywords:
- Measures element
ms.assetid: d2107112-f620-4fd7-a05f-bb2606b4be18
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca60ca2793e23db2bc6207414edb725d15c18b5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="measures-element-assl"></a>Measures 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  컬렉션을 포함 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 부모 요소와 관련 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup> <!-- or AggregationInstance, MeasureGroupBinding (out-of-line), PerspectiveMeasureGroup -->  
   ...  
   <Measures>  
      <Measure>...</Measure>  
   </Measures>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MeasureGroupBinding (아웃 아웃오브 라인)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md), [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|  
|자식 요소|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MeasureCollection> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasureCollection>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
