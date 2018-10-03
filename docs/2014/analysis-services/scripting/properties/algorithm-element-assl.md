---
title: Algorithm 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Algorithm Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb2ab30f6abd753f0c954ef41ad26d0af9dcda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149783"
---
# <a name="algorithm-element-assl"></a>Algorithm 요소(ASSL)
  알고리즘을 사용 하 여 정의 된 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModel](../objects/miningmodel-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Algorithm` 요소의 값은 알고리즘을 식별하는 문자열입니다. 예를 들어, 문자열 수 있습니다 *Microsoft_Naive_Bayes*를 *Microsoft_Decision_Trees*, 또는 *Microsoft_Clustering 합니다.* 제공 하는 알고리즘을 식별 하는 문자열 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 및 사용자가 제공한 사용자 지정 알고리즘입니다. 에 대 한 사용 가능한 값을 `Algorithm` 의 SERVICE_NAME 열에서 요소를 검색할 수 있습니다 합니다 [DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md) 스키마 행 집합입니다.  
  
 부모에 해당 하는 요소가 `Algorithm` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningModel>합니다. AMO 개체 모델에서 밀접하게 관련된 요소는 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [AlgorithmParameter 요소 &#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 요소 &#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
