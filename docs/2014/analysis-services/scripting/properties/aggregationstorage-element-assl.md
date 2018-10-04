---
title: AggregationStorage 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationStorage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationStorage
helpviewer_keywords:
- AggregationStorage element
ms.assetid: dd082388-534d-4847-9232-8f80fc9fe96e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3ec001116b63816d0b1e2831a266ec3029a38a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187073"
---
# <a name="aggregationstorage-element-assl"></a>AggregationStorage 요소(ASSL)
  집계 저장 방법을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <AggregationStorage>...</AggregationStorage>  
   ...  
</ProactiveCaching>  
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
|부모 요소|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|집계 데이터가 기본 방식으로 저장됩니다.|  
|*MolapOnly*|집계 데이터가 MOLAP(다차원 OLAP) 저장소에만 저장됩니다.|  
  
 합니다 *MolapOnly* 옵션은만 사용할 수는 [파티션](../objects/partition-element-assl.md) 요소입니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `AggregationStorage`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
