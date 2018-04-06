---
title: ScriptCacheProcessingMode 요소 (ASSL) | Microsoft Docs
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
- ScriptCacheProcessingMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ScriptCacheProcessingMode
helpviewer_keywords:
- ScriptCacheProcessingMode element
ms.assetid: 95c0723c-69a4-43e7-b743-f712180a7681
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6a0430d99739470b46399b7ddef28bc7a13d0370
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]처리 하는 동안 아니면 처리 후 서버에서 스크립트 캐시를 작성 해야 하는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
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
|부모 요소|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|서버에서 스크립트를 처리 중에 작성합니다.|  
|*지연*|서버에서 스크립트를 처리 후에 작성합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>합니다.  
  
 부모에 해당 하는 요소 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
