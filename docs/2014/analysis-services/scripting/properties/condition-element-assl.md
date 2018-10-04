---
title: 요소 (ASSL) 조건 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Condition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- condition
helpviewer_keywords:
- Condition element
ms.assetid: 9c3cb31c-4aa1-49e4-aeb2-6cab54db0be3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fa61c470eaf39edc883aac73707e86c21a9e24c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227923"
---
# <a name="condition-element-assl"></a>Condition 요소(ASSL)
  결정 하는 MDX (Multidimensional Expressions) 식을 포함 하는지 여부를 [동작](../objects/action-element-assl.md) 부모 요소를 대상에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Condition>...</Condition  
      ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Condition` 요소는 Boolean 값을 평가하는 MDX 식을 포함합니다. 식을 반환 하는 경우 `True`, 해당 `Action` 에 지정 된 대상에 적용 합니다 [대상](target-element-assl.md) 요소입니다. 그렇지 않으면 `Action`이 적용되지 않습니다.  
  
 부모에 해당 하는 요소가 `Condition` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
