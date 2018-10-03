---
title: UnknownMember 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UnknownMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dab3908376520a67e1192a0a4a2d52c76b6a88df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052333"
---
# <a name="unknownmember-element-assl"></a>UnknownMember 요소(ASSL)
  알 수 없는 멤버의 표시 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Dimension](../objects/dimension-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*표시*|알 수 없는 멤버가 있고 표시됩니다.|  
|*숨겨진*|알 수 없는 멤버가 있지만 표시되지 않습니다.|  
|*없음*|알 수 없는 멤버가 사용되지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `UnknownMember`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [UnknownMemberName 요소 &#40;ASSL&#41;](name-element-assl.md)   
 [UnknownMemberTranslation 요소 &#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
