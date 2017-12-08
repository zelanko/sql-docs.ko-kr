---
title: "UName 요소 (XMLA) | Microsoft Docs"
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
apiname: UName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UName
- urn:schemas-microsoft-com:xml-analysis#UName
- microsoft.xml.analysis.uname
helpviewer_keywords: UName element
ms.assetid: b4916d44-cf77-4d4c-b4e5-a0a98192d057
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a70ba37314bddd8b96f417a28b0e1934f02b8c23
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="uname-element-xmla"></a>UName 요소(XMLA)
  부모 고유 이름을 포함 [HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md) 또는 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <UName>...</UName>  
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
 에 대 한 **HierarchyInfo** 요소는 **UName** 요소는 고유한 멤버는 계층의 이름을 제공 하는 속성의 이름을 포함 합니다. 이 값은 OLAP용 OLE DB 사양의 축 행 집합에 정의된 MEMBER_UNIQUE_NAME 속성과 같습니다.  
  
 에 대 한 **멤버** 요소는 **UName** 요소 부모 고유 이름을 포함 **멤버** 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
