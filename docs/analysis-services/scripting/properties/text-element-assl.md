---
title: Text 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 77e7fad88ddba7d6eaed048f1c2b1ef95bd9c5bb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062711"
---
# <a name="text-element-assl"></a>Text 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  텍스트를 포함 한 [명령](../../../analysis-services/scripting/objects/command-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/scripting/objects/command-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 **텍스트** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Command>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소는 명령 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)   
 [속성 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
