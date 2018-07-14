---
title: MiningModelID 요소 (ASSL) | Microsoft Docs
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
- MiningModelID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelID
helpviewer_keywords:
- MiningModelID element
ms.assetid: fada8720-1590-44be-bafc-0ab3612b00e5
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5cc241819884cd8307c03d39d2d4daa575454f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267279"
---
# <a name="miningmodelid-element-assl"></a>MiningModelID 요소(ASSL)
  마이닝 모델을 데이터 마이닝 차원과 연결합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
   ...  
   <MiningModelID>...</MiningModelID>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Dimension](../objects/dimension-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `MiningModelID` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MiningModel 요소 &#40;ASSL&#41;](../objects/miningmodel-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
