---
title: "ScriptCacheProcessingMode 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1982cc5b9266f8d69d0975043c307ec3272d8149
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 요소(ASSL)
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
|기본값|*일반*|  
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
|*일반*|서버에서 스크립트를 처리 중에 작성합니다.|  
|*지연*|서버에서 스크립트를 처리 후에 작성합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>합니다.  
  
 부모에 해당 하는 요소 **ScriptCacheProcessingMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

