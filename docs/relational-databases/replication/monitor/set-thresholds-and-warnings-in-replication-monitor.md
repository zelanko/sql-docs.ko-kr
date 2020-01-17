---
title: 임계값 및 경고 설정(복제 모니터)
description: SSMS(SQL Server Management Studio)에서 복제 모니터를 사용하여 복제에서 발생할 수 있는 다양한 상태에 경고를 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- Merge Agent, thresholds and warnings
- Distribution Agent, thresholds and warnings
- thresholds [SQL Server replication]
- Replication Monitor, thresholds and warnings
- monitoring performance [SQL Server replication], thresholds and warnings
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: bf3d9ba88f433619a79c9f4453823e81589b4ee3
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322285"
---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>복제 모니터에 임계값 및 경고 설정
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터에는 게시와 구독의 상태 정보가 표시됩니다. 기본적으로 복제 모니터는 초기화되지 않은 구독에 대해서만 경고를 표시하지만 다른 조건에 대한 경고를 활성화할 수 있습니다. 토폴로지에 대한 경고를 활성화하여 상태 및 성능 정보를 적시에 받아보는 것이 좋습니다.  
  
 경고를 활성화할 때는 임계값을 지정해야 합니다. 임계값에 도달하거나 임계값이 초과되면 우선 순위가 더 높은 문제점이 표시될 필요가 없는 한 경고가 표시됩니다. 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 다음 상황에 대해 경고를 설정할 수 있습니다.  
  
-   구독 만료가 임박한 경우  
  
     모든 복제 유형에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 구독 상태가 **곧 만료됨/만료됨**으로 표시됩니다.  
  
-   지정한 대기 시간(게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간의 시간 간격)이 초과된 경우  
  
     이 조건은 트랜잭션 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 구독 상태가 **성능 심각**으로 표시됩니다.  
  
-   지정된 동기화 시간이 초과된 경우  
  
     이 조건은 병합 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 상태가 **장기 실행 트랜잭션 병합**으로 표시됩니다. 전화 접속과 LAN 연결에 대해 서로 다른 임계값을 지정할 수 있습니다.  
  
-   지정된 시간 내에 지정된 수의 행을 처리하지 못한 경우  
  
     이 조건은 병합 복제에 적용됩니다. 지정한 임계값에 도달하거나 임계값을 초과하면 상태가 **성능 심각**으로 표시됩니다. 전화 접속과 LAN 연결에 대해 서로 다른 임계값을 지정할 수 있습니다.  
  
 **성능 심각** 및 **장기 실행 트랜잭션 병합** 경고에 대한 자세한 내용은 [복제 모니터로 성능 모니터링](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
 **항목 내용**  
  
-   [트랜잭션 게시에 대한 임계값 및 경고 설정](#Transactional)  
  
-   [병합 게시에 대한 임계값 및 경고 설정](#Merge)  
  
-   [스냅샷 게시에 대한 임계값 및 경고 설정](#Snapshot)  
  
##  <a name="Transactional"></a> 트랜잭션 게시에 대한 임계값 및 경고를 설정하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **경고** 탭을 클릭합니다. 이 탭의 옵션에 대한 자세한 내용을 보려면 메뉴 모음의 **도움말** 을 클릭하세요.  
  
3.  다음 중 해당 확인란을 선택하여 경고를 설정합니다. **구독이 임계값 내에 만료되는 경우 경고** 또는 **대기 시간이 임계값을 초과하는 경우 경고** 중 해당 사항을 선택하여 경고를 설정합니다.  
  
4.  **임계값** 열에서 경고에 대한 임계값을 설정합니다. 예를 들어 3단계에서 **대기 시간이 임계값을 초과하는 경우 경고** 를 선택한 경우 **임계값** 열에서 대기 시간에 대해 **60초** 를 선택할 수 있습니다.  
  
5.  **변경 내용 저장**을 클릭합니다.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>임계값에 대한 경고를 구성하려면  
  
1.  **경고 구성**을 클릭합니다.  
  
2.  **복제 경고 구성** 대화 상자에서 경고를 선택한 다음 **구성**을 클릭합니다.  
  
     이 대화 상자에 모니터링 임계값과 관련 없는 경고를 포함하여 모든 게시 유형에 대한 경고가 표시됩니다. 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
3.  **\<AlertName> 경고 속성** 대화 상자에서 다음과 같은 옵션을 설정합니다.  
  
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.  
  
    -   **응답** 페이지에서 전자 메일의 발송 여부 및/또는 작업의 실행 여부를 지정합니다.  
  
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **닫기**를 클릭합니다.  
  
##  <a name="Merge"></a> 병합 게시에 대한 임계값 및 경고 설정  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **경고** 탭을 클릭합니다. 이 탭의 옵션에 대한 자세한 내용을 보려면 메뉴 모음의 **도움말** 을 클릭하세요.  
  
3.  다음 중 해당 확인란을 선택하여 경고를 설정합니다.  
  
    -   **구독이 임계값 내에 만료되는 경우 경고**  
  
    -   **전화 접속 연결 시 병합 길이가 임계값을 초과하는 경우 경고**  
  
    -   **LAN 연결 시 병합 길이가 임계값을 초과하는 경우 경고**  
  
    -   **LAN 연결 시 초당 병합된 행이 임계값 미만인 경우 경고**  
  
    -   **전화 접속 연결 시 초당 병합된 행이 임계값 미만인 경우 경고**  
  
4.  **임계값** 열에 경고 임계값을 설정합니다. 예를 들어 3단계에서 **전화 접속 연결 시 병합 길이가 임계값을 초과하는 경우 경고** 를 선택한 경우 **임계값** 열에서 **10분** 을 선택할 수 있습니다.  
  
5.  **변경 내용 저장**을 클릭합니다.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>임계값에 대한 경고를 구성하려면  
  
1.  **경고 구성**을 클릭합니다.  
  
2.  **복제 경고 구성** 대화 상자에서 경고를 선택한 다음 **구성**을 클릭합니다.  
  
     이 대화 상자에 모니터링 임계값과 관련 없는 경고를 포함하여 모든 게시 유형에 대한 경고가 표시됩니다.  
  
3.  **\<AlertName> 경고 속성** 대화 상자에서 다음과 같은 옵션을 설정합니다.  
  
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.  
  
    -   **응답** 페이지에서 전자 메일의 발송 여부 및/또는 작업의 실행 여부를 지정합니다.  
  
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **닫기**를 클릭합니다.  
  
##  <a name="Snapshot"></a> 스냅샷 게시에 대한 임계값 및 경고 설정  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **경고** 탭을 클릭합니다. 이 탭의 옵션에 대한 자세한 내용을 보려면 최상위 메뉴의 **도움말** 을 클릭하세요.  
  
3.  **구독이 임계값 내에 만료되는 경우 경고**확인란을 선택하여 경고를 설정합니다.  
  
4.  **임계값** 열에서 경고에 대한 임계값을 설정합니다. 예를 들어 **임계값** 열에서 **70%** 를 선택할 수 있습니다.  
  
5.  **변경 내용 저장**을 클릭합니다.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>임계값에 대한 경고를 구성하려면  
  
1.  **경고 구성**을 클릭합니다.  
  
2.  **복제 경고 구성** 대화 상자에서 경고를 선택한 다음 **구성**을 클릭합니다.  
  
     이 대화 상자에 모니터링 임계값과 관련 없는 경고를 포함하여 모든 게시 유형에 대한 경고가 표시됩니다. 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
3.  **\<AlertName> 경고 속성** 대화 상자에서 다음과 같은 옵션을 설정합니다.  
  
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.  
  
    -   **응답** 페이지에서 전자 메일의 발송 여부 및/또는 작업의 실행 여부를 지정합니다.  
  
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **닫기**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
