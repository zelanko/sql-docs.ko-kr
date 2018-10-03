---
title: AggregationDesigns 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesigns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesigns
helpviewer_keywords:
- AggregationDesigns element
ms.assetid: 7291956a-9c53-41fe-af2e-2418e26956c5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 03cab5a4737e88eb365f359f64490d67ab7e847f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174173"
---
# <a name="aggregationdesigns-element-assl"></a>AggregationDesigns 요소(ASSL)
  데이터베이스의 여러 파티션에서 공유할 수 있는 집계 디자인의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup>  
   ...  
   <AggregationDesigns>  
      <AggregationDesign>...</AggregationDesign>  
   </AggregationDesigns>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음(컬렉션)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값 그룹](../objects/group-element-assl.md)|  
|자식 요소|[AggregationDesign](../objects/aggregationdesign-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AggregationDesignCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 파티션 &#40;ASSL&#41;](../objects/partition-element-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
