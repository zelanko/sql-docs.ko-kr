---
title: ProactiveCaching 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCaching Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ProactiveCaching
helpviewer_keywords:
- ProactiveCaching element
ms.assetid: 85f9ed44-2ede-406f-b0ca-237ab2f49722
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c873cc6885d4f3a40f0de9e2f34048aff193c72
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183245"
---
# <a name="proactivecaching-element-assl"></a>ProactiveCaching 요소(ASSL)
  부모 요소에 대한 자동 관리 캐싱 설정을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProactiveCaching>  
      <OnlineMode>...</OnlineMode>  
      <AggregationStorage>...</AggregationStorage>  
      <Source>...</Source>  
      <SilenceInterval>...</SilenceInterval>  
      <Latency>...</Latency>  
      <SilenceOverrideInterval>...</SilenceOverrideInterval>  
      <ForceRebuildInterval>...</ForceRebuildInterval>  
      <Enabled >...</Enabled>  
   </ProactiveCaching>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](cube-element-assl.md)하십시오 [차원](dimension-element-assl.md), [MeasureGroup](group-element-assl.md), [파티션](partition-element-assl.md)|  
|자식 요소|[AggregationStorage](../properties/aggregationstorage-element-assl.md), [활성화](../properties/enabled-element-assl.md), [ForceRebuildInterval](../properties/forcerebuildinterval-element-assl.md)를 [대기 시간](../properties/latency-element-assl.md)를 [OnlineMode](../properties/onlinemode-element-assl.md), [ SilenceInterval](../properties/silenceinterval-element-assl.md)하십시오 [SilenceOverrideInterval](../properties/silenceoverrideinterval-element-assl.md), [원본](../properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCaching>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
