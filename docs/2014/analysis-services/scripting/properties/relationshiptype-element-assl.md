---
title: RelationshipType 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RelationshipType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cc0ca0577b63e655c42c9b8bdcb19b1a67cb538
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096713"
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 요소(ASSL)
  나타냅니다 여부에 대 한 멤버 관계를 [AttributeRelationship](../objects/attributerelationship-element-assl.md) 변경할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*유연한*|  
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
|*고정*|특성 및 관련 특성 사이의 멤버 관계를 변경할 수 없습니다.|  
|*유연한*|특성 및 관련 특성 사이의 멤버 관계를 변경할 수 있습니다.|  
  
 예를 들어 경우 `ZipCode` 간에 변경할 수 없습니다 `City` 간에 관계를 `ZipCode` 하 `City` 으로 표시 됩니다 *고정*합니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `RelationshipType`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.RelationshipType>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
