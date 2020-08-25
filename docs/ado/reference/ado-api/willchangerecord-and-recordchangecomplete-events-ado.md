---
description: WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)
title: WillChangeRecord 및 RecordChangeComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f69b16392204722e4efd3dc91602a920316919d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776882"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)
**WillChangeRecord** 이벤트는 [레코드 집합](./recordset-object-ado.md) 의 하나 이상의 레코드 (행)가 변경 되기 전에 호출 됩니다. **RecordChangeComplete** 이벤트는 하나 이상의 레코드가 변경 된 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 이 이벤트의 이유를 지정 하는 [EventReasonEnum](./eventreasonenum.md) 값입니다. 해당 값은 **Adrsnaddnew**, **adrsnaddnew**, **adrsnaddnew**, adRsnUndoUpdate, **adrsnaddnew**, **adRsnUndoUpdate** **adrsnaddnew 삭제**하거나 **adrsnfirstchange**일 수 있습니다.  
  
 *cRecords*  
 변경 된 레코드 수 (영향을 받음)를 나타내는 **Long** 값입니다.  
  
 *pError*  
 [오류](./error-object.md) 개체입니다. *Adstatus* 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md) 상태 값입니다.  
  
 **WillChangeRecord** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 됩니다. 이 이벤트는 보류 중인 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 **RecordChangeComplete** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 **WillChangeRecord** 가 반환 되기 전에이 매개 변수를 **adstatuscancel** 로 설정 하 여이 이벤트를 발생 시킨 작업의 취소를 요청 하거나 이후 알림을 방지 하기 위해이 매개 변수를 **adStatusUnwantedEvent** 로 설정 합니다.  
  
 **RecordChangeComplete** 가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pRecordset*  
 **레코드 집합** 개체입니다. 이 이벤트가 발생 한 **레코드 집합** 입니다.  
  
## <a name="remarks"></a>설명  
 [업데이트](./update-method.md), [삭제](./delete-method-ado-recordset.md), [CancelUpdate](./cancelupdate-method-ado.md), [AddNew](./addnew-method-ado.md), [UpdateBatch](./updatebatch-method.md)및 [CancelBatch](./cancelbatch-method-ado.md) **레코드 집합** 작업으로 인해 행의 첫 번째 변경 된 필드에 대해 **WillChangeRecord** 또는 **RecordChangeComplete** 이벤트가 발생할 수 있습니다. **레코드 집합** [CursorType](./cursortype-property-ado.md) 의 값은 이벤트를 발생 시키는 작업을 결정 합니다.  
  
 **WillChangeRecord** 이벤트 중에는 **레코드 집합** [필터](./filter-property.md) 속성이 **adFilterAffectedRecords**로 설정 됩니다. 이벤트를 처리 하는 동안에는이 속성을 변경할 수 없습니다.  
  
 **AdReason** 매개 변수를 포함 하는 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 하려면 각 가능한 **adReason** 값에 대해 **Adstatus** 매개 변수를 **adStatusUnwantedEvent** 로 설정 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../guide/data/ado-event-handler-summary.md)