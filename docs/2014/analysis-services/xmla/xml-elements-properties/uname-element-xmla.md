---
title: UName 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UName
- urn:schemas-microsoft-com:xml-analysis#UName
- microsoft.xml.analysis.uname
helpviewer_keywords:
- UName element
ms.assetid: b4916d44-cf77-4d4c-b4e5-a0a98192d057
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d348fe5f1474b44df2bd765e7c9d7db2df4c809e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083623"
---
# <a name="uname-element-xmla"></a>UName 요소(XMLA)
  부모의 고유 이름이 포함 되어 있습니다 [HierarchyInfo](hierarchyinfo-element-xmla.md) 하거나 [멤버](member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <UName>...</UName>  
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
 `HierarchyInfo` 요소의 경우 `UName` 요소는 계층의 고유한 멤버 이름을 제공하는 속성 이름을 포함합니다. 이 값은 OLAP용 OLE DB 사양의 축 행 집합에 정의된 MEMBER_UNIQUE_NAME 속성과 같습니다.  
  
 `Member` 요소의 경우 `UName` 요소는 부모 `Member` 요소의 고유한 이름을 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
