---
title: SolveOrder 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SolveOrder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SolveOrder
helpviewer_keywords:
- SolveOrder element
ms.assetid: ec43e055-97dd-4f2a-9a7c-2df2e1119e56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4fbd4132a0dc27d9055956d4b49a1ad02bc5dff5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219513"
---
# <a name="solveorder-element-assl"></a>SolveOrder 요소(ASSL)
  계산 순서를 나타냅니다 합니다 [CalculationProperty](../objects/calculationproperty-element-assl.md) 요소가 계산된 멤버 또는 계산된 셀 정의에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty>  
   ...  
   <SolveOrder>...</SolveOrder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 합니다 `SolveOrder` 속성에 적용 됩니다 `CalculationProperty` 사용 하 여 요소를 [CalculationType](calculationtype-element-assl.md) 의 *멤버* 또는 *셀*합니다.  
  
 부모에 해당 하는 요소가 `SolveOrder` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CalculationProperty>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CalculationProperties 요소 &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
