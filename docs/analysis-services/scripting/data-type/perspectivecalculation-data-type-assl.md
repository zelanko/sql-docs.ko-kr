---
title: "PerspectiveCalculation 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: PerspectiveCalculation Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: PerspectiveCalculation
helpviewer_keywords: PerspectiveCalculation data type
ms.assetid: 5a5173d2-c96d-4a55-a35c-0cbfd5b0e599
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 767641d72af98aa02cfa4c1008c0dd31d8c53ca2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="perspectivecalculation-data-type-assl"></a>PerspectiveCalculation 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]간의 관계를 나타내는 기본 데이터 형식을 정의 및 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PerspectiveCalculation>  
      <Name>...</Name>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</PerspectiveCalculation>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [유형](../../../analysis-services/scripting/properties/type-element-perspectivecalculation-assl.md)|  
|파생 요소|[계산](../../../analysis-services/scripting/objects/calculation-element-assl.md) ([계산](../../../analysis-services/scripting/collections/calculations-element-assl.md) 컬렉션 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.PerspectiveCalculation>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
