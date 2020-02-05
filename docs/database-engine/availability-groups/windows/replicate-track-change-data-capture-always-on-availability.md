---
title: 복제, 변경 내용 추적 및 변경 데이터 캡처 및 가용성 그룹
description: SQL Server Always On 가용성 그룹과 함께 사용하는 경우 복제, 변경 내용 추적 및 변경 데이터 캡처의 상호 운용성에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 08/21/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], AlwaysOn Availability Groups
- change data capture [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: e17a9ca9-dd96-4f84-a85d-60f590da96ad
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2e2a794a7e5bdafe4e07b5e7deb9a1007e4a7e73
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75235388"
---
# <a name="replication-change-tracking--change-data-capture---always-on-availability-groups"></a>복제, 변경 내용 추적 및 변경 데이터 캡처 - Always On 가용성 그룹
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제, CDC(변경 데이터 캡처) 및 CT(변경 내용 추적)는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 지원됩니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하면 고가용성 및 추가 데이터베이스 복구 기능을 제공할 수 있습니다.  
  
##  <a name="Overview"></a> 가용성 그룹을 사용한 복제 개요  
  
###  <a name="PublisherRedirect"></a> 게시자 리디렉션  
 게시된 데이터베이스가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 인식하는 경우 에이전트에 게시 데이터베이스에 대한 액세스 권한을 제공하는 배포자가 redirected_publishers 항목으로 구성됩니다. 이러한 항목은 가용성 그룹 수신기 이름을 사용하여 게시자 및 게시 데이터베이스에 연결함으로써 원래 구성되어 있는 게시자/데이터베이스 쌍을 리디렉션합니다. 가용성 그룹 수신기 이름을 통해 설정된 연결은 장애 조치(Failover) 시 실패합니다. 장애 조치(Failover) 후 복제 에이전트가 다시 시작되면 연결이 새 주 데이터베이스에 자동으로 리디렉션됩니다.  
  
 가용성 그룹에서 보조 데이터베이스는 게시자가 될 수 없습니다. 트랜잭션 복제가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]과 결합된 경우에만 다시 게시가 지원됩니다.  
  
 게시된 데이터베이스가 가용성 그룹의 구성원이고 게시자가 리디렉션되는 경우 가용성 그룹에 연결된 가용성 그룹 수신기 이름으로 리디렉션되어야 합니다. 게시자를 명시적 노드로 리디렉션할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 보조 복제본에 대한 장애 조치(Failover) 후에 복제 모니터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 게시 인스턴스 이름을 조정할 수 없으며 계속해서 원래 주 인스턴스 이름으로 복제 정보를 표시합니다. 장애 조치(Failover) 후 복제 모니터를 사용하여 추적 프로그램 토큰을 입력할 수 없지만 새 게시자가 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 입력한 추적 프로그램 토큰은 복제 모니터에 표시됩니다.  
  
###  <a name="Changes"></a> 가용성 그룹을 지원하기 위한 복제 에이전트에 대한 일반적 변경 사항  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하도록 세 가지 복제 에이전트가 수정되었습니다. 로그 판독기, 스냅샷 및 병합 에이전트는 배포 데이터베이스에서 리디렉션된 게시자를 쿼리하고 리디렉션된 게시자가 선언된 경우 반환된 가용성 그룹 수신기 이름을 사용하여 데이터베이스 게시자에 연결합니다.  
  
 기본적으로 원본 게시자가 리디렉션되었는지 확인하기 위해 에이전트가 배포자를 쿼리할 때는 리디렉션된 호스트를 에이전트에 반환하기 전에 현재 대상 또는 리디렉션의 적합성이 확인됩니다. 이 동작은 수행하는 것이 좋습니다. 하지만 에이전트 시작이 매우 자주 수행되는 경우 유효성 검사 저장 프로시저와 연결된 오버헤드의 비용이 너무 높은 것으로 간주될 수 있습니다. 로그 판독기, 스냅샷 및 병합 에이전트에는 새로운 명령줄 스위치인 *BypassPublisherValidation*이 추가되었습니다. 이 스위치를 사용하면 리디렉션된 게시자가 에이전트에 즉시 반환되고 유효성 검사 저장 프로시저의 실행이 무시됩니다.  
  
 유효성 검사 저장 프로시저에서 반환된 오류는 에이전트 기록 로그에 기록됩니다. 심각도가 16 이상인 오류가 발생할 경우 에이전트가 종료됩니다. 에이전트에는 새로운 주 데이터베이스로 장애 조치(Failover)를 수행할 때 게시된 데이터베이스로부터의 예상된 연결 해제를 처리할 수 있도록 몇 가지 재시도 기능이 기본 제공되어 있습니다.  
  
#### <a name="log-reader-agent-modifications"></a>로그 판독기 에이전트 수정 사항  
 로그 판독기 에이전트에는 다음과 같은 변경 사항이 포함됩니다.  
  
-   **복제된 데이터베이스 일관성**  
  
     게시된 데이터베이스가 가용성 그룹의 멤버인 경우, 기본적으로 로그 판독기는 모든 가용성 그룹 보조 복제본에서 아직 확정되지 않은 로그 레코드를 처리하지 않습니다. 이렇게 하면 장애 조치 시 구독자에 복제되는 모든 행이 새 주 복제본에도 있습니다.  
  
     게시자에 두 가용성 복제본(주 복제본 하나 및 보조 복제본 하나)만 있고 장애 조치가 발생하면, 모든 보조 데이터베이스가 다시 온라인 상태가 되거나 실패한 보조 복제본이 가용성 그룹에서 제거될 때까지 로그 판독기가 앞으로 이동하지 않기 때문에 원래의 주 복제본은 계속 중단된 상태로 유지됩니다. Always On이 보조 데이터베이스에 대한 변경 내용을 확정할 수 없으므로 보조 데이터베이스에 대해 실행 중인 로그 판독기는 앞으로 진행되지 않습니다. 로그 판독기를 계속 진행하고 재해 복구 기능을 포함하도록 하려면 ALTER AVAILABITY GROUP <group_name> REMOVE REPLICA를 사용하여 가용성 그룹에서 원래 주 복제본을 제거해야 합니다. 그런 다음 새 보조 복제본을 가용성 그룹에 추가합니다.  
  
-   **추적 플래그 1448**  
  
     추적 플래그 1448를 사용하면 비동기 보조 복제본이 변경 내용 수신을 확인하지 않은 경우에도 복제 로그 판독기가 앞으로 진행할 수 있습니다. 이 추적 플래그를 설정하면 로그 판독기가 항상 동기 보조 복제본을 기다립니다. 로그 판독기는 동기 보조 복제본에 대한 최소 승인을 넘지 않습니다. 이 추적 플래그는 단순히 가용성 그룹, 가용성 데이터베이스 또는 로그 판독기 인스턴스가 아니라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 적용됩니다. 이 추적 플래그는 다시 시작하지 않고 즉시 적용됩니다. 비동기 보조 복제본이 실패할 때 또는 미리 활성화할 수 있습니다.  
  
###  <a name="StoredProcs"></a> 가용성 그룹을 지원하는 저장 프로시저  
  
-   **sp_redirect_publisher**  
  
     저장 프로시저 **sp_redirect_publisher** 는 기존 게시자/데이터베이스 쌍에 대해 리디렉션된 게시자를 지정하는 데 사용됩니다. 게시자 데이터베이스가 가용성 그룹에 속하는 경우 리디렉션된 게시자는 가용성 그룹 수신기 이름입니다.  
  
-   **sp_get_redirected_publisher**  
  
     저장 프로시저 **sp_get_redirected_publisher** 는 복제 에이전트가 배포자에게 쿼리하여 게시자/데이터베이스 쌍에 정의된 리디렉션된 게시자가 있는지 여부를 확인하는 데 사용됩니다. 이 저장 프로시저는 두 가지 용도로 사용됩니다. 첫째, 에이전트가 원래 게시자가 리디렉션되었는지 여부를 확인할 수 있도록 해줍니다. 둘째, 명명된 데이터베이스에 대한 게시자 역할을 하는 대상 리디렉션 노드의 적합성을 확인하는 배포자(**sp_validate_redirected_publisher**)에서 실행되는 유효성 검사 저장 프로시저를 시작할 수 있습니다.  
  
     이 저장 프로시저를 실행하려면 호출자가 **sysadmin** 서버 역할 또는 배포 데이터베이스에 대한 **db_owner** 데이터베이스 역할의 구성원이거나 게시자 데이터베이스에 연결된 정의된 게시에 대한 **게시 액세스 목록** 의 구성원이어야 합니다.  
  
-   **sp_validate_redirected_publisher**  
  
     이 저장 프로시저는 현재 게시자가 게시된 데이터베이스를 호스팅할 수 있는지를 확인합니다. 언제든지 이 저장 프로시저를 호출하여 게시된 데이터베이스의 현재 호스트가 복제를 지원할 수 있는지 확인할 수 있습니다.  
  
-   **sp_validate_replicate_hosts_as_publishers**  
  
     에이전트에서 현재 주 복제본이 게시자 데이터베이스에 대한 복제 게시자로 작동할 수 있도록 하는 것이 유용하지만, Always On 가용성 데이터베이스에서 전체 복제 토폴로지의 유효성을 설정하려면 보다 일반적인 유효성 검사 기능이 필요합니다. 저장 프로시저 **sp_validate_replica_hosts_as_publishers** 는 이 요구를 충족하도록 설계되었습니다.  
  
     이 저장 프로시저는 항상 수동으로 실행됩니다. 호출자는 배포자의 **sysadmin** 이거나, 배포 데이터베이스의 **dbowner** 이거나, 게시자 데이터베이스 게시의 **게시 액세스 목록** 의 멤버여야 합니다. 또한 호출자의 로그인이 모든 가용성 복제본 호스트에 유효한 로그인이고 게시자 데이터베이스에 연결된 가용성 데이터베이스에 대한 선택 권한이 있어야 합니다.  
  
###  <a name="CDC"></a> 변경 데이터 캡처  
 CDC(변경 데이터 캡처)에 사용되는 데이터베이스는 장애 발생 시에도 데이터베이스를 사용할 수 있도록 유지할 뿐만 아니라 데이터베이스 테이블에 대한 변경 내용을 계속 모니터링하여 CDC 변경 테이블에 보관하기 위해 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 활용할 수 있습니다. CDC 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 이 구성되는 순서는 중요하지 않습니다. CDC 사용 데이터베이스는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 추가될 수 있으며 Always On 가용성 그룹의 멤버인 데이터베이스는 CDC를 사용하도록 설정될 수 있습니다. 그러나 두 경우 모두 CDC 구성은 항상 현재 또는 의도된 주 복제본에 대해 수행됩니다. CDC는 로그 판독기 에이전트를 사용하여 이 항목의 이전 **로그 판독기 에이전트 수정** 섹션에 설명된 대로 동일한 제한을 가집니다.  
  
-   **복제를 사용하지 않는 변경 데이터 캡처를 위한 변경 사항 수집**  
  
     CDC는 데이터베이스에 사용되지만 복제는 사용되지 않는 경우 로그에서 변경 사항을 수집하여 CDC 변경 테이블에 보관하는 데 사용되는 캡처 프로세스는 SQL 에이전트 작업을 소유한 CDC 호스트에서 실행됩니다.  
  
     장애 조치(Failover) 후 변경 사항 수집을 재개하려면 저장 프로시저 **sp_cdc_add_job** 이 새 주 복제본에서 실행되어 로컬 캡처 작업을 만들어야 합니다.  
  
     다음 예에서는 캡처 작업을 만듭니다.  
  
    ```sql  
    EXEC sys.sp_cdc_add_job @job_type = 'capture';  
    ```  
  
-   **복제를 사용하는 변경 데이터 캡처를 위한 변경 사항 수집**  
  
     데이터베이스에서 CDC와 복제를 모두 사용하는 경우 로그 판독기가 CDC 변경 테이블을 채웁니다. 이 경우 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 활용하기 위해 복제에서 사용되는 기술은 로그에서 변경 내용을 계속 수집하고 장애 조치 후 CDC 변경 테이블에 보관하도록 합니다. 변경 테이블이 채워지도록 하기 위해 이 구성에서 CDC에 대해 어떠한 추가 구성 작업도 수행할 필요가 없습니다.  
  
-   **변경 데이터 캡처 정리**  
  
     새 주 데이터베이스에서 적절한 정리가 수행되도록 하려면 항상 로컬 정리 작업을 만들어야 합니다. 다음 예에서는 정리 작업을 만듭니다.  
  
    ```sql  
    EXEC sys.sp_cdc_add_job @job_type = 'cleanup';  
    ```  
  
    > [!NOTE]  
    >  장애 조치(Failover)가 발생하기 전에 모든 가능한 장애 조치(Failover) 대상에서 작업을 만든 다음 호스트의 가용성 복제본이 새로운 주 복제본이 될 때까지 해당 작업을 사용 안 함으로 표시해야 합니다. 또한 이전 주 데이터베이스에서 실행 중인 CDC 작업은 로컬 데이터베이스가 보조 데이터베이스가 되면 해제되어야 합니다. 작업을 사용하지 않거나 사용하도록 설정하려면 *sp_update_job &#40;Transact-SQL&#41;\@의* [enabled](../../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md) 옵션을 사용합니다. CDC 작업을 만드는 방법은 [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)에서 지원됩니다.  
  
-   **Always On 주 데이터베이스 복제본에 CDC 역할 추가**  
  
     CDC에 대해 테이블이 사용하도록 설정된 경우 데이터베이스 역할을 캡처 인스턴스와 연결할 수 있습니다. 역할이 지정된 경우 테이블 변경 사항에 액세스하기 위해 CDC 테이블 반환 함수를 사용하려는 사용자는 추적된 테이블 열에 대한 액세스를 선택해야 할 뿐만 아니라 명명된 역할의 멤버여야 합니다. 지정된 역할이 아직 없으면 역할이 만들어집니다. Always On 주 데이터베이스에 데이터베이스 역할이 자동으로 추가된 경우 가용성 그룹의 보조 데이터베이스에도 해당 역할이 전파됩니다.  
  
-   **CDC 변경 데이터 및 Always On에 액세스하는 클라이언트 애플리케이션**  
  
     또한 TVF(테이블 반환 함수) 또는 연결된 서버를 사용하여 변경 테이블 데이터에 액세스하는 클라이언트 애플리케이션은 장애 조치(Failover) 후 적합한 CDC 호스트를 찾는 기능이 필요합니다. 가용성 그룹 수신기 이름은 연결 대상을 다른 호스트로 투명하게 다시 지정할 수 있도록 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서 제공하는 메커니즘입니다. 가용성 그룹 수신기 이름을 가용성 그룹에 연결한 다음에는 TCP 연결 문자열에서 이를 사용할 수 있습니다. 가용성 그룹 수신기 이름은 서로 다른 두 가지 연결 시나리오에서 사용할 수 있습니다.  
  
    -   한 시나리오에서는 연결 요청이 항상 현재 주 복제본으로 전달되도록 합니다.  
  
    -   다른 시나리오에서는 연결 요청이 읽기 전용 보조 복제본으로 전달되도록 합니다.  
  
     읽기 전용 보조 복제본을 찾기 위해서는 가용성 그룹에 대해 읽기 전용 라우팅 목록도 정의해야 합니다. 읽기 전용 보조 복제본으로 액세스 라우팅에 자세한 내용은 [읽기 전용 라우팅을 위해 가용성 복제본을 구성하려면](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConfigureARsForROR)을 참조하세요.  
  
    > [!NOTE]  
    >  가용성 그룹 수신기 이름을 만들고 이를 사용하여 클라이언트 애플리케이션이 가용성 그룹 데이터베이스 복제본에 액세스할 때는 약간의 전파 지연이 발생합니다.  
  
     CDC 데이터베이스를 호스팅하는 가용성 그룹에 대해 가용성 그룹 수신기 이름이 정의되었는지 여부를 확인하려면 다음 쿼리를 사용합니다. 이 쿼리는 가용성 그룹 수신기 이름이 만들어진 경우 이를 반환합니다.  
  
    ```sql  
    SELECT dns_name   
    FROM sys.availability_group_listeners AS l  
    INNER JOIN sys.availability_databases_cluster AS d  
        ON l.group_id = d.group_id  
    WHERE d.database_name = N'MyCDCDB';  
    ```  
  
-   **쿼리 부하를 읽기 가능한 보조 복제본으로 리디렉션**  
  
     대부분의 경우 클라이언트 애플리케이션은 항상 현재 주 복제본에 연결하려고 하지만 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 활용하기 위해 현재 주 복제본만 사용할 수 있는 것은 아닙니다. 가용성 그룹이 읽기 가능한 보조 복제본을 지원하도록 구성된 경우 보조 노드에서도 변경 데이터를 수집할 수 있습니다.  
  
     가용성 그룹이 구성된 경우 SECONDARY_ROLE과 연결된 ALLOW_CONNECTIONS 특성을 사용하여 지원되는 보조 액세스 유형을 지정합니다. ALL로 구성된 경우 보조 복제본에 대한 모든 연결이 허용되지만 읽기 전용 액세스가 필요한 연결만 성공합니다. READ_ONLY로 구성된 경우 연결이 성공하려면 보조 데이터베이스에 연결할 때 읽기 전용 의도를 지정해야 합니다. 자세한 내용은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
  
     다음 쿼리를 사용하면 읽기 가능한 보조 복제본에 연결하기 위해 읽기 전용 의도가 필요한지 여부를 확인할 수 있습니다.  
  
    ```sql  
    SELECT g.name AS AG, replica_server_name, secondary_role_allow_connections_desc  
    FROM sys.availability_replicas AS r  
    JOIN sys.availability_groups AS g  
        ON r.group_id = g.group_id  
    WHERE g.name = N'MY_AG_NAME;  
    ```  
  
     가용성 그룹 수신기 이름 또는 명시적인 노드 이름을 사용하여 보조 복제본을 찾을 수 있습니다. 가용성 그룹 수신기 이름을 사용하는 경우 액세스가 모든 적합한 보조 복제본으로 전송됩니다.  
  
     보조 복제본에 액세스하기 위해 **sp_addlinkedserver**를 사용하여 연결된 서버를 만들 경우, 가용성 그룹 수신기 이름 또는 명시적인 서버 이름에 *\@datasrc* 매개 변수가 사용되고 읽기 전용 의도를 지정하기 위해 *\@provstr* 매개 변수가 사용됩니다.  
  
    ```sql  
    EXEC sp_addlinkedserver   
    @server = N'linked_svr',   
    @srvproduct=N'SqlServer',  
    @provider=N'SQLNCLI11',   
    @datasrc=N'AG_Listener_Name',   
    @provstr=N'ApplicationIntent=ReadOnly',   
    @catalog=N'MY_DB_NAME';  
    ```  
  
-   **CDC 변경 데이터에 대한 클라이언트 액세스 및 도메인 로그인**  
  
     일반적으로 Always On 가용성 그룹의 멤버인 데이터베이스에 있는 데이터를 변경하기 위해서는 클라이언트 액세스에 대해 도메인 로그인을 사용해야 합니다. 장애 조치 후 변경 데이터에 대한 액세스를 계속하도록 하려면 가용성 그룹 복제본을 지원하는 모든 호스트에 대한 액세스 권한이 도메인 사용자에게 필요합니다. 데이터베이스 사용자를 주 복제본의 데이터베이스에 추가하고 사용자를 도메인 로그인과 연결하면 데이터베이스 사용자가 보조 데이터베이스에 전파되고 지정된 도메인 로그인과 계속 연결된 상태로 유지됩니다. 새 데이터베이스 사용자를 SQL Server 인증 로그인과 연결하면 로그인 없이도 보조 데이터베이스에서 해당 사용자가 전파됩니다. 데이터베이스 사용자가 원래 정의된 주 복제본에서 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 로그인을 사용하여 변경 데이터를 액세스할 수 있지만 이 노드는 액세스가 가능한 유일한 노드입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 로그인은 모든 보조 데이터베이스의 데이터에 액세스할 수 없으며 데이터베이스 사용자가 정의된 원래 데이터베이스가 아닌 다른 모든 새 주 데이터베이스의 데이터에 액세스할 수 없습니다.  
     
-   **변경 데이터 캡처 해제**  
Always On 가용성 그룹의 일부인 데이터베이스에서 변경 데이터 캡처를 사용하지 않도록 설정해야 하는 경우 로그 잘림이 영향을 받지 않도록 추가 단계를 수행해야 합니다. 변경 데이터 캡처를 비활성화한 후에 변경 데이터 캡처에서 로그 잘림을 차단하지 않도록 하려면 다음 단계 중 하나를 구현해야 합니다.
    - 모든 보조 복제본 인스턴스에서 SQL Server 서비스를 다시 시작합니다.
    - 또는 가용성 그룹의 모든 보조 복제본 인스턴스에서 데이터베이스를 제거하고, 자동 또는 수동 시드를 사용하여 가용성 그룹 복제본 인스턴스에 추가합니다.
  
###  <a name="CT"></a> 변경 내용 추적  
 CT(변경 내용 추적)에 사용되는 데이터베이스는 Always On 가용성 그룹의 일부가 될 수 있습니다. 추가 구성은 필요하지 않습니다. 변경 데이터에 액세스하기 위해 CDC TVF(테이블 반환 함수)를 사용하는 변경 추적 클라이언트 애플리케이션은 장애 조치(Failover) 후 주 복제본을 찾는 기능이 필요합니다. 클라이언트 애플리케이션이 가용성 그룹 수신기 이름을 통해 연결할 경우 연결 요청이 항상 현재 주 복제본으로 올바르게 전송됩니다.  
  
> [!NOTE]  
>  변경 추적 데이터는 항상 주 복제본으로부터 가져와야 합니다. 보조 복제본으로부터 변경 데이터에 액세스하려고 시도하면 다음과 같은 오류가 발생합니다.  
>   
>  메시지 22117, 수준 16, 상태 1, 줄 1  
>   
>  보조 가용성 복제본의 멤버인 데이터베이스(즉, 보조 데이터베이스)에서는 변경 내용 추적이 지원되지 않습니다. 주 복제본에서 데이터베이스에 대해 변경 내용 추적 쿼리를 실행하세요.  
  
##  <a name="Prereqs"></a> 복제 사용을 위한 필수 구성 요소, 제한 사항 및 고려 사항  
 이 섹션에서는 필수 구성 요소, 제한 사항 및 권장 사항을 비롯하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용하여 복제를 배포할 때의 고려 사항에 대해 설명합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
  
-   트랜잭션 복제를 사용할 때 게시 데이터베이스가 가용성 그룹에 있으면 게시자와 배포자 모두 최소한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]를 실행해야 합니다. 구독자는 낮은 수준의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 수 있습니다.  
  
-   병합 복제를 사용할 때 게시 데이터베이스가 가용성 그룹에 있는 경우:  
  
    -   밀어넣기 구독: 게시자와 배포자 모두 최소한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]를 실행해야 합니다.  
  
    -   끌어오기 구독: 게시자, 배포자 및 구독자 데이터베이스는 최소한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 있어야 합니다. 구독자의 병합 에이전트가 가용성 그룹이 보조 그룹으로 장애 조치(Failover)하는 방법을 이해해야 하기 때문입니다.  
  
-   게시자 인스턴스는 Always On 가용성 그룹에 참여하는 데 필요한 모든 사전 요구 사항을 충족합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)에서 지원됩니다.  
  
### <a name="restrictions"></a>제한  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 지원되는 복제 조합은 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||**게시자**|**배포자**|**구독자**|  
|**트랜잭션**|yes<br /><br /> 참고: 양방향 및 상호 트랜잭션 복제에 대한 지원을 포함하지 않습니다.|yes|yes| 
|**P2P**|예|예|예|  
|**병합**|yes|예|예|  
|**스냅샷**|yes|예|yes|
  
 **배포자 데이터베이스는 데이터베이스 미러링과 함께 사용할 수 없습니다.  
  
### <a name="considerations"></a>고려 사항  
  
-   배포 데이터베이스는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 또는 데이터베이스 미러링과 함께 사용할 수 없습니다. 복제 구성이 배포자가 구성되는 SQL Server 인스턴스에 연결되므로 배포 데이터베이스를 미러링하거나 복제할 수 없습니다. 배포자에 대해 고가용성을 제공하려면 SQL Server 장애 조치(Failover) 클러스터를 사용합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요.  
  
-   보조 데이터베이스에 대한 구독자 장애 조치(Failover)는 지원되지만 병합 복제 구독자에게는 수동 절차입니다. 절차는 미러링된 구독자 데이터베이스를 장애 조치하는 데 사용되는 방법과 동일합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]참여 시 트랜잭션 복제 구독자는 특수 조작이 필요하지 않습니다. 가용성 그룹에 참여하려면 구독자가 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상을 실행해야 합니다.  자세한 내용은 [복제 구독자 및 Always On 가용성 그룹(SQL Server)](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)을 참조하세요.
  
-   로그인, 작업, 연결된 서버를 포함하여 데이터베이스 외부에 있는 메타데이터 및 개체는 보조 복제본에 전파되지 않습니다. 장애 조치(Failover) 후 새로운 주 데이터베이스에 메타데이터 및 개체가 필요한 경우 이를 수동으로 복사해야 합니다. 자세한 내용은 [가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **복제**  
  
-   [Always On 가용성 그룹에 대한 복제 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
-   [Always On 게시 데이터베이스 유지 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [복제 관리 FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
 **변경 데이터 캡처**  
  
-   [변경 데이터 캡처 설정 및 해제&#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)  
  
-   [변경 데이터 캡처 관리 및 모니터링&#40;SQL Server&#41;](../../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
-   [변경 데이터 작업&#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
 **Change tracking**  
  
-   [변경 내용 추적 설정 및 해제&#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)  
  
-   [변경 내용 추적 관리&#40;SQL Server&#41;](../../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
-   [변경 내용 추적 사용&#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [복제 구독자 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹: 상호 운용성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Always On 장애 조치(Failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [변경 내용 추적 정보&#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [SQL Server 복제](../../../relational-databases/replication/sql-server-replication.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
