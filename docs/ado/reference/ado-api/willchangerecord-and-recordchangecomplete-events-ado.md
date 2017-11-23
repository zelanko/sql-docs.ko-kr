---
title: "WillChangeRecord 및 RecordChangeComplete 이벤트 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a421ba630b9cb9eeafaa2087144b765a64f78b9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 및 RecordChangeComplete 이벤트 (ADO)
**WillChangeRecord** 이벤트 하나 이상의 레코드 (행) 전에 호출 됩니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 변경 합니다. **RecordChangeComplete** 하나 후 이벤트를 호출 하거나 더 많은 레코드를 변경 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값으로 가능 **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, 또는 **adRsnFirstChange**합니다.  
  
 *cRecords*  
 A **긴** (영향을 받음) 변경 레코드의 수를 나타내는 값입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 은 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeRecord** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **RecordChangeComplete** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 또는 **adStatusErrorsOccurred** 경우 작업에 실패 했습니다.  
  
 하기 전에 **WillChangeRecord** 반환 되 면이 매개 변수를 설정 **adStatusCancel** 이 이벤트를 발생 시킨 또는이 매개 변수를 설정 하는 작업의 취소 요청에  **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 하기 전에 **RecordChangeComplete** 반환 되 면이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. **레코드 집합** 이 이벤트가 발생 하는 것에 대 한 합니다.  
  
## <a name="remarks"></a>주의  
 A **WillChangeRecord** 또는 **RecordChangeComplete** 다음으로 인해 행의 변경된 된 첫 번째 필드에 대 한 이벤트가 발생할 수 있습니다 **레코드 집합** 작업: [ 업데이트](../../../ado/reference/ado-api/update-method.md), [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 및 [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)합니다. 값은 **레코드 집합** [모두](../../../ado/reference/ado-api/cursortype-property-ado.md) 발생할 이벤트를 발생 하는 작업을 결정 합니다.  
  
 중에서 **WillChangeRecord** 이벤트에는 **레코드 집합** [필터](../../../ado/reference/ado-api/filter-property.md) 속성이로 설정 되어 **adFilterAffectedRecords**합니다. 이벤트를 처리 하는 동안이 속성을 변경할 수 없습니다.  
  
 설정 해야 합니다는 **adStatus** 매개 변수를 **adStatusUnwantedEvent** 각각의 가능한에 대 한 **adReason** 값 완전히 포함 된 모든 이벤트에 대 한 이벤트 알림을 중지 하려면 **adReason** 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
