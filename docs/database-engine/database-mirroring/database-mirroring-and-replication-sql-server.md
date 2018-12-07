---
title: 데이터베이스 미러링 및 복제(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- replication [SQL Server], database mirroring and
ms.assetid: 82796217-02e2-4bc5-9ab5-218bae11a2d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 029ad55778a1c4239bdb83d587ca9a1f21bcaf20
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534440"
---
# <a name="database-mirroring-and-replication-sql-server"></a>데이터베이스 미러링 및 복제(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 미러링은 게시 데이터베이스의 가용성을 제공하기 위해 복제와 함께 사용될 수 있습니다. 데이터베이스 미러링에는 일반적으로 서로 다른 컴퓨터에 있는 두 개의 단일 데이터베이스 복사본이 사용됩니다. 클라이언트는 항상 하나의 데이터베이스 복사본만 사용할 수 있습니다. 이 복사본을 주 데이터베이스라고 합니다. 클라이언트가 주 데이터베이스에 수행한 업데이트는 미러 데이터베이스라고 하는 다른 데이터베이스 복사본에 적용됩니다. 미러링에는 주 데이터베이스에 대해 수행된 모든 삽입, 업데이트 또는 삭제 작업의 트랜잭션 로그를 미러 데이터베이스에 적용하는 작업이 포함됩니다.  
  
 미러에 대한 복제 장애 조치(Failover)는 게시 데이터베이스에서 완전히 지원되지만 구독 데이터베이스에서는 지원이 제한적으로 제공됩니다. 배포 데이터베이스에서는 데이터베이스 미러링이 지원되지 않습니다. 복제를 다시 구성할 필요 없이 배포 데이터베이스나 구독 데이터베이스를 복구하는 방법은 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.   
  
> [!NOTE]  
>  장애 조치 이후에는 미러 서버가 주 서버가 됩니다. 이 항목에서 "주" 및 "미러"는 항상 원래의 주 서버와 미러 서버를 의미합니다.  
  
## <a name="requirements-and-considerations-for-using-replication-with-database-mirroring"></a>데이터베이스 미러링에서 복제 사용을 위한 요구 사항 및 고려 사항  
 데이터베이스 미러링에서 복제를 사용할 때는 다음 요구 사항과 고려 사항에 주의하십시오.  
  
-   주 서버와 미러 서버는 배포자를 공유해야 합니다. 이러한 배포자는 게시자에 예기치 않은 장애 조치가 있는 경우 더 큰 내결함성을 제공하는 원격 배포자가 좋습니다.  
  
-   복제에는 읽기 전용 구독자 또는 큐에 지정된 업데이트 구독자가 포함된 병합 복제 및 트랜잭션 복제에 대한 게시 데이터베이스 미러링이 지원됩니다. 즉시 업데이트 구독자, Oracle 게시자, 피어 투 피어 토폴로지의 게시자 및 다시 게시는 지원되지 않습니다.  
  
-   데이터베이스 외부에 있는 메타데이터 및 개체(예: 로그인, 작업, 연결된 서버 등)는 미러 서버에 복사되지 않습니다. 미러 서버에서 이러한 메타데이터 및 개체가 필요하면 이를 수동으로 복사해야 합니다. 자세한 내용은 [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)를 참조하세요.  
  
## <a name="configuring-replication-with-database-mirroring"></a>데이터베이스 미러링에서 복제 구성  
 복제와 데이터베이스 미러링은 다음 5단계에 따라 구성됩니다. 각 단계는 다음 섹션에서 자세히 설명됩니다.  
  
1.  게시자를 구성합니다.  
  
2.  데이터베이스 미러링을 구성합니다.  
  
3.  주 서버와 동일한 배포자를 사용하도록 미러 서버를 구성합니다.  
  
4.  장애 조치에 대한 복제 에이전트를 구성합니다.  
  
5.  복제 모니터에 주 서버와 미러 서버를 추가합니다.  
  
 1단계와 2단계는 순서를 바꿔서 수행할 수도 있습니다.  
  
#### <a name="to-configure-database-mirroring-for-a-publication-database"></a>게시 데이터베이스에 대한 데이터베이스 미러링을 구성하려면  
  
1.  게시자를 구성합니다.  
  
    1.  원격 배포자를 사용하는 것이 좋습니다. 배포 구성에 대한 자세한 내용은 [배포 구성](../../relational-databases/replication/configure-distribution.md)을 참조하세요.  
  
    2.  스냅숏용 데이터베이스와 트랜잭션 게시 및/또는 병합 게시를 설정할 수 있습니다. 하나 이상의 게시 유형이 포함되는 미러된 데이터베이스의 경우에는 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 사용하여 동일 노드에서 두 유형 모두에 대해 데이터베이스를 설정해야 합니다. 예를 들어 주 서버에서 다음 저장 프로시저 호출을 실행할 수 있습니다.  
  
        ```  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='publish', @value=true;  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='mergepublish', @value=true;  
        ```  
  
         게시를 만드는 방법은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조하세요.  
  
2.  데이터베이스 미러링을 구성합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md) 및 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)을 참조하세요.  
  
3.  미러 서버에 대한 배포를 구성합니다. 게시자로 미러 이름을 지정하고 주 서버에서 사용되는 것과 같은 배포자 및 스냅숏 폴더를 지정합니다. 예를 들어 저장 프로시저로 복제를 구성하는 경우 배포자에서 [sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) 를 실행한 다음 미러에서 [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) 를 실행합니다. **sp_adddistpublisher**의 경우 다음과 같이 합니다.  
  
    -   **@publisher** 매개 변수의 값을 미러 서버의 네트워크 이름으로 설정합니다.  
  
    -   **@working_directory** 매개 변수의 값을 주 서버에서 사용되는 스냅숏 폴더로 설정합니다.  
  
4.  **–PublisherFailoverPartner** 에이전트 매개 변수에 대한 미러 이름을 지정합니다. 이 에이전트 매개 변수는 다음 에이전트에서 장애 조치 후 미러 서버를 식별하는 데 필요합니다.  
  
    -   모든 게시에 대한 스냅숏 에이전트  
  
    -   모든 트랜잭션 게시에 대한 로그 판독기 에이전트  
  
    -   지연 업데이트 구독을 지원하는 트랜잭션 게시에 대한 큐 판독기 에이전트  
  
    -   병합 게시에 대한 병합 에이전트  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기(replisapi.dll: 웹 동기화를 사용하여 동기화된 병합 구독)  
  
    -   컨트롤로 동기화된 병합 구독에 대한 SQL 병합 ActiveX 컨트롤  
  
     배포 에이전트 및 배포 ActiveX 컨트롤은 게시자에 연결되지 않기 때문에 이 매개 변수가 없습니다.  
  
     에이전트 매개 변수에 대한 변경 사항은 다음에 에이전트가 시작될 때 적용됩니다. 에이전트가 연속적으로 실행되는 경우에는 에이전트를 중단했다가 다시 시작해야 합니다. 에이전트 프로필 및 명령 프롬프트에서 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
    -   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
     에이전트 프로필에 **–PublisherFailoverPartner**를 추가한 다음, 프로필에 미러 이름을 지정하는 것이 좋습니다. 예를 들어 저장 프로시저로 복제를 구성할 경우  
  
    ```  
    -- Execute sp_help_agent_profile in the context of the distribution database to get the list of profiles.  
    -- Select the profile id of the profile that needs to be updated from the result set.  
    -- In the agent_type column returned by sp_help_agent_profile:   
    -- 1 = Snapshot Agent; 2 = Log Reader Agent; 3 = Distribution Agent; 4 = Merge Agent; 9 = Queue Reader Agent.  
  
    exec sp_help_agent_profile;  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Snapshot Agent profile (profile 1).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 1, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Merge Agent profile (profile 6).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 6, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
    ```  
  
5.  복제 모니터에 주 서버와 미러 서버를 추가합니다. 자세한 내용은 [복제 모니터에서 게시자 추가 및 제거](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)를 참조하세요.  
  
## <a name="maintaining-a-mirrored-publication-database"></a>미러된 게시 데이터베이스 유지 관리  
 미러된 게시 데이터베이스를 유지 관리하는 작업은 미러되지 않은 데이터베이스를 유지 관리하는 방법과 본질적으로 동일하지만 다음 사항을 고려해야 합니다.  
  
-   관리 및 모니터링은 활성 서버에서 수행되어야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시는 활성 서버의 경우에만 **로컬 게시** 폴더에 표시됩니다. 예를 들어 미러 서버로 장애 조치된 경우, 게시는 미러 서버에 표시되고 주 서버에는 더 이상 표시되지 않습니다. 데이터베이스가 미러 데이터베이스로 장애 조치된 경우에는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 복제 모니터를 수동으로 새로 고쳐서 변경 내용을 적용해야 할 수 있습니다.  
  
-   복제 모니터는 개체 트리에 주 서버와 미러 서버의 게시 노드를 표시합니다. 주 서버가 활성 서버이면 게시 정보가 복제 모니터의 주 노드 아래에만 표시됩니다.  
  
     미러 서버가 활성 서버인 경우:  
  
    -   에이전트에서 오류가 발생한 경우 오류는 미러 노드가 아닌 주 노드에만 표시됩니다.  
  
    -   주 서버가 사용 가능하지 않은 경우 주 노드와 미러 노드는 동일한 게시 목록을 표시합니다. 미러 노드 아래의 게시에 대해 모니터링이 수행됩니다.  
  
-   게시자 이름 지정 등을 위해 저장 프로시저나 RMO(복제 관리 개체)를 사용하여 미러 서버에서 복제를 관리할 때는 복제용으로 데이터베이스가 설정된 인스턴스 이름을 지정해야 합니다. 올바른 이름을 확인하려면 [publishingservername](../../t-sql/functions/replication-functions-publishingservername.md)함수를 사용하십시오.  
  
     게시 데이터베이스가 미러된 경우 미러된 데이터베이스에 저장된 복제 메타데이터는 주 데이터베이스에 저장된 메타데이터와 동일합니다. 따라서 주 서버에서 복제용으로 설정된 게시 데이터베이스의 경우 미러 서버에서 시스템 테이블에 저장된 게시자 이름은 미러 서버가 아닌 주 서버의 이름입니다. 이러한 방식은 게시 데이터베이스가 미러 서버로 장애 조치되는 경우 복제 구성 및 유지 관리에 영향을 줍니다. 예를 들어 장애 조치(failover) 후에 미러 서버에서 저장 프로시저로 복제를 구성할 때 주 서버에서 설정된 게시 데이터베이스에 끌어오기 구독을 추가하려면 **@publisher** 또는 **sp_addmergepullsubscription** 의 **@publisher**을 참조하세요.  
  
     미러 서버로 장애 조치된 후 미러 서버에 게시 데이터베이스를 설정하면 시스템 테이블에 저장된 게시자 인스턴스 이름이 미러 서버의 이름이며, 이 경우 **@publisher** 매개 변수에 대해 미러 서버의 이름을 사용하게 됩니다.  
  
    > [!NOTE]  
    >  **sp_addpublication**과 같은 일부 경우에는 **@publisher** 매개 변수가 비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 대해서만 지원되며, 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 미러링과는 관련이 없습니다.  
  
-   장애 조치 후 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 구독을 동기화하려면 구독자에서 끌어오기 구독을 동기화하고 활성 게시자에서 밀어넣기 구독을 동기화합니다.  
  
### <a name="replication-behavior-if-mirroring-is-removed"></a>미러링이 제거된 경우의 복제 동작  
 게시된 데이터베이스에서 미러링이 제거된 경우에는 다음 문제에 주의하십시오.  
  
-   주 서버에서 게시 데이터베이스가 더 이상 미러되지 않는 경우에는 원래의 주 서버에 대해 변경되지 않은 상태로 복제가 계속 작동합니다.  
  
-   게시 데이터베이스가 주 서버에서 미러 서버로 장애 조치되고 미러링 관계가 이후에 해제되거나 제거되면 복제 에이전트가 미러 서버에 대해 더 이상 작동하지 않습니다. 주 서버가 영구적으로 손실된 경우, 게시자로 지정된 미러 서버에서 복제를 해제하고 다시 구성하십시오.  
  
-   데이터베이스 미러링이 완전히 제거된 경우 미러 데이터베이스는 복구 상태에 있으며 작동하려면 복원되어야 합니다. 복제와 관련하여 복구된 데이터베이스의 동작은 KEEP_REPLICATION 옵션이 지정되었는지 여부에 따라 달라집니다. 이 옵션은 복원 작업에서 게시된 데이터베이스를 해당 데이터베이스가 만들어진 서버 외의 다른 서버로 복원할 경우 복제 설정을 보존하도록 지정합니다. KEEP_REPLICATION 옵션은 다른 게시 데이터베이스를 사용할 수 없는 경우에만 사용하십시오. 다른 게시 데이터베이스가 변경되지 않은 상태로 복제 중인 경우에는 옵션이 지원되지 않습니다. KEEP_REPLICATION에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
## <a name="log-reader-agent-behavior"></a>로그 판독기 에이전트 동작  
 다음 표에서는 데이터베이스 미러링의 다양한 운영 모드에 대한 로그 판독기 에이전트 동작에 대해 설명합니다.  
  
|운영 모드|미러 서버를 사용할 수 없는 경우의 로그 판독기 에이전트 동작|  
|--------------------|------------------------------------------------------------|  
|자동 장애 조치 있는 보호 우선 모드|미러 서버를 사용할 수 없는 경우 로그 판독기 에이전트는 명령을 배포 데이터베이스에 전달합니다. 미러 서버가 다시 온라인 상태가 되고 주 서버의 모든 트랜잭션이 포함되기 전에는 주 서버가 미러 서버로 장애 조치될 수 없습니다.|  
|성능 우선 모드|미러 서버를 사용할 수 없으면 주 데이터베이스가 노출된 상태(즉, 미러되지 않은 상태)로 실행됩니다. 하지만 로그 판독기 에이전트는 미러 서버에 저장된 트랜잭션만 복제합니다. 서비스가 강제되고 미러 서버가 주 서버의 역할을 수행하는 경우 로그 판독기 에이전트는 미러 서버에 따라 작동되며 새로운 트랜잭션을 가져오기 시작합니다.<br /><br /> 미러 서버가 주 서버보다 뒤쳐지면 복제 지연이 증가할 수 있습니다.|  
|자동 장애 조치를 지원하지 않는 보호 우선 모드|커밋된 모든 트랜잭션이 미러 서버의 디스크에 확정됩니다. 로그 판독기 에이전트는 미러 서버에 확정된 트랜잭션만 복제합니다. 미러 서버를 사용할 수 없는 경우 주 서버는 데이터베이스에 대한 더 이상의 작동을 허용하지 않기 때문에 로그 에이전트에는 복제할 트랜잭션이 없게 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 기능 및 태스크](../../relational-databases/replication/replication-features-and-tasks.md)   
 [로그 전달 및 복제&#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)  
  
  
