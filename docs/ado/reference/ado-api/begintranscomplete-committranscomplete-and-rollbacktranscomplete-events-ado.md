---
title: "BeginTrans, CommitTrans RollbackTrans 이벤트 (ADO) | Microsoft Docs"
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
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1ba84d4b168bb90ddc9994fb20080b628cd26c5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete, 및 RollbackTransComplete 이벤트 (ADO)
이러한 이벤트에서 연결 된 작업 후 호출 되는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체가 실행을 완료 합니다.  
  
-   **BeginTransComplete** 이후에 호출 됩니다는 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
-   **CommitTransComplete** 이후에 호출 됩니다는 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
-   **RollbackTransComplete** 이후에 호출 됩니다는 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *TransactionLevel*  
 A **긴** 새 트랜잭션 수준을 포함 하는 값은 **BeginTrans** 이 이벤트를 발생 시키는 합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. EventStatusEnum 값이 발생 한 오류를 설명 **adStatusErrorsOccurred**; 그렇지 않으면 설정 되지 않은 것입니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 매개 변수 설정 되어 이러한 이벤트 중 하나가 호출 되 면 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 또는 **adStatusErrorsOccurred** 작업이 실패 합니다.  
  
 이러한 이벤트는이 매개 변수를 설정 하 여 알림 메시지가 방지할 수 **adStatusUnwantedEvent** 전에 이벤트를 반환 합니다.  
  
 *pConnection*  
 **연결** 이 이벤트가 발생 한 개체입니다.  
  
## <a name="remarks"></a>주의  
 Visual c + +에서 여러 **연결** 동일한 이벤트 처리 메서드를 공유할 수 있습니다. 메서드를 사용 하 여 반환 된 **연결** 이벤트를 발생 시킨 개체를 결정 하는 개체입니다.  
  
 경우는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성 **adXactCommitRetaining** 또는 **adXactAbortRetaining**, 커밋 또는 트랜잭션을 롤백 후 새 트랜잭션을 시작 합니다. 사용 하 여 **BeginTransComplete** 이벤트를 모두 무시 하지만 첫 번째 트랜잭션 시작 이벤트입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드(ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
