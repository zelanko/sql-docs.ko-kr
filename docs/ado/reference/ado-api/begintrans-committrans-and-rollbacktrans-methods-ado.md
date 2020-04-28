---
title: BeginTrans, CommitTrans 및 RollbackTrans 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3a8bc22e57d91ab64bdbbc5fc694575a8aa8ff9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920524"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans, CommitTrans 및 RollbackTrans 메서드(ADO)
이러한 트랜잭션 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 내에서 트랜잭션 처리를 다음과 같이 관리 합니다.  
  
-   **BeginTrans** 새 트랜잭션을 시작 합니다.  
  
-   **CommitTrans** 모든 변경 내용을 저장 하 고 현재 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
-   **RollbackTrans** 현재 트랜잭션 중에 수행 된 모든 변경 내용을 취소 하 고 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Return Value  
 **BeginTrans** 는 트랜잭션의 중첩 수준을 나타내는 **Long** 변수를 반환 하는 함수로 호출 될 수 있습니다.  
  
#### <a name="parameters"></a>매개 변수  
 *object*  
 **Connection** 개체입니다.  
  
## <a name="connection"></a>연결  
 원본 데이터에 대 한 일련의 변경 내용을 단일 단위로 저장 하거나 취소 하려는 경우 **연결** 개체에 이러한 메서드를 사용 합니다. 예를 들어 계정 간에 돈을 전송 하려면 1에서 금액을 빼서 동일한 금액을 다른에 추가 합니다. 업데이트 중 하나가 실패 하면 계정이 더 이상 균형을 유지 하지 않습니다. 열려 있는 트랜잭션 내에서 이러한 변경 작업을 수행 하면 변경 내용이 전부 또는 전혀 변경 되지 않습니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 하지 않습니다. 공급자 정의 속성 "**TRANSACTION DDL**"이 공급자가 트랜잭션을 지원 함을 나타내는 **연결** 개체의 [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 나타나는지 확인 합니다. 공급자가 트랜잭션을 지원 하지 않는 경우 이러한 메서드 중 하나를 호출 하면 오류가 반환 됩니다.  
  
 **BeginTrans** 메서드를 호출한 후에는 **CommitTrans** 또는 **RollbackTrans** 를 호출 하 여 트랜잭션을 종료할 때까지 공급자가 즉시 변경 내용을 커밋하지 않습니다.  
  
 중첩 된 트랜잭션을 지 원하는 공급자의 경우 열린 트랜잭션 내에서 **BeginTrans** 메서드를 호출 하면 중첩 된 새 트랜잭션이 시작 됩니다. 반환 값은 중첩 수준을 나타냅니다. 반환 값이 "1" 이면 최상위 트랜잭션을 열었습니다 (즉, 트랜잭션이 다른 트랜잭션 내에 중첩 되지 않음). "2"는 두 번째 수준 트랜잭션 (최상위 트랜잭션 내에 중첩 된 트랜잭션)을 열었는지 나타냅니다. **CommitTrans** 또는 **RollbackTrans** 를 호출 하면 가장 최근에 열린 트랜잭션만 영향을 받습니다. 상위 수준 트랜잭션을 해결 하려면 먼저 현재 트랜잭션을 닫거나 롤백해야 합니다.  
  
 **CommitTrans** 메서드를 호출 하면 연결에서 열린 트랜잭션 내에서 수행 된 변경 내용이 저장 되 고 트랜잭션이 종료 됩니다. **RollbackTrans** 메서드를 호출 하면 열린 트랜잭션 내에서 수행 된 모든 변경 내용이 취소 되 고 트랜잭션이 종료 됩니다. 열려 있는 트랜잭션이 없는 경우 두 메서드를 호출 하면 오류가 발생 합니다.  
  
 **Connection** 개체의 [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) 속성에 따라 **CommitTrans** 또는 **RollbackTrans** 메서드를 호출 하면 새 트랜잭션이 자동으로 시작 될 수 있습니다. **Attributes** 속성이 **adXactCommitRetaining**로 설정 된 경우 공급자는 **CommitTrans** 호출 후에 새 트랜잭션을 자동으로 시작 합니다. **Attributes** 속성이 **adXactAbortRetaining**로 설정 된 경우 공급자는 **RollbackTrans** 호출 후에 새 트랜잭션을 자동으로 시작 합니다.  
  
## <a name="remote-data-service"></a>원격 데이터 서비스  
 클라이언트 쪽 **연결** 개체에서는 **BeginTrans**, **CommitTrans**및 **RollbackTrans** 메서드를 사용할 수 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
