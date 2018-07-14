---
title: CurrentStorageMode 요소 (ASSL) | Microsoft Docs
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
- CurrentStorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b26d26138e7752b6b41f147f0cc1fd1051e5afc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233823"
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 요소(ASSL)
  부모 요소에 대한 현재 저장소 모드를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ROLAP*|  
|카디널리티|0-1: 한 번만 나타나거나 전혀 나타나지 않을 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[차원](../objects/dimension-element-assl.md), [파티션](../objects/partition-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `CurrentStorageMode` 요소는 자동 관리 캐싱을 위해 현재 사용 중인 저장소 모드를 나타내며 부모 요소의 모든 특성에 적용됩니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MOLAP*|부모가 MOLAP(다차원 OLAP) 저장소를 사용합니다.|  
|*ROLAP*|부모가 ROLAP(관계형 OLAP) 저장소를 사용합니다.|  
|*HOLAP*|부모가 HOLAP(하이브리드 OLAP) 저장소를 사용합니다. **참고:** 이 값에만 유효 [파티션](../objects/partition-element-assl.md) 부모 요소입니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `CurrentStorageMode`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.StorageMode>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
