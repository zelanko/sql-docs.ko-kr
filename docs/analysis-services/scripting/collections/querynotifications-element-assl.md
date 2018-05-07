---
title: QueryNotifications 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 422bedfa02ca199ab7321342c2d146a34f91f533
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="querynotifications-element-assl"></a>QueryNotifications 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  컬렉션을 포함 [QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md) 정보를 제공 하는 요소는 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 데이터 원본이 수정 되었는지 여부를 확인 하기 위해 실행할 쿼리에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   ...  
   <QueryNotifications>  
      <QueryNotification>...</QueryNotification>  
...</QueryNotifications>  
   ...  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|  
|자식 요소|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.QueryNotificationCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
