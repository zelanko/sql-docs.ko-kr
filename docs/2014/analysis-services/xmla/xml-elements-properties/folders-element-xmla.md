---
title: Folders 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Folders Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folders
- http://schemas.microsoft.com/analysisservices/2003/engine#Folders
- urn:schemas-microsoft-com:xml-analysis#Folders
helpviewer_keywords:
- Folders element
ms.assetid: fefb0469-22ea-4804-8dc3-9c49825b32f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e8097a5499f1d8d34d9dd5dd53726bf02a4b098
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174353"
---
# <a name="folders-element-xmla"></a>Folders 요소(XMLA)
  [Restore](folder-element-xmla.md) 또는 [Synchronize](location-element-xmla.md) 명령을 실행하는 동안 부모 [Location](../xml-elements-commands/restore-element-xmla.md) 요소에서 사용되는 [Folder](../xml-elements-commands/synchronize-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location>  
   ...  
   <Folders>  
      <Folder>...</Folder>  
   </Folders>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[위치](location-element-xmla.md)|  
|자식 요소|[Folder](folder-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [Restore 요소 &#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [Synchronize 요소 &#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
