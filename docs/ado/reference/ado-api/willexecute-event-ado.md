---
title: WillExecute 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 234a0eeba57958063a6f2eedb8510486df8a53a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642514"
---
# <a name="willexecute-event-ado"></a>WillExecute 이벤트(ADO)
합니다 **WillExecute** 이벤트 연결에서 보류 중인 명령이 실행 되기 전에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 A **문자열** SQL 명령 또는 저장된 프로시저 이름을 포함 하는 합니다.  
  
 *CursorType*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 에 대 한 커서의 형식을 포함 하는 합니다 **레코드 집합** 는 열립니다. 이 매개 변수를 사용 하 여 커서 중 임의의 형식으로 변경할 수 있습니다는 **Recordset**[Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 작업 합니다. *CursorType* 다른 작업에 대 한 무시 됩니다.  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 에 대 한 잠금 형식을 포함 하는 합니다 **레코드 집합** 는 열립니다. 이 매개 변수를 사용 하 여 잠금을 중 임의의 형식으로 변경할 수 있습니다는 **RecordsetOpen** 작업 합니다. *LockType* 다른 작업에 대 한 무시 됩니다.  
  
 *Options*  
 A **긴** 명령을 실행 하거나 열을 사용할 수 있는 옵션을 나타내는 값을 **레코드 집합**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 일 수 있는 상태 값 **adStatusCantDeny** 하거나 **adStatusOK** 이 이벤트는 호출 하는 경우. 있으면 **adStatusCantDeny**,이 이벤트는 보류 중인 작업의 취소를 요청 하지 않을 수 있습니다.  
  
 *pCommand*  
 합니다 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
 *pRecordset*  
 합니다 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
 *pConnection*  
 합니다 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 A **WillExecute** 이벤트를 연결으로 인해 발생할 수 있습니다.  [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [Execute 메서드 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md), 또는 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드는 *pConnection* 매개 변수는 항상 올바른 참조를 포함 한 **연결** 개체입니다. 이벤트로 인해 이면 **Connection.Execute**, *pRecordset* 하 고 *pCommand* 매개 변수를 설정 **Nothing**합니다. 이벤트로 인해 이면 **Recordset.Open**의 *pRecordset* 매개 변수는 참조를 **레코드 집합** 개체와 *pCommand* 매개 변수가 **Nothing**합니다. 이벤트로 인해 이면 **Command.Execute**, *pCommand* 매개 변수는 참조를 **명령** 개체와 *pRecordset* 매개 변수가 **Nothing**합니다.  
  
 **WillExecute** 검사 하 고 보류 중인 실행 매개 변수를 수정할 수 있습니다. 이 이벤트는 보류 중인 명령을 취소 요청을 반환할 수 있습니다.  
  
> [!NOTE]
>  원래 원본에 대 한를 **명령** 는 지정 된 스트림에 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 새 문자열을 할당 합니다 **WillExecute** _소스_ 매개 변수 변경의 소스를 **명령**입니다. 합니다 **CommandStream** 속성이 지워집니다 하며 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성은 새 소스를 사용 하 여 업데이트 됩니다. 지정 된 원래 스트림에 **CommandStream** 릴리스될 예정 이며 액세스할 수 없습니다.  
  
 원래 설정에서 새 소스 문자열의 언어와 다른 경우는 [Dialect 속성](../../../ado/reference/ado-api/dialect-property.md) 속성 (에 해당 하는 합니다 **CommandStream**)을 설정 하 여 올바른 언어를 지정 해야 합니다 합니다 **Dialect** 참조 하는 명령 개체의 속성 *pCommand*합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
