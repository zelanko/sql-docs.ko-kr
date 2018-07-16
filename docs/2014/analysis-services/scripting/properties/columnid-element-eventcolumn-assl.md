---
title: ColumnID 요소 (EventColumn) (ASSL) | Microsoft Docs
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
- ColumnID Element (EventColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82cc6d67aa0c1533b9779b93468fdf8845272cde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245603"
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 요소(EventColumn)(ASSL)
  이벤트의 일부로 캡처할 정보 열의 식별자 (ID)를 포함 한 [추적](../objects/trace-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[EventColumn](../data-type/eventcolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `ColumnID` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TraceColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Columns 요소 &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Event 요소 &#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Events 요소 &#40;ASSL&#41;](../collections/events-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
