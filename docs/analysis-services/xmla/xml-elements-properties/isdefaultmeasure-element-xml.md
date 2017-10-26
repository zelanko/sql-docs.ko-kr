---
title: "IsDefaultMeasure 요소 (XML) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 523cf3d7-9df0-4f9d-8486-9109de8d3cca
caps.latest.revision: 6
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7ec461cb8fea748a6bd6ad9521082e8c3c66547
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isdefaultmeasure-element-xml"></a>IsDefaultMeasure 요소(XML)
  다른 테이블에 대한 이 관계를 탐색하고 DefaultMeasure 특성이 있는 멤버를 인출하여 이 엔터티의 기본 측정값을 가져올 수 있음을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|false|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **RelationshipEndVisualizationProperties** 요소의 경우 **IsDefaultMeasure** 요소는 이 관계의 다른 끝을 탐색하여 이 엔터티의 기본 측정값을 가져올 수 있음을 나타냅니다. 기본값인 **false** 는 가져올 기본 측정값이 없음을 나타냅니다.  
  
  

