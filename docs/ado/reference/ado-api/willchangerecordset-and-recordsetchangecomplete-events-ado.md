---
description: WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c88cd48a16907e67813f90c06dd9ce69d11ed30
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776892"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)
**WillChangeRecordset** 이벤트는 보류 중인 작업이 [레코드 집합](./recordset-object-ado.md)을 변경 하기 전에 호출 됩니다. **RecordsetChangeComplete** 이벤트는 **레코드 집합이** 변경 된 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 이 이벤트의 이유를 지정 하는 [EventReasonEnum](./eventreasonenum.md) 값입니다. 해당 값은 **Adrsnrequery**, **adRsnResynch**, **adrsnrequery**, **adRsnOpen**일 수 있습니다.  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md) 상태 값입니다.  
  
 **WillChangeRecordset** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 됩니다. 이 이벤트는 보류 중인 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 **RecordsetChangeComplete** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 되 고, 작업이 실패 한 경우 **adStatusErrorsOccurred** 하거나, 이전에 허용 된 **WillChangeRecordset** 이벤트와 연결 된 작업이 취소 된 경우 **adstatusok** 로 설정 됩니다.  
  
 **WillChangeRecordset** 가 반환 되기 전에이 매개 변수를 **adstatuscancel** 로 설정 하 여 보류 중인 작업의 취소를 요청 하거나,이 매개 변수를 adStatusUnwantedEvent로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 **WillChangeRecordset** 또는 **RecordsetChangeComplete** 가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pError*  
 [오류](./error-object.md) 개체입니다. *Adstatus* 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *pRecordset*  
 **레코드 집합** 개체입니다. 이 이벤트가 발생 한 **레코드 집합** 입니다.  
  
## <a name="remarks"></a>설명  
 **WillChangeRecordset** 또는 **RecordsetChangeComplete** 이벤트는 **레코드 집합** [Requery](./requery-method.md) 또는 [Open](./open-method-ado-recordset.md) 메서드로 인해 발생할 수 있습니다.  
  
 공급자가 책갈피를 지원 하지 않는 경우 공급자에서 새 행을 검색할 때마다 **RecordsetChange** 이벤트 알림이 발생 합니다. 이 이벤트의 빈도는 **RecordsetCacheSize** 속성에 따라 달라 집니다.  
  
 **AdReason** 매개 변수를 포함 하는 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 하려면 각 가능한 **adReason** 값에 대해 **Adstatus** 매개 변수를 **adStatusUnwantedEvent** 로 설정 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../guide/data/ado-event-handler-summary.md)