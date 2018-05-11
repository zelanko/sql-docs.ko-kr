---
title: Update 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bb1fee17642935982b4ea67cafe0c9e6320eb45
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="update-element-xmla"></a>Update 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  차원의 특성 멤버를 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md), [MoveWithDescendants](../../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md), [개체](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md), [위치](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Update** 명령은 쓰기 가능 차원에서 특성 멤버를 이동시킵니다.  
  
 구성원을 업데이트 하는 방법에 대 한 자세한 내용은 참조 [삽입, 업데이트 및 삭제 멤버 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Drop 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [요소 & #40; 삽입 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
