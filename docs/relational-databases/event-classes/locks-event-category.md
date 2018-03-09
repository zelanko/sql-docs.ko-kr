---
title: "잠금 이벤트 범주 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Locks event category [SQL Server]
- SQL Server event classes, Locks event category
- event classes [SQL Server], Locks event category
- lock escalation [SQL Server], locks event category
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4254c204a91eb0696b7ee08eda0a234d596bb51b
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="locks-event-category"></a>잠금 이벤트 범주
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
**Locks** 이벤트 범주의 이벤트 클래스를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에서 잠금 작업을 모니터링합니다. 이러한 이벤트 클래스를 사용하면 여러 사용자들이 동시에 데이터를 읽고 수정하여 발생되는 잠금 문제를 조사할 수 있습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 종종 많은 수의 잠금을 처리하기 때문에 추적하는 동안 **Locks** 이벤트 클래스를 캡처하면 오버헤드가 증가하고 추적 파일이나 테이블도 많아집니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[Deadlock Graph 이벤트 클래스](../../relational-databases/event-classes/deadlock-graph-event-class.md)|교착 상태에 대한 XML 설명을 제공합니다.|  
|[Lock:Acquired 이벤트 클래스](../../relational-databases/event-classes/lock-acquired-event-class.md)|테이블의 행과 같은 리소스에 대해 잠금을 획득했음을 나타냅니다.|  
|[Lock:Cancel 이벤트 클래스](../../relational-databases/event-classes/lock-cancel-event-class.md)|교착 상태 등을 방지하기 위해 잠금을 획득하기 전에 취소된 잠금 요청을 추적합니다.|  
|[Lock:Deadlock Chain 이벤트 클래스](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|교착 상태 조건이 발생한 시기 및 관련 개체를 모니터링합니다.|  
|[Lock:Deadlock 이벤트 클래스](../../relational-databases/event-classes/lock-deadlock-event-class.md)|다른 트랜잭션에 의해 이미 잠겨 있는 리소스에 대해 트랜잭션이 잠금을 요청하여 교착 상태가 발생한 시기를 추적합니다.|  
|[Lock:Escalation 이벤트 클래스](../../relational-databases/event-classes/lock-escalation-event-class.md)|미세 잠금이 성긴 잠금으로 변환되었음을 나타냅니다.|  
|[Lock:Released 이벤트 클래스](../../relational-databases/event-classes/lock-released-event-class.md)|잠금이 해제된 시기를 추적합니다.|  
|[Lock:Timeout&#40;timeout &#62; 0&#41; 이벤트 클래스](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|요청된 리소스에 대한 다른 트랜잭션의 차단 잠금 때문에 잠금 요청을 완료할 수 없는 시기를 추적합니다. 이 이벤트는 잠금 제한 시간 값이 0보다 큰 경우에만 발생합니다.|  
|[Lock:Timeout 이벤트 클래스](../../relational-databases/event-classes/lock-timeout-event-class.md)|요청된 리소스에 대한 다른 트랜잭션의 차단 잠금 때문에 잠금 요청을 완료할 수 없는 시기를 추적합니다.|  
  
  
