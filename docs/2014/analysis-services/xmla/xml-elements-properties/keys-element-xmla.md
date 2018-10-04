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
- Keys Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Keys
- http://schemas.microsoft.com/analysisservices/2003/engine#Keys
- microsoft.xml.analysis.keys
helpviewer_keywords:
- Keys element
ms.assetid: 67291791-0032-412a-9a4f-74f68533e83d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48065d8c40c6cba3b60d405be77d0e1877e11910
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148713"
---
# <a name="keys-element-xmla"></a>Keys 요소(XMLA)
  컬렉션을 포함 [키](key-element-xmla.md) 부모를 나타내는 특성 멤버의 멤버 키를 식별 하는 데 사용 되는 요소 [특성](attribute-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute>  
   ...  
   <Keys>  
      <Key>...</Key>  
   </Keys>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Attribute](attribute-element-xmla.md)|  
|자식 요소|[키](key-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
