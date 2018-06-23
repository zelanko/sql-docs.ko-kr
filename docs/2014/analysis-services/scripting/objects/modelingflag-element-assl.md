---
title: ModelingFlag 요소 (ASSL) | Microsoft Docs
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
- ModelingFlag Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ModelingFlag
helpviewer_keywords:
- ModelingFlag element
ms.assetid: c9af1b9a-506f-4cc1-acd7-e57698cb672c
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe0dcb73d3d053edfe29059970c0d5c8ba0d0268
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080514"
---
# <a name="modelingflag-element-assl"></a>ModelingFlag 요소(ASSL)
  마이닝 구조 또는 마이닝 모델의 열에 대한 모델링 플래그를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ModelingFlags>  
   <ModelingFlag xsi:type="MiningModelingFlag">...</ModelingFlag>  
</ModelingFlags>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[MiningModelingFlag](../data-type/miningmodelingflag-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ModelingFlags](../collections/modelingflags-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Object) 개체 모델에서 밀접한 관련이 있는 요소는 <xref:Microsoft.AnalysisServices.MiningModelingFlags>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [MiningModel 요소 &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [MiningStructure 요소 &#40;ASSL&#41;](miningstructure-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  