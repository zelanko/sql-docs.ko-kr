---
title: Filter 요소 (바인딩) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Filter Element (Binding)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- filter
helpviewer_keywords:
- Filter element
ms.assetid: 3d4cd169-2903-4266-8541-540ece424b7b
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7235255d7098c582c9a244569fe48375b2639a0c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="filter-element-binding-assl"></a>Filter 요소(Binding)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소의 내용을 필터링하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Filter>...</Filter>  
   ...  
</CubeDimensionBinding>  
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
|부모 요소|[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 대 한 자세한 내용은 **바인딩** 의 테이블을 포함 하 여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 ASSL (Scripting Language) 개체는 **바인딩** 유형과의 상속 계층 구조 **바인딩**  형식 참조 [바인딩 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)합니다.  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 부모에 해당 하는 요소 **필터** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimensionBinding> 및 <xref:Microsoft.AnalysisServices.MeasureGroupBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Binding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
