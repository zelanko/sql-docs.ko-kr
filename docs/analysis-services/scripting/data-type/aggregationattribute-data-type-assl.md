---
title: "AggregationAttribute 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationAttribute
helpviewer_keywords:
- AggregationAttribute data type
ms.assetid: 636827c7-938d-4b7d-9827-46da3bc60d9a
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4e7ac84001e3b113f8a351d464b0bec35fe5272
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationattribute-data-type-assl"></a>AggregationAttribute 데이터 형식(ASSL)
  간의 연결을 나타내는 기본 데이터 형식을 정의 [집계](../../../analysis-services/scripting/objects/aggregation-element-assl.md) 요소와 특성입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|파생 요소|[특성](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([특성](../../../analysis-services/scripting/collections/attributes-element-assl.md) 컬렉션 [AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md))|  
  
## <a name="remarks"></a>주의  
 AMO(Analysis Management Objects) 개체 모델의 해당 클래스는 <xref:Microsoft.AnalysisServices.AggregationAttribute>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Aggregation 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

