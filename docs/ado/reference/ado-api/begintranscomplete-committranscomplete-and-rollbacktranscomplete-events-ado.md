---
title: BeginTrans, CommitTrans RollbackTrans 이벤트 (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8239a5f9069212b9413216bc3535e3c90e2d5316
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696358"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete, CommitTransComplete, 및 RollbackTransComplete 이벤트 (ADO)
이러한 이벤트에서 연결된 된 작업 후 호출 되는 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 실행이 완료 합니다.  
  
-   **BeginTransComplete** 후 호출 되는 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
-   **CommitTransComplete** 후 호출 되는 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
-   **RollbackTransComplete** 후 호출 되는 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *TransactionLevel*  
 A **긴** 의 새 트랜잭션 수준을 포함 하는 값을 **BeginTrans** 이 이벤트를 발생 시킨 합니다.  
  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. EventStatusEnum의 값이 발생 한 오류를 설명 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 매개 변수를로 이러한 이벤트 중 하나가 호출 될 때 **adStatusOK** 이벤트를 발생 시킨 작업에 성공, 또는 **adStatusErrorsOccurred** 작업이 실패 합니다.  
  
 이러한 이벤트를이 매개 변수를 설정 하 여 후속 알림을 방지할 수 있습니다 **adStatusUnwantedEvent** 전에 이벤트를 반환 합니다.  
  
 *pConnection*  
 합니다 **연결** 이 이벤트가 발생 한 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 시각적 개체의 C++, multiple **연결** 동일한 이벤트 처리 메서드를 공유할 수 있습니다. 메서드를 사용 하 여 반환 된 **연결** 이벤트를 발생 시킨 개체를 결정 하는 개체입니다.  
  
 경우는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성이 **adXactCommitRetaining** 또는 **adXactAbortRetaining**, 새 트랜잭션을 커밋 또는 트랜잭션 롤백 후 시작 합니다. 사용 된 **BeginTransComplete** 이벤트를 모두 무시 하지만 첫 번째 트랜잭션 시작 이벤트입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드(ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
