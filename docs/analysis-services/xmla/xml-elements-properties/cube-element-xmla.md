---
title: "큐브 요소 (XMLA) | Microsoft Docs"
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
apiname: Cube Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords: Cube element
ms.assetid: 2e8662f4-fb2e-43af-b70a-9e0b5872c9b9
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 475c302b61f10e86f43b1a2475734a1b345f431c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cube-element-xmla"></a>Cube 요소(XMLA)
  부모 나타내는 차원을 포함 하는 큐브를 식별 [개체](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Object>  
   ...  
   <Cube>...</Cube>  
   ...  
</Object>  
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
|부모 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **큐브** 요소가 나타내는 차원을 포함 하는 큐브의 이름을 포함 하는 개체 식별자는 **개체** 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Database 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)   
 [Dimension 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
