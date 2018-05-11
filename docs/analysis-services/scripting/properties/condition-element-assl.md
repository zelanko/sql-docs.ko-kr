---
title: 조건 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 615da5fb4d7a337bd50d0b2410da0955758bc859
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="condition-element-assl"></a>Condition 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  결정 하는 MDX (Multidimensional Expressions) 식을 포함 여부는 [동작](../../../analysis-services/scripting/objects/action-element-assl.md) 부모 요소는 대상에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Condition>...</Condition  
      ...  
</Action>  
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
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **조건** 요소는 부울 값으로 계산 되는 MDX 식을 포함 합니다. 식에서 반환 하는 경우 **True**, 하면 **동작** 에 지정 된 대상에 적용 됩니다는 [대상](../../../analysis-services/scripting/properties/target-element-assl.md) 요소입니다. 그렇지 않은 경우는 **동작** 적용 되지 않습니다.  
  
 부모에 해당 하는 요소 **조건** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
