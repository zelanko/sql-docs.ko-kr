---
description: ExecuteComplete 이벤트(ADO)
title: ExecuteComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: 36e27f8a86fce348dbf2061a1c7be91f43be9adc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973394"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 이벤트(ADO)
**ExecuteComplete** 이벤트는 명령 실행이 완료 된 후 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 명령의 영향을 받는 레코드 수를 나타내는 **Long** 값입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. **Adstatus** 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 이벤트가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **Adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 이 이벤트가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pCommand*  
 실행 된 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. **Connection.Exe귀여운** 또는 Recordset을 호출 하는 경우에도 **명령** 개체를 포함 합니다. **명령을**명시적으로 만들지 않고를 **엽니다.** 이 경우 **명령** 개체는 ADO에서 내부적으로 생성 됩니다.  
  
 *pRecordset*  
 실행 된 명령의 결과인 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이 **레코드 집합** 은 비어 있을 수 있습니다. 이 이벤트 처리기 내에서이 레코드 집합 개체를 삭제 하면 안 됩니다. 이렇게 하면 ADO에서 더 이상 존재 하지 않는 개체에 액세스 하려고 할 때 액세스 위반이 발생 합니다.  
  
 *pConnection*  
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 작업이 실행 된 연결입니다.  
  
## <a name="remarks"></a>설명  
 **ExecuteComplete** 이벤트는 연결로 인해 발생할 수 있습니다 **.** [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)명령을 실행 **합니다.** [실행](../../../ado/reference/ado-api/execute-method-ado-command.md), **레코드 집합** , **레코드 집합** 을 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md). [Requery](../../../ado/reference/ado-api/requery-method.md)또는 **레코드 집합입니다.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) 메서드.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
