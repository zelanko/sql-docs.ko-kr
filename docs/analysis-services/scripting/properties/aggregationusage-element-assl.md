---
title: AggregationUsage 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8809da56c10ffedb9ff2d8015a3bb0e8d50e90b9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationusage-element-assl"></a>AggregationUsage 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  컨트롤 어떻게에서 집계 디자이너로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 집계를 디자인 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeAttribute>  
   ...  
   <AggregationUsage>...</AggregationUsage>  
   ...  
</CubeAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*Default*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*전체*|큐브의 모든 집계에 이 특성이 포함되어야 합니다.|  
|*없음*|큐브의 집계에 이 특성이 포함되지 않아야 합니다.|  
|*제한 없음*|집계 디자이너에 제한 사항이 지정되지 않습니다.|  
|*Default*|집계 디자이너에서 특성 유형(키의 경우*Full* , 기타의 경우 *Unrestricted* )을 기반으로 기본 규칙을 적용합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **AggregationUsage** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AggregationUsage>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
