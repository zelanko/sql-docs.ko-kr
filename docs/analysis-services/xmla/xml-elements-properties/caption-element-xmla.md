---
title: "캡션 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Caption Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Caption
- http://schemas.microsoft.com/analysisservices/2003/engine#Caption
- microsoft.xml.analysis.caption
helpviewer_keywords: Caption element
ms.assetid: 3d10ee68-98ab-4da0-a409-800dea2f1c32
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b1d22c28c79adbefcdd136a7412fe39e53792299
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="caption-element-xmla"></a>Caption 요소(XMLA)
  부모의 캡션에 대 한 정보를 포함 [HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md) 또는 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <Caption>...</Caption>  
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
 에 대 한 **HierarchyInfo** 요소는 **캡션** 요소 멤버의 계층 구조는 캡션을 제공 하는 속성의 이름을 포함 합니다. 이 값은 OLAP 사양에 대한 OLE DB의 축 행 집합에 대해 정의된 MEMBER_CAPTION 속성과 동일합니다.  
  
 에 대 한 **멤버** 요소는 **캡션** 요소는 부모의 캡션을 포함 **멤버** Analysis (XMLA) 세션에 대 한 XML에 대해 지정 된 언어 요소입니다. 사용 가능한 캡션이 없으면 이 요소는 멤버의 고유한 이름을 포함합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
