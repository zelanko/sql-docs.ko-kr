---
title: "BeginTrans, CommitTrans 및 RollbackTrans 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e973503fcdd7a524bab21364428be6b955017af
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans, CommitTrans 및 RollbackTrans 메서드 (ADO)
이러한 트랜잭션 메서드 내에서 처리 하는 트랜잭션 관리는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 다음과 같이 개체:  
  
-   **BeginTrans** 새 트랜잭션을 시작 합니다.  
  
-   **CommitTrans** 변경 내용을 저장 하 고 현재 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
-   **RollbackTrans** 현재 트랜잭션 동안 변경 된 내용을 취소 하 고 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>반환 값  
 **BeginTrans** 반환 하는 함수를 호출할 수는 **긴** 트랜잭션의 중첩 수준을 나타내는 변수입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *개체*  
 A **연결** 개체입니다.  
  
## <a name="connection"></a>연결  
 이러한 메서드를 사용 하 여 한 **연결** 저장 또는 일련의 변경 내용을 하나의 단위로 원본 데이터를 취소 하려는 경우 개체입니다. 예를 들어 money 계정 간에 전송할 하나에서 추가 하는 동일한 다른 합니다. 실패 하면 업데이트 중 하나가 계정을 더 이상 균형을 조정 합니다. 열려 있는 트랜잭션에서 변경 되도록 모두 적용 되거나 변경를 통해 이동 합니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 합니다. 되어 있는지 확인 공급자 정의 속성 "**트랜잭션 DDL**"에 표시 된 **연결** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 공급자를 지원 한다는 것을 나타내는 컬렉션 트랜잭션입니다. 공급자 트랜잭션을 지원 하지 않는 경우 이러한 메서드 중 하나를 호출 오류가 반환 됩니다.  
  
 호출한 후의 **BeginTrans** , 공급자 더 이상으로 즉시 커밋됩니다 호출할 때까지 수행한 변경 내용을 **CommitTrans** 또는 **RollbackTrans** 종료 하는 트랜잭션입니다.  
  
 호출 중첩된 트랜잭션을 지 원하는 공급자에 대 한는 **BeginTrans** 열려 있는 트랜잭션에서 메서드 새, 중첩 된 트랜잭션을 시작 합니다. 반환 값의 중첩 수준을 나타냅니다: "1"의 반환 값은 최상위 트랜잭션을 연 나타냅니다 (즉, 트랜잭션이 중첩 되지 않은 다른 트랜잭션에서), "2" (a 2-수준 트랜잭션 연 나타냅니다. 트랜잭션 최상위 트랜잭션 내에서 중첩), 등입니다. 호출 **CommitTrans** 또는 **RollbackTrans** 에 영향을 가장 최근에 열어 트랜잭션; 맞춤법 검사기를 닫거나 더 높은 수준의 트랜잭션을 해결할 수 전에 현재 트랜잭션을 롤백합니다.  
  
 호출 된 **CommitTrans** 메서드 연결에서 열려 있는 트랜잭션에서 변경한 내용을 저장 하 고 트랜잭션을 종료 합니다. 호출 된 **RollbackTrans** 메서드 열려 있는 트랜잭션에서 변경 된 이동한 트랜잭션을 종료 합니다. 열린 트랜잭션이 없을 때 두 방법 중 하나를 호출 하면 오류가 발생 합니다.  
  
 에 따라는 **연결** 개체의 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 호출 속성의 **CommitTrans** 또는 **RollbackTrans** 메서드 수 있습니다. 자동으로 새 트랜잭션을 시작 합니다. 경우는 **특성** 속성이로 설정 되어 **adXactCommitRetaining**, 공급자에 자동으로 후 새로운 트랜잭션이 시작 되는 **CommitTrans** 호출 합니다. 경우는 **특성** 속성이로 설정 되어 **adXactAbortRetaining**, 공급자에 자동으로 후 새로운 트랜잭션이 시작 되는 **RollbackTrans** 호출 합니다.  
  
## <a name="remote-data-service"></a>원격 데이터 서비스  
 **BeginTrans**, **CommitTrans**, 및 **RollbackTrans** 메서드는 클라이언트 쪽에서 사용할 수 없는 **연결** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 예제 (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

