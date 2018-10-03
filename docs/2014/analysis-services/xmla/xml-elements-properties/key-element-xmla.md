---
title: 요소 (XMLA) 키 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Key Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords:
- Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1532db273c83f16678d278f068befefcd8df4b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101283"
---
# <a name="key-element-xmla"></a>Key 요소(XMLA)
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|전체|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[키](keys-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소에 사용되는 데이터 형식은 지정된 특성의 적절한 키 열에 대한 데이터 형식과 일치해야 합니다. `Key` 요소가 부모 `Attribute` 요소에 대해 지정되어 있지 않은 경우 부모 `AttributeName` 요소에 지정된 `Name` 및 `Attribute` 요소가 수정할 특성 멤버를 식별하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 특성 &#40;XMLA&#41;](attribute-element-xmla.md)   
 [AttributeName 요소 &#40;XMLA&#41;](name-element-xmla.md)   
 [Drop 요소 &#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 요소 &#40;ASSL&#41;](../../scripting/objects/column-element-assl.md)   
 [Update 요소 &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [여기서 요소 &#40;XMLA&#41;](where-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
