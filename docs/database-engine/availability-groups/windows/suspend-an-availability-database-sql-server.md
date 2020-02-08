---
title: 가용성 데이터베이스 일시 중단
description: SSMS(SQL Server Management Studio), T-SQL(Transact-SQL) 또는 PowerShell을 사용하여 Always On 가용성 그룹 내에서 데이터베이스에 대한 데이터 이동을 일시 중단하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.suspenddatamove.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], suspending a database
- Availability Groups [SQL Server], databases
ms.assetid: 86858982-6af1-4e80-9a93-87451f0d7ee9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92f83bb31569a055bf9158a0388d9cb0630e9a1d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75251270"
---
# <a name="suspend-an-availability-database-sql-server"></a>가용성 데이터베이스 일시 중지(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 가용성 데이터베이스를 일시 중지할 수 있습니다. 일시 중지하거나 재개할 데이터베이스를 호스팅하는 서버 인스턴스에서 일시 중지 명령을 실행해야 합니다.  
  
 일시 중지 명령의 효과는 일시 중지하는 데이터베이스가 보조 데이터베이스인지 주 데이터베이스인지에 따라 다음과 같이 다릅니다.  
  
|일시 중지된 데이터베이스|일시 중지 명령의 효과|  
|------------------------|-------------------------------|  
|보조 데이터베이스|로컬 보조 데이터베이스만 일시 중지되고 동기화 상태가 NOT SYNCHRONIZING이 됩니다. 다른 보조 데이터베이스는 영향을 받지 않습니다. 일시 중지된 데이터베이스는 데이터(로그 레코드)의 수신과 적용을 중지하고 주 데이터베이스보다 뒤처지기 시작합니다. 읽기 가능한 보조 복제본에 대한 기존 연결은 계속 사용할 수 있습니다. 읽기 가능한 보조 복제본의 일시 중단된 데이터베이스에 대한 새 연결은 데이터 이동이 다시 시작될 때까지 허용되지 않습니다.<br /><br /> 주 데이터베이스는 사용 가능한 상태로 남아 있습니다. 각각의 해당 보조 데이터베이스를 중지하면 주 데이터베이스가 노출된 상태로 실행됩니다.<br /><br /> **\*\* 중요 \*\*** 보조 데이터베이스를 일시 중지하면 해당 주 데이터베이스의 큐 보내기에서 보내지 않은 트랜잭션 로그 레코드를 누적합니다. 보조 복제본에 대한 연결은 데이터 이동이 일시 중단된 시간에 사용 가능했던 데이터를 반환합니다.|  
|주 데이터베이스|주 데이터베이스는 연결된 모든 보조 데이터베이스로의 데이터 이동을 중지합니다. 주 데이터베이스는 계속해서 노출된 모드에서 실행됩니다. 클라이언트에서 주 데이터베이스를 계속해서 사용할 수 있고 읽을 수 있는 보조 데이터베이스의 기존 연결을 계속해서 사용할 수 있으며 새로운 연결을 만들 수 있습니다.|  
  
> [!NOTE]  
>  Always On 보조 데이터베이스를 일시 중지해도 주 데이터베이스의 가용성에 직접 영향을 주지는 않습니다. 그러나 보조 데이터베이스를 일시 중지하면 주 데이터베이스의 중복 및 장애 조치(failover) 기능에 영향을 줄 수 있습니다. 이것은 데이터베이스 미러링과는 대조적입니다. 데이터베이스 미러링의 경우에는 미러 데이터베이스 및 주 데이터베이스에서 미러링 상태가 일시 중지됩니다. Always On 주 데이터베이스를 일시 중지하면 모든 해당 보조 데이터베이스에서 데이터 이동이 일시 중지되고 주 데이터베이스를 재개할 때까지 해당 데이터베이스에 대한 중복 및 장애 조치(failover) 기능이 중단됩니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스를 일시 중지하려면:**  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **후속 작업:** [꽉 찬 트랜잭션 로그 방지](#FollowUp)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 SUSPEND 명령은 대상 데이터베이스를 호스팅하는 복제본에서 수락되는 즉시 반환하지만 실제로 데이터베이스 일시 중지는 비동기식으로 발생합니다.  
  
###  <a name="Prerequisites"></a> 필수 조건  
 일시 중지할 데이터베이스를 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다. 주 데이터베이스와 해당 보조 데이터베이스를 일시 중지하려면 주 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 주 데이터베이스는 사용 가능한 상태로 두고 보조 데이터베이스를 일시 중지하려면 보조 복제본에 연결합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 병목 현상 중에 하나 이상의 보조 데이터베이스를 잠시 중단하면 주 복제본의 성능을 일시적으로 향상됩니다. 보조 데이터베이스가 일시 중지된 상태인 동안에는 해당 주 데이터베이스의 트랜잭션 로그를 자를 수 없으므로 로그 레코드가 주 데이터베이스에 누적됩니다. 따라서 일시 중지된 보조 데이터베이스를 신속하게 다시 시작하거나 제거하는 것이 좋습니다. 자세한 내용은 이 항목 뒷부분에 있는 [후속 작업: 꽉 찬 트랜잭션 로그 방지](#FollowUp)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **데이터베이스를 일시 중지하려면**  
  
1.  개체 탐색기에서 데이터베이스를 일시 중지할 가용성 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 확장합니다.  
  
4.  **가용성 데이터베이스** 노드를 확장하고 데이터베이스를 마우스 오른쪽 단추로 누른 다음 **데이터 이동 일시 중지**를 클릭합니다.  
  
5.  **데이터 이동 일시 중지** 대화 상자에서 **확인**을 클릭합니다.  
  
     개체 탐색기에서 데이터베이스 아이콘이 일시 중지 표시기로 변경되어 데이터베이스가 일시 중지되었음을 나타냅니다.  
  
> [!NOTE]  
>  이 복제본 위치에서 다른 데이터베이스를 일시 중지하려면 각 데이터베이스에 대해 4단계와 5단계를 반복합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **데이터베이스를 일시 중지하려면**  
  
1.  데이터베이스를 일시 중지할 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
2.  다음의 [ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) 문을 사용하여 데이터베이스를 일시 중단합니다.  
  
     ALTER DATABASE *database_name* SET HADR SUSPEND
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **데이터베이스를 일시 중지하려면**  
  
1.  데이터베이스를 일시 중단할 복제본을 호스트하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
2.  **Suspend-SqlAvailabilityDatabase** cmdlet을 사용하여 가용성 그룹을 일시 중단합니다.  
  
     예를 들어 다음 명령은 서버 인스턴스 `MyDb3` 에서 가용성 그룹 `MyAg` 에 있는 가용성 데이터베이스 `Computer\Instance`에 대한 데이터 동기화를 일시 중단합니다.  
  
    ```  
    Suspend-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 후속 작업: 꽉 찬 트랜잭션 로그 방지  
 일반적으로 데이터베이스에서 자동 검사점을 수행하면 다음 로그 백업 이후 해당 트랜잭션 로그가 이 검사점까지 잘립니다. 그러나 보조 데이터베이스를 일시 중지하는 동안 모든 현재 로그 레코드가 주 데이터베이스에서 활성 상태로 남아 있습니다. 서버 인스턴스의 공간이 부족하거나 최대 크기에 도달하여 트랜잭션 로그가 가득 차면 데이터베이스는 더 이상 업데이트를 수행할 수 없습니다.  
  
 이 문제를 방지하려면 다음 중 하나를 수행해야 합니다.  
  
-   주 데이터베이스에 대한 로그 공간을 추가합니다.  
  
-   로그가 꽉 차기 전에 보조 데이터베이스를 다시 시작합니다. 자세한 내용은 이 항목 뒷부분에 나오는 [가용성 데이터베이스 재개&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)에서 가용성 데이터베이스를 일시 중지할 수 있습니다.  
  
-   보조 데이터베이스를 제거하려면 자세한 내용은 [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
 **꽉 찬 트랜잭션 로그 문제를 해결하려면**  
  
-   [꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](../../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 데이터베이스 재개&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 데이터베이스 재개&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
  
