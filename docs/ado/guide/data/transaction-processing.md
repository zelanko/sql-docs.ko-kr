---
description: '트랜잭션 처리 '
title: 트랜잭션 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bde1338e56f4685359f8d1260b36c39a24455083
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979334"
---
# <a name="transaction-processing"></a>트랜잭션 처리
*트랜잭션은* 연결에서 실행 되는 일련의 데이터 액세스 작업의 시작과 끝을 구분 합니다. 데이터 원본의 트랜잭션 기능에 따라 **연결** 개체를 사용 하 여 트랜잭션을 만들고 관리할 수도 있습니다. 예를 들어 SQL Server에 대 한 Microsoft OLE DB 공급자를 사용 하 여 Microsoft SQL Server에서 데이터베이스에 액세스 하는 경우 실행 하는 명령에 대해 중첩 된 트랜잭션을 여러 개 만들 수 있습니다.  
  
 ADO를 사용 하면 트랜잭션의 작업으로 인해 발생 하는 데이터 원본에 대 한 변경 내용이 성공적으로 함께 발생 하거나 전혀 발생 하지 않을 수 있습니다.  
  
 트랜잭션을 취소 하거나 해당 작업 중 하나가 실패 한 경우 트랜잭션의 작업이 발생 하지 않은 것 처럼 결과가 반환 됩니다. 데이터 원본은 트랜잭션이 시작 되기 전의 상태로 유지 됩니다.  
  
 ADO에서는 **BeginTrans**, **CommitTrans**및 **RollbackTrans**트랜잭션을 제어 하기 위한 다음과 같은 방법을 제공 합니다. 원본 데이터에 대 한 일련의 변경 내용을 단일 단위로 저장 하거나 취소 하려는 경우 **연결** 개체에 이러한 메서드를 사용 합니다. 예를 들어 계정 간에 돈을 전송 하려면 1에서 금액을 빼서 동일한 금액을 다른에 추가 합니다. 업데이트 중 하나가 실패 하면 계정이 더 이상 균형을 유지 하지 않습니다. 열려 있는 트랜잭션 내에서 이러한 변경 작업을 수행 하면 변경 내용이 전부 또는 전혀 변경 되지 않습니다.  
  
> [!NOTE]
>  일부 공급자는 트랜잭션을 지원 하지 않습니다. 공급자 정의 속성 "**TRANSACTION DDL**"이 공급자가 트랜잭션을 지원 함을 나타내는 **연결** 개체의 [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 나타나는지 확인 합니다. 공급자가 트랜잭션을 지원 하지 않는 경우 이러한 메서드 중 하나를 호출 하면 오류가 반환 됩니다.  
  
 **BeginTrans** 메서드를 호출한 후에는 **CommitTrans** 또는 **RollbackTrans** 를 호출 하 여 트랜잭션을 종료할 때까지 공급자가 즉시 변경 내용을 커밋하지 않습니다.  
  
 **CommitTrans** 메서드를 호출 하면 연결에서 열린 트랜잭션 내에서 수행 된 변경 내용이 저장 되 고 트랜잭션이 종료 됩니다. **RollbackTrans** 메서드를 호출 하면 열린 트랜잭션 내에서 수행 된 모든 변경 내용이 취소 되 고 트랜잭션이 종료 됩니다. 열려 있는 트랜잭션이 없는 경우 두 메서드를 호출 하면 오류가 발생 합니다.  
  
 **Connection** 개체의 [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) 속성에 따라 **CommitTrans** 또는 **RollbackTrans** 메서드를 호출 하면 새 트랜잭션이 자동으로 시작 될 수 있습니다. **Attributes** 속성이 **adXactCommitRetaining**로 설정 된 경우 공급자는 **CommitTrans** 호출 후에 새 트랜잭션을 자동으로 시작 합니다. **Attributes** 속성이 **adXactAbortRetaining**로 설정 된 경우 공급자는 **RollbackTrans** 호출 후에 새 트랜잭션을 자동으로 시작 합니다.  
  
## <a name="transaction-isolation-level"></a>트랜잭션 격리 수준  
 **IsolationLevel** 속성을 사용 하 여 **연결** 개체에 대 한 트랜잭션의 격리 수준을 설정할 수 있습니다. 이 설정은 다음에 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드를 호출할 때까지 적용 되지 않습니다. 요청 하는 격리 수준을 사용할 수 없는 경우 공급자는 다음으로 높은 수준의 격리를 반환할 수 있습니다. 유효한 값에 대 한 자세한 내용은 ADO 프로그래머 참조에서 **IsolationLevel** 속성을 참조 하세요.  
  
## <a name="nested-transactions"></a>중첩 된 트랜잭션  
 중첩 된 트랜잭션을 지 원하는 공급자의 경우 열린 트랜잭션 내에서 **BeginTrans** 메서드를 호출 하면 중첩 된 새 트랜잭션이 시작 됩니다. 반환 값은 중첩 수준을 나타냅니다. 반환 값이 "1" 이면 최상위 트랜잭션을 열었습니다 (즉, 트랜잭션이 다른 트랜잭션 내에 중첩 되지 않음). "2"는 두 번째 수준 트랜잭션 (최상위 트랜잭션 내에 중첩 된 트랜잭션)을 열었는지 나타냅니다. **CommitTrans** 또는 **RollbackTrans** 를 호출 하면 가장 최근에 열린 트랜잭션만 영향을 받습니다. 상위 수준 트랜잭션을 해결 하려면 먼저 현재 트랜잭션을 닫거나 롤백해야 합니다.
