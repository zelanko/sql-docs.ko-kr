---
title: WillChangeRecordset 및 RecordsetChangeComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ed1c7a9f1ed86359eef75fdaf13c9e40d838f3f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718871"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)
**WillChangeRecordset** 보류 중인 작업을 변경 하기 전에 이벤트 라고 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md). 합니다 **RecordsetChangeComplete** 이벤트 후에 호출 됩니다 합니다 **레코드 집합** 변경 되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값이 될 수 있습니다 **adRsnRequery**를 **adRsnResynch**를 **adRsnClose**를 **adRsnOpen**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillChangeRecordset** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하는 경우. 로 설정 되어 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **RecordsetChangeComplete** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업을 성공적으로 수행 되었으면 **adStatusErrorsOccurred** 경우 작업이 실패 하거나 **adStatusCancel** 작업에 연결 된 이전에 동의한 경우 **WillChangeRecordset** 이벤트가 취소 되었으면 합니다.  
  
 앞 **WillChangeRecordset** 반환 되는 경우이 매개 변수를 설정 **adStatusCancel** 보류 중인 작업의 취소를 요청 또는 후속 방지 하기 위해 adStatusUnwantedEvent로이 매개 변수를 설정 하려면 알림입니다.  
  
 앞 **WillChangeRecordset** 하거나 **RecordsetChangeComplete** 반환 되는 경우이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 *adStatus* 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. 합니다 **레코드 집합** 이 이벤트가 발생 한입니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillChangeRecordset** 또는 **RecordsetChangeComplete** 이벤트 때문에 발생할 수 있습니다 합니다 **레코드 집합** [Requery](../../../ado/reference/ado-api/requery-method.md) 또는[열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드.  
  
 공급자는 책갈피를 지원 하지 않는 경우는 **RecordsetChange** 이벤트 알림이 발생 될 때마다 새 행이 공급자에서 검색 됩니다. 이 이벤트의 빈도에 따라 달라 집니다 합니다 **RecordsetCacheSize** 속성입니다.  
  
 설정 해야 합니다 **adStatus** 매개 변수를 **adStatusUnwantedEvent** 각 가능한 **adReason** 값을 포함 하는 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 **adReason** 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
