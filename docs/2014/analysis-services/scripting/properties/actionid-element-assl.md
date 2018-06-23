---
title: ActionID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ActionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ActionID
helpviewer_keywords:
- ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13e83d3a022416de56cba7bbf6693ea408b51562
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090750"
---
# <a name="actionid-element-assl"></a>ActionID 요소(ASSL)
  이름을 포함 한 [작업](../objects/action-element-assl.md) 에 정의 된 요소는 [큐브](../objects/cube-element-assl.md) 요소에서 사용할 수 있는 [관점](../objects/perspective-element-assl.md) 요소도는 [PerspectiveAction](../data-type/action-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
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
|부모 요소|[PerspectiveAction](../data-type/action-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 `ActionID` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.PerspectiveAction>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Actions 요소 &#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  