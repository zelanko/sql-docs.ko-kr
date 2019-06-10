---
title: 가용성 그룹에 보조 데이터베이스 조인
description: T-SQL(Transact-SQL), PowerShell 또는 SQL Server Management Studio를 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 단계입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.joindbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: fd7efe79-c1f9-497d-bfe7-b2a2b2321cf5
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 8e9fecbbe5894eb6a6804c48f4d37facf01359a1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772542"
---
# <a name="join-a-secondary-database-to-an-always-on-availability-group"></a>Always On 가용성 그룹에 보조 데이터베이스 조인
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다. 보조 복제본용 보조 데이터베이스를 준비한 후에는 가능한 한 빨리 해당 데이터베이스를 가용성 그룹에 조인해야 합니다. 그러면 해당 주 데이터베이스에서 보조 데이터베이스로 데이터 이동이 시작됩니다.  
   
> [!NOTE]  
>  보조 데이터베이스가 그룹에 조인된 후의 사항에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
   
##  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   보조 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   보조 복제본은 이미 가용성 그룹에 조인되어 있어야 합니다. 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
  
-   보조 데이터베이스는 최근에 준비된 것이어야 합니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
  
###  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹에 보조 데이터베이스를 조인하려면**  
  
1.  개체 탐색기에서 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  변경할 가용성 그룹을 확장하고 **가용성 데이터베이스** 노드를 확장합니다.  
  
4.  마우스 오른쪽 단추로 데이터베이스를 클릭하고 **가용성 그룹에 조인**을 클릭합니다.  
  
5.  **가용성 그룹에 데이터베이스 조인** 대화 상자가 열립니다. 제목 표시줄에 표시된 가용성 그룹 이름과 표에 표시된 데이터베이스 이름을 확인하고 **확인**이나 **취소**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹에 보조 데이터베이스를 조인하려면**  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같이 [ALTER DATABASE 문의 SET HADR 절](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) 을 사용합니다.  
  
     ALTER DATABASE *database_name* SET HADR AVAILABILITY GROUP = *group_name*  
  
     여기서 *database_name* 은 조인할 데이터베이스의 이름이고 *group_name* 은 가용성 그룹의 이름입니다.  
  
     다음 예에서는 `Db1`이라는 보조 데이터베이스를 `MyAG` 가용성 그룹의 로컬 보조 복제본에 조인합니다.  
  
    ```  
    ALTER DATABASE Db1 SET HADR AVAILABILITY GROUP = MyAG;  
    ```  
  
    > [!NOTE]  
    >  컨텍스트에서 사용되는 이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 보려면 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)를 참조하세요.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹에 보조 데이터베이스를 조인하려면**  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
2.  **Add-SqlAvailabilityDatabase** cmdlet을 사용하여 하나 이상의 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
     예를 들어 다음 명령은 보조 데이터베이스 `Db1`을 보조 복제본을 호스팅하는 서버 인스턴스 중 하나의 가용성 그룹 `MyAG` 에 조인합니다.  
  
    ```  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "Db1"  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
