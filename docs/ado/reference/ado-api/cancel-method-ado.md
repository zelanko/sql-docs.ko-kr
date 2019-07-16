---
title: Cancel 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db369b32737c0e2dae4603a4a5a6c26cdd3a7142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920234"
---
# <a name="cancel-method-ado"></a>Cancel 메서드(ADO)
보류 중인 비동기 메서드 호출의 실행을 취소 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>설명  
 사용 된 **취소** 비동기 메서드 호출의 실행을 종료 하는 방법:는 메서드를 호출 하는,는 **adAsyncConnect**, **adAsyncExecute**, 또는 **adAsyncFetch** 옵션입니다.  
  
 다음 표에서 사용 하는 경우 종료 되는 작업은 **취소** 메서드는 특정 유형의 개체를 합니다.  
  
|하는 경우 *개체* 되는|이 메서드를 마지막으로 비동기 호출 종료|  
|----------------------|-------------------------------------------------------------|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|[실행](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|[실행할](../../../ado/reference/ado-api/execute-method-ado-connection.md) 또는 [열기](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[레코드](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)하십시오 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), 또는 [열기](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)|[파일](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|[파일](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>관련 항목  
 [Cancel 메서드 예제 (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Cancel 메서드 예제 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 메서드 예제 (VC + +)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel 메서드 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute 메서드 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
