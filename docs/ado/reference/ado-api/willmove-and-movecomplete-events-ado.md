---
description: WillMove 및 MoveComplete 이벤트(ADO)
title: WillMove 및 MoveComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 27d86dc84960399be6b5738f72c69430c6834c7e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987764"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 및 MoveComplete 이벤트(ADO)
**WillMove** 이벤트는 보류 중인 작업이 [레코드 집합](./recordset-object-ado.md)의 현재 위치를 변경 하기 전에 호출 됩니다. **MoveComplete** 이벤트는 **레코드 집합** 의 현재 위치가 변경 된 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *adReason*  
 이 이벤트의 이유를 지정 하는 [EventReasonEnum](./eventreasonenum.md) 값입니다. 해당 값은 **Adrsnmovefirst**, **adrsnmovefirst**, **adrsnmovefirst**, **AdRsnMovePrevious**, **adrsnmovefirst**또는 **adrsnmovefirst**일 수 있습니다.  
  
 *pError*  
 [오류](./error-object.md) 개체입니다. *Adstatus* 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 매개 변수가 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md) 상태 값입니다.  
  
 **WillMove** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 됩니다. 이 이벤트는 보류 중인 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 **MoveComplete** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 **WillMove** 가 반환 되기 전에이 매개 변수를 **adstatuscancel** 로 설정 하 여 보류 중인 작업의 취소를 요청 하거나,이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 **MoveComplete** 가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pRecordset*  
 [레코드 집합](./recordset-object-ado.md) 개체입니다. 이 이벤트가 발생 한 **레코드 집합** 입니다.  
  
## <a name="remarks"></a>설명  
 **WillMove** 또는 **MoveComplete** 이벤트는 [Open](./open-method-ado-recordset.md), [Move](./move-method-ado.md), [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](./addnew-method-ado.md)및 [Requery](./requery-method.md)와 같은 **레코드 집합** 작업으로 인해 발생할 수 있습니다. 이러한 이벤트는 [Filter](./filter-property.md), [Index](./index-property.md), [Bookmark](./bookmark-property-ado.md), [AbsolutePage](./absolutepage-property-ado.md)및 [AbsolutePosition](./absoluteposition-property-ado.md)속성으로 인해 발생할 수 있습니다. 이러한 이벤트는 자식 **레코드** 집합에 연결 된 **레코드** 집합 이벤트가 있고 부모 **레코드 집합** 을 이동 하는 경우에도 발생 합니다.  
  
 *AdReason* 매개 변수를 포함 하는 모든 이벤트에 대 한 이벤트 알림을 완전히 중지 하려면 각 가능한 *adReason* 값에 대해 *Adstatus* 매개 변수를 **adStatusUnwantedEvent** 로 설정 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../guide/data/ado-event-handler-summary.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)