---
title: 가용성 그룹에서 데이터베이스 제거
description: T-SQL(Transact-SQL), PowerShell 또는 SQL Server Management Studio를 사용하여 Always On 가용성 그룹에서 주 데이터베이스를 제거하는 단계입니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dfba294b5c07fc7053669c5c4ebbbd46217efb18
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822638"
---
# <a name="remove-a-primary-database-from-an-always-on-availability-group"></a>Always On 가용성 그룹에서 주 데이터베이스 제거
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 Always On 가용성 그룹에서 주 데이터베이스와 해당 보조 데이터베이스를 모두 제거하는 방법에 대해 설명합니다.  
  
##  <a name="Prerequisites"></a> 사전 요구 사항 및 제한 사항  
  
-   이 태스크는 주 복제본에서만 지원됩니다. 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
 
##  <a name="Permissions"></a> 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 데이터베이스를 제거하려면**  
  
1.  개체 탐색기에서 제거할 데이터베이스의 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 선택하고 **가용성 데이터베이스** 노드를 확장합니다.  
  
4.  이 단계는 여러 데이터베이스 그룹을 제거할지 아니면 데이터베이스를 하나만 제거할지에 따라 다음과 같이 달라집니다.  
  
    -   여러 데이터베이스를 제거하려면 **개체 탐색기 정보** 창을 사용하여 제거할 모든 데이터베이스를 표시하고 선택합니다. 자세한 내용은 [개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)을 참조하세요.  
  
    -   단일 데이터베이스를 제거하려면 **개체 탐색기** 창 또는 **개체 탐색기 정보** 창에서 데이터베이스를 선택합니다.  
  
5.  선택한 데이터베이스를 마우스 오른쪽 단추로 클릭하고 명령 메뉴에서 **가용성 그룹에서 데이터베이스 제거** 를 선택합니다.  
  
6.  **가용성 그룹에서 데이터베이스 제거** 대화 상자에서 나열된 데이터베이스를 모두 제거하려면 **확인**을 클릭합니다. 모든 데이터베이스를 제거하지 않으려면 **취소**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 데이터베이스를 제거하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE DATABASE *availability_database_name*  
  
     여기서 *group_name* 은 가용성 그룹의 이름이고, *database_name* 은 제거할 데이터베이스의 이름입니다.  
  
     다음 예에서는 `Db6` 가용성 그룹에서 `MyAG` 이라는 데이터베이스를 제거합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 데이터베이스를 제거하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  **Remove-SqlAvailabilityDatabase** cmdlet을 사용하여 가용성 그룹에서 제거할 가용성 데이터베이스의 이름을 지정합니다. 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있는 경우 주 데이터베이스와 해당 보조 데이터베이스가 모두 가용성 그룹에서 제거됩니다.  
  
     예를 들어 다음 명령은 `MyDb9` 라는 가용성 그룹에서 `MyAg`가용성 데이터베이스를 제거합니다. 명령이 주 복제본을 호스팅하는 서버 인스턴스에서 실행되므로 주 데이터베이스와 모든 보조 데이터베이스가 모두 가용성 그룹에서 제거됩니다. 보조 복제본에서 더 이상 이 데이터베이스에 대한 데이터 동기화가 발생하지 않습니다.  
  
    ```  
    Remove-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\AvailabilityDatabases\MyDb9
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 그룹에서 가용성 데이터베이스를 제거한 후  
 가용성 데이터베이스를 가용성 그룹에서 제거하면 이전 주 데이터베이스와 해당 보조 데이터베이스 사이의 데이터 동기화가 해제됩니다. 이전 주 데이터베이스는 온라인 상태로 유지됩니다. 모든 해당 보조 데이터베이스는 복원 중 상태가 됩니다.  
  
 여기서 제거된 보조 데이터베이스를 다음과 같은 다른 방법으로 처리할 수 있습니다.  
  
-   해당 보조 데이터베이스가 더 이상 필요하지 않은 경우 삭제할 수 있습니다.  
  
     자세한 내용은 [데이터베이스 삭제](../../../relational-databases/databases/delete-a-database.md)를 참조하세요.  
  
-   가용성 그룹에서 제거된 보조 데이터베이스에 액세스하려면 데이터베이스를 복구할 수 있습니다. 그러나 제거된 보조 데이터베이스를 복구하면 같은 이름의 독립적인 두 분기 데이터베이스가 온라인 상태가 됩니다. 클라이언트가 이 두 데이터베이스 중 하나(일반적으로 가장 최근의 주 데이터베이스)에만 액세스할 수 있는지 확인해야 합니다.  
  
     자세한 내용은 [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
  
