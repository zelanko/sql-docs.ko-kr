---
title: DataAggregation 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataAggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01a86977cc6ebf85d004bf235b6d47a354e112a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134823"
---
# <a name="dataaggregation-element-assl"></a>DataAggregation 요소(ASSL)
  인스턴스가 영구 데이터 나 캐시 된 데이터를 집계할 수 있는지 여부를 결정 합니다 [MeasureGroup](../objects/group-element-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*DataAndCacheAggregatable*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값 그룹](../objects/group-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|이 측정값 그룹에서 집계가 수행되지 않습니다.|  
|*DataAggregatable*|이 측정값 그룹서 영구 데이터를 집계할 수 있습니다.|  
|*CacheAggregatable*|이 측정값 그룹에서 캐시된 데이터를 집계할 수 있습니다.|  
|*DataAndCacheAggregatable*|이 측정값 그룹에서 영구 데이터 및 캐시된 데이터를 모두 집계할 수 있습니다.|  
  
 부모에 해당 하는 요소가 `DataAggregation` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroup>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
