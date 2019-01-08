---
title: 가용성 그룹에 대한 읽기 전용 라우팅 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3af17b9ee12846fc89e406420fa6405cb59e0af3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367929"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>가용성 그룹에 대한 읽기 전용 라우팅 구성(SQL Server)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 읽기 전용 라우팅을 지원하도록 AlwaysOn 가용성 그룹을 구성하려면 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용할 수 있습니다. *읽기 전용 라우팅*이란 특정 읽기 전용 연결 요청을 AlwaysOn의 사용 가능하고 [읽기 가능한 보조 복제본](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(즉, 보조 역할로 실행될 때 읽기 전용 작업을 허용하도록 구성된 복제본)으로 라우팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기능을 말합니다. 읽기 전용 라우팅을 지원하려면 가용성 그룹에 [가용성 그룹 수신기](../../listeners-client-connectivity-application-failover.md)가 있어야 합니다. 읽기 전용 클라이언트는 해당 연결 요청을 이 수신기에 전달해야 하며, 클라이언트의 연결 문자열에서는 애플리케이션 의도를 "읽기 전용"으로 지정해야 합니다. 즉, 해당 연결 요청은 *읽기 전용 연결 요청*이어야 합니다.  
  
> [!NOTE]
>  읽기 가능한 보조 복제본을 구성하는 방법은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
> 
> 
> 
> [!NOTE]
>  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서는 읽기 전용 라우팅 구성이 지원되지 않습니다.  
  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   가용성 그룹에 가용성 그룹 수신기가 있어야 합니다. 자세한 내용은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)가 있어야 합니다.  
  
-   보조 역할에서 읽기 전용으로 수락 하도록 하나 이상의 가용성 복제본을 구성 해야 합니다 (즉, 되도록 [읽기 가능한 보조 복제본](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn %20Availability %20Groups\).md)). 자세한 내용은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
  
-   현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="RORReplicaProperties"></a> 읽기 전용 라우팅을 지원하도록 구성하는 데 필요한 복제본 속성  
  
-   읽기 전용 라우팅을 지원할 읽기 가능한 보조 복제본 각각에 대해 *읽기 전용 라우팅 URL*을 지정해야 합니다. 이 URL은 로컬 복제본이 보조 역할로 실행되는 경우에만 적용됩니다. 필요에 따라 복제본별로 읽기 전용 라우팅 URL을 지정해야 합니다. 각 읽기 전용 라우팅 URL은 읽기 전용 연결 요청을 지정된 읽기 가능한 보조 복제본으로 라우팅하는 데 사용됩니다. 일반적으로 모든 읽기 가능한 보조 복제본에는 읽기 전용 라우팅 URL이 할당됩니다.  
  
     가용성 복제본에 대한 읽기 전용 라우팅 URL을 계산하는 방법에 대한 자세한 내용은 [Calculating read_only_routing_url for AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)(AlwaysOn에 대한 read_only_routing_url 계산)을 참조하세요.  
  
-   주 복제본으로 사용될 때 읽기 전용 라우팅을 지원하도록 할 각 가용성 복제본에 대해 *읽기 전용 라우팅 목록*을 지정해야 합니다. 지정된 읽기 전용 라우팅 목록은 로컬 복제본이 주 역할로 실행되는 경우에만 적용됩니다. 필요에 따라 복제본별로 이 목록을 지정해야 합니다. 일반적으로 각 읽기 전용 라우팅 목록의 끝에는 로컬 복제본의 URL과 함께 모든 읽기 전용 라우팅 URL이 포함됩니다.  
  
    > [!NOTE]  
    >  읽기 전용 연결 요청은 현재 주 복제본의 읽기 전용 라우팅 목록에 있는 사용 가능하고 읽기 가능한 첫 번째 보조 복제본으로 라우팅됩니다. 부하 분산은 없습니다.  
  
> [!NOTE]  
>  가용성 그룹 수신기 및 읽기 전용 라우팅에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)가 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
|태스크|사용 권한|  
|----------|-----------------|  
|가용성 그룹을 만들 때 복제본을 구성하려면|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|가용성 복제본을 수정하려면|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.|  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **읽기 전용 라우팅을 구성 하려면**  
  
> [!NOTE]  
>  코드 예제를 보려면 이 섹션의 뒷부분에 나오는 [예(Transact-SQL)](#TsqlExample)를 참조하세요.  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  새 가용성 그룹에 대한 복제본을 지정하려는 경우 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다. 기존 가용성 그룹에 대한 복제본을 추가하거나 수정하려는 경우 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    -   보조 역할에 대한 읽기 전용 라우팅을 구성하려면 ADD REPLICA 또는 MODIFY REPLICA WITH 절에서 다음과 같이 SECONDARY_ROLE 옵션을 지정합니다.  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*')**  
  
         읽기 전용 라우팅 URL의 매개 변수는 다음과 같습니다.  
  
         *system-address*  
         대상 컴퓨터 시스템을 명확하게 식별하는 시스템 이름, 정규화된 도메인 이름 또는 IP 주소 등의 문자열입니다.  
  
         *port*  
         [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스 엔진에서 사용하는 포트 번호입니다.  
  
         예를 들어   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         복제본이 읽기 전용 연결을 허용하도록 이미 구성되어 있는 경우 MODIFY REPLICA 절에서 ALLOW_CONNECTIONS는 선택 사항입니다.  
  
         자세한 내용은 [AlwaysOn에 대한 read_only_routing_url 계산](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)을 참조하십시오.  
  
    -   주 역할에 대한 읽기 전용 라우팅을 구성하려면 ADD REPLICA 또는 MODIFY REPLICA WITH 절에서 다음과 같이 PRIMARY_ROLE 옵션을 지정합니다.  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **= ('*`server`*'** [ **하십시오**하는 중... *n* ] **))**  
  
         여기서 *server* 는 가용성 그룹의 읽기 전용 보조 복제본을 호스트하는 서버 인스턴스를 식별합니다.  
  
         예를 들어   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  읽기 전용 라우팅 목록을 구성하기 전에 읽기 전용 라우팅 URL을 설정해야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 기존 가용성 그룹 `AG1` 의 두 가용성 복제본 중 하나가 현재 주 역할을 소유하고 있는 경우 가용성 복제본이 읽기 전용 라우팅을 지원하도록 수정합니다. 가용성 복제본을 호스팅하는 서버 인스턴스를 식별하려면 이 예제에서는 `COMPUTER01` 및 `COMPUTER02` 인스턴스 이름을 지정합니다.  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **읽기 전용 라우팅을 구성 하려면**  
  
> [!NOTE]  
>  코드 예제를 보려면 이 섹션의 뒷부분에 나오는 [예제(PowerShell)](#PSExample)을 참조하세요.  
  
1.  기본값(`cd`)을 주 복제본을 호스팅하는 서버 인스턴스로 설정합니다.  
  
2.  가용성 그룹에 가용성 복제본을 추가하는 경우 `New-SqlAvailabilityReplica` cmdlet을 사용합니다. 기존 가용성 복제본을 수정하는 경우 `Set-SqlAvailabilityReplica` cmdlet을 사용합니다. 관련 매개 변수는 다음과 같습니다.  
  
    -   보조 역할에 대 한 읽기 전용 라우팅을 구성 하려면 지정 된 **ReadonlyRoutingConnectionUrl "*`url`*"** 매개 변수입니다.  
  
         여기서 *url* 은 읽기 전용 연결을 위해 복제본으로 라우팅할 때 사용할 연결 FQDN(정규화된 도메인 이름) 및 포트입니다. 예를 들어  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         자세한 내용은 [AlwaysOn에 대한 read_only_routing_url 계산](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)을 참조하십시오.  
  
    -   주 역할에 대 한 연결 액세스를 구성 하려면 지정할 **ReadonlyRoutingList "*`server`*"** [ **,**... *n* ] 여기서 *server* 가용성 그룹의 읽기 전용 보조 복제본을 호스팅하는 서버 인스턴스를 식별 합니다. 예를 들어  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  복제본의 읽기 전용 라우팅 목록을 구성하기 전에 읽기 전용 라우팅 URL을 설정해야 합니다.  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경에서 `Get-Help` cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> 예제(PowerShell)  
 다음 예에서는 읽기 전용 라우팅을 위해 가용성 그룹에 주 복제본과 보조 복제본 하나를 구성합니다. 먼저, 이 예에서는 각 복제본에 읽기 전용 라우팅 URL을 할당합니다. 그런 다음 주 복제본에 읽기 전용 라우팅 목록을 설정합니다. 연결 문자열에 "ReadOnly" 속성이 설정된 연결은 보조 복제본으로 리디렉션됩니다. 이 보조 복제본을 읽을 수 없는 경우(`ConnectionModeInSecondaryRole` 설정으로 확인) 연결이 다시 주 복제본으로 전달됩니다.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> 후속편: 읽기 전용 라우팅을 구성한 후의 작업  
 현재 주 복제본과 읽기 가능한 보조 복제본 두 역할 모두가 읽기 전용 라우팅을 지원하도록 구성되고 나면 읽기 가능한 보조 복제본은 가용성 그룹 수신기를 통해 연결한 클라이언트로부터 읽기 전용 연결 요청을 받을 수 있습니다.  
  
> [!TIP]  
>  사용 하는 경우는 [bcp 유틸리티](../../../tools/bcp-utility.md) 또는 [sqlcmd 유틸리티](../../../tools/sqlcmd-utility.md)를 지정 하 여 읽기 전용 액세스를 위해 사용 되는 모든 보조 복제본에 읽기 전용 액세스를 지정할 수 있습니다는 `-K ReadOnly` 전환 합니다.  
  
###  <a name="ConnStringReqsRecs"></a> 클라이언트 연결 문자열에 대한 요구 사항 및 권장 사항  
 클라이언트 애플리케이션에서 읽기 전용 라우팅을 사용하려면 해당 연결 문자열이 다음 요구 사항을 충족해야 합니다.  
  
-   TCP 프로토콜을 사용합니다.  
  
-   애플리케이션 의도 특성/속성을 읽기 전용으로 설정합니다.  
  
-   읽기 전용 라우팅을 지원하도록 구성된 가용성 그룹의 수신기를 참조합니다.  
  
-   해당 가용성 그룹의 데이터베이스를 참조합니다.  
  
 또한 연결 문자열에서 각 서브넷의 각 복제본에 대해 병렬 클라이언트 스레드를 지원하는 다중 서브넷 장애 조치(Failover)를 설정하는 것이 좋습니다. 이렇게 하면 장애 조치 후 클라이언트 재연결 시간이 최소화됩니다.  
  
 연결 문자열 구문은 애플리케이션에서 사용하는 SQL Server 공급자에 따라 달라집니다. 다음 예에 나온 .NET Framework Data Provider 4.0.2 for SQL Server용 연결 문자열은 읽기 전용 라우팅에 사용해야 하며 권장되는 연결 문자열을 보여 줍니다.  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 읽기 전용 응용 프로그램 방식 및 읽기 전용 라우팅에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)가 있어야 합니다.  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>읽기 전용 라우팅이 올바르게 작동하지 않는 경우  
 읽기 전용 라우팅 구성 문제를 해결 하는 방법에 대 한 내용은 [ 읽기 전용 라우팅이 올바르게 작동 하지 않음](troubleshoot-always-on-availability-groups-configuration-sql-server.md)합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **읽기 전용 라우팅 구성을 보려면**  
  
-   [sys.availability_read_only_routing_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)(**read_only_routing_url** column)  
  
 **클라이언트 연결 액세스를 구성하려면**  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **응용 프로그램에서 연결 문자열을 사용하려면**  
  
-   [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [SQL Server Native Client에서 연결 문자열 키워드 사용](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [AlwaysOn에 대 한 read_only_routing_url 계산](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **백서:**  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [활성 보조: 읽기 가능한 보조 복제본 (AlwaysOn 가용성 그룹)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
  
  
