---
title: LName 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#LName
- http://schemas.microsoft.com/analysisservices/2003/engine#LName
- microsoft.xml.analysis.lname
helpviewer_keywords:
- LName element
ms.assetid: 2c8c2fa9-cb2d-44ea-b253-5e6ff61f1b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ba25e2c379c4049e34e7586e0574332720403c9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168383"
---
# <a name="lname-element-xmla"></a>LName 요소(XMLA)
  부모에 대 한 고유한 수준 이름에 대 한 정보가 [HierarchyInfo](hierarchyinfo-element-xmla.md) 하거나 [멤버](member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LName>...</LName>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[HierarchyInfo](hierarchyinfo-element-xmla.md), [Member](member-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `HierarchyInfo` 요소의 경우 이 요소는 계층의 고유한 수준 이름을 제공하는 속성의 이름을 포함합니다. 이 값은 OLAP 사양에 대한 OLE DB의 축 행 집합에 대해 정의된 LEVEL_UNIQUE_NAME 속성과 동일합니다.  
  
 `Member` 요소의 경우 이 요소는 부모 `Member` 요소가 나타내는 멤버가 포함된 계층의 고유한 수준 이름을 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
