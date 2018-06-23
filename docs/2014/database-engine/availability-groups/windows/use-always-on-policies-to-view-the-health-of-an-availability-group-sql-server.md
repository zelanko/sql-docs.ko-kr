---
title: AlwaysOn 정책을 사용 하 여 가용성 그룹 (SQL Server)의 상태를 보려면 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: ba1f977cf2846438494bedc7b084ade659fca753
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184335"
---
# <a name="use-alwayson-policies-to-view-the-health-of-an-availability-group-sql-server"></a>AlwaysOn 정책을 사용하여 가용성 그룹의 상태 보기(SQL Server)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 AlwaysOn 정책 또는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 PowerShell을 사용하여 AlwaysOn 가용성 그룹의 작동 상태를 확인하는 방법에 대해 설명합니다. AlwaysOn 정책 기반 관리에 대 한 정보를 참조 하십시오. [운영 문제 AlwaysOn 가용성 그룹 (SQL Server)에 대 한 AlwaysOn 정책](always-on-policies-for-operational-issues-always-on-availability.md)합니다.  
  
> [!IMPORTANT]  
>  AlwaysOn 정책의 경우 범주 이름이 ID로 사용됩니다. AlwaysOn 범주의 이름을 변경하면 상태 평가 기능이 작동하지 않으므로 따라서 AlwaysOn 범주의 이름을 수정해서는 안 됩니다.  
  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 연결, 서버 상태 보기 및 모든 정의 보기 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> AlwaysOn 대시보드 사용  
 **AlwaysOn 대시보드를 열려면**  
  
1.  개체 탐색기에서 가용성 복제본 중 하나를 호스팅하는 서버 인스턴스에 연결합니다. 가용성 그룹의 모든 가용성 복제본에 대한 정보를 보려면 주 복제본을 호스팅하는 서버 인스턴스를 사용합니다.  
  
2.  서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
3.  **AlwaysOn 고가용성** 노드를 확장합니다.  
  
     **가용성 그룹**을 마우스 오른쪽 단추로 클릭하거나 이 노드를 확장하고 특정 가용성 그룹을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  **대시보드 표시** 명령을 선택합니다.  
  
 AlwaysOn 대시보드를 사용하는 방법에 대한 자세한 내용은 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)을 참조하세요.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **AlwaysOn 정책을 사용 하 여 가용성 그룹의 상태를 보려면**  
  
1.  기본 설정 (`cd`) 가용성 복제본 중 하나를 호스팅하는 서버 인스턴스에 있습니다. 가용성 그룹의 모든 가용성 복제본에 대한 정보를 보려면 주 복제본을 호스팅하는 서버 인스턴스를 사용합니다.  
  
2.  다음 cmdlet을 사용합니다.  
  
     `Test-SqlAvailabilityGroup`  
     SQL Server PBM(정책 기반 관리) 정책을 평가하여 가용성 그룹의 상태를 평가합니다. 이 cmdlet을 실행하려면 연결, 서버 상태 보기 및 모든 정의 보기 권한이 있어야 합니다.  
  
     예를 들어 다음 명령은 서버 인스턴스 `Computer\Instance`에서 상태가 "오류"인 모든 가용성 그룹을 보여 줍니다.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     `Test-SqlAvailabilityReplica`  
     SQL Server PBM(정책 기반 관리) 정책을 평가하여 가용성 복제본의 상태를 평가합니다. 이 cmdlet을 실행하려면 연결, 서버 상태 보기 및 모든 정의 보기 권한이 있어야 합니다.  
  
     예를 들어 다음 명령은 `MyReplica` 가용성 그룹에서 `MyAg` 라는 가용성 복제본의 상태를 평가하고 간단한 요약을 출력합니다.  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     `Test-SqlDatabaseReplicaState`  
     SQL Server PBM(정책 기반 관리) 정책을 평가하여 모든 조인된 가용성 복제본에 대한 가용성 데이터베이스 상태를 평가합니다.  
  
     예를 들어 다음 명령은 `MyAg` 가용성 그룹에서 모든 가용성 데이터베이스의 상태를 평가하고 각 데이터베이스에 대해 간단한 요약을 출력합니다.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     이러한 cmdlet은 다음 옵션을 사용합니다.  
  
    |옵션|Description|  
    |------------|-----------------|  
    |`AllowUserPolicies`|AlwaysOn 정책 범주에 있는 사용자 정책을 실행합니다.|  
    |`InputObject`|사용 중인 cmdlet에 따라 가용성 그룹, 가용성 복제본 또는 가용성 데이터베이스 상태를 나타내는 개체 모음입니다. cmdlet은 지정된 개체의 상태를 계산합니다.|  
    |`NoRefresh`|이 매개 변수를 설정한 경우 cmdlet 수동으로 새로 고치지 것입니다 지정 된 개체는 `-Path` 또는 `-InputObject` 매개 변수입니다.|  
    |`Path`|사용 중인 cmdlet에 따라 가용성 그룹의 경로, 하나 이상의 가용성 복제본 또는 가용성 데이터베이스의 데이터베이스 복제본 클러스터 상태입니다. 선택적 매개 변수입니다. 지정하지 않으면 이 매개 변수의 값은 기본적으로 현재 작업 위치입니다.|  
    |`ShowPolicyDetails`|이 cmdlet에서 수행하는 각 정책 평가의 결과를 표시합니다. cmdlet은 정책 평가당 하나의 개체를 출력하며, 이 개체에는 평가 결과(정책 통과 여부, 정책 이름과 범주 등)를 설명하는 필드가 있습니다.|  
  
     예를 들어 다음 `Test-SqlAvailabilityGroup` 명령은 `-ShowPolicyDetails` 매개 변수를 지정하고 `MyAg`라는 가용성 그룹에서 실행된 각 PBM(정책 기반 관리) 정책에 대해 이 cmdlet에서 수행한 정책 평가 결과를 각각 표시합니다.  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  Cmdlet의 구문을 보려면에서 사용 하 여는 `Get-Help` cmdlet에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
 **SQL Server AlwaysOn 팀 블로그 — PowerShell 사용 하 여 AlwaysOn 상태 모니터링:**  
  
-   [1부: 기본 Cmdlet 개요](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)  
  
-   [2부: 고급 Cmdlet 사용](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)  
  
-   [3부: 간단한 모니터링 응용 프로그램](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)  
  
-   [4부: SQL Server 에이전트와의 통합](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 관리&#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [운영 문제 AlwaysOn 가용성 그룹 (SQL Server)에 대 한 AlwaysOn 정책](always-on-policies-for-operational-issues-always-on-availability.md) 
  
  