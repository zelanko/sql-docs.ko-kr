---
title: 동기화 일정 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9bfbb62c58efea29df26cb9fc6e632bc4e2b3642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62630802"
---
# <a name="specify-synchronization-schedules"></a>동기화 일정 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 동기화 일정을 지정하는 방법에 대해 설명합니다. 구독을 만드는 경우 구독에 대한 복제 에이전트를 실행하는 시기를 제어하는 동기화 일정을 정의할 수 있습니다. 일정 매개 변수를 지정하지 않으면 기본 일정이 사용됩니다.  
  
 구독은 배포 에이전트(스냅샷 및 트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)에 의해 동기화됩니다. 에이전트는 지속적으로 실행하거나 수요에 따라 실행하거나 일정에 따라 실행할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 동기화 일정을 지정하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 구독 마법사의 **동기화 일정** 페이지에서 동기화 일정을 지정합니다. 이 마법사의 액세스 방법은 [Create a Push Subscription](create-a-push-subscription.md) 및 [Create a Pull Subscription](create-a-pull-subscription.md)를 참조하세요.  
  
 **작업 일정 속성** 대화 상자에서 동기화 일정을 수정합니다. 이 대화 상자는 **의** 작업 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 폴더와 복제 모니터의 에이전트 세부 정보 창에서 사용할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](monitor/start-the-replication-monitor.md)을 참조하세요.  
  
 **작업** 폴더에서 일정을 지정하는 경우에는 다음 표를 사용하여 에이전트 작업 이름을 결정합니다.  
  
|에이전트|작업 이름|  
|-----------|--------------|  
|끌어오기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|밀어넣기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>** <sup>1</sup>|  
|끌어오기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>** <sup>2</sup>|  
|SQL Server 이외 구독자의 밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
  
 <sup>1</sup> Oracle 게시에서 밀어넣기 구독의 경우 **\<Publisher>-\<PublicationDatabase>** 가 아닌 **\<Publisher>-\<Publisher**>입니다.  
  
 <sup>2</sup> Oracle 게시에서 끌어오기 구독에 대한 작업 이름은 **\<Publisher>-\<PublicationDatabase>** 가 아닌 **\<Publisher>-\<DistributionDatabase**>입니다.  
  
#### <a name="to-specify-synchronization-schedules"></a>동기화 일정을 지정하려면  
  
1.  새 구독 마법사의 **SynchronizationSchedule** 페이지에 있는 **에이전트 일정** 드롭다운 목록에서 만들려는 각 구독에 대해 다음 값 중 하나를 선택합니다.  
  
    -   **계속 실행**  
  
    -   **요청 시에만 실행**  
  
    -   **\<일정 정의...>**  
  
2.  **\<일정 정의...>** 를 선택하면 **작업 일정 속성** 대화 상자에서 일정을 지정한 다음, **확인**을 클릭합니다.  
  
3.  마법사를 완료합니다.  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>복제 모니터에서 밀어넣기 구독에 대한 동기화 일정을 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
4.  에 **구독 \< SubscriptionName >** 창 클릭 **동작**를 클릭 하 고  **\<AgentName > 작업 속성**합니다.  
  
5.  **작업 속성 - \<JobName>** 대화 상자의 **일정** 페이지에서 **편집**을 클릭합니다.  
  
6.  **작업 일정 속성** 대화 상자의 **일정 유형** 드롭다운 목록에서 값을 선택합니다.  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
7.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>Management Studio에서 밀어넣기 구독에 대한 동기화 일정을 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  구독과 연결된 배포 에이전트 또는 병합 에이전트의 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<JobName>** 대화 상자의 **일정** 페이지에서 **편집**을 클릭합니다.  
  
5.  **작업 일정 속성** 대화 상자의 **일정 유형** 드롭다운 목록에서 값을 선택합니다.  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
6.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>Management Studio에서 끌어오기 구독에 대한 동기화 일정을 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  구독과 연결된 배포 에이전트 또는 병합 에이전트의 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<JobName>** 대화 상자의 **일정** 페이지에서 **편집**을 클릭합니다.  
  
5.  **작업 일정 속성** 대화 상자의 **일정 유형** 드롭다운 목록에서 값을 선택합니다.  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
6.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 동기화 일정을 정의할 수 있습니다. 사용되는 저장 프로시저는 복제 유형 및 구독 유형(끌어오기 또는 밀어넣기)에 따라 달라집니다.  
  
 일정은 다음 일정 매개 변수로 정의되며 해당 동작은 [sp_add_schedule&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)에서 상속됩니다.  
  
-   **@frequency_type** - 에이전트를 예약할 때 사용하는 빈도 유형  
  
-   **@frequency_interval** - 에이전트에서 작업을 실행하는 요일  
  
-   **@frequency_relative_interval** - 지정된 월에서 에이전트가 월별로 실행되도록 예약된 주입니다.  
  
-   **@frequency_recurrence_factor** - 동기화 사이에 발생하는 frequency-type 단위 수입니다.  
  
-   **@frequency_subday** - 에이전트가 하루에 두 번 이상 실행할 경우 빈도 단위입니다.  
  
-   **@frequency_subday_interval** - 에이전트가 하루에 두 번 이상 실행할 경우 실행 간의 빈도 단위 수입니다.  
  
-   **@active_start_time_of_day** - 지정된 날짜에서 에이전트가 실행되는 시작 시간  
  
-   **@active_end_time_of_day** - 지정된 날짜에서 에이전트가 실행되는 마지막 시간  
  
-   **@active_start_date** - 에이전트 예약이 처음 적용되는 날짜  
  
-   **@active_end_date** - 에이전트 예약이 마지막으로 적용되는 날짜  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독의 동기화 일정을 정의하려면  
  
1.  트랜잭션 게시에 대한 새 끌어오기 구독을 만듭니다. 자세한 내용은 [끌어오기 구독 만들기](create-a-pull-subscription.md)를 참조하세요.  
  
2.  구독자에서 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. **@publisher** , **@publisher_db** , **@publication** 와 **@job_name** 및 **@password** 에 대해 구독자에서 배포 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명을 지정합니다. 구독을 동기화하는 배포 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독의 동기화 일정을 정의하려면  
  
1.  트랜잭션 게시에 대한 새 밀어넣기 구독을 만듭니다. 자세한 내용은 [밀어넣기 구독 만들기](create-a-push-subscription.md)을 참조하세요.  
  
2.  구독자에서 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)를 실행합니다. **@subscriber** , **@subscriber_db** , **@publication** 와 **@job_name** 및 **@password** 에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 구독을 동기화하는 배포 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독의 동기화 일정을 정의하려면  
  
1.  병합 게시에 대한 새 끌어오기 구독을 만듭니다. 자세한 내용은 [끌어오기 구독 만들기](create-a-pull-subscription.md)를 참조하세요.  
  
2.  구독자에서 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. **@publisher** , **@publisher_db** , **@publication** 와 **@job_name** 및 **@password** 에 대해 구독자에서 병합 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 구독을 동기화하는 병합 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독의 동기화 일정을 정의하려면  
  
1.  병합 게시에 대한 새 밀어넣기 구독을 만듭니다. 자세한 내용은 [밀어넣기 구독 만들기](create-a-push-subscription.md)을 참조하세요.  
  
2.  구독자에서 [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)를 실행합니다. **@subscriber** , **@subscriber_db** , **@publication** 와 **@job_name** 및 **@password** 에 대해 구독자에서 병합 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 구독을 동기화하는 병합 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 복제에서는 SQL Server 에이전트를 사용하여 스냅샷 생성이나 구독 동기화와 같이 정기적으로 수행하는 작업의 일정을 지정합니다. RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 복제 에이전트 작업의 일정을 지정할 수 있습니다.  
  
> [!NOTE]  
>  구독을 만들고 `false`에 `CreateSyncAgentByDefault` 값을 지정하면(끌어오기 구독에 대한 기본 동작) 에이전트 작업은 생성되지 않으며 일정 속성은 무시됩니다. 이 경우에는 애플리케이션에서 동기화 일정을 결정해야 합니다. 자세한 내용은 [Create a Pull Subscription](create-a-pull-subscription.md) 및 [Create a Push Subscription](create-a-push-subscription.md)를 참조하세요.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  만들려는 구독에 대해 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스의 인스턴스를 만듭니다. 자세한 내용은 [Create a Push Subscription](create-a-push-subscription.md)을 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>를 호출하기 전에 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 속성의 다음 필드 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 에이전트를 예약할 때 사용하는 빈도 유형(예: 매일 또는 매주)입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 에이전트가 실행하는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 지정된 월에서 에이전트가 월별로 실행되도록 예약된 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 동기화 사이에 발생하는 frequency-type 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 지정된 날짜에서 에이전트가 실행되는 시작 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 지정된 날짜에서 에이전트가 실행되는 마지막 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 에이전트 예약이 처음 적용되는 날짜입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 에이전트 예약이 마지막으로 적용되는 날짜입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출하여 구독을 만듭니다.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  만들려는 구독에 대해 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만듭니다. 자세한 내용은 [끌어오기 구독 만들기](create-a-pull-subscription.md)를 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>를 호출하기 전에 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 속성의 다음 필드 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 에이전트를 예약할 때 사용하는 빈도 유형(예: 매일 또는 매주)입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 에이전트가 실행하는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 지정된 월에서 에이전트가 월별로 실행되도록 예약된 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 동기화 사이에 발생하는 frequency-type 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 지정된 날짜에서 에이전트가 실행되는 시작 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 지정된 날짜에서 에이전트가 실행되는 마지막 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 에이전트 예약이 처음 적용되는 날짜입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 에이전트 예약이 마지막으로 적용되는 날짜입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출하여 구독을 만듭니다.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  만들려는 구독에 대해 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만듭니다. 자세한 내용은 [끌어오기 구독 만들기](create-a-pull-subscription.md)를 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>를 호출하기 전에 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 속성의 다음 필드 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 에이전트를 예약할 때 사용하는 빈도 유형(예: 매일 또는 매주)입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 에이전트가 실행하는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 지정된 월에서 에이전트가 월별로 실행되도록 예약된 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 동기화 사이에 발생하는 frequency-type 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 지정된 날짜에서 에이전트가 실행되는 시작 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 지정된 날짜에서 에이전트가 실행되는 마지막 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 에이전트 예약이 처음 적용되는 날짜입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 에이전트 예약이 마지막으로 적용되는 날짜입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 메서드를 호출하여 구독을 만듭니다.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  만들려는 구독에 대해 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스의 인스턴스를 만듭니다. 자세한 내용은 [Create a Push Subscription](create-a-push-subscription.md)을 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>를 호출하기 전에 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 속성의 다음 필드 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 에이전트를 예약할 때 사용하는 빈도 유형(예: 매일 또는 매주)입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 에이전트가 실행하는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 지정된 월에서 에이전트가 월별로 실행되도록 예약된 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 동기화 사이에 발생하는 frequency-type 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 에이전트가 하루에 두 번 이상 실행할 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 지정된 날짜에서 에이전트가 실행되는 시작 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 지정된 날짜에서 에이전트가 실행되는 마지막 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 에이전트 예약이 처음 적용되는 날짜입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 에이전트 예약이 마지막으로 적용되는 날짜입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 메서드를 호출하여 구독을 만듭니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 병합 계시에 대한 밀어넣기 구독을 만들고 구독의 동기화 일정을 지정합니다.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>관련 항목  
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [밀어넣기 구독 동기화](synchronize-a-push-subscription.md)   
 [끌어오기 구독 동기화](synchronize-a-pull-subscription.md)   
 [데이터 동기화](synchronize-data.md)  
  
  
