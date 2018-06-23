---
title: SourceMeasureGroup 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SourceMeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SourceMeasureGroup
helpviewer_keywords:
- SourceMeasureGroup element
ms.assetid: aaa7cc0b-162a-4c31-ab03-a90f81eeca00
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9eab12a6f29d73d242c8987f7719092e9974e164
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093620"
---
# <a name="sourcemeasuregroup-element-assl"></a>SourceMeasureGroup 요소(ASSL)
  마이닝 구조 열의 데이터 원본으로 사용되는 측정값 그룹을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <SourceMeasureGroup xsi:type="MeasureGroupBinding">...</SourceMeasureGroup>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 유형의 [MiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 `Binding` 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 `Binding` 유형과의 상속 계층 구조 `Binding` 형식 참조 [바인딩 데이터 형식 &#40;ASSL &#41;](../data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 부모에 해당 하는 요소 `SourceMeasureGroup` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructureColumn> 및 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  