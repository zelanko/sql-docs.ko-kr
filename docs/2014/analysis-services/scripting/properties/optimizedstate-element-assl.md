---
title: OptimizedState 요소 (ASSL) | Microsoft Docs
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
- OptimizedState Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OptimizedState
helpviewer_keywords:
- OptimizedState element
ms.assetid: 120dcc4c-8fe8-4471-bbd6-99ad534364f0
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 932ef541a0e9613ad46a032be5c218eccd5276ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224075"
---
# <a name="optimizedstate-element-assl"></a>OptimizedState 요소(ASSL)
  계층에 적용되는 최적화 수준을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeHierarchy>  
   ...  
   <OptimizedState>...</OptimizedState>  
   ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*FullyOptimized*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeHierarchy](../data-type/hierarchy-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*FullyOptimized*|인스턴스에서 계층에 대해 인덱스를 작성하여 쿼리 성능을 향상시킵니다.|  
|*NotOptimized*|인스턴스에서 추가 인덱스를 작성하지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `OptimizedState`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.OptimizationType>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
