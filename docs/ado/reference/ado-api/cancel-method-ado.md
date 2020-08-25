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
ms.openlocfilehash: c40b3f7d0c5a9f6669d41e4f90422dd3ce66ebd5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776342"
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
|[명령](./command-object-ado.md)|[실행](./execute-method-ado-command.md)|  
|[연결](./connection-object-ado.md)|[실행](./execute-method-ado-connection.md) 또는 [열기](./open-method-ado-connection.md)|  
|[레코드](./record-object-ado.md)|[Copyrecord](./copyrecord-method-ado.md), [DeleteRecord](./deleterecord-method-ado.md), [MoveRecord](./moverecord-method-ado.md)또는 [Open](./open-method-ado-record.md)|  
|[레코드 집합](./recordset-object-ado.md)|[열기](./open-method-ado-recordset.md)|  
|[스트림](./stream-object-ado.md)|[열기](./open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [명령 개체(ADO)](./command-object-ado.md)  
        [연결 개체(ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 개체(ADO)](./record-object-ado.md)  
        [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [스트림 개체(ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Cancel 메서드 예제 (VB)](./cancel-method-example-vb.md)   
 [Cancel 메서드 예제 (VBScript)](../rds-api/cancel-method-example-vbscript.md)   
 [Cancel 메서드 예제 (VC + +)](./cancel-method-example-vc.md)   
 [Cancel 메서드 (RDS)](../rds-api/cancel-method-rds.md)   
 [CancelBatch 메서드 (ADO)](./cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](./cancelupdate-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Execute 메서드 (ADO 명령)](./execute-method-ado-command.md)   
 [Execute 메서드 (ADO 연결)](./execute-method-ado-connection.md)   
 [Open 메서드 (ADO 연결)](./open-method-ado-connection.md)   
 [Open 메서드(ADO 레코드 집합)](./open-method-ado-recordset.md)