---
title: NamingTemplateTranslations 요소 (ASSL) | Microsoft Docs
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
- NamingTemplateTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslations
helpviewer_keywords:
- NamingTemplateTranslations element
ms.assetid: fde65778-1fa3-490a-9874-8bf2052ef25c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0e22eaea2ab6d19bf1da5620321f0d2002ed382d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081944"
---
# <a name="namingtemplatetranslations-element-assl"></a>NamingTemplateTranslations 요소(ASSL)
  에 대 한 지역화 된 번역의 컬렉션을 제공 된 [NamingTemplate](../properties/namingtemplate-element-assl.md) 부모 요소의 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <NamingTemplateTranslations>  
            <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
...</NamingTemplateTranslations>  
   ...  
</Attribute>  
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
|부모 요소|[특성](../objects/attribute-element-assl.md) 형식의 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|[NamingTemplateTranslation](../objects/translation-element-assl.md) 형식의 [변환](translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 값은 `NamingTemplateTranslation` 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용](../properties/usage-element-dimensionattribute-assl.md) 부모 `DimensionAttribute` 로 설정 되어 *부모*.)  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  