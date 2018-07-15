---
title: RestrictionList 요소 (XMLA) | Microsoft Docs
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
- RestrictionList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 045c5644608c7f9537124450ef2c5637eebbb796
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314593"
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 요소(XMLA)
  [Discover](../xml-elements-methods-discover.md) 메서드에서 사용되는 제한 열 및 값의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[제한 사항](restrictions-element-xmla.md)|  
|자식 요소|제한 열 및 값(주의 참조)|  
  
## <a name="remarks"></a>Remarks  
 `RestrictionList` 요소에는 `Discover` 메서드에서 반환한 데이터를 필터링할 수 있는 제한 열의 컬렉션이 포함되어 있습니다. `RestrictionList` 요소의 각 제한 열은 별도의 XML 요소로 정의됩니다. 제한 열의 값은 XML 요소에 포함된 데이터이고, 제한 열의 이름은 XML 요소의 이름과 일치합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
