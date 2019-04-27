---
title: AlwaysOn 게시 데이터베이스 (SQL Server)를 유지 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a862c5c9cea1087f54a4dbff13b6c39eb5e39385
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62791994"
---
# <a name="maintaining-an-alwayson-publication-database-sql-server"></a>AlwaysOn 게시 데이터베이스 유지 관리(SQL Server)
  이 항목에서는 AlwaysOn 가용성 그룹을 사용할 경우 게시 데이터베이스 유지 관리와 관련하여 특별히 고려해야 할 사항에 대해 설명합니다.  
  
 
  
##  <a name="MaintainPublDb"></a> 가용성 그룹에서 게시된 데이터베이스 유지 관리  
 AlwaysOn 게시 데이터베이스를 유지 관리하는 작업은 표준 게시 데이터베이스를 유지 관리하는 작업과 기본적으로 동일하지만 다음 사항을 고려해야 합니다.  
  
-   관리는 주 복제본 호스트에서 수행되어야 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 게시는 **로컬 게시** 폴더 아래에 주 복제본 호스트 및 읽을 수 있는 보조 복제본을 표시됩니다. 읽을 수 없는 보조 복제본이 주 복제본으로 승격된 경우 장애 조치(failover) 후 수동으로 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 를 새로 고쳐 변경 내용을 반영해야 합니다.  
  
-   복제 모니터는 항상 원래 게시자에서 게시 정보를 표시합니다. 그러나 원래 게시자를 서버로 추가하면 어떤 복제본에서든지 복제 모니터에서 이 정보를 볼 수 있습니다.  
  
-   게시자 이름 지정 등을 위해 저장 프로시저나 RMO(복제 관리 개체)를 사용하여 현재 주 복제본에서 복제를 관리할 때는 복제용으로 설정된 데이터베이스(원래 게시자)에서 인스턴스 이름을 지정해야 합니다. 올바른 이름을 확인하려면 `PUBLISHINGSERVERNAME` 함수를 사용하십시오. 게시 데이터베이스를 가용성 그룹에 조인하면 보조 데이터베이스 복제본에 저장된 복제 메타데이터가 주 데이터베이스 복제본의 복제 메타데이터와 동일해집니다. 따라서 주 서버에서 복제용으로 설정된 게시 데이터베이스의 경우 보조 서버에서 시스템 테이블에 저장된 게시자 인스턴스 이름은 보조 서버가 아닌 주 서버의 이름입니다. 이러한 방식은 게시 데이터베이스가 보조로 장애 조치되는 경우 복제 구성 및 유지 관리에 영향을 줍니다. 예를 들어 장애 조치 후 보조에서 저장된 프로시저를 사용 하 여 복제를 구성할 경우 다른 복제본에서 사용 하도록 설정 된 게시 데이터베이스에 끌어오기 구독을 대신 원래 게시자의 이름을 지정 해야 합니다 변수로 현재 게시자는 *@publisher* 의 매개 변수 `sp_addpullsubscription` 또는 `sp_addmergepulllsubscription`합니다. 그러나 장애 조치 후 게시 데이터베이스를 활성화하면 시스템 테이블에 저장된 게시자 인스턴스 이름이 현재 주 호스트의 이름이 됩니다. 이 경우 *@publisher* 매개 변수에 대해 현재 주 복제본의 호스트 이름을 사용합니다.  
  
    > [!NOTE]  
    >  일부 프로시저의 경우와 같은 `sp_addpublication`, *@publisher* 매개 변수는 인스턴스는 게시자에 대해서만 지원 됩니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; 이러한 경우에 관련 되지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 합니다.  
  
-   장애 조치 후 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 에서 구독을 동기화하려면 구독자에서 끌어오기 구독을 동기화하고 활성 게시자에서 밀어넣기 구독을 동기화합니다.  
  
##  <a name="RemovePublDb"></a> 가용성 그룹에서 게시된 데이터베이스 제거  
 게시된 데이터베이스를 가용성 그룹에서 제거하거나 게시된 멤버 데이터베이스가 있는 가용성 그룹을 삭제할 경우 다음 문제를 고려하세요.  
  
-   원래 게시자의 게시 데이터베이스의 가용성 그룹 주 복제본에서 제거 되 면 실행 해야 합니다 `sp_redirect_publisher` 값을 지정 하지 않고 합니다 *@redirected_publisher* 제거 하기 위해 매개 변수는 게시자/데이터베이스 쌍에 대 한 리디렉션입니다.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     주 복제본에서 데이터베이스가 복구 중 상태로 남게 되므로 복원해야 합니다. 이렇게 하면 원래 게시자에 대해 복제가 변함 없이 작동합니다.  
  
-   게시 데이터베이스를 원래 게시자에서 복제본으로 장애 조치하며 데이터베이스를 가용성 그룹 주 복제본에서 제거할 경우 `sp_redirect_publisher` 저장 프로시저를 실행하여 원래 게시자를 명시적으로 새 게시자로 리디렉션합니다. 데이터베이스가 복구 중 상태로 남게 되므로 복원해야 합니다. 이렇게 하면 가용성 그룹에 있을 때와 마찬가지로 복제가 작동합니다.  
  
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
  
     `sp_dropsubscription`을 실행하여 게시의 구독을 제거합니다. 배포자에서 활성 게시 데이터베이스에 대한 메타데이터를 유지하려면 *@ignore_distributributor* 매개 변수를 1로 설정해야 합니다.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     `sp_droppublication`을 실행하여 모든 게시를 제거합니다. 다시 *@ignore_distributor* 매개 변수를 1로 설정하여 배포자의 활성 게시 데이터베이스에 대한 메타데이터를 유지합니다.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     `sp_replicationdboption`을 실행하여 데이터베이스에 대해 복제를 비활성화합니다.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     이때 게시된 데이터베이스의 복사본을 유지하거나 삭제할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [AlwaysOn 가용성 그룹 (SQL Server)에 대 한 복제 구성](always-on-availability-groups-sql-server.md)  
  
-   [복제, 변경 내용 추적, 변경 데이터 캡처 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [복제 관리 FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
-   [복제 구독자 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹: 상호 운용성 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [SQL Server 복제](../../../relational-databases/replication/sql-server-replication.md)  
  
  
