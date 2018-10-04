---
title: AggregationAttribute 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationAttribute
helpviewer_keywords:
- AggregationAttribute data type
ms.assetid: 636827c7-938d-4b7d-9827-46da3bc60d9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05b0f2f1bc4ed517c289cb4e68810265118d9ea7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078673"
---
# <a name="aggregationattribute-data-type-assl"></a>AggregationAttribute 데이터 형식(ASSL)
  간의 연결을 나타내는 기본 데이터 형식을 정의 하는 [집계](../objects/aggregation-element-assl.md) 요소와 특성입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributeID](../properties/id-element-assl.md), [주석](../collections/annotations-element-assl.md)|  
|파생 요소|[특성](../objects/attribute-element-assl.md) ([특성](../collections/attributes-element-assl.md) 모음인 [AggregationDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 클래스는 <xref:Microsoft.AnalysisServices.AggregationAttribute>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Aggregation 요소 &#40;ASSL&#41;](../objects/aggregation-element-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
