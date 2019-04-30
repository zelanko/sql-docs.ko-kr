---
title: ExecuteComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec656a49963eb02cb204d5be96d403726bba8c56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301326"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 이벤트(ADO)
합니다 **ExecuteComplete** 이벤트 명령 실행이 완료 된 후 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 A **긴** 명령에 의해 영향을 받은 레코드 수를 나타내는 값입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 **adStatus** 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 매개 변수를로이 이벤트를 호출 하면 **adStatusOK** 이벤트를 발생 시킨 작업에 성공, 또는 **adStatusErrorsOccurred** 작업이 실패 합니다.  
  
 이 이벤트는 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pCommand*  
 합니다 [명령](../../../ado/reference/ado-api/command-object-ado.md) 실행 된 개체입니다. 포함 된 **명령** 호출 하는 경우에 개체 **Connection.Execute** 또는 **Recordset.Open** 명시적으로 만들지 않고를 **명령** 어떤 경우에는 **명령** 개체는 ADO에서 내부적으로 만들어집니다.  
  
 *pRecordset*  
 A [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 실행 명령의 결과 나타내는 개체입니다. 이렇게 **레코드 집합** 비어 있을 수 있습니다. 이 이벤트 처리기 내에서이 레코드 집합 개체를 파괴 되지 해야 합니다. 이렇게 ADO가 더 이상 존재 하는 개체에 액세스 하려고 할 때 액세스 위반이 발생 합니다.  
  
 *pConnection*  
 A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 작업이 실행 된 연결입니다.  
  
## <a name="remarks"></a>Remarks  
 **ExecuteComplete** 이벤트로 인해 발생할 수 있습니다 합니다 **연결 합니다.** [실행할](../../../ado/reference/ado-api/execute-method-ado-connection.md)하십시오 **명령입니다.** [실행할](../../../ado/reference/ado-api/execute-method-ado-command.md)하십시오 **Recordset.** [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md)하십시오 **레코드 집합.** [Requery](../../../ado/reference/ado-api/requery-method.md), 또는 **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) 메서드.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
