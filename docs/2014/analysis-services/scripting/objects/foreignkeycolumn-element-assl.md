---
title: ForeignKeyColumn 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ForeignKeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeignKeyColumn
helpviewer_keywords:
- ForeignKeyColumn element
ms.assetid: 6c00dcc6-8d5b-4293-8b72-c7a22e298c8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4688ac6efd03e10b5950abcbcc0da99a1cbc5b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149793"
---
# <a name="foreignkeycolumn-element-assl"></a>ForeignKeyColumn 요소(ASSL)
  관계형 데이터 원본에 대한 부모 테이블로의 조인을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ForeignKeyColumns>  
   <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
</ForeignKeyColumns>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ForeignKeyColumns](../collections/columns-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 추가 정보에 대 한는 `DataItem` 형식, Analysis Services Scripting Language (ASSL) 개체의 속성을 테이블을 포함 하는 `DataItem` 입력을 참조 하십시오 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 AMO(Analysis Management Object) 개체 모델에서 `ForeignKeyColumns` 컬렉션의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [TableMiningStructureColumn 데이터 형식 &#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructureColumn 데이터 형식 &#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 요소 &#40;ASSL&#41;](miningstructure-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
