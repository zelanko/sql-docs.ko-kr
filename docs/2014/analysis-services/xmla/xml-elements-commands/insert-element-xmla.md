---
title: Insert 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Insert Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Insert
- http://schemas.microsoft.com/analysisservices/2003/engine#Insert
- microsoft.xml.analysis.insert
helpviewer_keywords:
- Insert command
ms.assetid: d1137033-cc19-4bcb-b93d-8575f17bea6b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a077a263a66c4684279be6e2f353348f451d5435
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120933"
---
# <a name="insert-element-xmla"></a>Insert 요소(XMLA)
  특성 멤버를 차원에 삽입합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Insert>  
      <Object>...</Object>  
      <Attributes>...</Attributes>  
   </Insert>  
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
|자식 요소|[특성](../xml-elements-properties/attributes-element-xmla.md), [개체](../xml-elements-properties/object-element-dimension-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Insert` 명령은 쓰기 가능 차원에 새 특성 멤버를 삽입합니다.  
  
 구성원을 삭제 하는 방법에 대 한 자세한 내용은 참조 하세요. [삽입, 업데이트 및 삭제 하는 멤버 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](drop-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](update-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
