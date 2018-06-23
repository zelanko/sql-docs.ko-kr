---
title: AlgorithmParameter 요소 (ASSL) | Microsoft Docs
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
- AlgorithmParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AlgorithmParameter
helpviewer_keywords:
- AlgorithmParameter element
ms.assetid: 73211495-065c-43c6-a486-be6044617263
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 70e9e3619eb5f96ff2e64c87855b2bd33063aaf0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092967"
---
# <a name="algorithmparameter-element-assl"></a>AlgorithmParameter 요소(ASSL)
  사용 하는 알고리즘에 대 한 매개 변수 정의 [MiningModel](miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AlgorithmParameters>  
   <AlgorithmParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </AlgorithmParameter>  
</AlgorithmParameters>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AlgorithmParameters](../collections/algorithmparameters-element-assl.md)|  
|자식 요소|[Name](../properties/name-element-assl.md), [Value](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `AlgorithmParameter`는 마이닝 모델 알고리즘의 매개 변수입니다. `AlgorithmParameter`는 이름/값 쌍으로 이 매개 변수를 나타냅니다. `AlgorithmParameter`가 나타낼 수 있는 해당 매개 변수 집합은 알고리즘에 따라 다릅니다. 특정 알고리즘의 알고리즘 매개 변수에 대한 자세한 내용은 해당 알고리즘에 대한 적절한 설명서를 참조하십시오.  
  
 유효성 검사 및 표시 정보를 포함 하는 사용 가능한 알고리즘 매개 변수에서 검색할 수는 [DMSCHEMA_MINING_SERVICE_PARAMETERS](../../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md) 스키마 행 집합입니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AlgorithmParameter>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MiningModel 요소 &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [Algorithm 요소 &#40;ASSL&#41;](../properties/algorithm-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  