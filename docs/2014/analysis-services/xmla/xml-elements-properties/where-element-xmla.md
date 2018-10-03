---
title: 여기서 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Where Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords:
- Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b45926ec9022e8e8092721580c2419b423dd2b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191373"
---
# <a name="where-element-xmla"></a>Where 요소(XMLA)
  부모 [Drop](../xml-elements-commands/drop-element-xmla.md) 또는 [Update](../xml-elements-commands/update-element-xmla.md) 명령에 사용되는 필터 조건을 정의합니다.  
  
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
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Drop](../xml-elements-commands/drop-element-xmla.md), [Update](../xml-elements-commands/update-element-xmla.md)|  
|자식 요소|[특성](attributes-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 `Drop` 명령 합니다 `Where` 요소와 함께 합니다 [DeleteWithDescendants](deletewithdescendants-element-xmla.md) 삭제 될 특성 멤버의 범위를 식별 하는 요소.  
  
 `Update` 명령의 경우 `Where` 요소는 업데이트될 특성 멤버의 범위를 식별합니다. 부모 `Attributes` 명령의 `Update` 컬렉션과 `Attributes` 요소의 `Where` 컬렉션에 포함된 특성의 조합을 사용하여 여러 특성 멤버를 업데이트할 수 있습니다.  
  
 특성 멤버 삭제 및 업데이트에 대한 자세한 내용은 [멤버 삽입, 업데이트 및 삭제&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
