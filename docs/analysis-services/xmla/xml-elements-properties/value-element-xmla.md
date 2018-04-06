---
title: 값 요소 (XMLA) | Microsoft Docs
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
- Value Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d40497916d4ec482fae217dfbddac4a12bd011d0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="value-element-xmla"></a>Value 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]원하는 값이 포함 된 [특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) 요소에 추가할 수는 [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) 명령, 또는 [셀](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) 을 업데이트 하는 요소는 [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|전체|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [셀](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 에 대 한 **특성** 요소는 **값** 후 멤버가 포함 해야 하는 원하는 값을 포함 하는 요소는 **삽입** 명령 커밋됩니다. 멤버 삽입 하는 방법에 대 한 자세한 내용은 참조 [삽입, 업데이트 및 삭제 멤버 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
 에 대 한 **셀** 요소는 **값** 셀 후 포함 해야 하는 원하는 값을 포함 하는 요소는 **UpdateCells** 명령 커밋됩니다. 해당 셀의 쓰기 저장(writeback) 테이블에 저장되는 실제 값은 셀의 원본 값과 원하는 값 간의 차이입니다.  
  
 이 요소에 사용되는 데이터 형식은 업데이트할 셀의 데이터 형식과 일치해야 합니다.  
  
 셀 업데이트에 대한 자세한 내용은 [셀 업데이트&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [CellOrdinal 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [요소 &#40; 삽입 XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
