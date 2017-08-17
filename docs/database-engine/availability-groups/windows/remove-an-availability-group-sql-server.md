---
title: "가용성 그룹 제거(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 393f088ea977236aa7feba6107828eb64e646b64
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="remove-an-availability-group-sql-server"></a>가용성 그룹 제거(SQL Server)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 Always On 가용성 그룹을 삭제하는 방법을 설명합니다. 가용성 복제본 중 하나를 호스팅하는 서버 인스턴스가 오프라인 상태일 때 가용성 그룹을 삭제하면 나중에 서버 인스턴스가 온라인 상태가 되었을 때 서버 인스턴스에서 로컬 가용성 복제본을 삭제합니다. 가용성 그룹을 삭제하면 관련 가용성 그룹 수신기도 삭제됩니다.  
  
 필요한 경우 가용성 그룹에 대한 올바른 보안 자격 증명이 있는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에서 가용성 그룹을 삭제할 수 있습니다. 이렇게 하면 가용성 복제본이 더 이상 없을 때 가용성 그룹을 삭제할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능하면 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있는 동안에만 가용성 그룹을 제거하세요. 주 복제본에서 가용성 그룹을 제거하면 이전 주 데이터베이스에서 변경이 허용됩니다(고가용성 보호 없이). 보조 복제본에서 가용성 그룹을 삭제하면 주 복제본이 RESTORING 상태로 유지되고 데이터베이스에서 변경이 허용되지 않습니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항 및 권장 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **가용성 그룹을 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항 및 권장 사항  
  
-   가용성 그룹이 온라인일 때 보조 복제본에서 이 그룹을 삭제하면 주 복제본이 RESTORING 상태로 전환됩니다. 따라서 가능하면 주 복제본을 호스팅하는 서비스 인스턴스에서만 가용성 그룹을 제거하세요.  
  
-   WSFC 장애 조치(failover) 클러스터에서 삭제되었거나 제거된 컴퓨터에서 가용성 그룹을 삭제하는 경우 가용성 그룹은 로컬 위치에서만 삭제됩니다.  
  
-   WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 쿼럼이 없을 때 가용성 그룹이 삭제되지 않도록 합니다. 클러스터에 쿼럼이 부족할 때 가용성 그룹을 삭제해야 하는 경우 클러스터에 저장된 메타데이터 가용성 그룹은 제거되지 않습니다. 클러스터가 쿼럼을 다시 얻은 후에는 가용성 그룹을 다시 삭제하여 WSFC 클러스터에서 제거해야 합니다.  
  
-   보조 복제본에서 DROP AVAILABILITY GROUP은 응급용으로만 사용해야 합니다. 이는 가용성 그룹을 삭제하면 가용성 그룹이 오프라인 상태로 전환되기 때문입니다. 보조 복제본에서 가용성 그룹을 삭제하면 주 복제본에서 쿼럼 손실, 강제 장애 조치(failover) 또는 DROP AVAILABILITY GROUP 명령으로 인해 OFFLINE 상태가 발생했는지 여부를 확인할 수 없습니다. 주 복제본은 분리 장애(split-brain)가 발생하는 것을 방지하기 위해 RESTORING 상태로 전환됩니다. 자세한 내용은 [작동 방식: DROP AVAILABILITY GROUP 동작](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다. 로컬 서버 인스턴스에서 호스팅되지 않는 가용성 그룹을 삭제하려면 해당 가용성 그룹에 대한 CONTROL SERVER 권한이나 CONTROL 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹을 삭제하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하거나(가능한 경우) 가용성 그룹에 대한 올바른 보안 자격 증명을 소유한 WSFC 노드에 있으며 Always On 가용성 그룹을 사용하도록 설정된 다른 서버 인스턴스에 연결합니다. 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  이 단계는 여러 가용성 그룹을 삭제할지 아니면 가용성 그룹을 하나만 삭제할지에 따라 다음과 같이 달라집니다.  
  
    -   주 복제본이 연결된 서버 인스턴스에 있는 가용성 그룹을 여러 개 삭제하려면 **개체 탐색기 정보** 창을 사용하여 삭제할 모든 가용성 그룹을 확인하고 선택합니다. 자세한 내용은 [개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)을 참조하세요.  
  
    -   단일 가용성 그룹을 삭제하려면 **개체 탐색기** 창 또는 **개체 탐색기 정보** 창에서 해당 가용성 그룹을 선택합니다.  
  
4.  선택한 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **삭제** 명령을 선택합니다.  
  
5.  **가용성 그룹 제거** 대화 상자에서 나열된 가용성 그룹을 모두 삭제하려면 **확인**을 클릭합니다. 나열된 모든 가용성 그룹을 제거하지 않으려면 **취소**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹을 삭제하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결하거나(가능한 경우) 가용성 그룹에 대한 올바른 보안 자격 증명을 소유한 WSFC 노드에 있으며 Always On 가용성 그룹을 사용하도록 설정된 다른 서버 인스턴스에 연결합니다.  
  
2.  다음과 같이 [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md) 문을 사용합니다.  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     여기서 *group_name* 은 삭제할 가용성 그룹의 이름입니다.  
  
     다음 예에서는 `MyAG` 가용성 그룹을 삭제합니다.  
  
    ```  
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹을 삭제하려면**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 공급자에서 다음을 수행합니다.  
  
1.  디렉터리를 변경하여(**cd**) 주 복제본을 호스팅하는 서버 인스턴스에 연결하거나(가능한 경우) 가용성 그룹에 대한 올바른 보안 자격 증명을 소유한 WSFC 노드에 있으며 Always On 가용성 그룹을 사용하도록 설정된 다른 서버 인스턴스에 연결합니다.  
  
2.  **Remove-SqlAvailabilityGroup** cmdlet을 사용합니다.  
  
     예를 들어 다음 명령은 `MyAg`라는 가용성 그룹을 제거합니다. 이 명령은 가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 실행할 수 있습니다.  
  
    ```  
    Remove-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [작동 방식: DROP AVAILABILITY GROUP 동작](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server 엔지니어 블로그)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
  

