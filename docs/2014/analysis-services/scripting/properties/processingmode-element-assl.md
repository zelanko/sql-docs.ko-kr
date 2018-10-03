---
title: ProcessingMode 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProcessingMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ProcessingMode
helpviewer_keywords:
- ProcessingMode element
ms.assetid: dff6eeba-f09c-4d8c-ad81-caef76254af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 550b19dc291818052b954b476d3673fd717d38ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148603"
---
# <a name="processingmode-element-assl"></a>ProcessingMode 요소(ASSL)
  인스턴스에서 인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProcessingMode>...</ProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md)하십시오 [차원](../objects/dimension-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [파티션](../objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `ProcessingMode`의 `Cube` 값은 큐브의 기본값을 제공하며 각 파티션에 대해 `ProcessingMode`를 설정하여 이 기본값을 덮어쓸 수 있습니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|인스턴스가 처리 중에 인덱싱 및 집계를 수행합니다.|  
|*LazyOptimizations*|인스턴스가 처리 후에 인덱싱 및 집계를 수행합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `ProcessingMode`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ProcessingMode>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
