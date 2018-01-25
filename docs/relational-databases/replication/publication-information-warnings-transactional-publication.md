---
title: "게시 정보, 경고(트랜잭션 게시) | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
caps.latest.revision: "30"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5319bf83a366c849c0a9f849dbe4d6cab1679080
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="publication-information-warnings-transactional-publication"></a>게시 정보, 경고(트랜잭션 게시)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **경고** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에서 사용할 수 있습니다. **경고** 탭을 사용하면 선택한 게시에 대해 다음 태스크를 수행할 수 있습니다.  
  
-   복제 모니터에 경고를 표시하도록 설정  
  
-   경고와 연결된 임계값 지정  
  
-   경고와 연결된 알림 신호 정의  
  
## <a name="warnings-thresholds-and-alerts"></a>경고, 임계값 및 알림 신호  
 기본적으로 복제 모니터는 초기화되지 않은 구독에 대해 경고를 표시합니다. **초기화되지 않은 구독** 상태는 구독 정보가 포함된 페이지의 **상태** 열에 경고로 표시됩니다. 트랜잭션 게시의 경우 다음과 같은 추가 조건을 경고로 처리할 것인지 여부를 지정할 수 있습니다.  
  
-   구독 만료가 임박한 경우  
  
     이 조건은 **구독이 임계값 내에 만료되는 경우 경고**옵션에 해당합니다. 지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **곧 만료됨/만료됨** 으로 표시됩니다.  
  
-   지정한 대기 시간, 즉 게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간의 시간 간격이 초과된 경우  
  
     이 조건은 **대기 시간이 임계값을 초과하는 경우 경고**옵션에 해당합니다. 지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **성능 심각** 으로 표시됩니다. 또한 임계값은 구독 정보가 포함된 페이지의 **성능** 열에 표시되는 성능 등급을 제공하는 데 사용됩니다. 성능 등급은 다음 값 중 하나입니다.  
  
    -   최고  
  
    -   좋음  
  
    -   보통  
  
    -   나쁨  
  
    -   심각  
  
 경고를 설정할 때는 임계값도 설정해야 합니다. 예를 들어 경고 **대기 시간이 임계값을 초과하는 경우 경고**를 설정하면 게시자에서 커밋 중인 트랜잭션과 구독자에서 커밋 중인 트랜잭션 간에 허용 가능한 시간을 선택해야 합니다.  
  
 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 알림 신호는 **경고 구성** 을 클릭하고 **복제 경고 구성** 대화 상자에서 정보를 제공하여 정의합니다.  
  
## <a name="options"></a>변수  
 **설정**  
 경고를 설정하고 임계값을 지정하려면 선택합니다.  
  
 **경고**  
 임계값과 연결된 경고에 대한 설명입니다.  
  
 **임계값**  
 임계값을 지정합니다.  
  
 **경고 구성**  
 **경고** 표에서 행을 선택하고 **경고 구성** 을 클릭하여 **복제 경고 구성** 대화 상자를 시작합니다. 이 대화 상자를 사용하면 선택한 임계값 및 경고와 연결된 알림 메시지를 정의할 수 있습니다.  
  
 **변경 내용 취소**  
 경고 및 임계값에 대한 모든 변경 내용을 취소하려면 클릭합니다.  
  
> [!NOTE]  
>  **변경 내용 취소** 를 클릭해도 **복제 경고 구성** 대화 상자에서 정의한 알림 신호에는 적용되지 않습니다.  
  
 **변경 내용 저장**  
 경고 및 임계값에 대한 모든 변경 내용을 저장하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [게시에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [복제 모니터에 임계값 및 경고 설정](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
