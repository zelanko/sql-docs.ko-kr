---
title: Cardinality 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cardinality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Cardinality element
ms.assetid: 60ac8a26-7c8b-4011-9b9b-a29863779428
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c75017321a0f00a3e88a74d12336768f1bfc78b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197843"
---
# <a name="cardinality-element-assl"></a>Cardinality 요소(ASSL)
  설명 되는 관계의 카디널리티를 나타냅니다는 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 하거나 [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship> <!-- or RegularMeasureGroupDimension -->  
   ...  
   <Cardinality>...</Cardinality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*많은*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeRelationship](../objects/attributerelationship-element-assl.md), [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*많은*|다 대 일 관계|  
|*하나*|일 대 일 관계|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Cardinality`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.Cardinality>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
