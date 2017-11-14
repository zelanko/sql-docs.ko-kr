---
title: "DisplayFolder 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DisplayFolder Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc9e0f1479821a0559c9ac105cdbc2fb4f9f666c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="displayfolder-element-assl"></a>DisplayFolder 요소(ASSL)
  부모 요소를 나열할 폴더를 지정합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 응용 프로그램 개발자와 관리자에 대 한 여러 요소를 시각적으로 범주화 표시 폴더의 사용을 지원 될 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md), [번역](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 보다 큰 큐브에는 수백 개의 측정값과 계층이 있을 수 있습니다. **DisplayFolder** 속성은 클라이언트의 사용자 모양을 정의합니다. **DisplayFolder** 속성의 값은 다음 옵션 중 하나를 포함할 수 있습니다.  
  
-   비워 둡니다. 측정값이 폴더에 속하지 않음을 나타냅니다.  
  
-   단일 폴더 이름을 포함합니다. 측정값이 동일한 이름의 폴더에 속하는 것으로 렌더링되어야 함을 나타냅니다.  
  
-   백슬래시로 구분 된 여러 폴더 이름을 포함 (\\), 포함된 된 폴더 계층을 나타냅니다.  
  
 **DisplayFolder** 속성에 적용 됩니다. **CalculationProperty** 경우에만 요소 값 [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) 로 설정 된 *멤버* .  
  
 부모에 해당 하는 요소 **DisplayFolder** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure>, 및 <xref:Microsoft.AnalysisServices.Translation>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationProperties 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

