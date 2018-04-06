---
title: CalendarLanguage 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CalendarLanguage Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalendarLanguage
helpviewer_keywords:
- CalendarLanguage element
ms.assetid: e43a0f48-a583-418b-a0a4-d73a40035573
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9b9f8888f4d034ae01d92c4f166073336e253490
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="calendarlanguage-element-assl"></a>CalendarLanguage 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 사용 되는 달력 언어를 정의 고 [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   ...  
   <CalendarLanguage>...</CalendarLanguage>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|**1033**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 차원 멤버 이름을 만들 때 사용하는 언어입니다. 캡션 언어는 정수 기반 LCID 코드로 정의되어야 합니다. 예를 들어 기본값은 미국 영어 LCID를 나타냅니다.  
  
 부모에 해당 하는 요소 **CalendarLanguage** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TimeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
