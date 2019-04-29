---
title: 게시 정보, 모든 구독(스냅숏 게시) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.allsubscriptions.snapshot.f1
ms.assetid: 7ce656c2-6e60-4625-8955-1daff641070c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3665647e89c03b75230acf58d2f5193fceefe878
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63021822"
---
# <a name="publication-information-all-subscriptions-snapshot-publication"></a>게시 정보, 모든 구독(스냅숏 게시)
  **모든 구독** 탭은 선택한 스냅숏 게시의 모든 구독에 대한 정보를 표시합니다.  
  
## <a name="options"></a>변수  
 자세한 내용 및 구독과 관련된 태스크를 보려면 해당 구독에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대 한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **표시**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 선택한 구독 유형에 대해 표시할 구독 상태를 선택합니다. 예를 들어 오류가 있는 구독만 표시하도록 선택할 수 있습니다.  
  
 **상태**  
 스냅숏 에이전트 또는 배포 에이전트의 상태에 따라 결정되는 각 구독의 상태입니다. 우선 순위가 높은 상태가 표시됩니다.  
  
 기본적으로 구독 정보가 포함된 표는 **상태** 열을 기준으로 정렬됩니다. 다음 목록에서는 가능한 상태 값 및 값 정렬 순서를 보여 줍니다. 예를 들어 오류는 항상 표의 맨 위에 표시됩니다.  
  
-   Error  
  
-   곧 만료됨/만료됨([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전만 해당)  
  
-   초기화되지 않은 구독([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당)  
  
-   실패한 명령 다시 시도 중  
  
-   동기화 중  
  
-   비동기화 중  
  
 정렬 순서는 지정한 구독의 상태가 두 가지 이상일 경우에 표시할 값도 결정합니다. 예를 들어 구독에 오류가 있고 곧 만료될 예정이면 **상태** 열에 **오류**가 표시됩니다.  
  
 **곧 만료됨/만료됨** 및 **초기화되지 않은 구독** 상태 값은 경고입니다. 경고를 표시할 때 **상태** 열은 에이전트가 실행 중인지 여부도 표시합니다. 예를 들어 상태가 **실행 중, 곧 만료됨/만료됨**과 같이 표시될 수 있습니다.  
  
 **곧 만료됨/만료됨** 상태 값은 임계값을 설정한 경우에만 표시됩니다. 임계값 설정에 대한 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
 **구독**  
 폼에서 각 구독의 이름: *SubscriberName: SubscriptionDatabaseName*입니다.  
  
 **마지막 동기화**  
 배포 에이전트가 마지막으로 실행된 시간입니다. 동기화가 진행 중인 경우 **진행 중** 이 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  
