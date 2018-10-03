---
title: DiscretizationMethod 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DiscretizationMethod Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 75308b5270eb762236be22fc0838a480474898dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200480"
---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 요소(ASSL)
  불연속화에 사용할 방법을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `DiscretizationMethod` 요소의 값은 `DimensionAttribute` 또는 `ScalarMiningStructureColumn`에 대한 값을 불연속화하거나 특정 그룹 집합으로 구성하는 방법을 결정합니다. 불연속화 방법에 대 한 자세한 내용은 참조 하세요. [분할 메서드 &#40;데이터 마이닝&#41;](../../data-mining/discretization-methods-data-mining.md)합니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*자동*|마이닝 구조 열의 AUTOMATIC 불연속화 메서드와 같습니다.|  
|*EqualAreas*|마이닝 구조 열의 EQUAL_AREAS 불연속화 메서드와 같습니다.|  
|*클러스터*|마이닝 구조 열의 CLUSTERS 불연속화 메서드와 같습니다.|  
|*임계값*|마이닝 구조 열의 THRESHOLDS 불연속화 메서드와 같습니다.|  
|*EqualRanges*|마이닝 구조 열의 EQUAL_RANGES 불연속화 메서드와 같습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `DiscretizationMethod`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.DiscretizationMethod>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
