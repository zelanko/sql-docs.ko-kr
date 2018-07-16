---
title: 자동 장애 조치 (Always On 가용성 그룹)에 대 한 상태 제어 유연한 장애 조치 정책 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4868c07427230de655fc8a1742458f4b4c72cfbb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193983"
---
# <a name="configure-the-flexible-failover-policy-to-control-conditions-for-automatic-failover-always-on-availability-groups"></a>유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치(failover)의 상태 제어(Always On 가용성 그룹)
  이 항목에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에 대해 유연한 장애 조치(failover) 정책을 구성하는 방법에 대해 설명합니다. 유연한 장애 조치(failover) 정책을 통해 가용성 그룹에 대해 자동 장애 조치를 수행해야 하는 상태를 세부적으로 제어할 수 있습니다. 자동 장애 조치를 트리거하는 오류 상태 및 상태 확인 빈도를 변경하여 자동 장애 조치가 수행될 가능성을 높이거나 줄임으로써 고가용성에 대한 SLA를 지원할 수 있습니다.  
  
  
  
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Limitations"></a> 자동 장애 조치에 대한 제한 사항  
  
-   자동 장애 조치가 발생하려면 현재 주 복제본과 하나의 보조 복제본을 자동 장애 조치를 사용하는 동기-커밋 가용성 모드용으로 구성하고 보조 복제본을 주 복제본과 동기화해야 합니다.  
  
-   가용성 그룹이 해당 WSFC 오류 임계값을 초과하면 WSFC 클러스터가 가용성 그룹에 대해 자동 장애 조치를 시도하지 않습니다. 또한 클러스터 관리자가 실패한 리소스 그룹을 수동으로 온라인 상태로 만들거나 데이터베이스 관리자가 가용성 그룹의 수동 장애 조치를 수행할 때까지 가용성 그룹의 WSFC 리소스 그룹이 실패한 상태로 유지됩니다. *WSFC 오류 임계값* 은 특정 기간 동안 가용성 그룹에 대해 지원되는 최대 오류 수로 정의됩니다. 기본 기간은 6시간이며, 이 기간 동안의 최대 오류 수에 대한 기본값은 *n*-1입니다. 여기서 *n* 은 WSFC 노드의 수입니다. 지정된 가용성 그룹에 대한 오류-임계값 값을 변경하려면 WSFC 장애 조치(Failover) 관리자 콘솔을 사용하세요.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
|태스크|사용 권한|  
|----------|-----------------|  
|새로운 가용성 그룹에 대해 유연한 장애 조치(failover) 정책을 구성하려면|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|기존 가용성 그룹의 정책을 수정하려면|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.|  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **유연한 장애 조치(failover) 정책을 구성하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  새 가용성 그룹을 만들려는 경우 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다. 기존 가용성 그룹을 수정하려는 경우 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    -   장애 조치 상태 수준을 설정하려면 FAILURE_CONDITION_LEVEL = *n* 옵션을 사용합니다. 여기서 *n* 은 1부터 5까지의 정수입니다.  
  
         예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 기존 가용성 그룹 `AG1`의 오류 상태 수준을 수준 1로 변경합니다.  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         각 정수 값과 오류 상태 수준의 관계는 다음과 같습니다.  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] 값|Level|자동 장애 조치가 시작되는 경우|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|1|서버 작동 중지 시. 장애 조치나 재시작으로 인해 SQL Server 서비스가 중지된 경우|  
        |2|2|서버 응답 없음 발생 시. 낮은 값의 조건이 모두 충족되거나, SQL Server 서비스가 클러스터에 연결되었지만 상태 확인 제한 시간 임계값을 초과했거나, 현재 주 복제본이 오류 상태인 경우|  
        |3|3|중대 서버 오류 발생 시. 낮은 값의 조건이 모두 충족되거나 내부 중대 서버 오류가 발생한 경우<br /><br /> 이 값은 기본 수준입니다.|  
        |4|4|일반 서버 오류 발생 시. 낮은 값의 조건이 모두 충족되거나 일반 서버 오류가 발생한 경우|  
        |5|5|지정된 오류 상태 발생 시. 낮은 값의 조건이 모두 충족되거나 지정된 오류 상태가 발생한 경우|  
  
         장애 조치 상태 수준에 대한 자세한 내용은 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치(Failover) 정책&#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)을 참조하세요.  
  
    -   상태 확인 제한 시간 임계값을 구성하려면 HEALTH_CHECK_TIMEOUT = *n* 옵션을 사용합니다. 여기서 *n*은 15000밀리초(15초)부터 4294967295밀리초까지의 정수입니다. 기본값은 30000밀리초(30초)입니다.  
  
         예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 기존 가용성 그룹 `AG1`의 상태 확인 제한 시간 임계값을 60,000밀리초(1분)로 변경합니다.  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **유연한 장애 조치(failover) 정책을 구성하려면**  
  
1.  기본 설정 (`cd`) 주 복제본을 호스팅하는 서버 인스턴스에 있습니다.  
  
2.  가용성 그룹에 가용성 복제본을 추가하는 경우 `New-SqlAvailabilityGroup` cmdlet을 사용합니다. 기존 가용성 복제본을 수정하는 경우 `Set-SqlAvailabilityGroup` cmdlet을 사용합니다.  
  
    -   장애 조치 상태 수준을 설정 하려면 사용 합니다 `FailureConditionLevel` *수준* 매개 변수, 위치, *수준* 는 다음 값 중 하나:  
  
        |값|Level|자동 장애 조치가 시작되는 경우|  
        |-----------|-----------|-------------------------------------------|  
        |`OnServerDown`|1|서버 작동 중지 시. 장애 조치나 재시작으로 인해 SQL Server 서비스가 중지된 경우|  
        |`OnServerUnresponsive`|2|서버 응답 없음 발생 시. 낮은 값의 조건이 모두 충족되거나, SQL Server 서비스가 클러스터에 연결되었지만 상태 확인 제한 시간 임계값을 초과했거나, 현재 주 복제본이 오류 상태인 경우|  
        |`OnCriticalServerError`|3|중대 서버 오류 발생 시. 낮은 값의 조건이 모두 충족되거나 내부 중대 서버 오류가 발생한 경우<br /><br /> 이 값은 기본 수준입니다.|  
        |`OnModerateServerError`|4|일반 서버 오류 발생 시. 낮은 값의 조건이 모두 충족되거나 일반 서버 오류가 발생한 경우|  
        |`OnAnyQualifiedFailureConditions`|5|지정된 오류 상태 발생 시. 낮은 값의 조건이 모두 충족되거나 지정된 오류 상태가 발생한 경우|  
  
         장애 조치 상태 수준에 대한 자세한 내용은 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치(Failover) 정책&#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)을 참조하세요.  
  
         예를 들어 다음 명령은 기존 가용성 그룹 `AG1`의 오류 상태 수준을 수준 1로 변경합니다.  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `   
        -FailureConditionLevel OnServerDown  
        ```  
  
    -   상태 확인 제한 시간 임계값을 설정 하려면 사용 합니다 `HealthCheckTimeout` *n* 매개 변수, 위치, *n* 은 15000 밀리초 (15 초)부터 4294967295 밀리초 사이의 정수입니다. 기본값은 30000밀리초(30초)입니다.  
  
         예를 들어 다음 명령은 기존 가용성 그룹 `AG1`의 상태 확인 제한 시간 임계값을 120,000밀리초(2분)로 변경합니다.  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
        -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Cmdlet의 구문을 보려면 사용 하 여는 `Get-Help` cmdlet은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)   
 [장애 조치 및 장애 조치 모드 &#40;AlwaysOn 가용성 그룹&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
  
  
