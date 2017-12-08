---
title: "CubeID 요소 (XMLA) | Microsoft Docs"
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
apiname: CubeID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cubeid
- urn:schemas-microsoft-com:xml-analysis#CubeID
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeID
helpviewer_keywords: CubeID element
ms.assetid: 9dba605a-c45e-4730-827b-b7c55c8110da
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1080e0948258875b219c6ba859d6fc42d8d3d59e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cubeid-element-xmla"></a>CubeID 요소(XMLA)
  부모 요소에서 개체 참조를 포함하는 큐브를 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeID>...</CubeID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|카디널리티|  
|------------------------|-----------------|  
|[원본](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|[대상](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|나머지|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md), [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md), [Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
