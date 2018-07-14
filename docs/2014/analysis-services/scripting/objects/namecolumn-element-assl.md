---
title: NameColumn 요소 (ASSL) | Microsoft Docs
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
- NameColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NameColumn
helpviewer_keywords:
- NameColumn element
ms.assetid: 9ff79f2e-26d7-4ab9-a166-14c2c2d1fc07
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b2a0ae2308c14caaf46edaed876a31e04b82e46
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213943"
---
# <a name="namecolumn-element-assl"></a>NameColumn 요소(ASSL)
  부모 요소의 이름을 제공하는 열을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <NameColumn xsi:type="DataItem">...</NameColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|기본값|  
|------------------------|-------------------|  
|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|Varies(주의 참조)|  
|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|InclusionThresholdSetting|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 경우는 [KeyColumns](../collections/columns-element-assl.md) 컬렉션인 `DimensionAttribute` 하나를 포함 [KeyColumn](column-element-assl.md) 같은 문자열 데이터 형식의 키 열을 나타내는 요소 `DataItem` 값이 기본값으로 사용 됩니다 `NameColumn` 요소입니다.  
  
 에 대 한 자세한 내용은 합니다 `DataItem` 형식, Analysis Services Scripting Language (ASSL) 개체의 속성을 테이블을 포함 하는 `DataItem` 입력을 참조 하십시오 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 하는 요소가 `NameColumn` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.DimensionAttribute> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
