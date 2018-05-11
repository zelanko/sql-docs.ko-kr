---
title: ColumnID 요소 (EventColumn) (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dcbc88925b788c90f965e0b3b526979047f96b38
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 요소(EventColumn)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  일부로 이벤트에 대해 캡처할 정보 열의 식별자 (ID)를 포함 한 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **ColumnID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TraceColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Columns 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Event 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Events 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
