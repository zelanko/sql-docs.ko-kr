---
title: "WillMove 및 두 이벤트 (ADO) | Microsoft Docs"
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
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5a7fc2b4872a309bb93d249cda407c030f61be90
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 및 두 이벤트 (ADO)
**WillMove** 이벤트는 보류 중인 작업의 현재 위치를 변경 하기 전에 호출 됩니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. **두** 이벤트에서 현재 위치 이후에 호출 됩니다는 **레코드 집합** 변경 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값으로 가능 **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove** , 또는 **adRsnRequery**합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 은 **adStatusErrorsOccurred**; 그렇지 않으면 매개 변수가 설정 되지 됩니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillMove** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **두** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 또는 **adStatusErrorsOccurred** 경우는 작업이 실패 했습니다.  
  
 하기 전에 **WillMove** 반환 되 면이 매개 변수를 설정 **adStatusCancel** 를 보류 중인 작업의 취소를 요청 하거나이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 하지 않으려면입니다.  
  
 하기 전에 **두** 반환 되 면이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pRecordset*  
 A [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. **레코드 집합** 이 이벤트가 발생 하는 것에 대 한 합니다.  
  
## <a name="remarks"></a>주의  
 A **WillMove** 또는 **두** 이벤트는 다음으로 인해 발생할 수 있습니다 **레코드 집합** 작업: [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md), [이동](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), 및 [Requery](../../../ado/reference/ado-api/requery-method.md)합니다. 이러한 이벤트는 다음 속성이 있기 때문에 발생할 수 있습니다: [필터](../../../ado/reference/ado-api/filter-property.md), [인덱스](../../../ado/reference/ado-api/index-property.md), [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), 및 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)합니다. 이러한 이벤트는 자식 경우에 발생할 **레코드 집합** 가 **레코드 집합** 연결 된 이벤트와 부모 **레코드 집합** 이동 됩니다.  
  
 설정 해야 합니다는 *adStatus* 매개 변수를 **adStatusUnwantedEvent** 각각의 가능한에 대 한 *adReason* 완전히 모든 이벤트에 대 한 이벤트 알림을 중지 하려면 값입니다 포함 된 *adReason* 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

