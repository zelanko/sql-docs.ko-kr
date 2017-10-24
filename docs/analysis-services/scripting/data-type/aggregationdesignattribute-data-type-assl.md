---
title: "AggregationDesignAttribute 데이터 형식 (ASSL) | Microsoft Docs"
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
- AggregationDesignAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationDesignAttribute
helpviewer_keywords:
- AggregationDesignAttribute data type
ms.assetid: 03d29d76-e4bd-4035-92cc-35149d83fbf9
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98e6e6fa25ece247ab5ec1a84fc7ca0f61871d34
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationdesignattribute-data-type-assl"></a>AggregationDesignAttribute 데이터 형식(ASSL)
  특성 간의 연결을 나타내는 기본 데이터 형식을 정의 및 [AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationDesignAttribute>  
   <AttributeID>...</AttributeID>  
      <EstimatedCount>...</EstimatedCount>  
</AggregationDesignAttribute>  
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
|자식 요소|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)|  
|파생 요소|[특성](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([특성](../../../analysis-services/scripting/collections/attributes-element-assl.md) 컬렉션 [AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md))|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AggregationDesignAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AggregationDesignDimension 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

