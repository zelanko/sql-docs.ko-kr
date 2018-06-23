---
title: OnlineMode 요소 (ASSL) | Microsoft Docs
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
- OnlineMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3efda242b0563f4b6b853d3bf87b831da1ea8e00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185942"
---
# <a name="onlinemode-element-assl"></a>OnlineMode 요소(ASSL)
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*직접 실행*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*직접 실행*|캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만듭니다.|  
|*OnCacheComplete*|캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만듭니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `OnlineMode`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ProactiveCaching>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCaching 요소 &#40;ASSL&#41;](../objects/proactivecaching-element-assl.md)  
  
  