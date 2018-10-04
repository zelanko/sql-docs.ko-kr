---
title: OverrideBehavior 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OverrideBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88cf3dd287e1b55fee5377e2238d4d7c738cfe16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203623"
---
# <a name="overridebehavior-element-assl"></a>OverrideBehavior 요소(ASSL)
  설명 되는 관계의 재정의 동작을 나타냅니다는 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*강력한*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `OverrideBehavior` 요소는 관련 특성의 위치 지정이 특성의 위치 지정에 영향을 주는 방식을 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*강력한*|AttributeRelationship 요소로 설명되는 관계의 재정의 동작을 나타냅니다. 한 특성의 위치 지정이 다른 특성의 위치에 영향을 주는 방식을 나타냅니다.|  
|*없음*|아무런 영향이 없습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `OverrideBehavior`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.OverrideBehavior>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
