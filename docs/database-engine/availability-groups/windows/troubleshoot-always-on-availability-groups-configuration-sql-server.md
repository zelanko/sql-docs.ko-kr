---
title: 가용성 그룹에 대한 일반적인 문제 및 해결 방법
description: SQL Server에서 Always On 가용성 그룹에 대한 서버 인스턴스 구성과 관련된 일반적인 문제를 해결합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [SQL Server], deploying
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], configuring
ms.assetid: 8c222f98-7392-4faf-b7ad-5fb60ffa237e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4c2f30813e84591d41c9dc1e78f0679fea59fcf
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670706"
---
# <a name="troubleshoot-always-on-availability-groups-configuration-sql-server"></a>Always On 가용성 그룹 구성 문제 해결(SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 서버 인스턴스를 구성하는 것과 관련된 일반적인 문제를 해결하는 데 유용한 정보를 제공합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용할 수 없거나, 계정이 잘못 구성되거나, 데이터베이스 미러링 엔드포인트가 없거나, 엔드포인트에 액세스할 수 없거나(SQL Server 오류 1418), 네트워크 액세스 권한이 없거나, 데이터베이스 조인 명령이 실패(SQL Server 오류 35250)하는 경우가 일반적인 구성 문제에 해당합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 사전 요구 사항을 충족하는지 확인합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)를 참조하세요.  
  
 **항목 내용:**  
  
|섹션|Description|  
|-------------|-----------------|  
|[Always On 가용성 그룹을 사용할 수 없음](#IsHadrEnabled)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]의 인스턴스를 사용할 수 없는 경우 해당 인스턴스는 가용성 그룹 만들기를 지원하지 않고 가용성 복제본을 호스팅할 수 없습니다.|  
|[계정](#Accounts)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 실행되고 있는 계정을 올바르게 구성하기 위한 요구 사항에 대해 설명합니다.|  
|[엔드포인트](#Endpoints)|서버 인스턴스의 데이터베이스 미러링 엔드포인트 관련 문제를 진단하는 방법에 대해 설명합니다.|  
|[시스템 이름](#SystemName)|엔드포인트 URL에서 서버 인스턴스의 시스템 이름을 지정하는 대안이 요약되어 있습니다.|  
|[네트워크 액세스](#NetworkAccess)|가용성 복제본을 호스팅하는 각 서버 인스턴스에서 TCP를 통해 다른 각 서버 인스턴스의 포트에 액세스할 수 있어야 한다는 요구 사항에 대해 설명합니다.|  
|[엔드포인트 액세스(SQL Server 오류 1418)](#Msg1418)|이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 메시지에 대한 정보를 포함합니다.|  
|[데이터베이스 조인 실패(SQL Server 오류 35250)](#JoinDbFails)|주 복제본 연결이 활성화되지 않아서 가용성 그룹에 대한 보조 데이터베이스 조인에 실패하는 원인과 해결 방법에 대해 설명합니다.|  
|[읽기 전용 라우팅이 올바르게 작동하지 않음](#ROR)||  
|[관련 작업](#RelatedTasks)|가용성 그룹 구성 문제를 해결하는 방법에 대해 설명하는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 온라인 설명서에 있는 태스크 지향 항목 목록을 포함합니다.|  
|[관련 내용](#RelatedContent)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서에 포함되어 있지 않은 관련 리소스 목록을 포함합니다.|  
  
##  <a name="always-on-availability-groups-is-not-enabled"></a><a name="IsHadrEnabled"></a> Always On 가용성 그룹을 사용할 수 없음  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 각 인스턴스에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]기능을 사용하도록 설정해야 합니다. 자세한 내용은 [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
##  <a name="accounts"></a><a name="Accounts"></a> 계정  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 실행하고 있는 계정이 올바르게 구성되어 있어야 합니다.  
  
1.  계정에 올바른 권한이 있어야 합니다.  
  
    1.  파트너가 동일한 도메인 사용자 계정으로 실행되는 경우 올바른 사용자 로그인이 자동으로 두 **master** 데이터베이스에 모두 포함됩니다. 데이터베이스에 대한 간단한 보안 구성으로 권장됩니다.  
  
    2.  두 서버 인스턴스가 서로 다른 계정으로 실행되는 경우, 원격 서버 인스턴스의 **master** 에 각 계정에 대한 로그인을 만들고 이 로그인에 해당 서버 인스턴스의 데이터베이스 미러링 엔드포인트에 연결할 수 있는 CONNECT 권한을 부여해야 합니다. 자세한 내용은 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대한 로그인 계정 설정&#40;SQL Server&#41;](../../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)을 참조하세요.  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스와 같은 기본 제공 계정이나 비도메인 계정으로 실행 중인 경우에는 사용자가 엔드포인트 인증을 위한 인증서를 사용해야 합니다. 서비스 계정에서 동일한 도메인의 도메인 계정을 사용 중인 경우 모든 복제본 위치의 각 서비스 계정에 연결 권한을 부여하거나, 인증서를 사용할 수 있습니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트에 대한 인증서 사용 &#40;Transact-SQL &#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)을 참조하세요.  
  
##  <a name="endpoints"></a><a name="Endpoints"></a> 엔드포인트  
 엔드포인트를 올바르게 구성해야 합니다.  
  
1.  가용성 복제본을 호스트할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 각 인스턴스(각 *복제본 위치*)에 데이터베이스 미러링 엔드포인트가 있는지 확인합니다. 지정된 서버 인스턴스에 데이터베이스 미러링 엔드포인트가 있는지 여부를 확인하려면 [sys.database_mirroring_endpoints](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md) 카탈로그 뷰를 사용합니다. 자세한 내용은 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기 &#40;Transact-SQL &#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) 또는 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용 &#40;Transact-SQL &#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)을 참조하세요.  
  
2.  포트 번호가 정확한지 확인합니다.  
  
     서버 인스턴스의 데이터베이스 미러링 엔드포인트와 현재 연결된 포트를 식별하려면 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints;  
    GO  
    ```  
  
3.  설명하기 어려운 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 설치 문제의 경우 각 서버 인스턴스를 조사하여 올바른 포트에서 수신하고 있는지 확인하는 것이 좋습니다.  
  
4.  엔드포인트가 시작되었는지 확인합니다(STATE=STARTED). 각 서버 인스턴스에서 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     **state_desc** 열에 대한 자세한 내용은 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)를 참조하세요.  
  
     엔드포인트를 시작하려면 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     자세한 내용은 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-endpoint-transact-sql.md)을 참조하세요.  
  
5.  다른 서버에서 로그인할 경우 CONNECT 권한이 있는지 확인합니다. 엔드포인트에 대한 CONNECT 권한이 있는 사용자를 파악하려면 각 서버 인스턴스에서 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="system-name"></a><a name="SystemName"></a> System Name  
 엔드포인트 URL에서 서버 인스턴스의 시스템 이름에는 시스템을 명확하게 식별하는 모든 이름을 사용할 수 있습니다. 서버 주소는 시스템 이름(시스템이 같은 도메인에 있는 경우), 정규화된 도메인 이름 또는 IP 주소(가급적 고정 IP 주소)일 수 있습니다. 정규화된 도메인 이름을 사용하는 것이 좋습니다. 자세한 내용은 [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.  
  
##  <a name="network-access"></a><a name="NetworkAccess"></a> Network Access  
 가용성 복제본을 호스팅하는 각 서버 인스턴스에서 TCP를 통해 다른 각 서버 인스턴스의 포트에 액세스할 수 있어야 합니다. 이는 서버 인스턴스가 서로 트러스트하지 않는 다른 도메인(트러스트되지 않은 도메인)에 있을 경우 특히 유용합니다.  
  
##  <a name="endpoint-access-sql-server-error-1418"></a><a name="Msg1418"></a> 엔드포인트 액세스(SQL Server 오류 1418)  
 이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 메시지는 엔드포인트 URL에 지정된 서버 네트워크 주소가 없거나 도달할 수 없음을 나타내며 네트워크 주소 이름을 확인한 후 명령을 다시 실행하도록 제안합니다.  
  
##  <a name="join-database-fails-sql-server-error-35250"></a><a name="JoinDbFails"></a> 데이터베이스 조인 실패(SQL Server 오류 35250)  
 이 섹션에서는 주 복제본 연결이 활성화되지 않아서 가용성 그룹에 대한 보조 데이터베이스 조인에 실패하는 원인과 해결 방법에 대해 설명합니다.  
  
 **해결 방법:**  
  
1.  방화벽 설정을 검사하여 주 복제본과 보조 복제본(기본적으로 포트 5022)을 호스팅하는 서버 인스턴스 사이의 엔드포인트 포트 통신을 허용하는지 여부를 확인합니다.  
  
2.  네트워크 서비스 계정에 엔드포인트에 대한 연결 권한이 있는지 여부를 확인합니다.  
  
##  <a name="read-only-routing-is-not-working-correctly"></a><a name="ROR"></a> 읽기 전용 라우팅이 올바르게 작동하지 않음  
 다음 구성 값 설정을 확인하고 필요한 경우 수정합니다.  
  
|On...|작업|주석|링크|  
|---------|------------|--------------|----------|  
|현재 주 복제본|가용성 그룹 수신기가 온라인 상태인지 확인합니다.|**수신기가 온라인 상태인지 여부를 확인하려면:**<br /><br /> `SELECT * FROM sys.dm_tcp_listener_states;`<br /><br /> **오프라인 수신기를 다시 시작하려면:**<br /><br /> `ALTER AVAILABILITY GROUP myAG RESTART LISTENER 'myAG_Listener';`|[sys.dm_tcp_listener_states&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|현재 주 복제본|READ_ONLY_ROUTING_LIST에 읽기 가능한 보조 복제본을 호스팅하는 서버 인스턴스만 포함되어 있는지 확인합니다.|**읽기 가능한 보조 복제본을 확인하려면:** sys.availability_replicas(**secondary_role_allow_connections_desc** 열)<br /><br /> **읽기 전용 라우팅 목록을 보려면:** sys.availability_read_only_routing_lists<br /><br /> **읽기 전용 라우팅 목록을 변경하려면:** ALTER AVAILABILITY GROUP|[sys.availability_replicas&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)<br /><br /> [sys.availability_read_only_routing_lists&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|read_only_routing_list에 있는 모든 복제본|Windows 방화벽이 READ_ONLY_ROUTING_URL 포트를 차단하고 있는지 확인합니다.|-|[데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|read_only_routing_list에 있는 모든 복제본|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 다음을 확인합니다.<br /><br /> SQL Server 원격 연결이 사용되고 있는지 여부<br /><br /> TCP/IP가 사용되고 있는지 여부<br /><br /> IP 주소가 올바르게 구성되어 있는지 여부|-|[서버 속성 보기 또는 변경&#40;SQL Server&#41;](../../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)<br /><br /> [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)|  
|read_only_routing_list에 있는 모든 복제본|READ_ONLY_ROUTING_URL(TCP<strong>://</strong>*system-address*<strong>:</strong>*port*)에 올바른 FQDN(정규화된 도메인 이름) 및 포트 번호가 포함되어 있는지 확인합니다.|-|[Always On에 대한 read_only_routing_url 계산](/archive/blogs/mattn/calculating-read_only_routing_url-for-alwayson)<br /><br /> [sys.availability_replicas&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|클라이언트 시스템|클라이언트 드라이버가 읽기 전용 라우팅을 지원하는지 확인합니다.|-|[Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)|  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
-   [가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md)  
  
-   [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [장애 조치(Failover) 클러스터에 대한 이벤트 및 로그 보기](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 장애 조치(Failover) 클러스터 Cmdlet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461045(v=technet.10))  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [클라이언트 네트워크 구성](../../../database-engine/configure-windows/client-network-configuration.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
