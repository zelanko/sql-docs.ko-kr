---
title: 복제 에이전트 프로필 작업 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- agents [SQL Server replication], profiles
- profiles [SQL Server], replication agents
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7b0a47ff73186642e0b0b48aec06e5320fc44d15
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288243"
---
# <a name="work-with-replication-agent-profiles"></a>복제 에이전트 프로필 작업
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 복제 에이전트 프로필로 작업하는 방법에 대해 설명합니다. 각 복제 에이전트의 동작은 에이전트 프로필을 통해 설정할 수 있는 매개 변수 집합으로 제어할 수 있습니다. 각 에이전트에는 기본 프로필이 있으며 일부 에이전트에는 미리 정의된 프로필이 추가되어 있습니다. 이러한 프로필은 에이전트에 대해 한 번에 하나만 활성화됩니다.  
  
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
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
###  <a name="to-access-the-agent-profiles-dialog-box-from-sql-server-management-studio"></a><a name="Access_SSMS"></a> SQL Server Management Studio에서 에이전트 프로필 대화 상자에 액세스하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 **프로필 기본값**을 클릭합니다.  

#### <a name="to-access-the-agent-profiles-dialog-box-from-replication-monitor"></a>복제 모니터에서 에이전트 프로필 대화 상자에 액세스하려면  
  
-   모든 에이전트에 대한 대화 상자를 열려면 게시자를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필**을 클릭합니다.  
  
-   단일 에이전트에 대한 대화 상자를 열려면 다음을 수행하세요.  
  
    1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
    2.  배포 에이전트 및 병합 에이전트 프로필의 경우 **모든 구독** 탭에서 구독을 마우스 오른쪽 단추로 클릭한 다음 **에이전트 프로필**을 클릭합니다. 다른 에이전트의 경우 **에이전트** 탭에서 에이전트를 마우스 오른쪽 단추로 클릭하고 **에이전트 프로필**을 클릭합니다.  
  
###  <a name="to-specify-a-profile-for-an-agent"></a><a name="Specify_SSMS"></a> 에이전트에 대해 프로필을 지정하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  **에이전트 프로필** 표의 **새 에이전트에 대한 기본값** 열에서 프로필을 선택합니다. 기본적으로 프로필은 새 게시 및 구독에 대한 에이전트에만 적용됩니다.  
  
3.  기존 게시 또는 구독에 대해 선택한 유형의 모든 에이전트에서 이 프로필을 사용하려면 **기존 에이전트 변경**을 클릭합니다.  
  
###  <a name="to-view-and-edit-the-parameters-associated-with-a-profile"></a><a name="Modify_SSMS"></a> 프로필과 연결된 매개 변수를 보고 편집하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  프로필 옆에 있는 속성 단추( **...** )를 클릭합니다.  
  
3.  **\<ProfileName> 프로필 속성** 대화 상자에서 매개 변수 및 값을 봅니다.  
  
    -   사용자 정의 프로필의 매개 변수는 편집할 수 있지만 미리 정의된 시스템 프로필의 매개 변수는 편집할 수 없습니다.  
  
    -   에이전트에 대한 모든 매개 변수를 보려면 **이 프로필에서 사용되는 매개 변수만 표시** 확인란의 선택을 취소합니다. 에이전트 매개 변수에 대한 자세한 내용은 이 항목 끝에 있는 링크를 참조하세요.  
  
4.  **닫기**를 클릭합니다.  
  
###  <a name="to-create-a-user-defined-profile"></a><a name="Create_SSMS"></a> 사용자 정의 프로필을 만들려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  **새로 만들기**를 클릭합니다.  
  
3.  **새 에이전트 프로필** 초기화 대화 상자에서 새 프로필의 기반으로 사용할 기존 프로필을 선택합니다.  
  
4.  **새 에이전트 프로필** 대화 상자에서 **이름** 및 **설명** 입력란에 값을 입력합니다.  
  
5.  매개 변수를 수정하여 프로필을 변경합니다. 에이전트에 대한 모든 매개 변수를 보려면 **이 프로필에서 사용되는 매개 변수만 표시** 확인란의 선택을 취소합니다. 에이전트 매개 변수에 대한 자세한 내용은 이 항목 끝에 있는 링크를 참조하세요.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="to-delete-a-user-defined-profile"></a><a name="Delete_SSMS"></a> 사용자 정의 프로필을 삭제하려면  
  
1.  **에이전트 프로필** 대화 상자에 둘 이상의 에이전트에 대한 프로필이 표시되면 에이전트를 선택합니다.  
  
2.  프로필이 하나 이상의 에이전트와 연결되어 있으면 해당 에이전트의 프로필을 변경합니다.  
  
    1.  **에이전트 프로필** 표에서 다른 프로필을 선택합니다.  
  
    2.  **기존 에이전트 변경**을 클릭합니다.  
  
        > [!NOTE]  
        >  이렇게 하면 삭제할 프로필을 사용하는 에이전트 외에 기존 게시 또는 구독에 대해 선택한 유형의 모든 에이전트에 대한 프로필까지 변경됩니다.  
  
3.  삭제할 프로필을 선택한 다음 **삭제**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
###  <a name="to-create-a-new-agent-profile"></a><a name="Create_tsql"></a> 새 에이전트 프로필을 만들려면  
  
1.  배포자에서 [sp_add_agent_profile&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)을 실행합니다. **\@name**을 지정하고 **\@profile_type**에 값 **1**을 지정한 후 **\@agent_type**에 다음 값 중 하나를 지정합니다.  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이 프로필이 해당 유형의 복제 에이전트에 대한 새 기본 프로필이 될 경우 **\@default**에 값 **1**을 지정합니다. 새 프로필의 식별자는 **\@profile_id** 출력 매개 변수를 통해 반환됩니다. 이 출력 매개 변수는 지정된 에이전트 유형의 기본 프로필을 기반으로 한 프로필 매개 변수 집합을 사용하여 새 프로필을 만듭니다.  
  
2.  새 프로필이 만들어진 후 기본 매개 변수를 추가, 제거 또는 수정하여 프로필을 사용자 지정합니다.  
  
###  <a name="to-modify-an-existing-agent-profile"></a><a name="Modify_tsql"></a> 기존 에이전트 프로필을 수정하려면  
  
1.  배포자에서 [sp_help_agent_profile&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)을 실행합니다. **\@agent_type**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 변경할 프로필의 결과 집합에 있는 **profile_id** 값을 확인합니다.  
  
2.  배포자에서 [sp_help_agent_parameter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)를 실행합니다. **\@profile_id**에 1단계에서 얻은 프로필 식별자를 지정합니다. 그러면 해당 프로필의 모든 매개 변수가 반환됩니다. 프로필에서 수정하거나 제거할 매개 변수의 이름을 확인합니다.  
  
3.  프로필에서 매개 변수의 값을 변경하려면 [sp_change_agent_parameter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)를 실행합니다. **\@profile_id**에 1단계에서 얻은 프로필 식별자를 지정하고 **\@parameter_name**에 변경할 매개 변수의 이름을 지정한 후 **\@parameter_value**에 매개 변수의 새 값을 지정합니다.  
  
    > [!NOTE]  
    >  기존 에이전트 프로필은 에이전트의 기본 프로필이 되도록 변경할 수 없습니다. 대신 이전 절차에서와 같이 새 프로필을 기본 프로필로 만들어야 합니다.  
  
4.  프로필에서 매개 변수를 제거하려면 [sp_drop_agent_parameter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)를 실행합니다. **\@profile_id**에 1단계에서 얻은 프로필 식별자를 지정하고 **\@parameter_name**에 제거할 매개 변수의 이름을 지정합니다.  
  
5.  프로필에 새 매개 변수를 추가하려면 다음을 수행해야 합니다.  
  
    -   배포자에서 [MSagentparameterlist&#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) 테이블을 쿼리하여 각 에이전트 유형에 설정할 수 있는 프로필 매개 변수를 확인합니다.  
  
    -   배포자에서 [sp_add_agent_parameter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)를 실행합니다. **\@profile_id**에 1단계에서 얻은 프로필 식별자를 지정하고 **\@parameter_name**에 추가할 유효한 매개 변수의 이름을 지정한 후 **\@parameter_value**에 매개 변수의 값을 지정합니다.  
  
###  <a name="to-delete-an-agent-profile"></a><a name="Delete_tsql"></a> 에이전트 프로필을 삭제하려면  
  
1.  배포자에서 [sp_help_agent_profile&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)을 실행합니다. **\@agent_type**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 제거할 프로필의 결과 집합에 있는 **profile_id** 값을 확인합니다.  
  
2.  배포자에서 [sp_drop_agent_profile&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)을 실행합니다. **\@profile_id**에 1단계에서 얻은 프로필 식별자를 지정합니다.  
  
###  <a name="to-use-agent-profiles-during-synchronization"></a><a name="Synch_tsql"></a> 동기화 중 에이전트 프로필을 사용하려면  
  
1.  배포자에서 [sp_help_agent_profile&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)을 실행합니다. **\@agent_type**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     이렇게 하면 지정된 에이전트 유형에 대해 모든 이벤트가 반환됩니다. 사용할 프로필의 결과 집합에 있는 **profile_name** 값을 확인합니다.  
  
2.  에이전트가 에이전트 작업에서 시작되는 경우 에이전트를 시작하는 작업 단계를 수정하여 **-ProfileName** 명령줄 매개 변수 뒤에 1단계에서 얻은 **profile_name** 의 값을 지정합니다. 자세한 내용은 [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)을 참조하세요.  
  
3.  명령 프롬프트에서 에이전트를 시작하는 경우 **-ProfileName** 명령줄 매개 변수 뒤에 1단계에서 얻은 **profile_name** 의 값을 지정합니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 **custom_merge**라는 병합 에이전트의 사용자 지정 프로필을 만들고, **-UploadReadChangesPerBatch** 매개 변수의 값을 변경하고, 새 **-ExchangeType** 매개 변수를 추가하고, 만들어진 프로필에 대한 정보를 반환합니다.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="using-rmo"></a><a name="RMOProcedure"></a> RMO 사용  
  
###  <a name="to-create-a-new-agent-profile"></a><a name="Create_RMO"></a> 새 에이전트 프로필을 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스의 인스턴스를 사용하여 배포자에 대한 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.AgentProfile> 클래스의 인스턴스를 만듭니다.  
  
3.  개체의 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> - 프로필의 이름입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - 프로필을 만들 복제 에이전트의 유형을 지정하는 <xref:Microsoft.SqlServer.Replication.AgentType> 값입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> (옵션) - 프로필에 대한 설명입니다.  
  
    -   (옵션) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> - 이 <xref:Microsoft.SqlServer.Replication.AgentType>의 모든 새 에이전트 작업에서 기본적으로 이 프로필이 사용되는 경우 이 속성을 **true**로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> 메서드를 호출하여 서버에 프로필을 만듭니다.  
  
5.  서버에 프로필이 있으면 복제 에이전트 매개 변수의 값을 추가, 제거 또는 변경하여 프로필을 사용자 지정할 수 있습니다.  
  
6.  기존 복제 에이전트 작업에 프로필을 할당하려면 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> 메서드를 호출합니다. *distributionDBName* 에 대한 배포 데이터베이스 이름 및 *agentID*에 대한 작업 ID를 전달합니다.  
  
###  <a name="to-modify-an-existing-agent-profile"></a><a name="Modify_RMO"></a> 기존 에이전트 프로필을 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스의 인스턴스를 사용하여 배포자에 대한 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 배포자가 있는지 확인합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> 메서드를 호출합니다. <xref:Microsoft.SqlServer.Replication.AgentType> 값을 전달하여 반환되는 프로필의 범위를 특정 유형의 복제 에이전트로 좁힙니다.  
  
5.  반환된 <xref:Microsoft.SqlServer.Replication.AgentProfile> 에서 원하는 <xref:System.Collections.ArrayList>개체를 가져옵니다. 이때 개체의 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 속성은 프로필 이름과 일치합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.AgentProfile> 의 다음 메서드 중 하나를 호출하여 프로필을 변경합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> - 프로필에 지원되는 매개 변수를 추가합니다. 여기서 *name* 은 복제 에이전트 매개 변수의 이름이고 *value* 는 지정된 값입니다. 지정된 에이전트 유형에 대해 지원되는 모든 에이전트 매개 변수를 열거하려면 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 메서드를 호출합니다. 이 메서드는 지원되는 모든 매개 변수를 나타내는 <xref:System.Collections.ArrayList> 개체의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> - 프로필에서 기존 매개 변수를 제거합니다. 여기서 *name* 은 복제 에이전트 매개 변수의 이름입니다. 프로필에 대해 정의된 현재의 모든 에이전트 매개 변수를 열거하려면 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 메서드를 호출합니다. 이 메서드는 이 프로필의 기존 매개 변수를 나타내는 <xref:System.Collections.ArrayList> 개체의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> - 프로필의 기존 매개 변수 설정을 변경합니다. 여기서 *name* 은 에이전트 매개 변수의 이름이고 *newValue* 는 매개 변수를 변경할 값입니다. 프로필에 대해 정의된 현재의 모든 에이전트 매개 변수를 열거하려면 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 메서드를 호출합니다. 이 메서드는 이 프로필의 기존 매개 변수를 나타내는 <xref:System.Collections.ArrayList> 개체의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 를 반환합니다. 지원되는 모든 에이전트 매개 변수 설정을 열거하려면 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 메서드를 호출합니다. 이 메서드는 모든 매개 변수에 대해 지원되는 값을 나타내는 <xref:System.Collections.ArrayList> 개체의 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 를 반환합니다.  
  
###  <a name="to-delete-an-agent-profile"></a><a name="Delete_RMO"></a> 에이전트 프로필을 삭제하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스의 인스턴스를 사용하여 배포자에 대한 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.AgentProfile> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 에 프로필 이름을 설정하고 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>을 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. 이 메서드가 **false**를 반환하는 경우 지정한 이름이 올바르지 않거나 해당 프로필이 서버에 없는 것입니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> 속성이 고객 프로필을 나타내는 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>로 설정되어 있는지 확인합니다. <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> 의 값이 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>인 프로필은 제거하면 안 됩니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> 메서드를 호출하여 이 개체가 나타내는 사용자 정의 프로필을 서버에서 제거합니다.  
  
##  <a name="follow-up-after-changing-agent-parameters"></a><a name="FollowUp"></a> 후속 작업: 에이전트 매개 변수 변경 후  
에이전트 매개 변수에 대한 변경 사항은 다음에 에이전트가 시작될 때 적용됩니다. 에이전트가 연속적으로 실행되는 경우에는 에이전트를 중단했다가 다시 시작해야 합니다. SQL Server 2017 CU3부터 일부 에이전트 매개 변수 변경 내용은 에이전트를 다시 시작할 필요 없이 적용됩니다. 
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 프로필](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  
