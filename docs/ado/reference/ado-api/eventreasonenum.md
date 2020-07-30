---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 94b36cbab5ffe7c22f4d1941e61af8fabc8b9973
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242733"
---
# <a name="eventreasonenum"></a>EventReasonEnum
이벤트를 발생 시킨 이유를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|작업에서 새 레코드를 추가 했습니다.|  
|**adRsnClose**|9|작업에서 **레코드 집합**을 닫았습니다.|  
|**adRsnDelete**|2|작업에서 레코드를 삭제 했습니다.|  
|**adRsnFirstChange**|11|레코드에 대 한 첫 번째 변경을 수행 하는 작업입니다.|  
|**adRsnMove**|10|작업이 레코드 **집합**내에서 레코드 포인터를 이동 했습니다.|  
|**adRsnMoveFirst**|12|작업에서 레코드 포인터를 레코드 **집합**의 첫 번째 레코드로 이동 했습니다.|  
|**adRsnMoveLast**|15|작업에서 레코드 포인터를 레코드 **집합**의 마지막 레코드로 이동 했습니다.|  
|**adRsnMoveNext**|13|작업에서 레코드 포인터를 레코드 **집합**의 다음 레코드로 이동 했습니다.|  
|**adRsnMovePrevious**|14|작업에서 레코드 포인터를 레코드 **집합**의 이전 레코드로 이동 했습니다.|  
|**adRsnRequery**|7|작업에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 쿼리하면|  
|**adRsnResynch**|8|작업은 데이터베이스와 함께 **레코드 집합** 을 다시 동기화 합니다.|  
|**Adrsn를 위한 Addnew**|5|새 레코드를 추가 하는 작업을 취소 한 작업입니다.|  
|**Adrsn제거**|6|레코드 삭제를 취소 한 작업입니다.|  
|**adRsnUndoUpdate**|4|레코드 업데이트를 취소 한 작업입니다.|  
|**adRsnUpdate**|3|작업에서 기존 레코드를 업데이트 했습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums 이유. 닫기|  
|AdoEnums 이유. 삭제|  
|AdoEnums 이유. FIRSTCHANGE|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. MOVELAST|  
|AdoEnums|  
|AdoEnums. MOVEPREVIOUS|  
|AdoEnums|  
|AdoEnums. RESYNCH|  
|AdoEnums.|  
|AdoEnums 삭제|  
|AdoEnums. UNDOUPDATE|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  

        [WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillMove 및 MoveComplete 이벤트(ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
