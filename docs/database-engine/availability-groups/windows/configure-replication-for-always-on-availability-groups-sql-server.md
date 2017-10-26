---
title: "Always On 가용성 그룹에 대한 복제 구성(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 4e001426-5ae0-4876-85ef-088d6e3fb61c
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b1c8cbe1c3b1682b6994859d134bd2a4de432fd6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="configure-replication-for-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹에 대한 복제 구성(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 및 Always On 가용성 그룹을 구성하는 과정은 7단계로 구성됩니다. 각 단계에 대해서는 다음 섹션에서 자세하게 설명합니다.  
  
1.  [데이터베이스 게시 및 구독 구성](#step1)  
  
2.  [Always On 가용성 그룹을 구성합니다.](#step2)  
  
3.  [모든 보조 복제본 호스트에 대해 복제가 구성되었는지 확인](#step3)  
  
4.  [보조 복제본 호스트를 복제 게시자로 구성](#step4)  
  
5.  [원래 게시자를 가용성 그룹 수신기 이름으로 리디렉션](#step5)  
  
6.  [유효성 검사 저장 프로시저를 실행하여 구성 확인](#step6)  
  
7.  [원래 게시자를 복제 모니터에 추가](#step7)  
  
 1단계와 2단계는 순서를 바꿔서 수행할 수도 있습니다.  
  
##  <a name="step1"></a> 1. 데이터베이스 게시 및 구독 구성  
 **배포자 구성**  
  
 배포 데이터베이스를 가용성 그룹에 배치할 수 없습니다.  
  
1.  배포자에서 배포를 구성합니다. 구성에 저장 프로시저를 사용하는 경우 **sp_adddistributor**를 실행합니다. *@password* 매개 변수를 사용하여 원격 게시자에서 배포자에 연결할 때 사용될 암호를 식별합니다. 암호는 원격 배포자를 설정할 때 각 원격 게시자에서도 필요합니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = '**Strong password for distributor**';  
    ```  
  
2.  배포자에서 배포 데이터베이스를 만듭니다. 구성에 저장 프로시저를 사용하는 경우 **sp_adddistributiondb**를 실행합니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributiondb  
        @database = 'distribution',  
        @security_mode = 1;  
    ```  
  
3.  원격 게시자를 구성합니다. 배포자 구성에 저장 프로시저를 사용하는 경우 **sp_adddistpublisher**를 실행합니다. *@security_mode* 매개 변수는 복제 에이전트에서 실행되는 게시자 유효성 검사 저장 프로시저에서 현재 주 복제본에 연결하는 방법을 결정하는 데 사용됩니다. 1로 설정하면 Windows 인증을 사용하여 현재 주 복제본에 연결합니다. 0으로 설정하면 지정된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @login *@login* @password *@password* 인증을 사용합니다. 지정된 로그인 및 암호가 각 보조 복제본에서 유효해야만 유효성 검사 저장 프로시저가 해당 복제본에 연결할 수 있습니다.  
  
    > [!NOTE]  
    >  수정된 복제 에이전트가 배포자와는 다른 컴퓨터에서 실행될 경우 Windows 인증으로 주 복제본에 연결하려면 복제본 호스트 컴퓨터 간 통신에 대해 Kerberos 인증이 구성되어 있어야 합니다. 현재 주 복제본 연결에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 사용하는 경우에는 Kerberos 인증이 필요하지 않습니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistpublisher  
        @publisher = 'AGPrimaryReplicaHost',  
        @distribution_db = 'distribution',  
        @working_directory = '\\MyReplShare\WorkingDir',  
        @login = 'MyPubLogin',  
        @password = '**Strong password for publisher**';  
    ```  
  
 자세한 내용은 [sp_adddistpublisher&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)를 참조하세요.  
  
 **원래 게시자에서 게시자 구성**  
  
1.  원격 배포를 구성합니다. 게시자 구성에 저장 프로시저를 사용하는 경우 **sp_adddistributor**를 실행합니다. *@password* 값은 배포를 설정하기 위해 배포자에서 **sp_adddistrbutor**를 실행할 때 사용한 것과 동일한 값으로 지정합니다.  
  
    ```  
    exec sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = 'MyDistPass'  
    ```  
  
2.  데이터베이스를 복제할 수 있도록 설정합니다. 게시자 구성에 저장 프로시저를 사용하는 경우 **sp_replicationdboption**을 실행합니다. 데이터베이스에 대해 트랜잭션 복제와 병합 복제를 모두 구성하려는 경우 각각을 따로 설정해야 합니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'true';  
  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'merge publish',  
        @value = 'true';  
    ```  
  
3.  복제 게시, 아티클 및 구독을 만듭니다. 복제 구성 방법은 데이터 및 데이터베이스 개체 게시를 참조하세요.  
  
##  <a name="step2"></a> 2. Always On 가용성 그룹 구성  
 의도한 주 복제본에서 게시되거나 게시할 데이터베이스를 멤버 데이터베이스로 추가하여 가용성 그룹을 만듭니다. 가용성 그룹 마법사를 사용하는 경우 마법사가 초기에 보조 복제본 데이터베이스를 동기화하도록 할 수 있습니다. 또는 백업 및 복원을 사용하여 직접 초기화를 수행할 수 있습니다.  
  
 가용성 그룹에 대해 복제 에이전트가 현재 주 복제본에 연결할 때 사용할 DNS 수신기를 만듭니다. 지정한 수신기 이름은 원래 게시자/게시된 데이터베이스 쌍의 리디렉션 대상으로 사용됩니다. 예를 들어 DDL을 사용하여 가용성 그룹을 구성하는 경우 다음 코드 예제를 사용하여 `MyAG`라는 기존 가용성 그룹에 대한 가용성 그룹 수신기를 지정할 수 있습니다.  
  
```  
ALTER AVAILABILITY GROUP 'MyAG'   
    ADD LISTENER 'MyAGListenerName' (WITH IP (('10.120.19.155', '255.255.254.0')));  
```  
  
 자세한 내용은 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)을 참조하세요.  
  
##  <a name="step3"></a> 3. 모든 보조 복제본 호스트에 대해 복제가 구성되었는지 확인  
 각 보조 복제본 호스트에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 복제를 지원하도록 구성되어 있는지 확인합니다. 각 보조 복제본 호스트에서 다음 쿼리를 실행하여 복제가 설치되었는지 확인할 수 있습니다.  
  
```  
USE master;  
GO  
DECLARE @installed int;  
EXEC @installed = sys.sp_MS_replication_installed;  
SELECT @installed;  
```  
  
 원래 게시자에 *@installed* 가 0이면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에 복제를 추가해야 합니다.  
  
##  <a name="step4"></a> 4. 보조 복제본 호스트를 복제 게시자로 구성  
 보조 복제본은 복제 게시자나 재게시자로 작동할 수 없지만 복제가 구성되어 있어야만 장애 조치(failover) 후 보조 복제본이 작업을 넘겨 받을 수 있습니다. 배포자에서 각 보조 복제본 호스트에 대해 배포를 구성합니다. 원래 게시자를 배포자에 추가할 때 지정한 것과 동일한 배포 데이터베이스 및 작업 디렉터리를 지정합니다. 배포 구성에 저장 프로시저를 사용하는 경우 **sp_adddistpublisher** 를 사용하여 원격 게시자를 배포자에 연결합니다. 원래 게시자에 *@login* @password *@password* 를 사용한 경우 보조 복제본 호스트를 게시자로 추가할 때 각각에 대해 동일한 값을 지정합니다.  
  
```  
EXEC sys.sp_adddistpublisher  
    @publisher = 'AGSecondaryReplicaHost',  
    @distribution_db = 'distribution',  
    @working_directory = '\\MyReplShare\WorkingDir',  
    @login = 'MyPubLogin',  
    @password = '**Strong password for publisher**';  
```  
  
 각 보조 복제본 호스트에서 배포를 구성합니다. 원래 게시자의 배포자를 원격 배포자로 식별합니다. 배포자에서 원래 **sp_adddistributor** 를 실행했을 때와 동일한 암호를 사용합니다. 배포 구성에 저장 프로시저를 사용하는 경우 *@password* 의 **sp_adddistributor** 매개 변수를 사용하여 암호를 지정합니다.  
  
```  
EXEC sp_adddistributor   
    @distributor = 'MyDistributor',  
    @password = '**Strong password for distributor**';  
```  
  
 각 보조 복제본 호스트에서 데이터베이스 게시의 밀어넣기 구독자가 연결된 서버로 표시되는지 확인합니다. 원격 게시자 구성에 저장 프로시저를 사용하는 경우 **sp_addlinkedserver** 를 사용하여 구독자(아직 없는 경우)를 게시자에 연결된 서버로 추가합니다.  
  
```  
EXEC sys.sp_addlinkedserver   
    @server = 'MySubscriber';  
```  
  
##  <a name="step5"></a> 5. 원래 게시자를 AG 수신기 이름으로 리디렉션  
 배포자의 배포 데이터베이스에서 **sp_redirect_publisher** 저장 프로시저를 실행하여 원래 게시자와 게시된 데이터베이스를 가용성 그룹의 가용성 그룹 수신기 이름에 연결합니다.  
  
```  
USE distribution;  
GO  
EXEC sys.sp_redirect_publisher   
@original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = 'MyAGListenerName';  
```  
  
##  <a name="step6"></a> 6. 복제 유효성 검사 저장 프로시저를 실행하여 구성 확인  
 배포자의 배포 데이터베이스에서 **sp_validate_replica_hosts_as_publishers** 저장 프로시저를 실행하여 이제 모든 복제본 호스트가 게시된 데이터베이스의 게시자로 작동하도록 구성되었는지 확인합니다.  
  
```  
USE distribution;  
GO  
DECLARE @redirected_publisher sysname;  
EXEC sys.sp_validate_replica_hosts_as_publishers  
    @original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = @redirected_publisher output;  
```  
  
 가용성 그룹에 대한 정보를 쿼리하려면 각 가용성 그룹 복제본 호스트에서 충분한 권한이 있는 로그인으로 **sp_validate_replica_hosts_as_publishers** 저장 프로시저를 실행해야 합니다. **sp_validate_redirected_publisher**와는 달리 이 저장 프로시저는 가용성 그룹 복제본에 연결할 때 호출자의 자격 증명을 사용하며 msdb.dbo.MSdistpublishers에 저장된 로그인을 사용하지 않습니다.  
  
> [!NOTE]  
>  읽기 권한을 허용하지 않거나 읽기 전용으로 지정해야 하는 보조 복제본 호스트의 유효성을 검사할 경우에는 다음 오류와 함께**sp_validate_replica_hosts_as_publishers** 가 실패합니다.  
>   
>  메시지 21899, 수준 11, 상태 1, 프로시저 **sp_hadr_verify_subscribers_at_publisher**, 줄 109  
>   
>  '976' 오류로 인해 리디렉션된 게시자 'MyReplicaHostName'에서 원래 게시자 'MyOriginalPublisher'의 구독자에 대한 sysserver 항목이 있는지 확인하기 위한 쿼리에 실패했습니다(오류 메시지 '오류 976, 수준 14, 상태 1, 메시지: 대상 데이터베이스 'MyPublishedDB'이(가) 가용성 그룹에 참여 중이며 현재 쿼리로 액세스할 수 없습니다. 데이터 이동이 일시 중지되었거나 가용성 복제본이 읽기 액세스로 설정되지 않았습니다. 이 데이터베이스 및 가용성 그룹 내 다른 데이터베이스에 읽기 전용 액세스를 허용하려면 그룹 내 하나 이상의 보조 가용성 복제본에 읽기 액세스를 설정하세요.  자세한 내용은 **온라인 설명서의** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문을 참조하세요.'.  
>   
>  복제본 호스트 'MyReplicaHostName'에 대해 하나 이상의 게시자 유효성 검사 오류가 발생했습니다.  
  
 이 동작은 정상적인 동작입니다. 이러한 보조 복제본 호스트에서 직접 sysserver 항목을 쿼리하여 구독자 서버 항목이 있는지 확인해야 합니다.  
  
##  <a name="step7"></a> 7. 원래 게시자를 복제 모니터에 추가  
 각 가용성 그룹 복제본에서 원래 게시자를 복제 모니터에 추가합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **복제**  
  
-   [Always On 게시 데이터베이스 유지 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [복제, 변경 내용 추적, 변경 데이터 캡처 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)  
  
-   [관리&#40;복제&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
 **가용성 그룹을 만들고 구성하려면**  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [가용성 복제본 추가 또는 수정 시 끝점 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Always On 가용성 그룹에 대한 데이터베이스 미러링 끝점 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹: 상호 운용성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [SQL Server 복제](../../../relational-databases/replication/sql-server-replication.md)  
  
  

