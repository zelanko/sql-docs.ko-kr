---
title: EventStatusEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e0b963373521b7d981e192dbbfc94d5fe008bf6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="eventstatusenum"></a>EventStatusEnum
이벤트의 실행의 현재 상태를 지정합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|이벤트를 발생 시킨 작업의 취소를 요청 합니다.|  
|**adStatusCantDeny**|3|작업을 보류 중인 작업의 취소를 요청할 수 없습니다 것을 나타냅니다.|  
|**adStatusErrorsOccurred**|2|이벤트를 발생 시킨 작업 오류로 인해 실패 했음을 나타냅니다.|  
|**adStatusOK**|1.|이벤트를 발생 시킨 작업에 성공 했음을 나타냅니다.|  
|**adStatusUnwantedEvent**|5|이벤트 메서드에서 실행이 끝나면 전에 알림 메시지가 방지 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[BeginTransComplete, CommitTransComplete, 및 RollbackTransComplete 이벤트 (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete 및 Disconnect 이벤트(ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset 이벤트(ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete 이벤트(ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete 이벤트(ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage 이벤트(ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField 및 FieldChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect 이벤트(ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute 이벤트(ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove 및 MoveComplete 이벤트(ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
