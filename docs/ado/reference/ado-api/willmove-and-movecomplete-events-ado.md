---
title: WillMove 및 MoveComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88a04ff636f06589515f409b7c2274217ae8f3f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710016"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 및 MoveComplete 이벤트(ADO)
**WillMove** 보류 중인 작업을 현재 위치를 변경 하기 전에 이벤트 라고 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md). **MoveComplete** 이벤트 후의 현재 위치 라고 합니다 **레코드 집합** 변경.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) 이 이벤트에 대 한 이유를 지정 하는 값입니다. 해당 값이 될 수 있습니다 **adRsnMoveFirst**를 **adRsnMoveLast**를 **adRsnMoveNext**를 **adRsnMovePrevious**, **adRsnMove** , 또는 **adRsnRequery**합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 됩니다 **adStatusErrorsOccurred**; 매개 변수는 설정 되지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **WillMove** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하는 경우. 로 설정 되어 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 때 **MoveComplete** 가 호출이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업 성공 하거나 **adStatusErrorsOccurred** 경우는 작업이 실패 했습니다.  
  
 앞 **WillMove** 반환 되는 경우이 매개 변수를 설정 **adStatusCancel** 보류 중인 작업의 취소를 요청 하거나이 매개 변수를 설정 하려면 **adStatusUnwantedEvent** 후속 알림을 방지 하기 위해  
  
 앞 **MoveComplete** 반환 되는 경우이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pRecordset*  
 A [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 합니다 **레코드 집합** 이 이벤트가 발생 한입니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillMove** 하거나 **MoveComplete** 이벤트는 다음으로 인해 발생할 수 있습니다 **레코드 집합** 작업: [오픈](../../../ado/reference/ado-api/open-method-ado-recordset.md), [이동](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)를 [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)를 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)를 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), 및 [Requery](../../../ado/reference/ado-api/requery-method.md)합니다. 이러한 이벤트는 다음 속성으로 인해 발생할 수 있습니다. [필터](../../../ado/reference/ado-api/filter-property.md), [인덱스](../../../ado/reference/ado-api/index-property.md)합니다 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md)를 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), 및 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)합니다. 이러한 이벤트는 경우 자식에도 발생할 **레코드 집합** 가 **레코드 집합** 연결 된 이벤트 및 부모 **레코드 집합** 이동 됩니다.  
  
 설정 해야 합니다 *adStatus* 매개 변수를 **adStatusUnwantedEvent** 각 가능한 *adReason* 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 하려면 값은 포함 된 *adReason* 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
