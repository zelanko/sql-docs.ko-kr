---
title: StatusGraphic 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0caf023d5405b6b97b24f733a59624d0d7dea9bd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="statusgraphic-element-assl"></a>StatusGraphic 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소의 상태에 대해 권장되는 그래픽 표현을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpi>  
   ...  
   <StatusGraphic>...</StatusGraphic>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*단일 신호등*|신호등(단일)|  
|*다중 신호등*|신호등(다중)|  
|*도 표지*|도로 표지|  
|*계기-오름차순*|계기|  
|*계기-내림차순*|역방향 계기|  
|*온도계*|온도계|  
|*실린더*|실린더|  
|*웃는 얼굴*|얼굴|  
  
 부모에 해당 하는 요소 **StatusGraphic** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
