---
title: Source 요소 (측정값) (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5995a841eeba92718d065c75930d0e8bee3bf60a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-measure-assl"></a>Source 요소(측정값)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  값을 포함 하는 원본에 대 한 정보가 포함 된 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **소스** 의 **DataItem**로 제공 되는 **소스** 의 **측정값**, 차례로 유형일 수 [RowBinding ](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), 또는 [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)합니다.  
  
 에 대 한 자세한 내용은 **DataItem** ASSL 개체 및 속성의 표를 포함 하 여는 **DataItem** 입력을 참조 하십시오. [DataItem 데이터 형식 &#40;ASSL&#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 하는 요소 **소스** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Measure>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
