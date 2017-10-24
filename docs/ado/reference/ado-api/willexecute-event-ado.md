---
title: "WillExecute 이벤트 (ADO) | Microsoft Docs"
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
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63062a2b16cc423c1188aef4302f5b0f8b1e0677
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="willexecute-event-ado"></a>WillExecute 이벤트 (ADO)
**WillExecute** 이벤트는 연결에서 보류 중인 명령이 실행 되기 전에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 A **문자열** SQL 명령 또는 저장된 프로시저 이름이 들어 있는입니다.  
  
 *모두*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 에 대 한 커서의 형식을 포함 하는 **레코드 집합** 는 열립니다. 이 매개 변수를 사용 하는 동안 모든 형식에 커서를 변경할 수는 **레코드 집합**[Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 작업 합니다. *모두* 다른 작업에 대해 무시 됩니다.  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 에 대 한 잠금 유형을 포함 하는 **레코드 집합** 는 열립니다. 이 매개 변수를 사용 하는 동안 모든 형식에 잠금을 변경할 수는 **RecordsetOpen** 작업 합니다. *LockType* 다른 작업에 대해 무시 됩니다.  
  
 *옵션*  
 A **긴** 명령을 실행 하거나 열에 사용할 수 있는 옵션을 나타내는 값의 **레코드 집합**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 일 수 있는 상태 값 **adStatusCantDeny** 또는 **adStatusOK** 이 이벤트를 불러옵니다. 이 경우 **adStatusCantDeny**,이 이벤트는 보류 중인 작업의 취소를 요청 하지 않을 수 있습니다.  
  
 *pCommand*  
 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
 *pRecordset*  
 [Recordset 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
 *pConnection*  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
## <a name="remarks"></a>주의  
 A **WillExecute** 연결 이벤트가 발생할 수 있습니다.  [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [메서드 실행 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md), 또는 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드는 *pConnection* 해야 하는 매개 변수 항상에 대 한 유효한 참조를 포함 한 **연결** 개체입니다. 이벤트로 인해 이면 **Connection.Execute**, *pRecordset* 및 *pCommand* 매개 변수를 설정 **Nothing**합니다. 이벤트로 인해 이면 **Recordset.Open**, *pRecordset* 매개 변수는 참조는 **레코드 집합** 개체 및 *pCommand* 로 설정 된 **Nothing**합니다. 이벤트로 인해 이면 **Command.Execute**, *pCommand* 매개 변수는 참조는 **명령** 개체 및 *pRecordset* 로 설정 된 **Nothing**합니다.  
  
 **WillExecute** 검사 하 고 보류 중인 실행 매개 변수를 수정할 수 있습니다. 이 이벤트는 보류 중인 명령을 취소 요청을 반환할 수 있습니다.  
  
> [!NOTE]
>  원본에 대 한 소스는 **명령** 은으로 지정 된 스트림은 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 새 문자열을 할당는 **WillExecute** *소스* 의 원본을 변경 하는 매개 변수는 **명령**합니다. **CommandStream** 속성이 지워집니다 및 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) 새 원본과 속성이 업데이트 됩니다. 로 지정 된 원래 스트림에 **CommandStream** 출시 될 예정 이므로 액세스할 수 없습니다.  
  
 원래 설정으로 인해 새 소스 문자열의 언어와 다른 경우는 [Dialect 속성](../../../ado/reference/ado-api/dialect-property.md) 속성 (에 상응 하는 **CommandStream**)을 설정 하 여 올바른 언어를 지정 해야 합니다 **언어** 참조 하는 명령 개체의 속성 *pCommand*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

