---
title: "복제 에이전트 프로필 작업 | Microsoft Docs"
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
  - "복제 [SQL Server], 에이전트 및 프로필"
  - "복제 에이전트 프로필 [SQL Server]"
  - "에이전트 [SQL Server 복제], 프로필"
  - "프로필 [SQL Server], 복제 에이전트"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# 복제 에이전트 프로필 작업
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 복제 에이전트 프로필로 작업하는 방법에 대해 설명합니다. 각 복제 에이전트의 동작은 에이전트 프로필을 통해 설정할 수 있는 매개 변수 집합으로 제어할 수 있습니다. 각 에이전트에는 기본 프로필이 있으며 일부 에이전트에는 미리 정의된 프로필이 추가되어 있습니다. 이러한 프로필은 에이전트에 대해 한 번에 하나만 활성화됩니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 복제 에이전트 프로필로 작업하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   에이전트 프로필 대화 상자에 액세스  
  
    -   에이전트에 대해 프로필 지정  
  
    -   프로필 만들기  
  
    -   프로필 수정  
  
    -   프로필 삭제  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   프로필 만들기  
  
    -   프로필 수정  
  
    -   프로필 삭제  
  
    -   동기화 중 에이전트 프로필 사용  
  
    -   Transact-SQL 예  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
    -   프로필 만들기  
  
    -   프로필 수정  
  
    -   프로필 삭제  
  
-   **후속 작업:**  [에이전트 매개 변수 변경 후](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
###  <a name="Access_SSMS"></a> SQL Server Management Studio에서 에이전트 프로필 대화 상자에 액세스하려면  
  
1.  에 **일반** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자를 클릭 하 여 **프로필의 기본**합니다.  
  
#### 복제 모니터에서 에이전트 프로필 대화 상자에 액세스하려면  
  
-   모든 에이전트에 대 한 대화 상자를 열려면 게시자를 마우스 오른쪽 단추로 클릭 **에이전트 프로필**합니다.  
  
-   단일 에이전트에 대한 대화 상자를 열려면 다음을 수행하세요.  
  
    1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
    2.  배포 에이전트 및 병합 에이전트 프로필에 대 한 마우스 오른쪽 단추로 클릭 한 구독에서 **모든 구독** 탭을 클릭 한 후 **에이전트 프로필**합니다. 다른 에이전트에 대 한 마우스 오른쪽 단추로 클릭 에이전트는 **에이전트** 탭을 클릭 한 후 **에이전트 프로필**합니다.  
  
###  <a name="Specify_SSMS"></a> 에이전트에 대해 프로필을 지정하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  **에이전트 프로필** 표의 **새 에이전트에 대한 기본값** 열에서 프로필을 선택합니다. 기본적으로 프로필은 새 게시 및 구독에 대한 에이전트에만 적용됩니다.  
  
3.  기존 게시 또는 구독에 대해 선택한 유형의 모든 에이전트에서 이 프로필을 사용하려면 **기존 에이전트 변경**을 클릭합니다.  
  
###  <a name="Modify_SSMS"></a> 프로필과 연결된 매개 변수를 보고 편집하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  속성 단추를 클릭 (**...**) 프로필 옆에 있습니다.  
  
3.  매개 변수 및 값을 보기는 **\< ProfileName> 프로필 속성** 대화 상자입니다.  
  
    -   사용자 정의 프로필의 매개 변수는 편집할 수 있지만 미리 정의된 시스템 프로필의 매개 변수는 편집할 수 없습니다.  
  
    -   에이전트에 대한 모든 매개 변수를 보려면 **이 프로필에서 사용되는 매개 변수만 표시** 확인란의 선택을 취소합니다. 에이전트 매개 변수에 대한 자세한 내용은 이 항목 끝에 있는 링크를 참조하세요.  
  
4.  **닫기**를 클릭합니다.  
  
###  <a name="Create_SSMS"></a> 사용자 정의 프로필을 만들려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  **새로 만들기**를 클릭합니다.  
  
3.  **새 에이전트 프로필** 초기화 대화 상자에서 새 프로필의 기반으로 사용할 기존 프로필을 선택합니다.  
  
4.  **새 에이전트 프로필** 대화 상자에서 **이름** 및 **설명** 입력란에 값을 입력합니다.  
  
5.  매개 변수를 수정하여 프로필을 변경합니다. 에이전트에 대한 모든 매개 변수를 보려면 **이 프로필에서 사용되는 매개 변수만 표시** 확인란의 선택을 취소합니다. 에이전트 매개 변수에 대한 자세한 내용은 이 항목 끝에 있는 링크를 참조하세요.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> 사용자 정의 프로필을 삭제하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  프로필이 하나 이상의 에이전트와 연결되어 있으면 해당 에이전트의 프로필을 변경합니다.  
  
    1.  **에이전트 프로필** 표에서 다른 프로필을 선택합니다.  
  
    2.  **기존 에이전트 변경**을 클릭합니다.  
  
        > [!NOTE]  
        >  이렇게 하면 삭제할 프로필을 사용하는 에이전트 외에 기존 게시 또는 구독에 대해 선택한 유형의 모든 에이전트에 대한 프로필까지 변경됩니다.  
  
3.  삭제할 프로필을 선택한 다음 **삭제**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
###  <a name="Create_tsql"></a> 새 에이전트 프로필을 만들려면  
  
1.  배포자에서 실행 [sp_add_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)합니다. 지정 **@name**, 값이 **1** 에 대 한 **@profile_type**, 는 다음 값 중 하나에 대 한 고 **@agent_type**:  
  
    -   **1** - [복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이 프로필이 해당 유형의 복제 에이전트에 대한 새 기본 프로필이 될 경우 **@default** 에 값 **1**을 지정합니다. 새 프로필에 대 한 식별자를 사용 하 여 반환 되는 **@profile_id** 출력 매개 변수입니다. 이 출력 매개 변수는 지정된 에이전트 유형의 기본 프로필을 기반으로 한 프로필 매개 변수 집합을 사용하여 새 프로필을 만듭니다.  
  
2.  새 프로필이 만들어진 후 기본 매개 변수를 추가, 제거 또는 수정하여 프로필을 사용자 지정합니다.  
  
###  <a name="Modify_tsql"></a> 기존 에이전트 프로필을 수정하려면  
  
1.  배포자에서 실행 [sp_help_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)합니다. 에 대해 다음 값 중 하나를 지정 **@agent_type**:  
  
    -   **1** - [복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 값을 확인 **profile_id** 결과 변경 하려면 프로필에 대 한 집합에 있습니다.  
  
2.  배포자에서 실행 [sp_help_agent_parameter (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)합니다. 에 대해 1 단계에서 프로필 식별자를 지정 **@profile_id**합니다. 그러면 해당 프로필의 모든 매개 변수가 반환됩니다. 프로필에서 수정하거나 제거할 매개 변수의 이름을 확인합니다.  
  
3.  실행 프로필에 대 한 매개 변수 값을 변경 하려면 [sp_change_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)합니다. 에 대해 1 단계에서 프로필 식별자를 지정 **@profile_id**, 변경에 대 한 매개 변수의 이름을 **@property**, 및에 대 한 매개 변수에 대 한 새 값을 **@value**합니다.  
  
    > [!NOTE]  
    >  기존 에이전트 프로필은 에이전트의 기본 프로필이 되도록 변경할 수 없습니다. 대신 이전 절차에서와 같이 새 프로필을 기본 프로필로 만들어야 합니다.  
  
4.  실행 프로필에서 매개 변수를 제거 하려면 [sp_drop_agent_parameter (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)합니다. 에 대해 1 단계에서 프로필 식별자를 지정 **@profile_id** 및 제거에 대 한 매개 변수의 이름을 **@parameter_name**합니다.  
  
5.  프로필에 새 매개 변수를 추가하려면 다음을 수행해야 합니다.  
  
    -   쿼리는 [MSagentparameterlist (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) 각 에이전트 유형에 대 한 프로필 매개 변수를 설정할 수 확인 하려면 배포자에서 테이블입니다.  
  
    -   배포자에서 실행 [sp_add_agent_parameter (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)합니다. 에 대해 1 단계에서 프로필 식별자를 지정 **@profile_id**, 에 대 한 추가 하려면 유효한 매개 변수 이름을 **@parameter_name**, 및에 대 한 매개 변수 값 **@parameter_value**합니다.  
  
###  <a name="Delete_tsql"></a> 에이전트 프로필을 삭제하려면  
  
1.  배포자에서 실행 [sp_help_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)합니다. 에 대해 다음 값 중 하나를 지정 **@agent_type**:  
  
    -   **1** - [복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 값을 확인 **profile_id** 결과 제거 하려면 프로필에 대 한 집합에 있습니다.  
  
2.  배포자에서 실행 [sp_drop_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)합니다. 에 대해 1 단계에서 프로필 식별자를 지정 **@profile_id**합니다.  
  
###  <a name="Synch_tsql"></a> 동기화 중 에이전트 프로필을 사용하려면  
  
1.  배포자에서 실행 [sp_help_agent_profile (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)합니다. 에 대해 다음 값 중 하나를 지정 **@agent_type**:  
  
    -   **1** - [복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 값을 확인 **profile_name** 결과 사용 하 여 프로필에 대 한 집합에 있습니다.  
  
2.  에이전트는 에이전트 작업에서 시작 되는 경우의 값을 지정 하는 에이전트를 시작 하는 작업 단계 편집 **profile_name** 뒤에 1 단계에서 얻은 **-ProfileName** 명령줄 매개 변수입니다. 자세한 내용은 참조 [보기 및 복제 에이전트 명령 프롬프트 매개 변수 수정 & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)합니다.  
  
3.  명령 프롬프트에서 에이전트를 시작할 때의 값을 지정 합니다. **profile_name** 뒤에 1 단계에서 얻은 **-ProfileName** 명령줄 매개 변수입니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 라는 병합 에이전트에 대 한 사용자 지정 프로필을 만듭니다 **custom_merge**, 의 값을 변경 하는 **-UploadReadChangesPerBatch** 매개 변수를 추가 하는 새 **-ExchangeType** 매개 변수 및 생성 된 프로필 정보를 반환 합니다.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> RMO 사용  
  
###  <a name="Create_RMO"></a> 새 에이전트 프로필을 만들려면  
  
1.  인스턴스를 사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.AgentProfile> 클래스입니다.  
  
3.  개체의 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -프로필에 대 한 이름입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - <xref:Microsoft.SqlServer.Replication.AgentType> 프로필을 만든 복제 에이전트의 유형을 지정 하는 값입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다.  
  
    -   (선택 사항) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -프로필에 관한 설명입니다.  
  
    -   (선택 사항) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -이 속성을 설정 **true** 하는 경우이 대 한 모든 새 에이전트 작업 <xref:Microsoft.SqlServer.Replication.AgentType> 기본적으로이 프로필을 사용 합니다.  
  
4.  호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> 메서드를 서버에 프로필을 만듭니다.  
  
5.  서버에 프로필이 있으면 복제 에이전트 매개 변수의 값을 추가, 제거 또는 변경하여 프로필을 사용자 지정할 수 있습니다.  
  
6.  프로필에 기존 복제 에이전트 작업을 할당 하려면 호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> 메서드. *distributionDBName* 에 대한 배포 데이터베이스 이름 및 *agentID*에 대한 작업 ID를 전달합니다.  
  
###  <a name="Modify_RMO"></a> 기존 에이전트 프로필을 수정하려면  
  
1.  인스턴스를 사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스입니다. 전달 된 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 개체입니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환하는 경우 배포자가 있는지 확인합니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> 메서드. 전달 된 <xref:Microsoft.SqlServer.Replication.AgentType> 값 범위를 좁히는 복제 에이전트의 특정 형식으로 반환 되는 프로필입니다.  
  
5.  원하는 가져오기 <xref:Microsoft.SqlServer.Replication.AgentProfile> 에서 반환 된 개체 <xref:System.Collections.ArrayList>, 여기서는 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 개체의 속성은 프로필 이름과 일치 합니다.  
  
6.  다음 메서드 중 하나를 호출 <xref:Microsoft.SqlServer.Replication.AgentProfile> 프로필을 변경 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -프로필에 지원 되는 매개 변수를 추가 합니다. 여기서 *이름* 복제 에이전트 매개 변수의 이름 및 *값* 지정 된 값입니다. 지정된 된 에이전트 유형에 대 한 모든 지원 되는 에이전트 매개 변수를 열거 하려면 호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 메서드. 이 메서드는 반환 된 <xref:System.Collections.ArrayList> 의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 지원 되는 모든 매개 변수를 나타내는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -프로필에서 기존 매개 변수를 제거 합니다. 여기서 *이름* 복제 에이전트 매개 변수 이름입니다. 프로필에 대해 정의 된 모든 현재 에이전트 매개 변수를 열거 하려면 호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 메서드. 이 메서드는 반환 된 <xref:System.Collections.ArrayList> 의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 이 프로필에 대 한 기존 매개 변수를 나타내는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -프로필의 기존 매개 변수의 설정을 변경 합니다. 여기서 *이름* 에이전트 매개 변수의 이름 및 *newValue* 매개 변수를 변경할 값입니다. 프로필에 대해 정의 된 모든 현재 에이전트 매개 변수를 열거 하려면 호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 메서드. 이 메서드는 반환 된 <xref:System.Collections.ArrayList> 의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 이 프로필에 대 한 기존 매개 변수를 나타내는 개체입니다. 모든 열거 하기 위해 에이전트 매개 변수 설정을 지원, 호출 된 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 메서드. 이 메서드는 <xref:System.Collections.ArrayList> 의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 모든 매개 변수에 대해 지원 되는 값을 나타내는 개체입니다.  
  
###  <a name="Delete_RMO"></a> 에이전트 프로필을 삭제하려면  
  
1.  인스턴스를 사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.AgentProfile> 클래스입니다. 에 대 한 프로필의 이름을 설정 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드. 이 메서드가 **false**를 반환하는 경우 지정한 이름이 올바르지 않거나 해당 프로필이 서버에 없는 것입니다.  
  
4.  있는지 확인는 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> 속성이 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, 고객 프로필을 나타냅니다. 값이 있는 프로필을 제거 하면 안 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> 에 대 한 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>합니다.  
  
5.  호출의 <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> 메서드를 서버에서이 개체가 나타내는 사용자 정의 프로필을 제거 합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 에이전트 매개 변수 변경 후  
 에이전트 매개 변수에 대한 변경 사항은 다음에 에이전트가 시작될 때 적용됩니다. 에이전트가 연속적으로 실행되는 경우에는 에이전트를 중단했다가 다시 시작해야 합니다.  
  
## 참고 항목  
 [복제 에이전트 프로필](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [복제 스냅숏 에이전트](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [복제 로그 판독기 에이전트](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [복제 배포 에이전트](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [복제 병합 에이전트](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  