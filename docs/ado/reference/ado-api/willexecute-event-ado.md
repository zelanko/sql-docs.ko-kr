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
ms.openlocfilehash: e0e7c29be102e9c5c7709816895a6647c95337c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936610"
---
# <a name="willexecute-event-ado"></a>WillExecute 이벤트(ADO)
**WillExecute** 이벤트는 연결에서 보류 중인 명령이 실행 되기 직전에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 SQL 명령이 나 저장 프로시저 이름이 포함 된 **문자열** 입니다.  
  
 *CursorType*  
 열 **레코드 집합** 에 대 한 커서 유형을 포함 하는 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 입니다. 이 매개 변수를 사용 하 여 **레코드 집합**[OPEN 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 작업 중에 커서를 모든 형식으로 변경할 수 있습니다. *CursorType* 는 다른 작업에 대해 무시 됩니다.  
  
 *LockType*  
 열 **레코드 집합** 의 잠금 유형을 포함 하는 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 입니다. 이 매개 변수를 사용 하면 **RecordsetOpen** 작업을 수행 하는 동안 잠금을 모든 형식으로 변경할 수 있습니다. 다른 작업의 경우에는 *LockType* 가 무시 됩니다.  
  
 *옵션*  
 명령을 실행 하거나 **레코드 집합**을 여는 데 사용할 수 있는 옵션을 나타내는 **Long** 값입니다.  
  
 *adStatus*  
 이 이벤트가 호출 될 때 **adStatusCantDeny** 또는 **adstatusok** 일 수 있는 [eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. **AdStatusCantDeny**인 경우이 이벤트는 보류 중인 작업의 취소를 요청 하지 않을 수 있습니다.  
  
 *pCommand*  
 이 이벤트 알림이 적용 되는 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
 *pRecordset*  
 이 이벤트 알림이 적용 되는 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
 *pConnection*  
 이 이벤트 알림이 적용 되는 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 **WillExecute** 이벤트는 연결로 인해 발생할 수 있습니다.  [Execute 메서드 (Ado 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [EXECUTE 메서드 (ado 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)또는 [Open 메서드 (Ado 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드 *pconnection* 매개 변수는 항상 **연결** 개체에 대 한 유효한 참조를 포함 해야 합니다. 이벤트가 **Execute**로 인해 발생 한 경우 *Precordset* 및 *Precordset* 매개 변수는 **Nothing**으로 설정 됩니다. 이 이벤트가 **레코드 집합**으로 인 한 것 이면 *precordset* 매개 변수는 **레코드 집합** 개체를 참조 하 고 *precordset* 매개 변수는 **Nothing**으로 설정 됩니다. **명령이 Execute**로 인해 발생 한 경우 *pcommand* 매개 변수는 **command** 개체를 참조 하 고 *pcommand* 매개 변수는 **Nothing**으로 설정 됩니다.  
  
 **WillExecute** 를 사용 하면 보류 중인 실행 매개 변수를 검사 하 고 수정할 수 있습니다. 이 이벤트는 보류 중인 명령이 취소 된 요청을 반환할 수 있습니다.  
  
> [!NOTE]
>  **명령의** 원본 원본이 [commandstream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성으로 지정 된 스트림이 면 새 문자열을 **WillExecute**_source_ 매개 변수에 할당 하면 **명령의**원본이 변경 됩니다. **Commandstream** 속성이 지워지고 [COMMANDTEXT 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성이 새 원본으로 업데이트 됩니다. **Commandstream** 에 의해 지정 된 원래 스트림은 해제 되 고 액세스할 수 없습니다.  
  
 새 원본 문자열의 언어가 [언어 속성](../../../ado/reference/ado-api/dialect-property.md) 속성의 원래 설정과 다른 경우 ( **commandstream**으로 속하는지를) *pcommand*에서 참조 하는 command 개체의 **언어** 속성을 설정 하 여 올바른 언어를 지정 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
