---
title: 개체 요소 (차원) (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Object Element (Dimension)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: db7feb39-7cc1-4b54-8979-77ce402ef71f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4c9fea7e5971bec14f172f482db2ae72efdf154
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051063"
---
# <a name="object-element-dimension-xmla"></a>Object 요소(차원)(XMLA)
  차원에 대 한 개체 참조가 포함 부모 [삽입](../xml-elements-commands/insert-element-xmla.md)를 [업데이트](../xml-elements-commands/update-element-xmla.md), 또는 [Drop](../xml-elements-commands/drop-element-xmla.md) 명령을 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Insert> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <Database>...</Database>  
      <Cube>...</Cube>  
      <Dimension>...</Dimension>  
   </Object>  
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
|부모 요소|[Drop](../xml-elements-commands/drop-element-xmla.md)하십시오 [삽입](../xml-elements-commands/insert-element-xmla.md), [업데이트](../xml-elements-commands/update-element-xmla.md)|  
|자식 요소|[큐브](cube-element-xmla.md)하십시오 [데이터베이스](database-element-xmla.md), [차원](dimension-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
