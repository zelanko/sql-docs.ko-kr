---
title: 언어 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 66b14ca19b6c86d6fb959ff462a0cd0d5118843b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="language-element-xmla"></a>Language 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 대 한 로캘 식별자 (LCID)를 포함 [번역](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[번역](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **언어** 요소는 부모에 의해 사용 되는 LCID를 지정 **번역** 할당 하는 요소는 **이름** 부모 **번역** 지정 된 언어는 특성 멤버에는 요소 중는 **삽입** 또는 **업데이트** 명령입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 & #40; 삽입 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Name 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [Update 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
