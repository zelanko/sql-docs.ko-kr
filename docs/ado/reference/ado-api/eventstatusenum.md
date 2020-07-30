---
title: EventStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: rothja
ms.author: jroth
ms.openlocfilehash: a1174538ec14eab150d5874b7d6b5b51bcd554ff
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242723"
---
# <a name="eventstatusenum"></a>EventStatusEnum
이벤트 실행의 현재 상태를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|이벤트를 발생 시킨 작업의 취소를 요청 합니다.|  
|**adStatusCantDeny**|3|작업에서 보류 중인 작업의 취소를 요청할 수 없음을 나타냅니다.|  
|**adStatusErrorsOccurred**|2|오류 또는 오류로 인해 이벤트를 발생 시킨 작업이 실패 했음을 나타냅니다.|  
|**adStatusOK**|1|이벤트를 발생 시킨 작업이 성공 했음을 나타냅니다.|  
|**adStatusUnwantedEvent**|5|이벤트 메서드의 실행이 완료 되기 전에 후속 알림을 방지 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums 상태입니다. 취소|  
|AdoEnums CANTDENY|  
|AdoEnums ERRORSOCCURRED|  
|AdoEnums 상태입니다.|  
|AdoEnums UNWANTEDEVENT|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [BeginTransComplete, CommitTransComplete 및 RollbackTransComplete Events (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)  

        [ConnectComplete 및 Disconnect 이벤트(ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)  

        [EndOfRecordset 이벤트(ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)  

        [ExecuteComplete 이벤트(ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)  
    :::column-end:::
    :::column:::
        [FetchComplete 이벤트(ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)  

        [InfoMessage 이벤트(ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)  

        [WillChangeField 및 FieldChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)  

        [WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  

        [WillConnect 이벤트(ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)  

        [WillExecute 이벤트(ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  

        [WillMove 및 MoveComplete 이벤트(ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
