---
description: Cancel 메서드(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 24d4beba2c703d2c8e21f51dd5bac9d06444a651
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451065"
---
# <a name="cancel-method-ado"></a>Cancel 메서드(ADO)
보류 중인 비동기 메서드 호출의 실행을 취소 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>설명  
 **Cancel** 메서드를 사용 하 여 비동기 메서드 호출의 실행을 종료 합니다. 즉, **adasyncconnect**, **Adasyncconnect**또는 **adasyncconnect** 옵션을 사용 하 여 호출 되는 메서드입니다.  
  
 다음 표에서는 특정 형식의 개체에서 **Cancel** 메서드를 사용할 때 종료 되는 작업을 보여 줍니다.  
  
|*개체가* 인 경우|이 메서드에 대 한 마지막 비동기 호출이 종료 되었습니다.|  
|----------------------|-------------------------------------------------------------|  
|[명령](../../../ado/reference/ado-api/command-object-ado.md)|[실행할](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|[실행](../../../ado/reference/ado-api/execute-method-ado-connection.md) 또는 [열기](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[레코드](../../../ado/reference/ado-api/record-object-ado.md)|[Copyrecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)또는 [Open](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)|[열기](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[스트림](../../../ado/reference/ado-api/stream-object-ado.md)|[열기](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
        [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
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
