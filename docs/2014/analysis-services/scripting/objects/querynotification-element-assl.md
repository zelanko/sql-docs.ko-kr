---
title: QueryNotification 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- QueryNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- QueryNotification element
ms.assetid: 0ee06730-81ff-4913-96e6-f39b6f181650
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3c9bc13772d549d6ade640af4c3f57ac52efbbec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182649"
---
# <a name="querynotification-element-assl"></a>QueryNotification 요소(ASSL)
  데이터 원본이 수정되었는지 여부를 확인하기 위해 실행할 쿼리에 대한 [ProactiveCaching](proactivecaching-element-assl.md) 요소의 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<QueryNotifications>  
   <QueryNotification>  
      <Query>...</Query>  
...</QueryNotification>  
</QueryNotifications>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[QueryNotifications](../collections/querynotifications-element-assl.md)|  
|자식 요소|[쿼리](../properties/query-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.QueryNotification>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCachingQueryBinding 데이터 형식 &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  