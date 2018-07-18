---
title: MoveWithDescendants 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 518c95efa36c6a234036a1c7f293c3df8283749a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969193"
---
# <a name="movewithdescendants-element-xmla"></a>MoveWithDescendants 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  특성 멤버의 하위 항목의 부모에 의해 업데이트 되는지 여부를 나타냅니다 [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Update>  
   ...  
   <MoveWithDescendants>...</MoveWithDescendants>  
   ...  
</Update>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **MoveWithDescendants** 요소 결정 여부를 **업데이트** 명령에서 식별 한 특성 멤버를 바로 업데이트 하지 않아야 합니다 [특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) 요소 하지만 또한 해당 특성 멤버의 하위 항목은도 업데이트 합니다.  
  
> [!NOTE]  
>  이 요소는 부모-자식 계층에 있는 특성 멤버에만 적용됩니다.  
  
 구성원을 업데이트 하는 방법에 대 한 자세한 내용은 참조 하세요. [삽입, 업데이트 및 삭제 하는 멤버 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
