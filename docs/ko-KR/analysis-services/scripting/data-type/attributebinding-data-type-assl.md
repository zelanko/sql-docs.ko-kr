---
title: AttributeBinding 데이터 형식 (ASSL) | Microsoft Docs
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
- AttributeBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeBinding
helpviewer_keywords:
- AttributeBinding data type
ms.assetid: 24d511a9-d0eb-4150-9f78-541e03963d67
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1beaa67164faf68603bc1fad0753d2276ded6bb0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="attributebinding-data-type-assl"></a>AttributeBinding 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) 요소에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeBinding>  
   <AttributeID>...</AttributeID>  
      <Type>...</Type>  
   <Ordinal>...</Ordinal>  
</AttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Ordinal](../../../analysis-services/scripting/properties/ordinal-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|  
|파생 요소|[Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)참조|  
  
## <a name="remarks"></a>주의  
 에 대 한 자세한 내용은 **바인딩** 데이터 형식에서 파생 되는 Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 **바인딩** 참조 데이터 형식, [데이터 바인딩 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)합니다.  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AttributeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
