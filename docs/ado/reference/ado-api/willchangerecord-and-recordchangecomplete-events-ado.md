---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd31a75a45bd38bda04655bbb47daca09714803c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642897"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)
합니다 **WillChangeRecord** 이벤트에서 하나 이상의 레코드 (행) 하기 전에 호출 되는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 변경 합니다. 합니다 **RecordChangeComplete** 후 이벤트를 호출 하거나 더 많은 레코드를 변경 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값이 될 수 있습니다 **adRsnAddNew**를 **adRsnDelete**를 **adRsnUpdate**를 **adRsnUndoUpdate**, **adRsnUndoAddNew**하십시오 **adRsnUndoDelete**, 또는 **adRsnFirstChange**합니다.  
  
 *cRecords*  
 A **긴** (영향을 받음) 변경 레코드의 수를 나타내는 값입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 *adStatus* 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeRecord** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하는 경우. 로 설정 되어 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **RecordChangeComplete** 가 호출 하 고,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업 성공 하거나 **adStatusErrorsOccurred** 경우 작업에 실패 했습니다.  
  
 앞 **WillChangeRecord** 반환 되는 경우이 매개 변수를 설정 **adStatusCancel** 이 이벤트를 발생 시킨 또는이 매개 변수를 설정 하는 작업의 취소 요청에  **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 앞 **RecordChangeComplete** 반환 되는 경우이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. 합니다 **레코드 집합** 이 이벤트가 발생 한입니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillChangeRecord** 하거나 **RecordChangeComplete** 다음으로 인해 행의 변경된 된 첫 번째 필드에 대 한 이벤트가 발생할 수 있습니다 **Recordset** 작업: [업데이트](../../../ado/reference/ado-api/update-method.md), [삭제할](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)를 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)를 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 및 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). 값을 **레코드 집합** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) 작업 발생할 이벤트를 결정 합니다.  
  
 중 합니다 **WillChangeRecord** 이벤트를 **레코드 집합** [필터](../../../ado/reference/ado-api/filter-property.md) 속성이로 설정 되어 **adFilterAffectedRecords**합니다. 이벤트를 처리 하는 동안이 속성을 변경할 수 없습니다.  
  
 설정 해야 합니다 **adStatus** 매개 변수를 **adStatusUnwantedEvent** 각 가능한 **adReason** 값을 포함 하는 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 **adReason** 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
