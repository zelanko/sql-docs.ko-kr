---
title: 상태 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e2baf0425b1ba82830c991fdbe1057d5d4d5b495
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="state-element-assl"></a>State 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소의 현재 처리 상태를 나타내는 읽기 전용 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningModel, MiningStructure, Partition -->  
      ...  
   <State>...</State>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*처리*|요소가 완전히 처리되었습니다.|  
|*PartiallyProcessed*|요소가 부분적으로 처리되었습니다. ([큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 및 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) 만 합니다.)|  
|*처리 되지 않았습니다.*|요소가 처리되지 않았습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **상태** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AnalysisState>합니다.  
  
 부모에 해당 하는 요소 **상태** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, 및 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
