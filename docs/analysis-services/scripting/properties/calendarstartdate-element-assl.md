---
title: CalendarStartDate 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d51ede3b67f2eb96fd25ce54c8f230d72fc8e7dc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="calendarstartdate-element-assl"></a>CalendarStartDate 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  정의 대 한 달력 기간의 시작 날짜는 [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   ...  
   <CalendarStartDate>...</CalendarStartDate>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|과 같이 지원되는|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **CalendarEndDate** 보다 이후 여야 합니다는 **CalendarStartDate**합니다.  
  
 부모에 해당 하는 요소 **CalendarStartDate** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TimeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
