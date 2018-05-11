---
title: 쿼리 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4d56e995f96771128f6395afb614d36121cd785e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="query-element-assl"></a>Query 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  알림을 위해 실행할 쿼리의 텍스트를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<QueryNotification>  
   <Query>...</Query>  
</QueryNotification>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **쿼리** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.QueryNotification>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ProactiveCachingQueryBinding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
