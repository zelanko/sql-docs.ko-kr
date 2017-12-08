---
title: "CommonIdentifierPosition 요소 (XML) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: c3b64132-3b2e-46f5-ae11-a3cb3c42099c
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37055c0766a2403c1c4274a166299ca08fdc7616
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|-1|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **RelationshipEndVisualizationProperties** 요소의 경우 **CommonIdentifierPosition** 요소는 세부 정보 컬렉션의 공통 식별자 요소 위치를 포함합니다. 기본값인 **false** 는 사용할 공통 식별자가 없음을 나타냅니다.  
  
  
