---
title: Optionality 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Optionality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Optionality element
ms.assetid: 6cd2ef0a-6fbe-4462-ab27-4cdfeb33f8ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d59b04dad688d438ca2f4777b404dcc4fe8976b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099173"
---
# <a name="optionality-element-assl"></a>Optionality 요소(ASSL)
  에 대 한 멤버의 옵션을 나타냅니다는 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <Optionality>...</OPtionality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*필수*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*필수*|관련 특성의 각 멤버는 `AttributeRelationship` 요소를 소유하는 특성에 있는 하나 이상의 멤버와 연결됩니다.|  
|*선택 사항*|관련 특성의 각 멤버는 `AttributeRelationship` 요소를 소유하는 특성에 있는 멤버와 연결되지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Cardinality`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.Optionality>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
