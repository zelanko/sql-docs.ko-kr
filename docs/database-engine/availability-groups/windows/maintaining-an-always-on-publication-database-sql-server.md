---
title: 가용성 그룹의 일부로 복제된 게시자 데이터베이스 관리
description: SQL 복제에서 게시자 역할을 하고 Always On 가용성 그룹에 참여하는 데이터베이스를 관리하고 유지하는 방법에 대한 설명입니다.
ms.custom: seodec18
ms.date: 05/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6962df1084579693ec5b281514b12db83fdb07da
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896085"
---
# <a name="manage-a-replicated-publisher-database-as-part-of-an-always-on-availability-group"></a>Always On 가용성 그룹의 일부로 복제된 게시자 데이터베이스 관리
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 Always On 가용성 그룹을 사용할 경우 게시 데이터베이스 유지 관리와 관련하여 특별히 고려해야 할 사항에 대해 설명합니다.  
  
##  <a name="maintaining-a-published-database-in-an-availability-group"></a><a name="MaintainPublDb"></a> 가용성 그룹에서 게시된 데이터베이스 유지 관리  
 Always On 게시 데이터베이스를 유지 관리하는 작업은 표준 게시 데이터베이스를 유지 관리하는 작업과 기본적으로 동일하지만 다음 사항을 고려해야 합니다.  
  
-   관리는 주 복제본 호스트에서 수행되어야 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 게시는 **로컬 게시** 폴더 아래에 주 복제본 호스트 및 읽을 수 있는 보조 복제본을 표시됩니다. 읽을 수 없는 보조 복제본이 주 복제본으로 승격된 경우 장애 조치(failover) 후 수동으로 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 를 새로 고쳐 변경 내용을 반영해야 합니다.  
  
-   복제 모니터는 항상 원래 게시자에서 게시 정보를 표시합니다. 그러나 원래 게시자를 서버로 추가하면 어떤 복제본에서든지 복제 모니터에서 이 정보를 볼 수 있습니다.  
  
-   게시자 이름 지정 등을 위해 저장 프로시저나 RMO(복제 관리 개체)를 사용하여 현재 주 복제본에서 복제를 관리할 때는 복제용으로 설정된 데이터베이스(원래 게시자)에서 인스턴스 이름을 지정해야 합니다. 올바른 이름을 확인하려면 **PUBLISHINGSERVERNAME** 함수를 사용하십시오. 게시 데이터베이스를 가용성 그룹에 조인하면 보조 데이터베이스 복제본에 저장된 복제 메타데이터가 주 데이터베이스 복제본의 복제 메타데이터와 동일해집니다. 따라서 주 서버에서 복제용으로 설정된 게시 데이터베이스의 경우 보조 서버에서 시스템 테이블에 저장된 게시자 인스턴스 이름은 보조 서버가 아닌 주 서버의 이름입니다. 이러한 방식은 게시 데이터베이스가 보조로 장애 조치되는 경우 복제 구성 및 유지 관리에 영향을 줍니다. 예를 들어 장애 조치(failover) 후에 보조 서버에서 저장 프로시저를 사용하여 복제를 구성하는 경우, 다른 복제본에서 사용하도록 설정된 게시 데이터베이스에 대한 끌어오기 구독을 설정하려면 현재 게시자가 아닌 원래 게시자의 이름을 **sp_addpullsubscription** 또는 **sp_addmergepullsubscription**의 *\@publisher* 매개 변수로 지정해야 합니다. 그러나 장애 조치 후 게시 데이터베이스를 활성화하면 시스템 테이블에 저장된 게시자 인스턴스 이름이 현재 주 호스트의 이름이 됩니다. 이 경우 *\@publisher* 매개 변수에 대해 현재 주 복제본의 호스트 이름을 사용합니다.  
  
    > [!NOTE]  
    >  **sp_addpublication** 같은 일부 프로시저의 경우 *\@publisher* 매개 변수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이외 게시자에 대해서만 지원되며, 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always On과는 관련이 없습니다.  
  
-   장애 조치 후 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 에서 구독을 동기화하려면 구독자에서 끌어오기 구독을 동기화하고 활성 게시자에서 밀어넣기 구독을 동기화합니다.  
  
##  <a name="removing-a-published-database-from-an-availability-group"></a><a name="RemovePublDb"></a> 가용성 그룹에서 게시된 데이터베이스 제거  
 게시된 데이터베이스를 가용성 그룹에서 제거하거나 게시된 멤버 데이터베이스가 있는 가용성 그룹을 삭제할 경우 다음 문제를 고려하세요.  
  
-   원래 게시자의 게시 데이터베이스를 가용성 그룹 주 복제본에서 제거할 경우 *\@redirected_publisher* 매개 변수 값을 지정하지 않고 **sp_redirect_publisher**를 실행하여 게시자/데이터베이스 쌍에 대한 리디렉션을 제거해야 합니다.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     주 복제본에서 데이터베이스가 복구 중 상태로 남게 되므로 복원해야 합니다. 이렇게 하면 원래 게시자에 대해 복제가 변함 없이 작동합니다.  
  
-   게시 데이터베이스를 원래 게시자에서 복제본으로 장애 조치하며 데이터베이스를 가용성 그룹 주 복제본에서 제거할 경우 **sp_redirect_publisher** 저장 프로시저를 실행하여 원래 게시자를 명시적으로 새 게시자로 리디렉션합니다. 데이터베이스가 복구 중 상태로 남게 되므로 복원해야 합니다. 이렇게 하면 가용성 그룹에 있을 때와 마찬가지로 복제가 작동합니다.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     서버에 더 이상 액세스할 수 없더라도 원래 게시자의 원격 서버를 배포자에서 제거하지 마세요. 게시 메타데이터 쿼리를 충족하려면 배포자에 원래 게시자의 서버 메타데이터가 필요합니다.  
  
-   가용성 그룹 전체를 제거할 경우 복제된 멤버 데이터베이스와 관련된 동작은 게시된 데이터베이스를 가용성 그룹에서 제거할 때와 동일합니다. 데이터베이스를 복원하고 리디렉션을 수정한 후 곧바로 마지막 주 복제본부터 복제를 다시 시작할 수 있습니다. 데이터베이스를 원래 게시자에서 복원하는 경우 리디렉션을 제거해야 합니다. 데이터베이스를 다른 호스트에서 복원하는 경우 새 호스트로 명시적으로 리디렉션을 설정해야 합니다.  
  
    > [!NOTE]  
    >  게시된 멤버 데이터베이스가 있는 가용성 그룹을 제거하거나 게시된 데이터베이스를 가용성 그룹에서 제거하면 게시된 데이터베이스의 모든 복사본이 복구 중 상태로 남게 됩니다. 데이터베이스를 복원하면 각각이 게시된 데이터베이스로 표시됩니다. 한 복사본에만 게시 메타데이터를 유지해야 합니다. 게시된 데이터베이스 복사본에 대해 복제를 비활성화하려면 먼저 모든 구독 및 게시를 데이터베이스에서 제거합니다.  
  
     **sp_dropsubscription** 을 실행하여 게시 구독을 제거합니다. *\@ignore_distributor* 매개 변수를 1로 설정하여 배포자의 활성 게시 데이터베이스에 관한 메타데이터를 유지합니다.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     **sp_droppublication** 을 실행하여 모든 게시를 제거합니다. 다시 *\@ignore_distributor* 매개 변수를 1로 설정하여 배포자의 활성 게시 데이터베이스에 대한 메타데이터를 유지합니다.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     **sp_replicationdboption** 을 실행하여 데이터베이스에 대한 복제를 사용하지 않도록 설정합니다.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     이때 게시된 데이터베이스의 복사본을 유지하거나 삭제할 수 있습니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [Always On 가용성 그룹에 대한 복제 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
-   [복제, 변경 내용 추적, 변경 데이터 캡처 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)  
  
-   [복제 관리 FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
-   [복제 구독자 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹: 상호 운용성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [SQL Server 복제](../../../relational-databases/replication/sql-server-replication.md)  
  
  
