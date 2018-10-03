---
title: TableNotifications 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableNotifications Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotifications element
ms.assetid: 4cecdfea-0d4d-4bd6-bbb3-4d0d2284c665
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4c48ef76db4a1dd2a96008c108d050ff832fd52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188833"
---
# <a name="tablenotifications-element-assl"></a>TableNotifications 요소(ASSL)
  컬렉션을 포함 [TableNotification](../objects/tablenotification-element-assl.md) 에 대 한 정보를 제공 하는 요소는 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블이 나 수정 된 데이터 원본 뷰에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
...</TableNotifications>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCachingTablesBinding](../data-type/binding-data-type-assl.md)|  
|자식 요소|[TableNotification](../objects/tablenotification-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TableNotificationCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding 데이터 형식 &#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
