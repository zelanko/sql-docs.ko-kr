---
title: 가용성 그룹에 데이터베이스 추가
description: 'T-SQL(Transact-SQL), PowerShell 또는 SQL Server Management Studio를 사용하여 Always On 가용성 그룹에 데이터베이스를 추가합니다. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 262a4538774d2827d60367d1d96a12fb15e2d0f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66789428"
---
# <a name="add-a-database-to-an-always-on-availability-group"></a>Always On 가용성 그룹에 데이터베이스 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 Always On 가용성 그룹에 데이터베이스를 추가하는 방법을 설명합니다.  
  

  
## <a name="prerequisites-and-restrictions"></a>사전 요구 사항 및 제한 사항  
  
-   주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   데이터베이스는 주 복제본을 호스팅하는 서버 인스턴스에 있어야 하며 가용성 데이터베이스에 대한 사전 요구 사항과 제한 사항을 준수해야 합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)를 참조하세요.  
  
 
##  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  

  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 마우스 오른쪽 단추로 클릭하고 다음 명령 중 하나를 선택합니다.  
  
    -   가용성 그룹에 데이터베이스 추가 마법사를 시작하려면 **데이터베이스 추가** 명령을 선택합니다. 자세한 내용은 [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)을 참조하세요.  
  
    -   **가용성 그룹 속성** 대화 상자에서 데이터베이스를 지정하여 하나 이상의 데이터베이스를 추가하려면 **속성** 명령을 선택합니다. 데이터베이스를 추가하는 단계는 다음과 같습니다.  
  
        1.  **가용성 데이터베이스** 창에서 **추가** 단추를 클릭합니다. 그러면 빈 데이터베이스 필드가 만들어지고 선택됩니다.  
  
        2.  가용성 데이터베이스 선행 조건을 충족하는 데이터베이스의 이름을 입력합니다.  
  
         다른 데이터베이스를 추가하려면 위의 단계를 반복합니다. 데이터베이스 지정을 마치면 **확인** 을 클릭하여 작업을 완료합니다.  
  
         **가용성 그룹 속성** 대화 상자를 사용하여 가용성 그룹에 데이터베이스를 추가한 후에는 보조 복제본을 호스팅하는 각 서버 인스턴스에서 해당 보조 데이터베이스를 구성해야 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  

  
1.  주 복제본을 호스팅하는 서버 인스턴스를 호스팅하는 서버 인스턴스에 연결합니다.    
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* ADD DATABASE *database_name* [,...*n*]  
  
     여기서 *group_name* 은 가용성 그룹의 이름이고, *database_name* 은 그룹에 추가할 데이터베이스의 이름입니다.  
  
     다음 예에서는 *MyDb3* 데이터베이스를 *MyAG* 가용성 그룹에 추가합니다.  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  가용성 그룹에 데이터베이스를 추가한 후에는 보조 복제본을 호스팅하는 각 서버 인스턴스에서 해당 보조 데이터베이스를 구성해야 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  

  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  **Add-SqlAvailabilityDatabase** cmdlet을 사용합니다.  
  
     예를 들어 다음 명령은 보조 데이터베이스 `MyDd` 을(를) `MyAG` 가용성 그룹에 추가합니다. 이 가용성 그룹의 주 복제본은 `PrimaryServer\InstanceName`에 의해 호스트됩니다.  
  
    ```  
  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
3.  가용성 그룹에 데이터베이스를 추가한 후에는 보조 복제본을 호스팅하는 각 서버 인스턴스에서 해당 보조 데이터베이스를 구성해야 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
 전체 예제를 보려면 아래의 [예제(PowerShell)](#PSExample)를 참조하세요.  
  
###  <a name="PSExample"></a> 예제(PowerShell)  
 다음 예는 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스에 있는 데이터베이스에서 보조 데이터베이스를 준비하고, 이 데이터베이스를 가용성 그룹에 주 데이터베이스로 추가한 다음, 보조 데이터베이스를 가용성 그룹에 조인하는 전체 과정을 보여 줍니다. 가장 먼저, 이 예에서는 데이터베이스와 해당 트랜잭션 로그를 백업합니다. 그런 다음 보조 복제본을 호스팅하는 서버 인스턴스로 데이터베이스 및 로그 백업을 복원합니다.  
  
 이 예제에서는 **Add-SqlAvailabilityDatabase** 를 두 번 호출합니다. 먼저 주 복제본에서 호출해서 데이터베이스를 가용성 그룹에 추가한 다음 보조 복제본에서 호출해서 해당 복제본에 있는 보조 데이터베이스를 가용성 그룹에 조인합니다. 보조 복제본이 두 개 이상인 경우 각 보조 복제본에서 보조 데이터베이스를 복원 및 조인합니다.  
  
```  
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
