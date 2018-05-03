---
title: AggregationAttribute 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 09295db73608fa040960a709271f1c72816848b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationattribute-data-type-assl"></a>AggregationAttribute 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) 요소와 특성 간의 연결을 나타내는 기본 데이터 형식을 정의합니다.  
  
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
|자식 요소|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|파생 요소|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([AggregationDimension](../../../analysis-services/scripting/collections/attributes-element-assl.md) 의 [Attributes](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)컬렉션)|  
  
## <a name="remarks"></a>주의  
 AMO(Analysis Management Objects) 개체 모델의 해당 클래스는 <xref:Microsoft.AnalysisServices.AggregationAttribute>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Aggregation 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
