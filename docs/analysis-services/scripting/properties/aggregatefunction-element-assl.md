---
title: AggregateFunction 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09ac3bb4798538fad0d91a40b385887dd3285060
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  사용 하는 집계 함수의 유형을 정의 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*합계*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*합계*|측정값이 **Sum** 함수를 사용하여 집계됩니다.|  
|*개수*|측정값이 **Count** 함수를 사용하여 집계됩니다.|  
|*Min*|측정값이 **Min** 함수를 사용하여 집계됩니다.|  
|*Max*|측정값이 **Max** 함수를 사용하여 집계됩니다.|  
|*DistinctCount*|측정값이 **DistinctCount** 함수를 사용하여 집계됩니다.|  
|*없음*|측정값이 집계되지 않습니다.|  
|*ByAccount*|측정값이 계정별로 집계됩니다.|  
|*AverageOfChildren*|측정값은 자식의 평균을 반환하여 집계됩니다.|  
|*FirstChild*|측정값이 해당 첫 번째 자식 멤버를 반환하여 집계됩니다.|  
|*LastChild*|측정값이 해당 마지막 자식 멤버를 반환하여 집계됩니다.|  
|*FirstNonEmpty*|측정값이 비어 있지 않은 해당 첫 번째 멤버를 반환하여 집계됩니다.|  
|*LastNonEmpty*|측정값이 비어 있지 않은 해당 마지막 멤버를 반환하여 집계됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **AggregateFunction** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AggregationFunction>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
