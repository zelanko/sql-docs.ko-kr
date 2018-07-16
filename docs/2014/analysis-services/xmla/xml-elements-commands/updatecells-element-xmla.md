---
title: UpdateCells 요소 (XMLA) | Microsoft Docs
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
- UpdateCells Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.updatecells
- urn:schemas-microsoft-com:xml-analysis#UpdateCells
- http://schemas.microsoft.com/analysisservices/2003/engine#UpdateCells
helpviewer_keywords:
- UpdateCells command
ms.assetid: 18336a35-8a46-4532-9ee7-71828b2982af
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05b3b1dae8f409f367a88b696accb77484304b4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219983"
---
# <a name="updatecells-element-xmla"></a>UpdateCells 요소(XMLA)
  쓰기 가능 큐브의 셀을 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <UpdateCells>  
      <Cell>...</Cell>  
   </UpdateCells>  
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
|자식 요소|[Cell](../xml-elements-properties/cell-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `UpdateCells` 명령은 쓰기 저장(writeback)을 지원하는 큐브의 셀을 업데이트합니다.  
  
 셀 업데이트에 대한 자세한 내용은 [셀 업데이트&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](drop-element-xmla.md)   
 [요소를 삽입 &#40;XMLA&#41;](insert-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](update-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
