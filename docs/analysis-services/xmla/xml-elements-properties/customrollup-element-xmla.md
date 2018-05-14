---
title: CustomRollup 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f96d2c41e2b05fddfab1231d197d6bc67ba0093
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="customrollup-element-xmla"></a>CustomRollup 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모를 나타내는 특성 멤버에 대 한 사용자 지정 롤업 수식을 포함 [특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollup>...</CustomRollup>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **CustomRollup** 요소는 부모 **Attribute** 요소에서 정의하는 특성 멤버의 롤업 동작을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
 MDX 식에 대 한 자세한 내용은 참조 [식 & #40; Mdx& #41; ](../../../mdx/expressions-mdx.md).  
  
## <a name="see-also"></a>관련 항목:  
 [요소 & #40; 삽입 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
