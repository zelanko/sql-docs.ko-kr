---
title: CommonIdentifierPosition 요소 (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: c3b64132-3b2e-46f5-ae11-a3cb3c42099c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4cb7efbb9f77c3f753149e7069127ea34aa03b6d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090633"
---
# <a name="commonidentifierposition-element-xml"></a>CommonIdentifierPosition 요소(XML)
  요소 컬렉션의 요소 위치에 대한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|-1|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `RelationshipEndVisualizationProperties` 요소의 경우 `CommonIdentifierPosition` 요소는 세부 정보 컬렉션의 공통 식별자 요소 위치를 포함합니다. 기본값인 `false`는 사용할 공통 식별자가 없음을 나타냅니다.  
  
  
