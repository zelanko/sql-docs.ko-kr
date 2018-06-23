---
title: HideMemberIf 요소 (ASSL) | Microsoft Docs
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
- HideMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HideMemberIf
helpviewer_keywords:
- HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2b1540a3b7f5d1e1a93ea3b4628bfbde186e5bb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091804"
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 요소(ASSL)
  클라이언트 응용 프로그램에서 수준의 멤버를 숨길지 여부와 숨길 조건을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*하지*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Level](../objects/level-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*하지*|멤버를 숨기지 않습니다.|  
|*OnlyChildWithNoName*|멤버가 부모의 유일한 자식이고 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*OnlyChildWithParentName*|멤버가 부모의 유일한 자식이고 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
|*NoName*|멤버의 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*ParentName*|멤버의 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `HideMemberIf`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.HideIfValue>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  