---
title: LNum 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49ab7672d51a90e30701666fbf391ffec6060f29
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575475"
---
# <a name="lnum-element-xmla"></a>LNum 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 수준 서 수 위치에 대 한 정보를 포함 [HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md) 또는 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|ssNoversion|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md), [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 **HierarchyInfo** 요소는 **LNum** 요소는 계층의 수준 서 수 위치를 제공 하는 속성의 이름을 포함 합니다. 이 값은 OLAP용 OLE DB 사양 축 행 집합에 정의된 LEVEL_NUMBER 속성과 같습니다.  
  
 에 대 한 **멤버** 요소는 **LNum** 요소 포함 0부터 시작 서 수 위치를 계층의 루트 수준에서 부모 나타내는 멤버의 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)요소입니다. 값 0은 계층의 루트 수준을 나타냅니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
