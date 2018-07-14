---
title: Source 요소 (측정값) (ASSL) | Microsoft Docs
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
- Source Element (Measure)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4e374490fdfe04e5da39a0f4e9424b2cb1ccde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323213"
---
# <a name="source-element-measure-assl"></a>Source 요소(측정값)(ASSL)
  값이 포함 된 원본에 대 한 정보가 포함 된 [측정값](../objects/measure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값](../objects/measure-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Source` 의 `DataItem`, 역할을 하는 합니다 `Source` 의 `Measure`, 형식이 될 수 있습니다 [RowBinding](../data-type/binding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [MeasureBinding ](../data-type/measurebinding-data-type-assl.md), 또는 [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md)합니다.  
  
 에 대 한 추가 정보에 대 한는 `DataItem` ASSL 개체 및 속성의 테이블을 포함 하 여 형식이 합니다 `DataItem` 입력을 참조 하십시오 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 요소가 `Source` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Measure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
