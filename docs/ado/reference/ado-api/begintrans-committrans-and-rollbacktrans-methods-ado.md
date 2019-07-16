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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920524"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans, CommitTrans 및 RollbackTrans 메서드(ADO)
트랜잭션 내에서 처리를 관리 하는 이러한 트랜잭션 메서드를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 다음과 같이 개체:  
  
-   **BeginTrans** 새 트랜잭션을 시작 합니다.  
  
-   **CommitTrans** 변경 내용을 저장 하 고 현재 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
-   **RollbackTrans** 현재 트랜잭션 동안 이루어진 모든 변경 내용을 취소 하 고 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>반환 값  
 **BeginTrans** 로 반환 하는 함수 호출 될 수는 **긴** 변수는 트랜잭션의 중첩 수준을 나타내는입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *object*  
 A **연결** 개체입니다.  
  
## <a name="connection"></a>연결  
 이러한 메서드를 사용 하는 **연결** 개체에 저장 하거나 일련의 단일 단위와 원본 데이터에 대 한 변경 취소 하려는 경우. 예를 들어, money 계정 간에 전송할 하나에서 추가 하는 동일한 다른 합니다. 실패를 업데이트 하거나 계정을 더 이상 분산 합니다. 열린 트랜잭션 내에서 이러한 변경을 수행한 되도록 하거나 아무것도 변경 내용을 이동 합니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 합니다. 확인 하는 공급자가 정의한 속성 "**트랜잭션 DDL**"에 표시 되는 **연결** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 공급자를 지원함을 나타내는 컬렉션 트랜잭션입니다. 공급자는 트랜잭션을 지원 하지 않습니다, 경우 다음이 방법 중 하나를 호출 하는 오류가 반환 됩니다.  
  
 호출한 후 합니다 **BeginTrans** 메서드를 공급자를 호출할 때까지 수행한 변경 내용 커밋 즉시 더 이상 **CommitTrans** 또는 **RollbackTrans** 종료 하는 트랜잭션입니다.  
  
 호출 중첩된 트랜잭션을 지 원하는 공급자에 대 한 합니다 **BeginTrans** 열려 있는 트랜잭션에서 메서드 새, 중첩 된 트랜잭션을 시작 합니다. 반환 값은 중첩 수준을 나타냅니다: 반환 값이 "1"는 최상위 트랜잭션을 열면 나타냅니다 (즉, 트랜잭션이 중첩 되지 않은 다른 트랜잭션 내에서), "2" (a 두 번째 수준 트랜잭션 열었던 나타냅니다. 트랜잭션 최상위 트랜잭션 내에서 중첩), 등입니다. 호출 **CommitTrans** 하거나 **RollbackTrans** 영향을 가장 최근에 트랜잭션이 연; 닫거나 트랜잭션을 모두 더 높은 수준의 확인 하려면 먼저 현재 트랜잭션을 롤백합니다.  
  
 호출 된 **CommitTrans** 메서드는 연결에서 열려 있는 트랜잭션에서 변경 내용을 저장 하 고 트랜잭션을 종료 합니다. 호출 된 **RollbackTrans** 메서드 열려 있는 트랜잭션에서 변경한 내용을 취소 하 고 트랜잭션을 종료 합니다. 열려 있는 트랜잭션이 있으면 두 방법 중 하나를 호출 하면 오류가 발생 합니다.  
  
 에 따라 합니다 **연결** 개체의 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성을 호출 합니다 **CommitTrans** 또는 **RollbackTrans** 메서드 수 있습니다. 자동으로 새 트랜잭션을 시작 합니다. 경우는 **특성** 속성이 **adXactCommitRetaining**, 공급자는 자동으로 후 새 트랜잭션을 시작을 **CommitTrans** 호출 합니다. 경우는 **특성** 속성이 **adXactAbortRetaining**, 공급자는 자동으로 후 새 트랜잭션을 시작을 **RollbackTrans** 호출 합니다.  
  
## <a name="remote-data-service"></a>원격 데이터 서비스  
 합니다 **BeginTrans**, **CommitTrans**, 및 **RollbackTrans** 메서드를 클라이언트 쪽에서 사용할 수 없는 **연결** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
