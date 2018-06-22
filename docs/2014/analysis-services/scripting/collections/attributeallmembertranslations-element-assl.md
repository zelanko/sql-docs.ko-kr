---
title: AttributeAllMemberTranslations 요소 (ASSL) | Microsoft Docs
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
- AttributeAllMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeAllMemberTranslations
helpviewer_keywords:
- AttributeAllMemberTranslations element
ms.assetid: 1a0d86ea-d95d-4d93-b321-acd35ed4ac26
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fa787c7c3731962690c1b8d25e736f061caf74e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081219"
---
# <a name="attributeallmembertranslations-element-assl"></a>AttributeAllMemberTranslations 요소(ASSL)
  차원에 있는 All 멤버의 캡션에 대한 번역의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
   ...  
   <AttributeAllMemberTranslations>  
      <AttributeAllMemberTranslation xsi:type="Translation">...</AttributeAllMemberTranslation>  
   </AttributeAllMemberTranslations>  
      ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Dimension](../objects/dimension-element-assl.md)|  
|자식 요소|[AttributeAllMemberTranslation](../objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 `AttributeAllMemberTranslations` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Translation 요소 &#40;ASSL&#41;](translations-element-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  