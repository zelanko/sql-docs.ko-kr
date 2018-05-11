---
title: LName 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5d0569d5d90abb2496da32c44a5587211269e90
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="lname-element-xmla"></a>LName 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 대 한 고유한 수준 이름에 대 한 정보를 포함 [HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md) 또는 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LName>...</LName>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md), [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 대 한 **HierarchyInfo** 요소의 경우이 요소는 계층의 고유한 수준 이름을 제공 하는 속성의 이름을 포함 합니다. 이 값은 OLAP 사양에 대한 OLE DB의 축 행 집합에 대해 정의된 LEVEL_UNIQUE_NAME 속성과 동일합니다.  
  
 에 대 한 **멤버** 요소의 경우이 요소는 부모가 나타낸 멤버를 포함 하는 계층에서 수준의 고유 이름을 포함 **멤버** 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
