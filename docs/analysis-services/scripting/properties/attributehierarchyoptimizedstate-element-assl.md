---
title: "AttributeHierarchyOptimizedState 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: AttributeHierarchyOptimizedState Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeHierarchyOptimizedState
helpviewer_keywords: AttributeHierarchyOptimizedState element
ms.assetid: d87148c8-2011-45ae-94c3-851f48babc5f
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0277cb002eee99f738bfcdb0b54570fa10a3daea
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="attributehierarchyoptimizedstate-element-assl"></a>AttributeHierarchyOptimizedState 요소(ASSL)
  특성 계층에 적용되는 최적화 수준을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute -->  
   ...  
   <AttributeHierarchyOptimizedState>...  
   </AttributeHierarchyOptimizedState>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*FullyOptimized*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*FullyOptimized*|인스턴스에서 특성 계층에 대한 인덱스를 작성하여 쿼리 성능을 향상시킵니다.|  
|*NotOptimized*|인스턴스에서 추가 인덱스를 작성하지 않습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거 **AttributeHierarchyOptimizedState** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.OptimizationType>합니다. 부모에 해당 하는 요소 **AttributeHierarchyOptimizedState** AMO 개체 모델에는 <xref:Microsoft.AnalysisServices.CubeAttribute> 및 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
