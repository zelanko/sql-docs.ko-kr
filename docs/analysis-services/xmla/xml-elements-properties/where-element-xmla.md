---
title: 여기서 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 119a702b28956c5570d30e3692b7d7339f49486f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580015"
---
# <a name="where-element-xmla"></a>Where 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 또는 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) 명령에 사용되는 필터 조건을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|자식 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **Drop** 명령의 경우 [DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) 요소와 함께 **Where** 요소를 사용하면 삭제될 특성 멤버의 범위가 식별됩니다.  
  
 **Update** 명령의 경우 **Where** 요소는 업데이트될 특성 멤버의 범위를 식별합니다. 부모 **Attributes** 명령의 **Update** 컬렉션과 **Attributes** 요소의 **Where** 컬렉션에 포함된 특성의 조합을 사용하여 여러 특성 멤버를 업데이트할 수 있습니다.  
  
 특성 멤버 삭제 및 업데이트에 대한 자세한 내용은 [멤버 삽입, 업데이트 및 삭제&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
