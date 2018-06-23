---
title: Insert 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 6b381a2b0cd45e80309f2b6a759374fd9f214f51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090527"
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
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[특성](../xml-elements-properties/attributes-element-xmla.md), [개체](../xml-elements-properties/object-element-dimension-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Insert` 명령은 쓰기 가능 차원에 새 특성 멤버를 삽입합니다.  
  
 구성원을 삭제 하는 방법에 대 한 자세한 내용은 참조 [삽입, 업데이트 및 삭제 멤버 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](drop-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](update-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  