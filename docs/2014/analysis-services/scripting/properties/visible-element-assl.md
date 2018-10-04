---
title: Visible 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Visible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Visible
helpviewer_keywords:
- Visible element
ms.assetid: 3e9baf1b-351f-4ebf-b57d-13d561f72d6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a28fa446eb1753ce85458a19b849729f57c67a7a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166663"
---
# <a name="visible-element-assl"></a>Visible 요소(ASSL)
  부모 요소의 표시 유형을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|True|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../objects/calculationproperty-element-assl.md), [큐브](../objects/cube-element-assl.md)를 [CubeDimension](../data-type/dimension-data-type-assl.md)를 [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)를 [데이터베이스](../objects/database-element-assl.md), [측정값 ](../objects/measure-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Visible` 요소는 사용자 인터페이스 구성 요소에서 부모 요소를 표시할 것인지 여부를 결정합니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 `Visible`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.CubeHierarchy>, <xref:Microsoft.AnalysisServices.Database> 및 <xref:Microsoft.AnalysisServices.Measure>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
