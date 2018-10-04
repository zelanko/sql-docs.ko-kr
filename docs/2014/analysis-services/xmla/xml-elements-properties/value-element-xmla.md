---
title: 값 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 054da002271711d4b86a08e694b18e01e796b3ea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205720"
---
# <a name="value-element-xmla"></a>Value 요소(XMLA)
  원하는 값이 포함을 [특성](attribute-element-xmla.md) 요소에 추가할 수는 [삽입](../xml-elements-commands/insert-element-xmla.md) 명령, 또는 [셀](cell-element-xmla.md) 을 업데이트 하는 요소는 [UpdateCells](../xml-elements-commands/updatecells-element-xmla.md)명령입니다.  
  
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
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](attribute-element-xmla.md), [셀](cell-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Attribute` 요소의 경우 `Value` 요소에는 `Insert` 명령이 커밋된 후 멤버가 포함해야 하는 원하는 값이 포함됩니다. 멤버를 삽입 하는 방법에 대 한 자세한 내용은 참조 하세요. [삽입, 업데이트 및 삭제 하는 멤버 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
 `Cell` 요소의 경우 `Value` 요소에는 `UpdateCells` 명령이 커밋된 후 셀이 포함해야 하는 원하는 값이 포함됩니다. 해당 셀의 쓰기 저장(writeback) 테이블에 저장되는 실제 값은 셀의 원본 값과 원하는 값 간의 차이입니다.  
  
 이 요소에 사용되는 데이터 형식은 업데이트할 셀의 데이터 형식과 일치해야 합니다.  
  
 셀 업데이트에 대한 자세한 내용은 [셀 업데이트&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CellOrdinal 요소 &#40;XMLA&#41;](cellordinal-element-xmla.md)   
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 요소 &#40;XMLA&#41;](../xml-elements-commands/updatecells-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
