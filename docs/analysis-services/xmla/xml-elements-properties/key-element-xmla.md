---
title: 키 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd43ad594acb118be0e7fb8d39cb34f2ae3e6ef6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="key-element-xmla"></a>Key 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  특성 멤버의 멤버 키 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|전체|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[키](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소에 사용되는 데이터 형식은 지정된 특성의 적절한 키 열에 대한 데이터 형식과 일치해야 합니다. **Key** 요소가 부모 **Attribute** 요소에 대해 지정되어 있지 않은 경우 부모 **AttributeName** 요소에 지정된 **Name** 및 **Attribute** 요소가 수정할 특성 멤버를 식별하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Attribute 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [AttributeName 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Drop 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [요소 & #40; 삽입 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Update 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [여기서 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
