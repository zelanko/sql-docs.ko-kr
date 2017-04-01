---
title: "동기화 일정 지정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "구독 [SQL Server 복제], 동기화"
  - "동기화 일정 [SQL Server 복제]"
  - "동기화 [SQL Server 복제], 일정"
  - "복제 [SQL Server], 동기화"
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 동기화 일정 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 동기화 일정을 지정하는 방법에 대해 설명합니다. 구독을 만드는 경우 구독에 대한 복제 에이전트를 실행하는 시기를 제어하는 동기화 일정을 정의할 수 있습니다. 일정 매개 변수를 지정하지 않으면 기본 일정이 사용됩니다.  
  
 구독은 배포 에이전트(스냅숏 및 트랜잭션 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)에 의해 동기화됩니다. 에이전트는 지속적으로 실행하거나 수요에 따라 실행하거나 일정에 따라 실행할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 동기화 일정을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 구독 마법사의 **동기화 일정** 페이지에서 동기화 일정을 지정합니다. 이 마법사의 액세스 방법은 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) 및 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)를 참조하세요.  
  
 **작업 일정 속성** 대화 상자에서 동기화 일정을 수정합니다. 이 대화 상자는 **의** 작업 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 폴더와 복제 모니터의 에이전트 세부 정보 창에서 사용할 수 있습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
 **작업** 폴더에서 일정을 지정하는 경우에는 다음 표를 사용하여 에이전트 작업 이름을 결정합니다.  
  
|에이전트|작업 이름|  
|-----------|--------------|  
|끌어오기 구독에 대한 병합 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< SubscriptionDatabase>-\< 정수>**|  
|밀어넣기 구독에 대한 병합 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>**|  
|밀어넣기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>** <sup>1</sup>|  
|끌어오기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< SubscriptionDatabase>-\< GUID>** <sup>2</sup>|  
|SQL Server 이외 구독자의 밀어넣기 구독에 대한 배포 에이전트|**\< 게시자>-\< PublicationDatabase>-\< 게시>-\< 구독자>-\< 정수>**|  
  
 <sup>1</sup> 은 Oracle 게시에 밀어넣기 구독의 경우 **\< 게시자>-\< 게시자**> 보다는 **\< 게시자>-\< PublicationDatabase>**  
  
 <sup>2</sup> 는 Oracle 게시에 끌어오기 구독의 경우 **\< 게시자>-\< DistributionDatabase**> 보다는 **\< 게시자>-\< PublicationDatabase>**  
  
#### 동기화 일정을 지정하려면  
  
1.  에 **SynchronizationSchedule** 선택은 다음 값 중 하나에서 새 구독 마법사의 페이지는 **에이전트 일정** 만들려는 각 구독에 대 한 드롭 다운 목록:  
  
    -   **계속 실행**  
  
    -   **요청 시에만 실행**  
  
    -   **\<일정 정의...>**  
  
2.  선택 하는 경우 **\< 일정 정의... >**, 에서 일정을 지정한는 **작업 일정 속성** 대화 상자를 닫은 다음 **확인**합니다.  
  
3.  마법사를 완료합니다.  
  
#### 복제 모니터에서 밀어넣기 구독에 대한 동기화 일정을 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  구독을 마우스 오른쪽 단추로 누른 **세부 정보 보기**합니다.  
  
4.  에 **구독 \< SubscriptionName >** 창 클릭 **작업**, 를 클릭 하 고 **\< AgentName> 작업 속성**.  
  
5.  에 **일정** 의 페이지는 **작업 속성-\< JobName>** 대화 상자를 클릭 하 여 **편집 합니다.**  
  
6.  에 **작업 일정 속성** 대화 상자에서 값을 선택 된 **일정 유형** 드롭 다운 목록:  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
7.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Management Studio에서 밀어넣기 구독에 대한 동기화 일정을 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  구독과 연결 된 배포 에이전트 또는 병합 에이전트에 대 한 작업을 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
4.  에 **일정** 의 페이지는 **작업 속성-\< JobName>** 대화 상자를 클릭 하 여 **편집 합니다.**  
  
5.  에 **작업 일정 속성** 대화 상자에서 값을 선택 된 **일정 유형** 드롭 다운 목록:  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
6.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Management Studio에서 끌어오기 구독에 대한 동기화 일정을 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  구독과 연결 된 배포 에이전트 또는 병합 에이전트에 대 한 작업을 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
4.  에 **일정** 의 페이지는 **작업 속성-\< JobName>** 대화 상자를 클릭 하 여 **편집 합니다.**  
  
5.  에 **작업 일정 속성** 대화 상자에서 값을 선택 된 **일정 유형** 드롭 다운 목록:  
  
    -   에이전트가 계속 실행되도록 지정하려면 **SQL Server 에이전트가 시작될 때 자동으로 시작**을 선택합니다.  
  
    -   에이전트가 일정대로 실행되도록 지정하려면 **되풀이**를 선택합니다.  
  
    -   에이전트가 요청 시 실행되도록 지정하려면 **한 번**을 선택합니다.  
  
6.  **되풀이**를 선택할 경우에는 에이전트의 일정을 지정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 동기화 일정을 정의할 수 있습니다. 사용되는 저장 프로시저는 복제 유형 및 구독 유형(끌어오기 또는 밀어넣기)에 따라 달라집니다.  
  
 일정에서 해당 동작은 상속 된 다음 일정 매개 정의한 [sp_add_schedule (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** -에이전트를 예약할 때 사용 하는 빈도 유형입니다.  
  
-   **@frequency_interval** -에이전트를 실행할 때 요일입니다.  
  
-   **@frequency_relative_interval** -주 지정 된 월에서 에이전트가 월별로 실행 되도록 예약 됩니다.  
  
-   **@frequency_recurrence_factor** -동기화 사이 발생 하는 빈도 유형 단위 수입니다.  
  
-   **@frequency_subday** -에이전트가 하루에 한 번 이상 실행할 경우 빈도 단위입니다.  
  
-   **@frequency_subday_interval** -에이전트가 하루에 한 번 이상 실행 하는 경우 실행 간의 빈도 단위 수입니다.  
  
-   **@active_start_time_of_day** -에이전트가 실행 됩니다 시작 하는 경우 지정된 된 날에 가장 이른 시간입니다.  
  
-   **@active_end_time_of_day** -에이전트가 실행 됩니다 시작 하는 경우 지정된 된 날에 최신 시간입니다.  
  
-   **@active_start_date** -에이전트 예약이 적용 되어 첫 번째 날입니다.  
  
-   **@active_end_date** -마지막 날짜에 에이전트 일정 적용 됩니다.  
  
#### 트랜잭션 게시에 대한 끌어오기 구독의 동기화 일정을 정의하려면  
  
1.  트랜잭션 게시에 대한 새 끌어오기 구독을 만듭니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
2.  구독자에서 실행 [sp_addpullsubscription_agent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, **@publication**, 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명에 대 한 구독자에서 배포 에이전트가 실행 되는 **@job_name** 및 **@password**합니다. 구독을 동기화하는 배포 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### 트랜잭션 게시에 대한 밀어넣기 구독의 동기화 일정을 정의하려면  
  
1.  트랜잭션 게시에 대한 새 밀어넣기 구독을 만듭니다. 자세한 내용은 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
2.  구독자에서 실행 [sp_addpushsubscription_agent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)합니다. 지정 **@subscriber**, **@subscriber_db**, **@publication**, 및에 대 한 구독자에서 배포 에이전트가 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 구독을 동기화하는 배포 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### 병합 게시에 대한 끌어오기 구독의 동기화 일정을 정의하려면  
  
1.  병합 게시에 대한 새 끌어오기 구독을 만듭니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
2.  구독자에서 실행 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, **@publication**, 및에 대 한 구독자에서 병합 에이전트가 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 구독을 동기화하는 병합 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
#### 병합 게시에 대한 밀어넣기 구독의 동기화 일정을 정의하려면  
  
1.  병합 게시에 대한 새 밀어넣기 구독을 만듭니다. 자세한 내용은 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
2.  구독자에서 실행 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)합니다. 지정 **@subscriber**, **@subscriber_db**, **@publication**, 및에 대 한 구독자에서 병합 에이전트가 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 구독을 동기화하는 병합 에이전트 작업 일정을 정의하는 동기화 매개 변수(위에서 자세히 설명)를 지정합니다.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 복제에서는 SQL Server 에이전트를 사용하여 스냅숏 생성이나 구독 동기화와 같이 정기적으로 수행하는 작업의 일정을 지정합니다. RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 복제 에이전트 작업의 일정을 지정할 수 있습니다.  
  
> [!NOTE]  
>  구독을 만들 하 고 값을 지정 **false** 에 대 한 **CreateSyncAgentByDefault** (끌어오기 구독에 대 한 기본 동작) 에이전트 작업이 만들어지지 않으며 일정 속성은 무시 됩니다. 이 경우에는 응용 프로그램에서 동기화 일정을 결정해야 합니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 및 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)를 참조하세요.  
  
#### 트랜잭션 게시에 대한 밀어넣기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 만들려는 구독에 대 한 클래스입니다. 자세한 내용은 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
2.  호출 하기 전에 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, 의 다음 필드 중 하나 이상을 설정는 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 속성:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -에이전트를 예약할 때 사용 (예: 매일 또는 매주) 빈도의 유형입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -에이전트가 실행 되는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -주 지정 된 월에서 에이전트가 월별로 실행 되도록 예약 됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -동기화 사이 발생 하는 빈도 유형 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -에이전트가 하루에 한 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -에이전트가 하루에 한 번 이상 실행 하는 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에는 가장 빠른 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에 최신 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -에이전트 예약이 적용 되는 첫 번째 날입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -에이전트 예약이 적용 되는 마지막 날입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 구독을 만드는 방법.  
  
#### 트랜잭션 게시에 대한 끌어오기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 만들려는 구독에 대 한 클래스입니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
2.  호출 하기 전에 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, 의 다음 필드 중 하나 이상을 설정는 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 속성:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -는 (예: 매일 또는 매주) 에이전트를 예약할 때 사용 하는 빈도 유형입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -에이전트가 실행 되는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -에서 에이전트가 월별로 실행 되도록 예약 된 지정된 된 월의 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -동기화 사이 발생 하는 빈도 유형 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -에이전트가 하루에 한 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -에이전트가 하루에 한 번 이상 실행 하는 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에는 가장 빠른 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에 최신 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -에이전트 예약이 적용 되는 첫 번째 날입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -에이전트 예약이 적용 되는 마지막 날입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 구독을 만드는 방법.  
  
#### 병합 게시에 대한 끌어오기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 만들려는 구독에 대 한 클래스입니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
2.  호출 하기 전에 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, 의 다음 필드 중 하나 이상을 설정는 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 속성:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -는 (예: 매일 또는 매주) 에이전트를 예약할 때 사용 하는 빈도 유형입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -에이전트가 실행 되는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -에서 에이전트가 월별로 실행 되도록 예약 된 지정된 된 월의 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -동기화 사이 발생 하는 빈도 유형 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -에이전트가 하루에 한 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -에이전트가 하루에 한 번 이상 실행 하는 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에는 가장 빠른 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에 최신 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -에이전트 예약이 적용 되는 첫 번째 날입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -에이전트 예약이 적용 되는 마지막 날입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 구독을 만드는 방법.  
  
#### 병합 게시에 대한 밀어넣기 구독을 만들 때 복제 에이전트 일정을 정의하려면  
  
1.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 만들려는 구독에 대 한 클래스입니다. 자세한 내용은 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
2.  호출 하기 전에 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, 의 다음 필드 중 하나 이상을 설정는 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 속성:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -는 (예: 매일 또는 매주) 에이전트를 예약할 때 사용 하는 빈도 유형입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -에이전트가 실행 되는 요일입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -에서 에이전트가 월별로 실행 되도록 예약 된 지정된 된 월의 주입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -동기화 사이 발생 하는 빈도 유형 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -에이전트가 하루에 한 번 이상 실행할 경우 빈도 단위입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -에이전트가 하루에 한 번 이상 실행 하는 경우 실행 간의 빈도 단위 수입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에는 가장 빠른 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -에이전트가 실행을 시작 하는 지정된 된 날에 최신 시간입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -에이전트 예약이 적용 되는 첫 번째 날입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -에이전트 예약이 적용 되는 마지막 날입니다.  
  
    > [!NOTE]  
    >  이러한 속성 중 하나를 지정하지 않으면 기본값이 설정됩니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 구독을 만드는 방법.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 병합 계시에 대한 밀어넣기 구독을 만들고 구독의 동기화 일정을 지정합니다.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## 참고 항목  
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)  
  
  