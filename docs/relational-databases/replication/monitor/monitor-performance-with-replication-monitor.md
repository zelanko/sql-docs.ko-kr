---
title: "복제 모니터로 성능 모니터링 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Log Reader Agent, monitoring
- Replication Monitor, performance
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication]
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae1be084b689f760b6d10db4d7d975b0489048f7
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="monitor-performance-with-replication-monitor"></a>복제 모니터로 성능 모니터링
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터를 사용하여 다음 방법으로 트랜잭션 복제 및 병합 복제의 성능을 모니터링할 수 있습니다.  
  
-   경고 및 임계값 설정  
  
-   성능 측정값 보기  
  
-   추적 프로그램 토큰으로 대기 시간 확인(트랜잭션 복제)  
  
-   자세한 동기화 통계 보기(병합 복제)  
  
-   트랜잭션 및 배달 시간 보기(트랜잭션 복제)  
  
## <a name="set-warnings-and-thresholds"></a>경고 및 임계값 설정  
 복제 모니터를 사용하여 다양한 성능 조건에 대한 경고를 설정할 수 있습니다. 경고를 활성화할 때는 임계값을 지정해야 합니다. 임계값에 도달하거나 임계값이 초과되면 우선 순위가 더 높은 문제점이 표시될 필요가 없는 한 구독과 구독이 동기화하는 게시에 대한 **상태** 열에 경고가 표시됩니다. 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 다음 성능 조건에 대한 경고를 설정할 수 있습니다.  
  
-   지정한 대기 시간(게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간의 시간 간격)이 초과된 경우  
  
     이 조건은 트랜잭션 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 상태가 **성능 심각**으로 표시됩니다.  
  
-   지정된 동기화 시간이 초과된 경우  
  
     이 조건은 병합 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 상태가 **장기 실행 트랜잭션 병합**으로 표시됩니다. 전화 접속과 LAN 연결에 대해 서로 다른 임계값을 지정할 수 있습니다.  
  
-   지정된 시간 내에 지정된 수의 행을 처리하지 못한 경우  
  
     이 조건은 병합 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 상태가 **성능 심각**으로 표시됩니다. 전화 접속과 LAN 연결에 대해 서로 다른 임계값을 지정할 수 있습니다.  
  
 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
  
## <a name="view-performance-measurements"></a>성능 측정값 보기  
 복제 모니터는 게시에 대해서는 **현재 평균 성능** 및 **현재 가장 낮은 성능** 열에, 구독에 대해서는 **성능** 열에 트랜잭션 복제 및 병합 복제에 대한 성능 품질 값을 표시합니다. 값은 다음과 같습니다.  
  
-   최고  
  
-   좋음  
  
-   보통  
  
-   나쁨  
  
-   중요(트랜잭션 복제만)  
  
 값은 다음과 같은 방법으로 결정됩니다.  
  
-   트랜잭션 복제의 경우 성능 품질은 대기 시간 임계값으로 결정됩니다. 임계값을 설정하지 않으면 값이 표시되지 않습니다. 다음 표에서는 임계값과 성능 품질 값의 상관 관계를 나타냅니다. 예를 들어 임계값이 60초로 설정되고 실제 대기 시간이 30초이면 대기 시간은 임계값의 50%이므로 값은 좋음이 됩니다.  
  
    |최고|좋음|보통|나쁨|심각|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   병합 복제의 경우 성능 품질은 임계값과 관련이 없습니다. 행 처리 임계값은 **성능 심각** 값이 **상태** 열에 표시되는지 여부를 확인합니다. 성능 품질은 개별 구독 성능과 게시에 대한 구독(연결 유형이 전화 접속 또는 LAN 등으로 동일한 구독)의 평균 기록 성능을 비교하여 결정됩니다. 복제 모니터는 같은 유형의 연결별로 50개 이상의 변경 사항을 5번 동기화한 후에 값을 표시합니다. 50개 이상 변경 내용이 포함된 동기화가 5회 미만이거나 최신 동기화의 변경 내용 수가 50개 미만이면 복제 모니터에서 값을 표시하지 않습니다.  
  
     다음 표에서는 평균 성능과 성능 품질 값의 상관 관계를 나타냅니다. 예를 들어 LAN 연결에서 10개의 구독자가 초당 100개 행을 처리하는 평균 속도로 동기화하고 구독 중 하나가 초당 125개 행을 처리하는 속도로 동기화하는 경우 해당 구독자의 동기화 성능은 평균 125%가 되어 값은 좋음이 됩니다.  
  
    |최고|좋음|보통|나쁨|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 구독 정보를 표시하는 방법에 대한 자세한 내용은 [구독에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)을 참조하세요.  
  
## <a name="determine-latency-with-tracer-tokens"></a>추적 프로그램 토큰으로 대기 시간 결정  
 트랜잭션 복제를 사용하면 게시 데이터베이스의 트랜잭션 로그에 토큰(소량 데이터)을 삽입하고 배포자 및 구독자에 트랜잭션 로그가 전달되는 시간을 기록하여 시스템의 대기 시간을 측정할 수 있습니다. 또한 데이터가 배포자나 구독자에 도달하지 않았는지 여부를 확인하는 데도 토큰을 사용할 수 있습니다. 자세한 내용은 [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)을 참조하세요.  
  
## <a name="view-detailed-synchronization-performance-for-merge-replication"></a>병합 복제에 대한 자세한 동기화 성능 보기  
 병합 복제의 경우 복제 모니터는 각 처리 단계(변경 내용 업로드, 변경 내용 다운로드 등)에 소요된 시간을 포함하여 동기화 중에 처리된 각 아티클에 대한 자세한 통계를 표시합니다. 이 통계는 속도 저하의 원인이 되고 병합 구독의 성능 문제를 해결하기에 가장 적합한 특정 테이블을 정확히 찾아내는 데 도움이 될 수 있습니다. 자세한 통계를 보는 방법은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
## <a name="view-transactions-and-delivery-time-for-transactional-replication"></a>트랜잭션 복제에 대한 트랜잭션 및 배달 시간 보기  
 트랜잭션 복제의 경우 복제 모니터는 구독자로 아직 배포되지 않은 배포 데이터베이스의 트랜잭션 수와 이러한 트랜잭션에 대한 예상 배포 시간에 대한 정보를 표시합니다. 자세한 내용은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
