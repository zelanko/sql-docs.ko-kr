---
title: "Usage 요소 (DimensionAttribute) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Usage Element (DimensionAttribute)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Usage
helpviewer_keywords: Usage element
ms.assetid: c5e38d2e-5a8e-4157-84e9-285e78c84e74
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 74eead7c703d1d5708eb9351125b07c6c266253f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="usage-element-dimensionattribute-assl"></a>Usage 요소(DimensionAttribute)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]특성의 사용 방법을 설명 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Usage>...</Usage>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|일반 특성입니다.|  
|*키*|키 특성입니다.|  
|*Parent*|부모 특성입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **사용량** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeUsage>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [특성 및 특성 계층](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
