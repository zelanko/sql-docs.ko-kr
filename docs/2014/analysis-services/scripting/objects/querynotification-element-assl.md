---
title: QueryNotification 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eddd5a96c5c5ab541ba9349d7b664b110589a74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177739"
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
|데이터 형식 및 길이|없음|  
|기본값|없음|  
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
  
  
