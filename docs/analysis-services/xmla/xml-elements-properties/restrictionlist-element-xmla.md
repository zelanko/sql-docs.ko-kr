---
title: "RestrictionList 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RestrictionList Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords: RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: af4df63d245aacd861c9f4a2a1d8a4c9d8a9b01d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 요소(XMLA)
  [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드에서 사용되는 제한 열 및 값의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[제한 사항](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|자식 요소|제한 열 및 값(주의 참조)|  
  
## <a name="remarks"></a>주의  
 **RestrictionList** 요소에는 **Discover** 메서드에서 반환한 데이터를 필터링할 수 있는 제한 열의 컬렉션이 포함되어 있습니다. **RestrictionList** 요소의 각 제한 열은 별도의 XML 요소로 정의됩니다. 제한 열의 값은 XML 요소에 포함된 데이터이고, 제한 열의 이름은 XML 요소의 이름과 일치합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
