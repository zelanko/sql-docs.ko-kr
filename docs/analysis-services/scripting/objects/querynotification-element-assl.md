---
title: "QueryNotification 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- QueryNotification Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- QueryNotification element
ms.assetid: 0ee06730-81ff-4913-96e6-f39b6f181650
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 610b18f6c9c02f2ce6cfa8dd33d9eaca53abecd3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="querynotification-element-assl"></a>QueryNotification 요소(ASSL)
  데이터 원본이 수정되었는지 여부를 확인하기 위해 실행할 쿼리에 대한 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소의 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<QueryNotifications>  
   <QueryNotification>  
      <Query>...</Query>  
...</QueryNotification>  
</QueryNotifications>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[QueryNotifications](../../../analysis-services/scripting/collections/querynotifications-element-assl.md)|  
|자식 요소|[쿼리](../../../analysis-services/scripting/properties/query-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.QueryNotification>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ProactiveCachingQueryBinding 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
