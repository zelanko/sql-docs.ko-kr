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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8883679a85d1e134b1759c90cde524bb97995130
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932865"
---
# <a name="eventstatusenum"></a>EventStatusEnum
이벤트 실행의 현재 상태를 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|이벤트를 발생 시킨 작업의 취소를 요청 합니다.|  
|**adStatusCantDeny**|3|작업에서 보류 중인 작업의 취소를 요청할 수 없음을 나타냅니다.|  
|**adStatusErrorsOccurred**|2|오류 또는 오류로 인해 이벤트를 발생 시킨 작업이 실패 했음을 나타냅니다.|  
|**adStatusOK**|1|이벤트를 발생 시킨 작업이 성공 했음을 나타냅니다.|  
|**adStatusUnwantedEvent**|5|이벤트 메서드의 실행이 완료 되기 전에 후속 알림을 방지 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums 상태입니다. 취소|  
|AdoEnums CANTDENY|  
|AdoEnums ERRORSOCCURRED|  
|AdoEnums 상태입니다.|  
|AdoEnums UNWANTEDEVENT|  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[BeginTransComplete, CommitTransComplete 및 RollbackTransComplete Events (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete 및 Disconnect 이벤트(ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset 이벤트(ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete 이벤트(ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete 이벤트(ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage 이벤트(ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField 및 FieldChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect 이벤트(ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute 이벤트(ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove 및 MoveComplete 이벤트(ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
