---
title: TableNotification 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotification element
ms.assetid: 3afd075a-74f9-428c-b527-ee497cbe71e7
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e952acc38173462440ec94c050fb27e7a96cce89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321133"
---
# <a name="tablenotification-element-assl"></a>TableNotification 요소(ASSL)
  에 대 한 정보를 포함 합니다 [ProactiveCaching](proactivecaching-element-assl.md) 에서 수정 된 데이터 원본 뷰나 테이블에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableNotifications>  
   <TableNotification>  
      <DbTableName>...</DbTableName>  
      <DbSchemaName>...</DbSchemaName>  
...</TableNotification>  
</TableNotifications>  
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
|부모 요소|[TableNotifications](../collections/tablenotifications-element-assl.md)|  
|자식 요소|[DbSchemaName](../properties/name-element-assl.md), [DbTableName](../properties/dbtablename-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TableNotification>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCachingTablesBinding 데이터 형식 &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding 데이터 형식 &#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
