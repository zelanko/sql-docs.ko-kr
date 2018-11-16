---
title: 가용성 복제본에 백업 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 74bc40bb-9f57-44e4-8988-1d69c0585eb6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 791253a685908baf69fe789aabd199a5cad7e921
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600753"
---
# <a name="configure-backup-on-availability-replicas-sql-server"></a>가용성 복제본에 백업 구성(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹의 보조 복제본에 백업을 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  보조 복제본에 백업에 대한 개요를 보려면 [활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)또는 PowerShell을 사용하여 Always On 가용성 그룹의 보조 복제본에 백업을 구성하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 보조 복제본에 백업을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **후속 작업:**  [보조 복제본에 백업을 구성한 후의 작업](#FollowUp)  
  
-   [백업 기본 설정에 대한 정보를 가져오려면](#ForInfoAboutBuPref)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
|태스크|Permissions|  
|----------|-----------------|  
|가용성 그룹을 만들 때 보조 복제본에 백업을 구성하려면|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|가용성 그룹 또는 가용성 복제본을 수정하려면|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.|  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **보조 복제본에 백업을 구성하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장할 서버 이름을 클릭합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  백업 기본 설정을 구성할 가용성 그룹을 클릭하고 **속성** 명령을 선택합니다.  
  
4.  **가용성 그룹 속성** 대화 상자에서 **백업 기본 설정** 페이지를 선택합니다.  
  
5.  **백업 수행 위치** 패널에서 가용성 그룹의 자동화된 백업 기본 설정을 다음 옵션 중 선택합니다.  
  
     **보조 사용**  
     백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 이 옵션이 기본 옵션입니다.  
  
     **보조만**  
     백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
     **주**  
     백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
    > [!IMPORTANT]  
    >  로그 전달을 사용하여 가용성 그룹의 보조 데이터베이스를 준비하려는 경우 모든 보조 데이터베이스가 준비되고 가용성 그룹에 조인될 때까지 자동화된 백업 기본 설정을 **주** 로 설정합니다.  
  
     **임의의 복제본**  
     백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  자동화된 백업 기본 설정은 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자동화된 백업 기본 설정은 임시 백업에는 영향을 미치지 않습니다. 자세한 내용은 이 항목 뒷부분에 있는 [후속 작업: 보조 복제본에 백업을 구성한 후](#FollowUp) 을 참조하세요.  
  
6.  **복제본 백업 우선 순위** 표를 사용하여 가용성 복제본의 백업 우선 순위를 변경할 수 있습니다. 이 표는 가용성 그룹에 대한 복제본을 호스팅하는 각 서버 인스턴스의 현재 백업 우선 순위를 표시합니다. 표 열은 다음과 같습니다.  
  
     **서버 인스턴스**  
     가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스 이름입니다.  
  
     **백업 우선 순위(최저 = 1, 최고 = 100)**  
     이 복제본에 대한 백업을 수행하기 위한 우선 순위를 지정하며 동일한 가용성 그룹의 다른 복제본을 기준으로 합니다. 이 값은 0에서 100  사이의 정수입니다. 1은 가장 낮은 우선 순위를 나타내고 100은 가장 높은 우선 순위를 나타냅니다. **백업 우선 순위** 가 1이면 현재 사용 가능한 더 높은 우선 순위의 가용성 복제본이 없는 경우에만 해당 가용성 복제본이 백업 수행을 위해 선택됩니다.  
  
     **복제본 제외**  
     백업 수행을 위해 이 가용성 백업을 선택하지 않으려는 경우에 선택합니다. 이 값은 예를 들어 백업을 장애 조치할 대상으로 사용하지 않을 원격 가용성 복제본의 경우에 유용합니다.  
  
7.  변경 내용을 커밋하려면 **확인**을 클릭합니다.  
  
 **백업 기본 설정 페이지에 액세스하는 다른 방법**  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **보조 복제본에 백업을 구성하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  새 가용성 그룹을 만들려는 경우 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)을 사용하세요. 기존 가용성 그룹을 수정하려는 경우 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **보조 복제본에 백업을 구성하려면**  
  
1.  기본값(**cd**)을 주 복제본을 호스트하는 서버 인스턴스로 설정합니다.  
  
2.  필요한 경우 추가하거나 수정할 각 가용성 복제본의 백업 우선 순위를 구성합니다. 이 우선 순위는 어느 복제본이 가용성 그룹의 데이터베이스에서 자동 백업 요청을 지원해야 하는지를 결정하기 위해(우선 순위가 가장 높은 복제본이 선택됨) 주 복제본을 호스팅하는 서버 인스턴스가 사용합니다. 이 우선 순위는 1부터 100까지의 임의의 숫자일 수 있습니다. 우선 순위 0은 백업 요청 지원을 위한 후보로 해당 복제본을 고려하지 않아야 함을 나타냅니다.  기본 설정은 50입니다.  
  
     가용성 그룹에 가용성 복제본을 추가하는 경우 **New-SqlAvailabilityReplica** cmdlet을 사용합니다. 기존 가용성 복제본을 수정하는 경우 **Set-SqlAvailabilityReplica** cmdlet을 사용합니다. 두 경우 모두 **BackupPriority***n* 매개 변수를 지정해야 하며 여기서 *n*은 0부터 100 사이의 값입니다.  
  
     예를 들어 다음 명령은 가용성 복제본 `MyReplica` 의 백업 우선 순위를 **60**으로 설정합니다.  
  
    ```  
    Set-SqlAvailabilityReplica -BackupPriority 60 `  
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
3.  필요한 경우 만들거나 수정하는 가용성 그룹에 대해 자동화된 백업 기본 설정을 구성합니다. 이 기본 설정은 백업을 수행할 위치를 선택할 때 백업 작업에서 주 복제본을 평가하는 방식을 나타냅니다. 기본 설정은 보조 복제본을 사용하는 것입니다.  
  
     가용성 그룹을 만들 때 **New-SqlAvailabilityGroup** cmdlet을 사용합니다. 기존 가용성 그룹을 수정할 때 **Set-SqlAvailabilityGroup** cmdlet을 사용합니다. 두 경우 모두 **AutomatedBackupPreference** 매개 변수를 지정합니다.  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     **주**  
     백업이 항상 주 복제본에서 수행되도록 지정합니다. 이 옵션은 백업이 보조 복제본에서 실행될 때 지원되지 않는 차등 백업 만들기와 같은 백업 기능이 필요한 경우에 유용합니다.  
  
    > [!IMPORTANT]  
    >  로그 전달을 사용하여 가용성 그룹의 보조 데이터베이스를 준비하려는 경우 모든 보조 데이터베이스가 준비되고 가용성 그룹에 조인될 때까지 자동화된 백업 기본 설정을 **주** 로 설정합니다.  
  
     **SecondaryOnly**  
     백업이 주 복제본에서 수행되지 않도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우에는 백업이 수행되지 않아야 합니다.  
  
     **보조**  
     백업이 보조 복제본에서 수행되도록 지정합니다. 주 복제본이 유일한 온라인 복제본인 경우는 예외로, 이 경우에는 백업이 주 복제본에서 수행되어야 합니다. 이것이 기본 동작입니다.  
  
     **없음**  
     백업을 수행할 복제본을 선택할 때 백업 작업에서 가용성 복제본의 역할을 무시하도록 지정합니다. 백업 작업에서는 각 가용성 복제본의 작동 상태 및 연결 상태와 함께 백업 우선 순위 등의 기타 요인을 평가할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  **AutomatedBackupPreference**는 적용되지 않습니다. 이 기본 설정의 해석은 지정된 가용성 그룹의 데이터베이스에 대한 백업 작업으로 스크립팅하는 논리(있는 경우)에 따라 달라집니다. 자동화된 백업 기본 설정은 임시 백업에는 영향을 미치지 않습니다. 자세한 내용은 이 항목 뒷부분에 있는 [후속 작업: 보조 복제본에 백업을 구성한 후](#FollowUp) 을 참조하세요.  
  
     예를 들어 다음 명령은 가용성 그룹 **의** AutomatedBackupPreference `MyAg` 속성을 **SecondaryOnly**로 설정합니다. 주 복제본에서는 이 가용성 그룹의 데이터베이스 자동 백업이 절대 발생하지 않으며 대신 백업 우선 순위 설정 값이 가장 높은 보조 복제본으로 백업이 리디렉션됩니다.  
  
    ```  
    Set-SqlAvailabilityGroup `  
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `  
    -AutomatedBackupPreference SecondaryOnly  
    ```  
  
> [!NOTE]  
>  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 보조 복제본에 백업을 구성한 후  
 지정된 가용성 그룹에 대해 자동화된 백업 기본 설정을 고려하도록 하려면 백업 우선 순위가 0보다 큰(>0) 가용성 복제본을 호스팅하는 각 서버 인스턴스에서 가용성 그룹의 데이터베이스에 대한 백업 작업을 스크립팅해야 합니다. 현재 복제본이 기본 백업 복제본인지 여부를 확인하려면 백업 스크립트에서 [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) 함수를 사용합니다. 현재 서버 인스턴스가 호스팅하는 가용성 복제본이 백업에 대한 선호 복제본인 경우 이 함수가 1을 반환합니다. 그렇지 않으면 함수가 0을 반환합니다. 각 가용성 복제본에서 이 함수를 쿼리하는 간단한 스크립트를 실행하여 지정된 백업 작업을 실행할 복제본을 확인할 수 있습니다. 예를 들어 백업 작업 스크립트의 일반적인 코드 조각은 다음과 같습니다.  
  
```  
IF (NOT sys.fn_hadr_backup_is_preferred_replica(@DBNAME))  
BEGIN  
      Select ‘This is not the preferred replica, exiting with success’;  
      RETURN 0 – This is a normal, expected condition, so the script returns success  
END  
BACKUP DATABASE @DBNAME TO DISK=<disk>  
   WITH COPY_ONLY;  
```  
  
 이 논리를 사용하여 백업 작업을 스크립팅하면 동일한 일정으로 모든 가용성 복제본에 대해 실행할 작업을 예약할 수 있습니다. 이러한 각 작업은 동일한 데이터를 조사하여 실행해야 하는 작업을 확인하므로 예약된 작업 중 하나만이 실제로 백업 단계로 진행됩니다.  장애 조치(Failover)의 경우 스크립트나 작업을 수정할 필요가 없습니다. 가용성 복제본을 추가하도록 가용성 그룹을 다시 구성한 경우 백업 작업을 관리하려면 백업 작업을 복사하거나 예약하기만 하면 됩니다. 가용성 복제본을 제거한 경우 해당 복제본을 호스팅하는 서버 인스턴스에서 백업 작업을 삭제합니다.  
  
> [!TIP]  
>  [유지 관리 계획 마법사](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)를 사용하여 지정된 백업 작업을 만드는 경우 해당 작업에는 **sys.fn_hadr_backup_is_preferred_replica** 함수를 호출하고 확인하는 스크립팅 논리가 자동으로 포함됩니다. 그러나 백업 작업이 "기본 복제본이 아닙니다..." 메시지를 반환하지는 않습니다. 가용성 그룹의 가용성 복제본을 호스트하는 각 서버 인스턴스에서 각 가용성 데이터베이스에 대한 작업을 만들어야 합니다.  
  
##  <a name="ForInfoAboutBuPref"></a> 백업 기본 설정에 대한 정보를 가져오려면  
 다음은 보조 복제본에서의 백업과 관련된 정보를 가져오는 데 유용합니다.  
  
|보기|정보|관련 열|  
|----------|-----------------|----------------------|  
|[sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)|현재 복제본이 기본 백업 복제본인지 여부|이 오류에는 이 작업을 적용할 수 없습니다.|  
|[sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)|자동화된 백업 기본 설정|**automated_backup_preference**<br /><br /> **automated_backup_preference_desc**|  
|[sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)|지정된 가용성 복제본의 백업 우선 순위|**backup_priority**|  
|[sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)|복제본이 서버 인스턴스의 로컬 복제본인지 여부<br /><br /> 현재 역할<br /><br /> 작동 상태<br /><br /> 연결 상태<br /><br /> 가용성 복제본의 동기화 상태|**is_local**<br /><br /> **role**, **role_desc**<br /><br /> **operational_state**, **operational_state_desc**<br /><br /> **connected_state**, **connected_state_desc**<br /><br /> **synchronization_health**, **synchronization_health_desc**|  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
