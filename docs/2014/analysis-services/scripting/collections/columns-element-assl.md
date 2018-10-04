---
title: Columns 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Columns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- COLUMNS
helpviewer_keywords:
- Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16e8d446b3ffeb4895bde76a739d7ec63a01337d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131513"
---
# <a name="columns-element-assl"></a>Columns 요소(ASSL)
  부모 요소와 연결된 열의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
  
|상위 항목 또는 부모|카디널리티|  
|------------------------|-----------------|  
|[이벤트](../objects/event-element-assl.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|나머지|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md) 형식의 [DrillThroughAction](../data-type/action-data-type-assl.md)를 [이벤트](../objects/event-element-assl.md)를 [MiningModel](../objects/miningmodel-element-assl.md)를 [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md) 또는 [MeasureBinding](../data-type/measurebinding-data-type-assl.md)|  
|[이벤트](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 `DrillThroughAction` 요소는 `Columns` 컬렉션은 동작이 수행 될 때 반환 될 데이터를 포함 하는 열을 식별 합니다.  
  
 에 대 한 `TableMiningStructureColumn` 요소는 `Columns` 컬렉션 재귀 수준이 하나만 허용 합니다. 즉, 모든 `TableMiningStructureColumn` 이 컬렉션에 포함 된 요소를 사용할 수 없습니다 `TableMiningStructureColumn` 요소에 해당 `Columns` 컬렉션입니다.  
  
 AMO(Analysis Management Objects) 개체 모델의 일부 해당 요소는 <xref:Microsoft.AnalysisServices.TraceColumnCollection>, <xref:Microsoft.AnalysisServices.MiningModelColumnCollection> 및 <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
