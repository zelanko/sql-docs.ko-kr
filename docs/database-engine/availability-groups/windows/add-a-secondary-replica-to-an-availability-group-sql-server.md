---
title: 가용성 그룹에 보조 복제본 추가(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 6669dcce-85f9-495f-aadf-7f62cff4a9da
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eaa6e495f3f4df128541deb6024b0c915abe378a
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34770119"
---
# <a name="add-a-secondary-replica-to-an-availability-group-sql-server"></a>가용성 그룹에 보조 복제본 추가(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [사전 요구 사항 및 제한 사항](#PrerequisitesRestrictions)  
  
     [보안](#Security)  
  
-   **복제본을 추가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **후속 작업:**  [복제본을 추가한 후](#FollowUp)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 가용성 그룹을 처음 만들어 보는 경우 이 섹션을 먼저 읽는 것이 좋습니다.  
  
##  <a name="PrerequisitesRestrictions"></a> 사전 요구 사항 및 제한 사항  
  
-   주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)를 참조하세요.  
  
##  <a name="Security"></a> 보안  
  
###  <a name="Permissions"></a> Permissions  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **복제본을 추가하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 마우스 오른쪽 단추로 클릭하고 다음 명령 중 하나를 선택합니다.  
  
    -   가용성 그룹에 복제본 추가 마법사를 실행하려면 **복제본 추가** 명령을 선택합니다. 자세한 내용은 [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)을 참조하세요.  
  
    -   또는 **속성** 명령을 선택하여 **가용성 그룹 속성** 대화 상자를 엽니다. 이 대화 상자에서 복제본을 추가하는 단계는 다음과 같습니다.  
  
        1.  대화 상자의 **가용성 복제본** 창에서 **추가** 단추를 클릭합니다. 그러면 빈 서버 인스턴스 필드가 선택된 상태로 복제본 항목이 만들어지고 선택됩니다.  
  
        2.  가용성 복제본 호스팅을 위한 사전 요구 사항을 충족하는 서버 인스턴스의 이름을 입력합니다.  
  
         다른 복제본을 추가하려면 위의 단계를 반복합니다. 복제본 지정을 마치면 **확인** 을 클릭하여 작업을 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **복제본을 추가하려면**  
  
1.  주 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  ALTER AVAILABILITY GROUP 문의 ADD REPLICA ON 절을 사용하여 가용성 그룹에 새 보조 복제본을 추가합니다. ENDPOINT_URL, AVAILABILITY_MODE 및 FAILOVER_MODE 옵션은 ADD REPLICA ON 절에 필요합니다. 다른 복제본 옵션 BACKUP_PRIORITY, SECONDARY_ROLE, PRIMARY_ROLE 및 SESSION_TIMEOUT은 선택 사항입니다. 자세한 내용은 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 끝점 URL이 `MyAG` 인 `COMPUTER04`에서 호스팅되는 기본 서버 인스턴스의 `TCP://COMPUTER04.Adventure-Works.com:5022'`라는 가용성 그룹에 새 복제본을 만듭니다. 이 복제본은 수동 장애 조치(Failover) 및 비동기 커밋 가용성 모드를 지원합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG ADD REPLICA ON 'COMPUTER04'   
       WITH (  
             ENDPOINT_URL = 'TCP://COMPUTER04.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **복제본을 추가하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  **New-SqlAvailabilityReplica** cmdlet을 사용합니다.  
  
     예를 들어 다음 명령은 `MyAg`라는 기존 가용성 그룹에 가용성 복제본을 추가합니다. 이 복제본은 수동 장애 조치(Failover) 및 비동기 커밋 가용성 모드를 지원합니다. 이 복제본은 이 보조 역할에서 읽기 액세스 연결을 지원하므로 읽기 전용 프로세싱을 이 복제본으로 오프로드할 수 있습니다.  
  
    ```  
    $agPath = "SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
    $endpointURL = "TCP://PrimaryServerName.domain.com:5022"  
    $failoverMode = "Manual"  
    $availabilityMode = "AsynchronousCommit"  
    $secondaryReadMode = "AllowAllConnections"  
  
    New-SqlAvailabilityReplica -Name SecondaryServer\Instance `   
    -EndpointUrl $endpointURL `   
    -FailoverMode $failoverMode `   
    -AvailabilityMode $availabilityMode `   
    -ConnectionModeInSecondaryRole $secondaryReadMode `   
    -Path $agPath  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 보조 복제본을 추가한 후  
 기존 가용성 그룹에 대한 복제본을 추가하려면 다음 단계를 수행해야 합니다.  
  
1.  새 보조 복제본을 호스팅할 서버 인스턴스에 연결합니다.  
  
2.  새 보조 복제본을 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 기존 Always On 가용성 그룹에 보조 복제본을 추가하는 방법에 대해 설명합니다.  
  
3.  가용성 그룹의 각 데이터베이스에 대해 보조 복제본을 호스팅하는 서버 인스턴스에 보조 데이터베이스를 만듭니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
  
4.  각각의 새로운 보조 데이터베이스를 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 복제본을 관리하려면**  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
