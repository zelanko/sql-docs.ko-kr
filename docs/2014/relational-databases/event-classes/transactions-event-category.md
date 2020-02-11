---
title: Transactions 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 076e68de4dc5d4e25f6cabe6b39ac4a61a05033a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63062231"
---
# <a name="transactions-event-category"></a>Transactions 이벤트 범주
  **Transactions** 이벤트 클래스를 사용하면 트랜잭션 상태를 모니터링할 수 있습니다. 접두사 **TM:** 으로 시작되는 이벤트 클래스 이름은 트랜잭션 관리 인터페이스를 통해 전송되는 트랜잭션 관련 작업을 추적하는 데 사용됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[DTCTransaction 이벤트 클래스](dtctransaction-event-class.md)|MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)가 관리하는 트랜잭션을 추적합니다. 이러한 트랜잭션은 둘 이상의 데이터베이스 또는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스 간에 분산된 트랜잭션입니다.|  
|[SQLTransaction 이벤트 클래스](sqltransaction-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN 및 ROLLBACK TRAN 문을 추적합니다.|  
|[TM: Begin Tran Completed 이벤트 클래스](tm-begin-tran-completed-event-class.md)|BEGIN TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Begin Tran Starting 이벤트 클래스](tm-begin-tran-starting-event-class.md)|BEGIN TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Commit Tran Completed 이벤트 클래스](tm-commit-tran-completed-event-class.md)|COMMIT TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Commit Tran Starting 이벤트 클래스](tm-commit-tran-starting-event-class.md)|COMMIT TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Promote Tran Completed 이벤트 클래스](tm-promote-tran-completed-event-class.md)|PROMOTE TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Promote Tran Starting 이벤트 클래스](tm-promote-tran-starting-event-class.md)|PROMOTE TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Rollback Tran Completed 이벤트 클래스](tm-rollback-tran-completed-event-class.md)|ROLLBACK TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Rollback Tran Starting 이벤트 클래스](tm-rollback-tran-starting-event-class.md)|ROLLBACK TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Save Tran Completed 이벤트 클래스](tm-save-tran-completed-event-class.md)|SAVE TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Save Tran Starting 이벤트 클래스](tm-save-tran-starting-event-class.md)|SAVE TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TransactionLog 이벤트 클래스](transactionlog-event-class.md)|트랜잭션이 데이터베이스 트랜잭션 로그에 기록되는 시기를 추적합니다.|  
  
  
