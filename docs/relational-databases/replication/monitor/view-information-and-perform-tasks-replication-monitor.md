---
title: 정보 보기 및 작업 수행(복제 모니터)
description: SSMS(SQL Server Management Studio)에서 복제 모니터를 사용하여 정보를 확인하고 다양한 작업을 수행하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 3628c3a508aed473604bcc0b3f1d3d7f2b8e5264
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432304"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>복제 모니터를 사용하여 정보 보기 및 태스크 수행
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
복제 모니터는 정보를 보고 다양한 작업을 수행할 수 있는 여러 가지 탭과 옵션을 제공합니다. 이 아티클에서는 복제 모니터를 사용할 때 보고 수행할 수 있는 여러 가지 사항을 설명합니다. 


## <a name="for-a-publication"></a>게시의 경우

### <a name="view-information"></a>보기 정보
복제 모니터에는 선택한 게시에 대한 정보를 포함하는 다음과 같은 탭이 있습니다.  
  
-   **모든 구독** - 이 탭에는 선택한 게시에 대한 모든 구독 정보가 표시됩니다.  
  
-   **에이전트** - 이 탭에는 게시에 사용되는 모든 에이전트에 대한 정보가 표시됩니다.   
    -   스냅샷 에이전트 - 모든 게시에서 사용   
    -   로그 판독기 에이전트 - 모든 트랜잭션 게시에서 사용   
    -   큐 판독기 에이전트 - 지연 업데이트 구독이 있는 트랜잭션 게시에서 사용  
  
-   **경고** - 이 탭에서는 에이전트에 대한 경고를 지정할 수 있습니다.  
  
-   **추적 프로그램 토큰**(트랜잭션 복제에만 해당) - 이 탭에서는 대기 시간(게시자에서 커밋될 트랜잭션과 구독자에서 상응하는 커밋될 트랜잭션 사이에 경과된 시간)을 측정할 수 있습니다.  
  
 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 선택한 다음, 메뉴 모음에서 **도움말** 을 선택합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="perform-tasks"></a>작업 수행
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 게시자를 확장한 다음, 게시를 선택합니다.   
2.  게시 속성을 보고 수정하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음, **속성** 을 선택합니다.    
3.  구독에 대한 정보를 보려면 **모든 구독** 탭을 선택하고 구독을 마우스 오른쪽 단추로 클릭한 다음, **속성** 을 선택합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 
4.  에이전트에 대한 정보를 보려면 **에이전트** 탭을 선택합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 
5.  에이전트 경고 및 임계값에 대한 정보를 보려면 **경고** 탭을 선택합니다. 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
6.  추적 프로그램 토큰에 대한 정보를 보려면 **추적 프로그램 토큰** 탭을 선택합니다. 추적 프로그램 토큰 사용 방법은 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)를 참조하십시오.  
  
## <a name="for-a-publisher"></a>게시자의 경우 

### <a name="view-information"></a>보기 정보
복제 모니터는 선택한 게시자에 대한 정보를 표시하는 다음 탭을 제공합니다.   
-   **게시** - 선택한 게시자에 있는 모든 게시 정보가 표시됩니다.   
-   **구독 감시 목록** - 오류, 경고 또는 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독에 대한 정보가 표시됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다.    
-   **에이전트** 탭 - 모든 복제 유형에 사용되는 에이전트 및 작업에 대한 세부 정보가 표시됩니다. 이 탭에서는 각 에이전트 및 작업을 시작하고 중지할 수 있습니다. 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="perform-tasks"></a>작업 수행
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.   
2.  모든 게시에 대한 정보를 보려면 **게시** 탭을 클릭합니다.    
3.  구독에 대한 정보를 보려면 **구독 조사 목록** 탭을 클릭합니다. 다음과 같이 이 탭에서 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.   
    -   구독과 연결된 에이전트에 대한 자세한 내용을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기** 를 클릭합니다.    
    -   구독 속성을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.    
    -   밀어넣기 구독을 동기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작** 을 클릭합니다.   
    -   구독을 다시 초기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화** 를 클릭합니다.   
4.  에이전트에 대한 정보를 보려면 **에이전트** 탭을 클릭합니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.    
    -   에이전트에 대한 자세한 정보(예: 정보 메시지 및 오류 메시지)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기** 를 클릭합니다.  
    -   에이전트를 실행하는 작업에 대한 자세한 정보(예: 일정, 자세한 작업 단계 정보 등)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.    
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필** 을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.    
    -   실행 중이지 않은 에이전트를 시작하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 시작** 을 클릭합니다.  
    -   실행 중인 에이전트를 중지하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 중지** 를 클릭합니다.  


## <a name="for-a-subscription"></a>구독의 경우 

### <a name="view-information"></a>보기 정보
  복제 모니터는 구독에 대한 정보가 들어 있는 다음 탭을 제공합니다.    
-   **모든 구독** - 선택한 게시에 대한 모든 구독 정보가 표시됩니다.   
-   **구독 감시 목록** - 오류, 경고 또는 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독에 대한 정보가 표시됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다. 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="perform-tasks"></a>작업 수행
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.   
2.  구독에 대한 정보를 보려면 **모든 구독** 탭을 클릭합니다. '동기화 중'과 같은 특정 상태에 있는 구독만 보려면 **표시** 드롭다운 목록에서 옵션을 선택합니다.    
3.  구독 속성을 보고 수정하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>구독 조사 목록 탭의 구독에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.    
2.  구독에 대한 정보를 보려면 **구독 조사 목록** 탭을 클릭합니다.    
3.  **\<SubscriptionType>구독 표시** 드롭다운 목록에서 표시할 구독 유형을 선택합니다. '동기화 중'과 같은 특정 상태에 있는 구독만 보려면 **표시** 드롭다운 목록에서 옵션을 선택합니다.    
4.  구독 속성을 보고 수정하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다. 이 탭에서 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다. 
  
  
## <a name="for-publication-agents"></a>게시 에이전트의 경우
복제 모니터에는 선택한 게시와 연결된 에이전트에 대한 정보가 포함된 **에이전트** 탭이 있습니다. 배포 에이전트와 병합 에이전트는 구독과 연결되어 있습니다. 
  
### <a name="view-information"></a>보기 정보
 이 탭에는 다음 에이전트에 대한 정보가 표시됩니다.  
  
-   스냅샷 에이전트 - 모든 게시에서 사용  
-   로그 판독기 에이전트 - 모든 트랜잭션 게시에서 사용  
-   큐 판독기 에이전트 - 지연 업데이트 구독이 활성화된 트랜잭션 게시에서 사용 
  
 이 탭의 옵션에 대한 자세한 내용을 보려면 메뉴 모음의 **도움말** 을 클릭하세요. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>게시와 연결된 에이전트에 대한 정보를 보고 태스크를 수행하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.    
2.  **에이전트** 탭을 클릭하여 에이전트에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.    
    -   에이전트에 대한 자세한 정보(예: 정보 메시지 및 오류 메시지)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기** 를 클릭합니다.  
    -   에이전트를 실행하는 작업에 대한 자세한 정보(예: 일정, 자세한 작업 단계 정보 등)를 보려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.    
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필** 을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.   
    -   실행 중이지 않은 에이전트를 시작하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 시작** 을 클릭합니다.   
    -   실행 중인 에이전트를 중지하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 중지** 를 클릭합니다.  
  
## <a name="for-subscription-agents"></a>구독 에이전트의 경우

### <a name="view-information"></a>보기 정보
-   **모든 구독** - 선택한 게시에 대한 모든 구독 정보가 표시됩니다.  
  
-   **구독 감시 목록** - 오류, 경고 또는 성능이 가장 낮은 선택된 게시자에서 사용 가능한 모든 게시의 구독 정보를 표시하기 위한 것입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전 버전을 실행하는 배포자의 경우 이 탭이 표시되지 않습니다. 각 탭의 옵션에 대한 자세한 내용을 보려면 오른쪽 창에서 해당 탭을 클릭한 다음 메뉴 모음에서 **도움말** 을 클릭합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="perform-tasks"></a>작업 수행
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.    
2.  **모든 구독** 탭을 클릭하여 구독에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.   
    -   구독과 연결된 에이전트에 대한 자세한 내용을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기** 를 클릭합니다. 자세한 정보에는 에이전트 기록과 오류 메시지, 트랜잭션 복제에 대한 성능 통계 및 병합 복제에 대한 아티클 수준의 동기화 통계가 포함됩니다.  
  
         시작된 세부 정보 창의 탭은 구독 유형에 따라 다릅니다. 스냅샷 구독의 경우 **배포자에서 구독자로의 연결 기록** 탭이고, 트랜잭션 구독의 경우 **게시자에서 배포자로의 연결 기록** 탭, **배포자에서 구독자로의 연결 기록** 탭 및 **배포되지 않은 명령** 탭이고, 병합 구독의 경우 **동기화 기록** 탭입니다.  
  
    -   밀어넣기 구독을 동기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작** 을 클릭합니다.    
    -   구독을 다시 초기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화** 를 클릭합니다.    
    -   단일 병합 구독의 유효성을 검사하려면 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사** 를 클릭합니다. 병합 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사** 를 클릭합니다. 트랜잭션 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사** 를 클릭합니다.    
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필** 을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.  
  
### <a name="subscription-watch-list-tab"></a>구독 조사 목록 탭 
  
1.  왼쪽 창에서 게시자 그룹을 확장한 다음 해당 게시자를 클릭합니다.    
2.  **구독 조사 목록** 탭을 클릭하여 구독에 대한 정보를 봅니다. 이 탭에서 다음과 같이 보다 자세한 정보에 액세스하고 태스크를 수행할 수도 있습니다.   
    -   구독과 연결된 에이전트에 대한 자세한 내용을 보려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기** 를 클릭합니다. 자세한 정보에는 에이전트 기록과 오류 메시지, 트랜잭션 복제에 대한 성능 통계 및 병합 복제에 대한 아티클 수준의 동기화 통계가 포함됩니다.    
         시작된 세부 정보 창의 탭은 구독 유형에 따라 다릅니다. 스냅샷 구독의 경우 **배포자에서 구독자로의 연결 기록** 탭이고, 트랜잭션 구독의 경우 **게시자에서 배포자로의 연결 기록** 탭, **배포자에서 구독자로의 연결 기록** 탭 및 **성능** 탭이고, 병합 구독의 경우 **동기화 기록** 탭입니다.  
  
    -   밀어넣기 구독을 동기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작** 을 클릭합니다.    
    -   구독을 다시 초기화하려면 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 다시 초기화** 를 클릭합니다.    
    -   단일 병합 구독의 유효성을 검사하려면 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사** 를 클릭합니다. 병합 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사** 를 클릭합니다. 트랜잭션 게시에 대한 모든 구독의 유효성을 검사하려면 해당 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사** 를 클릭합니다.    
    -   에이전트에 대한 프로필을 관리하려면 에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필** 을 클릭합니다. 자세한 내용은 [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)을 참조하세요.  

    


## <a name="see-also"></a>참고 항목  
 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [끌어오기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
 [복제 모니터에 임계값 및 경고 설정](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)    
  
  
