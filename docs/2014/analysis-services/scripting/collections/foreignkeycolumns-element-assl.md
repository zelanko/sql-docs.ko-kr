---
title: ForeignKeyColumns 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ForeignKeyColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeignKeyColumns
helpviewer_keywords:
- ForeignKeyColumns element
ms.assetid: 0a673c1a-73dd-4217-aa41-56b340b5e1ab
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da17077a4a75efc53de65b2168a5332db137bfd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093392"
---
# <a name="foreignkeycolumns-element-assl"></a>ForeignKeyColumns 요소(ASSL)
  관계형 데이터 원본에 대한 부모 테이블로의 조인을 식별하는 열의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <ForeignKeyColumns>  
      <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
...</ForeignKeyColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 유형의 [MiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
|자식 요소|[DataItem](../objects/column-element-assl.md) 유형의 [ForeignKeyColumn](../data-type/dataitem-data-type-assl.md)|  
  
## <a name="see-also"></a>관련 항목  
 [MiningStructure 요소 &#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  