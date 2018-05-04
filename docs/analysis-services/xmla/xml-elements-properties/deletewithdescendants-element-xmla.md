---
title: DeleteWithDescendants 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DeleteWithDescendants Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DeleteWithDescendants
- microsoft.xml.analysis.deletewithdescendants
- urn:schemas-microsoft-com:xml-analysis#DeleteWithDescendants
helpviewer_keywords:
- DeleteWithDescendants element
ms.assetid: adfc9437-aaa7-4364-bcdb-128fcc9a410d
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9844e13de56dddae48afc59d0e44fc5203cfdd40
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="deletewithdescendants-element-xmla"></a>DeleteWithDescendants 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 명령으로도 특성 멤버의 하위 항목을 삭제할 수 있는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **DeleteWithDescendants** 요소는 **Drop** 명령이 [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) 요소에서 식별하는 특성 멤버뿐만 아니라 해당 특성 멤버의 하위 항목도 함께 삭제할 수 있는지 여부를 결정합니다.  
  
> [!NOTE]  
>  이 요소는 부모-자식 계층에 있는 특성 멤버에만 적용됩니다.  
  
 특성 멤버 삭제 및 업데이트에 대한 자세한 내용은 [멤버 삽입, 업데이트 및 삭제&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
