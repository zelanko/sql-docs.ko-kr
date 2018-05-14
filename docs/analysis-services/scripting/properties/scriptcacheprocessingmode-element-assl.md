---
title: ScriptCacheProcessingMode 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c6d355029964905071bcef03ac8721e5df2208f9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  서버에서 스크립트 캐시를 처리 중에 작성할지, 아니면 처리 후에 작성할지를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*Regular*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Regular*|서버에서 스크립트를 처리 중에 작성합니다.|  
|*지연*|서버에서 스크립트를 처리 후에 작성합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>합니다.  
  
 부모에 해당 하는 요소 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
