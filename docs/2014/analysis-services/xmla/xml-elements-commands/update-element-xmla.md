---
title: Update 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Update Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords:
- Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9663fa3d44b91f53ac20a5a1b1dba117f7a2574
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200133"
---
# <a name="update-element-xmla"></a>Update 요소(XMLA)
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[특성](../xml-elements-properties/attributes-element-xmla.md)하십시오 [MoveWithDescendants](../xml-elements-properties/movewithdescendants-element-xmla.md), [개체](../xml-elements-properties/object-element-dimension-xmla.md), [위치](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Update` 명령은 쓰기 가능 차원에서 특성 멤버를 이동시킵니다.  
  
 구성원을 업데이트 하는 방법에 대 한 자세한 내용은 참조 하세요. [삽입, 업데이트 및 삭제 하는 멤버 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](drop-element-xmla.md)   
 [요소를 삽입 &#40;XMLA&#41;](insert-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
