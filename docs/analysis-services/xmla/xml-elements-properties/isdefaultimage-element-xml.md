---
title: IsDefaultImage 요소 (XML) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf053ce660091fa9b47048e9dccb9b7f470acaad
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036841"
---
# <a name="isdefaultimage-element-xml"></a>IsDefaultImage 요소(XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  다른 테이블에 대한 이 관계를 탐색하고 IsDefaultImage 특성이 있는 멤버를 인출하여 이 엔터티의 기본 이미지를 가져올 수 있음을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|false|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **RelationshipEndVisualizationProperties** 요소의 경우 **IsDefaultImage** 요소는 이 관계의 다른 끝을 탐색하여 이 엔터티의 기본 이미지를 가져올 수 있음을 나타냅니다. 기본값인 **false** 는 가져올 기본 이미지가 없음을 나타냅니다.  
  
  
