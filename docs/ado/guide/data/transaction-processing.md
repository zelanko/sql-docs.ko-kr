---
title: "트랜잭션 처리 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c37bf04fd14bb2d5f276efd3321b044759cbe7ee
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="transaction-processing"></a>트랜잭션 처리
A *트랜잭션* 일련의 연결을 통해 실행 하는 데이터 액세스 작업의 시작과 끝을 구분 합니다. 데이터 원본에서의 트랜잭션 기능에 따라는 **연결** 개체 또한 트랜잭션을 만들고 관리할 수 있습니다. 예를 들어 Microsoft OLE DB Provider for SQL Server를 사용 하 여 Microsoft SQL Server에서 데이터베이스에 액세스를 실행 하면 명령에 대 한 여러 개의 중첩 된 트랜잭션을 만들 수 있습니다.  
  
 ADO에서 트랜잭션의 작업으로 인해 발생 하는 데이터 원본에 대 한 변경 함께 성공적으로 또는 전혀 발생 있는지 확인 합니다.  
  
 트랜잭션, 취소 또는 작업 중 하나가 실패 하면 결과의 모든 작업이 트랜잭션에서 발생 한 처럼 됩니다. 트랜잭션이 시작 되기 전의 데이터 원본 유지 됩니다.  
  
 트랜잭션 제어 메서드를 제공 하는 ADO: **BeginTrans**, **CommitTrans**, 및 **RollbackTrans**합니다. 이러한 메서드를 사용 하 여 한 **연결** 저장 또는 일련의 변경 내용을 하나의 단위로 원본 데이터를 취소 하려는 경우 개체입니다. 예를 들어 money 계정 간에 전송할 하나에서 추가 하는 동일한 다른 합니다. 실패 하면 업데이트 중 하나가 계정을 더 이상 균형을 조정 합니다. 열려 있는 트랜잭션에서 변경 되도록 모두 적용 되거나 변경를 통해 이동 합니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 합니다. 되어 있는지 확인 공급자 정의 속성 "**트랜잭션 DDL**"에 표시 된 **연결** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 공급자를 지원 한다는 것을 나타내는 컬렉션 트랜잭션입니다. 공급자 트랜잭션을 지원 하지 않는 경우 이러한 메서드 중 하나를 호출 오류가 반환 됩니다.  
  
 호출한 후의 **BeginTrans** , 공급자 더 이상으로 즉시 커밋됩니다 호출할 때까지 수행한 변경 내용을 **CommitTrans** 또는 **RollbackTrans** 종료 하는 트랜잭션입니다.  
  
 호출 된 **CommitTrans** 메서드 연결에서 열려 있는 트랜잭션에서 변경한 내용을 저장 하 고 트랜잭션을 종료 합니다. 호출 된 **RollbackTrans** 메서드 열려 있는 트랜잭션에서 변경 된 이동한 트랜잭션을 종료 합니다. 열린 트랜잭션이 없을 때 두 방법 중 하나를 호출 하면 오류가 발생 합니다.  
  
 에 따라는 **연결** 개체의 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 호출 속성의 **CommitTrans** 또는 **RollbackTrans** 메서드 수 있습니다. 자동으로 새 트랜잭션을 시작 합니다. 경우는 **특성** 속성이로 설정 되어 **adXactCommitRetaining**, 공급자에 자동으로 후 새로운 트랜잭션이 시작 되는 **CommitTrans** 호출 합니다. 경우는 **특성** 속성이로 설정 되어 **adXactAbortRetaining**, 공급자에 자동으로 후 새로운 트랜잭션이 시작 되는 **RollbackTrans** 호출 합니다.  
  
## <a name="transaction-isolation-level"></a>트랜잭션 격리 수준  
 사용 하 여는 **IsolationLevel** 속성에 트랜잭션의 격리 수준을 설정할 수는 **연결** 개체입니다. 설정이 적용 되지 않습니다는 다음에 호출할 때까지는 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 요청한 격리 수준을 사용할 수 없는 경우 공급자는 다음으로 높은 격리 수준을 반환할 수 있습니다. 참조는 **IsolationLevel** 유효한 값에 대 한 자세한 내용은 ADO 프로그래머 참조에서 속성입니다.  
  
## <a name="nested-transactions"></a>중첩된 트랜잭션  
 호출 중첩된 트랜잭션을 지 원하는 공급자에 대 한는 **BeginTrans** 열려 있는 트랜잭션에서 메서드 새, 중첩 된 트랜잭션을 시작 합니다. 반환 값의 중첩 수준을 나타냅니다: "1"의 반환 값은 최상위 트랜잭션을 연 나타냅니다 (즉, 트랜잭션이 중첩 되지 않은 다른 트랜잭션에서), "2" (a 2-수준 트랜잭션 연 나타냅니다. 트랜잭션 최상위 트랜잭션 내에서 중첩), 등입니다. 호출 **CommitTrans** 또는 **RollbackTrans** 에 영향을 가장 최근에 열어 트랜잭션; 맞춤법 검사기를 닫거나 더 높은 수준의 트랜잭션을 해결할 수 전에 현재 트랜잭션을 롤백합니다.
