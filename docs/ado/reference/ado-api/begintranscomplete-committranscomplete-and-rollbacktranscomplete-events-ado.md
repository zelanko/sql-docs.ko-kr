---
description: BeginTransComplete, CommitTransComplete 및 RollbackTransComplete Events (ADO)
title: BeginTrans, CommitTrans, RollbackTrans Events (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 47f559f839c4dcb6b73b273cd09a0289468f9046
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776422"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete 및 RollbackTransComplete Events (ADO)
이러한 이벤트는 [연결](./connection-object-ado.md) 개체에 대 한 연결 된 작업의 실행이 완료 된 후에 호출 됩니다.  
  
-   **BeginTransComplete** 는 [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 후에 호출 됩니다.  
  
-   **CommitTransComplete** 는 [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 후에 호출 됩니다.  
  
-   **RollbackTransComplete** 는 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *TransactionLevel*  
 이 이벤트를 발생 시킨 **BeginTrans** 의 새 트랜잭션 수준을 포함 하는 **Long** 값입니다.  
  
 *pError*  
 [오류](./error-object.md) 개체입니다. EventStatusEnum의 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md) 상태 값입니다. 이러한 이벤트를 호출 하면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **Adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 이러한 이벤트는 이벤트가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림을 차단할 수 있습니다.  
  
 *pConnection*  
 이 이벤트가 발생 한 **연결** 개체입니다.  
  
## <a name="remarks"></a>설명  
 Visual C++ 여러 **연결이** 동일한 이벤트 처리 메서드를 공유할 수 있습니다. 메서드는 반환 된 **연결** 개체를 사용 하 여 이벤트를 발생 시킨 개체를 확인 합니다.  
  
 [Attributes](./attributes-property-ado.md) 속성이 **adXactCommitRetaining** 또는 **adXactAbortRetaining**로 설정 된 경우 트랜잭션을 커밋하거나 롤백하는 후 새 트랜잭션이 시작 됩니다. **BeginTransComplete** 이벤트를 사용 하 여 첫 번째 트랜잭션 시작 이벤트를 제외한 모든 이벤트를 무시 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](./ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 이벤트 처리기 요약](../../guide/data/ado-event-handler-summary.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드(ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)