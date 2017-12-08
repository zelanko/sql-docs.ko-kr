---
title: "DefaultMeasure 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
apiname: DefaultMeasure Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DefaultMeasure
helpviewer_keywords: DefaultMeasure element
ms.assetid: ceac8b3d-ebae-463f-9e8c-506281d42792
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ff93051b34b685bfe7d7138be0e7a6647d8b8e9c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="defaultmeasure-element-assl"></a>DefaultMeasure 요소(ASSL)
  에 대 한 기본 측정값을 정의 하는 MDX (Multidimensional Expressions) 식을 포함 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 또는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <DefaultMeasure>...</DefaultMeasure>  
   ...  
</Cube>  
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
|부모 요소|[큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **DefaultMeasure** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube> 및 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
