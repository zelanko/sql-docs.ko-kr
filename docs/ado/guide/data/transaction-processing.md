---
title: 트랜잭션 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 032677452fa80502d37383af8172ff9475dea363
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704816"
---
# <a name="transaction-processing"></a>트랜잭션 처리
A *트랜잭션* 일련의 연결을 통해 실행 하는 데이터 액세스 작업의 시작과 끝을 구분 합니다. 데이터 원본의 트랜잭션 기능에 따라 합니다 **연결** 개체도 트랜잭션을 만들고 관리할 수 있습니다. 예를 들어, Microsoft OLE DB Provider for SQL Server를 사용 하 여 Microsoft SQL Server에서 데이터베이스 액세스를 실행 하면 명령에 대 한 여러 중첩 된 트랜잭션을 만들 수 있습니다.  
  
 트랜잭션의 작업에서 결과 데이터 원본에 변경 내용을 함께 성공적으로 또는 전혀 수행 되도록 하는 ADO.  
  
 트랜잭션을 취소 하는 경우 또는 작업 중 하나가 실패할 경우 결과가 발생 하지 않았는데도 트랜잭션에서 작업 처럼 됩니다. 데이터 원본에는 트랜잭션이 시작 되기 전의 상태로 유지 됩니다.  
  
 ADO는 트랜잭션 제어에 대 한 메서드를 제공 합니다. **BeginTrans**하십시오 **CommitTrans**, 및 **RollbackTrans**합니다. 이러한 메서드를 사용 하는 **연결** 개체에 저장 하거나 일련의 단일 단위와 원본 데이터에 대 한 변경 취소 하려는 경우. 예를 들어, money 계정 간에 전송할 하나에서 추가 하는 동일한 다른 합니다. 실패를 업데이트 하거나 계정을 더 이상 분산 합니다. 열린 트랜잭션 내에서 이러한 변경을 수행한 되도록 하거나 아무것도 변경 내용을 이동 합니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 합니다. 확인 하는 공급자가 정의한 속성 "**트랜잭션 DDL**"에 표시 되는 **연결** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 공급자를 지원함을 나타내는 컬렉션 트랜잭션입니다. 공급자는 트랜잭션을 지원 하지 않습니다, 경우 다음이 방법 중 하나를 호출 하는 오류가 반환 됩니다.  
  
 호출한 후 합니다 **BeginTrans** 메서드를 공급자를 호출할 때까지 수행한 변경 내용 커밋 즉시 더 이상 **CommitTrans** 또는 **RollbackTrans** 종료 하는 트랜잭션입니다.  
  
 호출 된 **CommitTrans** 메서드는 연결에서 열려 있는 트랜잭션에서 변경 내용을 저장 하 고 트랜잭션을 종료 합니다. 호출 된 **RollbackTrans** 메서드 열려 있는 트랜잭션에서 변경한 내용을 취소 하 고 트랜잭션을 종료 합니다. 열려 있는 트랜잭션이 있으면 두 방법 중 하나를 호출 하면 오류가 발생 합니다.  
  
 에 따라 합니다 **연결** 개체의 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성을 호출 합니다 **CommitTrans** 또는 **RollbackTrans** 메서드 수 있습니다. 자동으로 새 트랜잭션을 시작 합니다. 경우는 **특성** 속성이 **adXactCommitRetaining**, 공급자는 자동으로 후 새 트랜잭션을 시작을 **CommitTrans** 호출 합니다. 경우는 **특성** 속성이 **adXactAbortRetaining**, 공급자는 자동으로 후 새 트랜잭션을 시작을 **RollbackTrans** 호출 합니다.  
  
## <a name="transaction-isolation-level"></a>트랜잭션 격리 수준  
 사용 하 여는 **IsolationLevel** 트랜잭션의 격리 수준을 설정 하는 속성을 **연결** 개체입니다. 설정이 적용 되지 않습니다 다음에 호출 될 때까지 합니다 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 요청 하는 격리 수준을 사용할 수 없는 경우 공급자는 다음 더 높은 수준의 격리를 반환할 수 있습니다. 참조 된 **IsolationLevel** 유효한 값에 대 한 자세한 내용은 ADO 프로그래머 참조에서 속성입니다.  
  
## <a name="nested-transactions"></a>중첩 된 트랜잭션  
 호출 중첩된 트랜잭션을 지 원하는 공급자에 대 한 합니다 **BeginTrans** 열려 있는 트랜잭션에서 메서드 새, 중첩 된 트랜잭션을 시작 합니다. 반환 값은 중첩 수준을 나타냅니다: 반환 값이 "1"는 최상위 트랜잭션을 열면 나타냅니다 (즉, 트랜잭션이 중첩 되지 않은 다른 트랜잭션 내에서), "2" (a 두 번째 수준 트랜잭션 열었던 나타냅니다. 트랜잭션 최상위 트랜잭션 내에서 중첩), 등입니다. 호출 **CommitTrans** 하거나 **RollbackTrans** 영향을 가장 최근에 트랜잭션이 연; 닫거나 트랜잭션을 모두 더 높은 수준의 확인 하려면 먼저 현재 트랜잭션을 롤백합니다.
