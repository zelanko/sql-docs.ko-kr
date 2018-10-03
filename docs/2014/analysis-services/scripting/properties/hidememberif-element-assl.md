---
title: HideMemberIf 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae715268b4b62c88e8d4f660c7d8d1772ccae02c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109003"
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
|기본값|*되지*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Level](../objects/level-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*되지*|멤버를 숨기지 않습니다.|  
|*OnlyChildWithNoName*|멤버가 부모의 유일한 자식이고 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*OnlyChildWithParentName*|멤버가 부모의 유일한 자식이고 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
|*NoName*|멤버의 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*ParentName*|멤버의 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `HideMemberIf`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.HideIfValue>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
