---
title: "ExecuteComplete 이벤트 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords: ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a6e5ca2b5590952ac01bf70b1c2e457336a79a2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 이벤트 (ADO)
**ExecuteComplete** 이벤트는 명령이 실행이 완료 된 후 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 A **긴** 명령에 의해 영향을 받는 레코드 수를 나타내는 값입니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 **adStatus** 은 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 이벤트를 호출할 때이로 설정 된 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 또는 **adStatusErrorsOccurred** 작업이 실패 합니다.  
  
 이 이벤트를 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pCommand*  
 [명령](../../../ado/reference/ado-api/command-object-ado.md) 실행 된 개체입니다. 포함 된 **명령** 를 호출 하는 경우에 개체 **Connection.Execute** 또는 **Recordset.Open** 명시적으로 만들지 않고는 **명령** 어떤 경우에는 **명령** 개체는 ADO에서 내부적으로 만들어집니다.  
  
 *pRecordset*  
 A [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 실행 된 명령의 결과로 생성 되는 개체입니다. 이 **레코드 집합** 비어 있을 수 있습니다. 이 이벤트 처리기에서이 레코드 집합 개체를 삭제 하지 해야 합니다. ADO에서 더 이상 존재 하는 개체에 액세스 하려고 할 때 이렇게 액세스 위반이 발생 합니다.  
  
 *pConnection*  
 A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 작업을 실행 하는 연결입니다.  
  
## <a name="remarks"></a>주의  
 **ExecuteComplete** 이벤트로 인해 발생할 수 있습니다는 **연결.** [실행](../../../ado/reference/ado-api/execute-method-ado-connection.md), **명령입니다.** [실행](../../../ado/reference/ado-api/execute-method-ado-command.md), **레코드 집합.** [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md), **레코드 집합.** [Requery](../../../ado/reference/ado-api/requery-method.md), 또는 **레코드 집합.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
