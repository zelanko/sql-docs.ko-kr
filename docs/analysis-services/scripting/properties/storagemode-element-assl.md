---
title: StorageMode 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f5dbcd8ebf37bb197ccb743a6b78d009ad93e19d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="storagemode-element-assl"></a>StorageMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소의 저장소 모드를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*MOLAP*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md), [요소 치수 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [파티션 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MOLAP*|부모가 MOLAP(다차원 OLAP) 저장소를 사용합니다.|  
|*ROLAP*|부모가 ROLAP(관계형 OLAP) 저장소를 사용합니다.|  
|*HOLAP*|부모가 HOLAP(하이브리드 OLAP) 저장소를 사용합니다.<br /><br /> 참고:이 값에 대해 올바르지 않습니다 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md) 부모 요소입니다.|  
|*InMemory*|부모가 IMBI 저장소를 사용합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **StorageMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.StorageMode>합니다.  
  
 부모에 해당 하는 요소 **StorageMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, 및 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
