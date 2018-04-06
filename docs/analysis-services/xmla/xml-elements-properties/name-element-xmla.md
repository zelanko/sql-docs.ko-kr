---
title: Name 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Name Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 995792653603bd7ff5954a34755e7704544675b6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="name-element-xmla"></a>Name 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]부모에 대 한 특성 멤버의 이름을 포함 [특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) 또는 [번역](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|카디널리티|  
|------------------------|-----------------|  
|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|[번역](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [번역](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 에 대 한 **특성** 요소는 **이름** 요소를 삽입 하거나 각각을 수행 하는 동안 업데이트 된 특성 멤버의 이름을 포함 된 **삽입** 또는 **업데이트** 명령입니다.  
  
 에 대 한 **번역** 요소는 **이름** 요소에서 지정 된 언어로 특성 멤버의 캡션을 포함는 **언어** 부모요소 **번역** 개체입니다. 경우는 **이름** 요소는 지정 하지 않거나 빈 문자열의 값을 포함는 **이름** 에 대 한 요소는 **특성** 요소를 포함 하는  **번역** 요소를 사용 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 &#40; 삽입 XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [언어 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Update 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
