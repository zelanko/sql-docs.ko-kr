---
title: ModelingFlag 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84fb8664ac5069c7a648308fced9d22ffec41a8a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="modelingflag-element-assl"></a>ModelingFlag 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  마이닝 구조 또는 마이닝 모델의 열에 대한 모델링 플래그를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ModelingFlags>  
   <ModelingFlag xsi:type="MiningModelingFlag">...</ModelingFlag>  
</ModelingFlags>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[MiningModelingFlag](../../../analysis-services/scripting/data-type/miningmodelingflag-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 AMO(Analysis Management Object) 개체 모델에서 밀접한 관련이 있는 요소는 <xref:Microsoft.AnalysisServices.MiningModelingFlags>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MiningModel 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [MiningStructure 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)   
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
