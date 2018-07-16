---
title: ValueColumn 요소 (ASSL) | Microsoft Docs
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
- ValueColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7279cb1f8f9bc5a7dc8c9e564081a227edc32f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231903"
---
# <a name="valuecolumn-element-assl"></a>ValueColumn 요소(ASSL)
  부모 요소의 값을 제공하는 열을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|기본값|Varies(주의 참조)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 경우는 [NameColumn](namecolumn-element-assl.md) 요소의 `DimensionAttribute` 지정 된 경우 동일 `DataItem` 값이 기본값으로 사용 됩니다는 `ValueColumn` 요소입니다. 경우는 `NameColumn` 요소의 `DimensionAttribute` 지정 하지 않으면 및 [KeyColumns](../collections/keycolumns-element-assl.md) 컬렉션 `DimensionAttribute` 하나를 포함 [KeyColumn](keycolumn-element-assl.md) 문자열을 사용 하 여 키 열을 나타내는 요소 동일한 데이터 형식 `DataItem` 값에 대 한 기본 값으로 사용 되는 `ValueColumn` 요소입니다.  
  
 에 대 한 자세한 내용은 합니다 `DataItem` 형식, Analysis Services Scripting Language (ASSL) 개체의 속성을 테이블을 포함 하는 `DataItem` 입력을 참조 하십시오 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 하는 요소가 `NameColumn` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.DimensionAttribute> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
