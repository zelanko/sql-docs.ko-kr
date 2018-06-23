---
title: StorageMode 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- StorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d65d778e54a712e3fce18bdac5b3a0e31426863
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172750"
---
# <a name="storagemode-element-assl"></a>StorageMode 요소(ASSL)
  부모 요소의 저장소 모드를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*MOLAP*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md), [요소 치수 &#40;ASSL&#41;](../objects/dimension-element-assl.md), [MeasureGroup 요소 &#40;ASSL&#41;](../objects/group-element-assl.md), [파티션 요소 &#40;ASSL&#41;](../objects/partition-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MOLAP*|부모가 MOLAP(다차원 OLAP) 저장소를 사용합니다.|  
|*ROLAP*|부모가 ROLAP(관계형 OLAP) 저장소를 사용합니다.|  
|*HOLAP*|부모가 HOLAP(하이브리드 OLAP) 저장소를 사용합니다. **참고:** 이 값에 대해 올바르지 않습니다. [차원](../objects/dimension-element-assl.md) 부모 요소입니다.|  
|*InMemory*|부모가 IMBI 저장소를 사용합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `StorageMode`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.StorageMode>입니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `StorageMode`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> 및 <xref:Microsoft.AnalysisServices.Partition>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  