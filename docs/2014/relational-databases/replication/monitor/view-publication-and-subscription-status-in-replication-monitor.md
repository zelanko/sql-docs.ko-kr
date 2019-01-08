---
title: 복제 모니터에서 게시 및 구독 상태 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, monitoring
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- publications [SQL Server replication], viewing information
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication], publication status
- monitoring performance [SQL Server replication], subscription status
- subscriptions [SQL Server replication], viewing status
- Replication Monitor, publication and subscription status
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95fbb61460c23ca0fedf0baec71aa21acaa50398
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786745"
---
# <a name="view-publication-and-subscription-status-in-replication-monitor"></a>복제 모니터에서 게시 및 구독 상태 보기
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터에는 게시와 구독에 대한 상태 정보가 표시됩니다.  
  
-   게시 상태는 해당 구독의 가장 높은 우선 순위 상태에 의해 결정됩니다. 예를 들어 게시에 대한 특정 구독에 오류가 있고 다른 구독에 성능 문제가 있으면 해당 게시에 대해 오류 상태가 표시됩니다.  
  
-   구독 상태는 해당 구독을 처리하는 에이전트의 상태에 의해 결정됩니다. 병합 복제의 경우 병합 에이전트가 상태를 결정합니다. 트랜잭션 복제의 경우 로그 판독기 에이전트나 배포 에이전트가 상태를 결정하며 우선 순위가 높은 상태가 표시됩니다. 지연 업데이트 구독을 사용하는 경우 큐 판독기 에이전트에 의해 상태가 결정될 수도 있습니다. 스냅숏 복제의 경우 스냅숏 에이전트나 배포 에이전트가 상태를 결정하며 우선 순위가 높은 상태가 표시됩니다.  
  
 다음 섹션의 표에서는 게시와 구독에 사용 가능한 상태 값을 나열합니다. 다음 3가지 상태 값은 임계값에 도달하거나 초과한 경우에만 표시됩니다.  
  
-   구독 만료  
  
     이 상태 값은 모든 유형의 복제에 적용됩니다. 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
  
-   성능 심각  
  
     이 상태 값은 트랜잭션 복제와 병합 복제에 적용됩니다. 자세한 내용은 [복제 모니터로 성능 모니터링](monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
-   장기 실행 트랜잭션 병합  
  
     이 상태 값은 병합 복제에 적용됩니다. 자세한 내용은 [복제 모니터로 성능 모니터링](monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
 게시 및 구독 상태 외에도 병합 복제는 아티클 수준의 통계를 제공합니다. 이 통계를 사용하여 병합 단계가 완료되기까지 남은 시간, 지정된 아티클 처리에 소요된 시간, 구독자가 사용 중인 연결 유형 및 기타 중요한 정보를 확인할 수 있습니다. 이 통계는 복제 모니터의 병합 에이전트 창에 표시됩니다. 스냅숏 및 트랜잭션 복제는 배포 에이전트 처리에 대한 자세한 정보를 제공합니다.  
  
 **게시 및 구독 상태를 보려면**  
  
-   복제 모니터: [정보 보기 및 게시에 대 한 작업을 수행 &#40;복제 모니터&#41; ](view-information-and-perform-tasks-for-a-publication-replication-monitor.md) 하 고 [정보 보기 및 구독에 대 한 작업을 수행할 &#40;복제 모니터&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
  
 **에이전트에 대한 자세한 정보를 보려면**  
  
-   복제 모니터: [정보 보기 및 게시 관련 에이전트에 대 한 작업을 수행 &#40;복제 모니터&#41; ](view-information-and-perform-tasks-for-publication-agents.md) 하 고 [정보를 확인 하 고 구독 관련 에이전트에 대 한 작업을 수행할 &#40;복제 모니터&#41;](view-information-and-perform-tasks-for-subscription-agents.md)합니다.  
  
## <a name="publication-status-values"></a>게시 상태 값  
 다음 표에서는 게시 상태 값과 해당 아이콘을 우선 순위순으로 보여 줍니다.  
  
|상태|아이콘|  
|------------|----------|  
|Error|![UI 아이콘: 오류](../media/repl-icon-error.gif "UI icon: error")|  
|성능 심각|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|실패한 명령 다시 시도 중|![UI 아이콘: 복제 에이전트 다시 시도](../media/repl-icon-retry.gif "UI icon: replication agent retry")|  
|확인|none|  
  
## <a name="subscription-status-values"></a>구독 상태 값  
 다음 표에서는 구독 상태 값과 해당 아이콘을 우선 순위순으로 보여 줍니다. 한 구독이 동시에 두 가지 상태에 있을 수 있습니다(예: **곧 만료됨/만료됨** 및 **실패한 명령 다시 시도 중**). 이 경우 우선 순위가 가장 높은 상태가 표시됩니다.  
  
 **성능 심각**, **곧 만료됨/만료됨**및 **초기화되지 않음** 의 상태 값은 경고입니다. 경고를 표시할 때 복제 모니터는 에이전트가 실행되고 있는지 여부도 표시합니다. 예를 들어 상태가 **실행 중, 성능 심각**과 같이 표시될 수 있습니다.  
  
### <a name="transactional-subscriptions"></a>트랜잭션 구독  
  
|상태|아이콘|  
|------------|----------|  
|Error|![UI 아이콘: 오류](../media/repl-icon-error.gif "UI icon: error")|  
|성능 심각|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|곧 만료됨/만료됨|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|초기화되지 않은 구독|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|실패한 명령 다시 시도 중|![UI 아이콘: 복제 에이전트 다시 시도](../media/repl-icon-retry.gif "UI icon: replication agent retry")|  
|실행 중이 아님|![UI 아이콘: 복제 에이전트 중지됨](../media/repl-icon-stopped.gif "UI icon: replication agent stopped")|  
|실행 중|![UI 아이콘: 복제 에이전트 실행 중](../media/repl-icon-running.gif "UI icon: replication agent running")|  
  
### <a name="merge-subscriptions"></a>병합 구독  
  
|상태|아이콘|  
|------------|----------|  
|Error|![UI 아이콘: 오류](../media/repl-icon-error.gif "UI icon: error")|  
|성능 심각|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|장기 실행 트랜잭션 병합|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|곧 만료됨/만료됨|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|초기화되지 않은 구독|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|실패한 명령 다시 시도 중|![UI 아이콘: 복제 에이전트 다시 시도](../media/repl-icon-retry.gif "UI icon: replication agent retry")|  
|동기화 중|![UI 아이콘: 복제 에이전트 실행 중](../media/repl-icon-running.gif "UI icon: replication agent running")|  
|비동기화 중|![UI 아이콘: 복제 에이전트 중지됨](../media/repl-icon-stopped.gif "UI icon: replication agent stopped")|  
  
### <a name="snapshot-subscriptions"></a>스냅숏 구독  
  
|상태|아이콘|  
|------------|----------|  
|Error|![UI 아이콘: 오류](../media/repl-icon-error.gif "UI icon: error")|  
|곧 만료됨/만료됨|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|초기화되지 않은 구독|![UI 아이콘: 경고](../media/repl-icon-warn.gif "UI icon: warning")|  
|실패한 명령 다시 시도 중|![UI 아이콘: 복제 에이전트 다시 시도](../media/repl-icon-retry.gif "UI icon: replication agent retry")|  
|동기화 중|![UI 아이콘: 복제 에이전트 실행 중](../media/repl-icon-running.gif "UI icon: replication agent running")|  
|비동기화 중|![UI 아이콘: 복제 에이전트 중지됨](../media/repl-icon-stopped.gif "UI icon: replication agent stopped")|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 모니터링](../monitoring-replication.md)  
  
  
