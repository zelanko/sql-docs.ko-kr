---
title: Name 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088dd6aa9ce8d9ecae3e3a8f293f64b3ddc93c70
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194233"
---
# <a name="name-element-xmla"></a>Name 요소(XMLA)
  부모 특성 멤버의 이름이 [특성](attribute-element-xmla.md) 또는 [번역](translation-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|상위 항목 또는 부모.|카디널리티|  
|[Attribute](attribute-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|[번역](translation-element-xmla.md)|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](attribute-element-xmla.md), [번역](translation-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Attribute` 요소의 경우 `Name` 요소는 각각 `Insert` 또는 `Update` 명령을 실행하는 동안 삽입 또는 업데이트할 특성 멤버 이름을 포함합니다.  
  
 `Translation` 요소의 경우 `Name` 요소는 부모 `Language` 개체의 `Translation` 요소에 지정된 언어로 표시되는 특성 멤버 캡션을 포함합니다. `Name` 요소가 지정되지 않았거나 이 요소에 빈 문자열이 포함된 경우 `Name` 요소를 포함하는 `Attribute` 요소의 `Translation` 요소 값이 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [언어 요소 &#40;XMLA&#41;](language-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
