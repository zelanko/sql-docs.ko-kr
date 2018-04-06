---
title: AggregationStorage 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregationStorage Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationStorage
helpviewer_keywords:
- AggregationStorage element
ms.assetid: dd082388-534d-4847-9232-8f80fc9fe96e
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 431f238f483bdf29ffec76aab63f11f660fb7255
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="aggregationstorage-element-assl"></a>AggregationStorage 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]집계 저장 방법을 식별합니다.  
  
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
|부모 요소|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|집계 데이터가 기본 방식으로 저장됩니다.|  
|*MolapOnly*|집계 데이터가 MOLAP(다차원 OLAP) 저장소에만 저장됩니다.|  
  
 *MolapOnly* 옵션은에 대해서만 사용할 수는 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **AggregationStorage** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
