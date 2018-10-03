---
title: TableMiningStructureColumn 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5195118322ff7de4b618dbbe11743639101c625
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082773"
---
# <a name="tableminingstructurecolumn-data-type-assl"></a>TableMiningStructureColumn 데이터 형식(ASSL)
  나타내는 파생된 데이터 형식을 정의 [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) 연결 된 스칼라 값과 달리 중첩된 테이블을 포함 하는 요소는 [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) 요소 스칼라 값을 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <ForeignKeyColumn>..</ForeignKeyColumn>  
   <SourceMeasureGroup>..</SourceMeasureGroup>  
   <Columns>..</Columns>  
   <Translations>..</Translations>  
</TableMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[열](../collections/columns-element-assl.md)하십시오 [ForeignKeyColumn](../objects/column-element-assl.md)합니다 [SourceMeasureGroup](../objects/group-element-assl.md), [번역](../collections/translations-element-assl.md)|  
|파생 요소|[열](../objects/column-element-assl.md) ([열](../collections/columns-element-assl.md) 모음인 [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
