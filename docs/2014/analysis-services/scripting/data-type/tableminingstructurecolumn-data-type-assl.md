---
title: TableMiningStructureColumn 데이터 형식 (ASSL) | Microsoft Docs
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
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e03fec81f796ccf87f19df9b2e43fe29b0e318e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319403"
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
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[열](../collections/columns-element-assl.md)하십시오 [ForeignKeyColumn](../objects/column-element-assl.md)합니다 [SourceMeasureGroup](../objects/group-element-assl.md), [번역](../collections/translations-element-assl.md)|  
|파생 요소|[열](../objects/column-element-assl.md) ([열](../collections/columns-element-assl.md) 모음인 [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
