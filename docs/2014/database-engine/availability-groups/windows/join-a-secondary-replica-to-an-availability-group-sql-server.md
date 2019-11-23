---
title: 가용성 그룹에 보조 복제본 조인(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39ee8bfc079445e177aa9b175019ae385b9f9f36
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797662"
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>가용성 그룹에 보조 복제본 조인(SQL Server)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 AlwaysOn 가용성 그룹에 보조 복제본을 조인하는 방법에 대해 설명합니다. AlwaysOn 가용성 그룹에 보조 복제본을 추가한 후에는 보조 복제본을 가용성 그룹에 조인해야 합니다. 복제본 조인 작업은 보조 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 수행해야 합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **보조 데이터베이스를 준비하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **후속 작업:** [보조 데이터베이스 구성](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   가용성 그룹의 주 복제본은 현재 온라인 상태여야 합니다.  
  
-   아직 가용성 그룹에 조인되지 않은 보조 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   로컬 서버 인스턴스에서 주 복제본을 호스팅하는 서버 인스턴스의 데이터베이스 미러링 엔드포인트에 연결할 수 있어야 합니다.  
  
> [!IMPORTANT]  
>  필수 구성 요소가 충족되지 않으면 조인 작업이 실패합니다. 조인 시도에 실패 후 가용성 그룹에 조인하기 전 보조 복제본을 제거하고 다시 추가하려면 주 복제본을 호스팅하는 서버 인스턴스에 연결해야 합니다. 자세한 내용은 [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md) 및 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹에 가용성 복제본을 조인하려면**  
  
1.  개체 탐색기에서 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장할 서버 이름을 클릭합니다.  
  
2.  **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  연결된 보조 복제본의 가용성 그룹을 선택합니다.  
  
4.  보조 복제본을 마우스 오른쪽 단추로 클릭하고 **가용성 그룹에 조인**을 클릭합니다.  
  
5.  **가용성 그룹에 복제본 조인** 대화 상자가 열립니다.  
  
6.  가용성 그룹에 보조 복제본을 조인하려면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹에 가용성 복제본을 조인하려면**  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     여기서 *group_name* 은 가용성 그룹의 이름입니다.  
  
     다음 예에서는 보조 복제본을 `MyAG` 가용성 그룹에 조인합니다.  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  컨텍스트에서 사용되는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 보려면 [가용성 그룹 만들기&#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)를 참조하세요.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹에 가용성 복제본을 조인하려면**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 공급자에서 다음을 수행합니다.  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스로 디렉터리를 변경(`cd`)합니다.  
  
2.  가용성 그룹의 이름으로 **Join-SqlAvailabilityGroup** cmdlet을 실행하여 보조 복제본을 가용성 그룹에 조인합니다.  
  
     예를 들어 다음 명령은 지정된 경로에 있는 서버 인스턴스가 호스팅하는 보조 복제본을 `MyAg`라는 가용성 그룹에 조인합니다.  이 서버 인스턴스는 이 가용성 그룹에서 보조 복제본을 호스팅해야 합니다.  
  
    ```powershell
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 `Get-Help` PowerShell 환경에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 보조 데이터베이스 구성  
 가용성 그룹의 모든 데이터베이스에 대해, 보조 복제본을 호스팅하는 서버 인스턴스에 보조 데이터베이스를 두어야 합니다. 다음과 같이 보조 복제본을 가용성 그룹에 조인하기 전이나 후에 보조 데이터베이스를 구성할 수 있습니다.  
  
1.  모든 복원 작업에는 RESTORE WITH NORECOVERY를 사용하여 각 주 데이터베이스의 최신 데이터베이스 및 로그 백업을 보조 복제본을 호스팅하는 서버 인스턴스에 복원합니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)를 참조하세요.  
  
2.  가용성 그룹에 각 보조 데이터베이스를 조인합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server&#41; 개요](overview-of-always-on-availability-groups-sql-server.md)   
 [삭제 SQL Server&#41;AlwaysOn 가용성 그룹 &#40;구성 문제 해결](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
