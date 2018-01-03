---
title: "WillChangeRecordset 및 RecordsetChangeComplete 이벤트 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 188bdb13879e4229686fb725edbc190db9ea59b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 및 RecordsetChangeComplete 이벤트 (ADO)
**WillChangeRecordset** 이벤트는 보류 중인 작업을 변경 하기 전에 호출 됩니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. **RecordsetChangeComplete** 이벤트 후에 호출 됩니다는 **레코드 집합** 변경 되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값으로 가능 **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeRecordset** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **RecordsetChangeComplete** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 **adStatusErrorsOccurred** 경우 작업이 실패 하거나 **adStatusCancel** 작업에 연결 된 이전에 동의한 경우 **WillChangeRecordset** 이벤트가 취소 되었으면 합니다.  
  
 하기 전에 **WillChangeRecordset** 반환 되 면이 매개 변수를 설정 **adStatusCancel** 를 보류 중인 작업의 취소를 요청 하거나이 매개 변수를 방지 하기 위해 adStatusUnwantedEvent 후속 설정 알림입니다.  
  
 하기 전에 **WillChangeRecordset** 또는 **RecordsetChangeComplete** 반환 되 면이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 은 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. **레코드 집합** 이 이벤트가 발생 하는 것에 대 한 합니다.  
  
## <a name="remarks"></a>주의  
 A **WillChangeRecordset** 또는 **RecordsetChangeComplete** 이벤트 때문에 발생할 수 있습니다는 **레코드 집합** [Requery](../../../ado/reference/ado-api/requery-method.md) 또는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드.  
  
 공급자 책갈피, 지원 하지 않는 경우는 **RecordsetChange** 이벤트 알림이 공급자에서 새 행이 검색 될 때마다 발생 합니다. 이 이벤트의 빈도에 따라 달라 집니다는 **RecordsetCacheSize** 속성입니다.  
  
 설정 해야 합니다는 **adStatus** 매개 변수를 **adStatusUnwantedEvent** 각각의 가능한에 대 한 **adReason** 값 완전히 포함 된 모든 이벤트에 대 한 이벤트 알림을 중지 하려면 **adReason** 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
