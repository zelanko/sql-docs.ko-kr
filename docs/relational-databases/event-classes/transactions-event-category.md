---
description: Transactions 이벤트 범주
title: Transactions 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 086ea0a7206c667242d3aa631fa0f46f86220b2d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88470644"
---
# <a name="transactions-event-category"></a>Transactions 이벤트 범주
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Transactions** 이벤트 클래스를 사용하면 트랜잭션 상태를 모니터링할 수 있습니다. 접두사 **TM:** 으로 시작되는 이벤트 클래스 이름은 트랜잭션 관리 인터페이스를 통해 전송되는 트랜잭션 관련 작업을 추적하는 데 사용됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[DTCTransaction 이벤트 클래스](../../relational-databases/event-classes/dtctransaction-event-class.md)|MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)가 관리하는 트랜잭션을 추적합니다. 이러한 트랜잭션은 둘 이상의 데이터베이스 또는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스 간에 분산된 트랜잭션입니다.|  
|[SQLTransaction 이벤트 클래스](../../relational-databases/event-classes/sqltransaction-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN 및 ROLLBACK TRAN 문을 추적합니다.|  
|[TM: Begin Tran Completed 이벤트 클래스](../../relational-databases/event-classes/tm-begin-tran-completed-event-class.md)|BEGIN TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Begin Tran Starting 이벤트 클래스](../../relational-databases/event-classes/tm-begin-tran-starting-event-class.md)|BEGIN TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Commit Tran Completed 이벤트 클래스](../../relational-databases/event-classes/tm-commit-tran-completed-event-class.md)|COMMIT TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Commit Tran Starting 이벤트 클래스](../../relational-databases/event-classes/tm-commit-tran-starting-event-class.md)|COMMIT TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Promote Tran Completed 이벤트 클래스](../../relational-databases/event-classes/tm-promote-tran-completed-event-class.md)|PROMOTE TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Promote Tran Starting 이벤트 클래스](../../relational-databases/event-classes/tm-promote-tran-starting-event-class.md)|PROMOTE TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Rollback Tran Completed 이벤트 클래스](../../relational-databases/event-classes/tm-rollback-tran-completed-event-class.md)|ROLLBACK TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Rollback Tran Starting 이벤트 클래스](../../relational-databases/event-classes/tm-rollback-tran-starting-event-class.md)|ROLLBACK TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TM: Save Tran Completed 이벤트 클래스](../../relational-databases/event-classes/tm-save-tran-completed-event-class.md)|SAVE TRANSACTION 요청이 완료되었음을 나타냅니다.|  
|[TM: Save Tran Starting 이벤트 클래스](../../relational-databases/event-classes/tm-save-tran-starting-event-class.md)|SAVE TRANSACTION 요청이 시작 중임을 나타냅니다.|  
|[TransactionLog 이벤트 클래스](../../relational-databases/event-classes/transactionlog-event-class.md)|트랜잭션이 데이터베이스 트랜잭션 로그에 기록되는 시기를 추적합니다.|  
  
  
