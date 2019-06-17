---
title: 가용성 데이터베이스 재개(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b85a2b6e7d574c1752eba84d1bfc2bce8dbafc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788720"
---
# <a name="resume-an-availability-database-sql-server"></a>가용성 데이터베이스 재개(SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 일시 중지된 가용성 데이터베이스를 재개할 수 있습니다. 일시 중지된 데이터베이스를 재개하면 데이터베이스는 SYNCHRONIZING 상태가 됩니다. 주 데이터베이스를 재개하면 주 데이터베이스를 일시 중지함에 따라 함께 일시 중지된 보조 데이터베이스도 재개됩니다. 보조 데이터베이스가 보조 복제본을 호스팅하는 서버 인스턴스에서 로컬로 일시 중지된 경우 해당 보조 데이터베이스를 로컬로 재개해야 합니다. 지정된 보조 데이터베이스와 해당 주 데이터베이스가 SYNCHRONIZING 상태이면 보조 데이터베이스에서 데이터 동기화가 재개됩니다.  
  
> [!NOTE]  
>  AlwaysOn 보조 데이터베이스를 일시 중지하고 재개해도 주 데이터베이스의 가용성에 직접 영향을 주지는 않습니다. 그러나 보조 데이터베이스를 일시 중지하면 일시 중지된 보조 데이터베이스가 재개될 때까지 주 데이터베이스의 중복 및 장애 조치(failover) 기능에 영향을 줄 수는 있습니다. 이것은 데이터베이스 미러링과는 대조적입니다. 데이터베이스 미러링의 경우에는 미러링을 재개할 때까지 미러 데이터베이스 및 주 데이터베이스에서 미러링 상태가 일시 중지됩니다. AlwaysOn 주 데이터베이스를 일시 중지하면 모든 해당 보조 데이터베이스에서 데이터 이동이 일시 중지되고 주 데이터베이스를 재개할 때까지 해당 데이터베이스에 대한 중복 및 장애 조치(failover) 기능이 중단됩니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **보조 데이터베이스를 재개하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 RESUME 명령은 대상 데이터베이스를 호스팅하는 복제본에서 수락되는 즉시 반환하지만 실제로 데이터베이스 재개는 비동기식으로 발생합니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   재개할 데이터베이스를 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   가용성 그룹이 온라인 상태여야 합니다.  
  
-   주 데이터베이스가 온라인이고 사용 가능한 상태여야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **보조 데이터베이스를 재개하려면**  
  
1.  개체 탐색기에서 데이터베이스를 재개할 가용성 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **AlwaysOn 고가용성** 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 확장합니다.  
  
4.  **가용성 데이터베이스** 노드를 확장하고 데이터베이스를 마우스 오른쪽 단추로 누른 다음 **데이터 이동 재개**를 클릭합니다.  
  
5.  **데이터 이동 재개** 대화 상자에서 **확인**을 클릭합니다.  
  
> [!NOTE]  
>  이 복제본 위치에서 추가 데이터베이스를 재개하려면 각 데이터베이스에 대해 4-5단계를 반복합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **로컬로 일시 중지된 보조 데이터베이스를 재개하려면**  
  
1.  데이터베이스를 재개할 보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)문을 사용하여 보조 데이터베이스를 재개합니다.  
  
     ALTER DATABASE *database_name* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **보조 데이터베이스를 재개하려면**  
  
1.  데이터베이스를 재개할 복제본을 호스팅하는 서버 인스턴스로 디렉터리를 변경(`cd`)합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
2.  **Resume-SqlAvailabilityDatabase** cmdlet을 사용하여 가용성 그룹을 재개합니다.  
  
     예를 들어 다음 명령은 `MyDb3` 가용성 그룹의 `MyAg`가용성 데이터베이스에 대한 데이터 동기화를 재개합니다.  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경에서 `Get-Help` cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 데이터베이스 일시 중지&#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
