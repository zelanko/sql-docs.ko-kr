---
title: UnknownMemberTranslations 요소 (ASSL) | Microsoft Docs
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
- UnknownMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMemberTranslations
helpviewer_keywords:
- UnknownMemberTranslations element
ms.assetid: 72920843-2d43-4ff4-b38e-19c9a7451cb2
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 331f61e1e0cea88ee8dfb58b5d69333f99961be4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159344"
---
# <a name="unknownmembertranslations-element-assl"></a>UnknownMemberTranslations 요소(ASSL)
  캡션에 대 한 번역의 컬렉션을 포함 합니다 [UnknownMember](../objects/member-element-assl.md) 차원의 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
   ...  
   <UnknownMemberTranslations>  
      <UnknownMemberTranslation xsi:type="Translation ">...</UnknownMemberTranslation>  
      </UnknownMemberTranslations>  
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
|자식 요소|[UnknownMemberTranslation](../objects/translation-element-assl.md) 형식의 [변환](../data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `UnknownMemberTranslations` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Translation 데이터 형식 &#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
