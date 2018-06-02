---
title: CommonIdentifierPosition 요소 (XML) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc4a30e8c2886c97157e121fb3f70f892457e1ca
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574105"
---
# <a name="commonidentifierposition-element-xml"></a>CommonIdentifierPosition 요소(XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|부모 요소|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **RelationshipEndVisualizationProperties** 요소의 경우 **CommonIdentifierPosition** 요소는 세부 정보 컬렉션의 공통 식별자 요소 위치를 포함합니다. 기본값인 **false** 는 사용할 공통 식별자가 없음을 나타냅니다.  
  
  
