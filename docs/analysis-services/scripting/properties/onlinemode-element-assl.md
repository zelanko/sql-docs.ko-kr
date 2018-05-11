---
title: OnlineMode 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d566ff327a08b6c9c0cd7f0f7ee8d0cd5c219abc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="onlinemode-element-assl"></a>OnlineMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만들지, 아니면 캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만들지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*직접 실행*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*직접 실행*|캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만듭니다.|  
|*OnCacheComplete*|캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만듭니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **OnlineMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ProactiveCaching>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ProactiveCaching 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
  
