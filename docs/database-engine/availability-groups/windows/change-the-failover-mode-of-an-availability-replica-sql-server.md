---
title: "가용성 복제본의 장애 조치(failover) 모드 변경(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "장애 조치(failover) 모드 [SQL Server]"
  - "가용성 그룹 [SQL Server], 배포"
  - "가용성 그룹 [SQL Server], 장애 조치(Failover) 모드"
  - "가용성 그룹 [SQL Server], 구성"
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
caps.latest.revision: 27
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 27
---
# 가용성 복제본의 장애 조치(failover) 모드 변경(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 Always On 가용성 그룹의 가용성 복제본에 대한 장애 조치(failover) 모드를 변경하는 방법에 대해 설명합니다. 장애 조치(failover) 모드는 동기-커밋 가용성 모드에서 실행되는 복제본에 대한 장애 조치(failover) 모드를 결정하는 복제본 속성입니다. 자세한 내용은 [장애 조치(failover) 및 장애 조치(failover) 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 및 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)를 참조하세요.  
  
-   **시작하기 전에:**  
  
     [사전 요구 사항 및 제한 사항](#Prerequisites)  
  
     [보안](#Security)  
  
-   **가용성 복제본의 가용성 모드를 변경하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항 및 제한 사항  
  
-   이 태스크는 주 복제본에서만 지원됩니다. 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)는 가용성 그룹에 따라 AlwaysOn 자동 장애 조치(Failover)를 지원하지 않으므로 FCI에서 호스팅하는 모든 가용성 복제본은 수동 장애 조치(Failover)에 대해서만 구성될 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 복제본의 장애 조치(failover) 모드를 변경하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  복제본을 변경할 가용성 그룹을 클릭합니다.  
  
4.  복제본을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 **장애 조치(failover) 모드** 드롭 목록을 사용하여 이 복제본의 장애 조치(failover) 모드를 변경합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본의 장애 조치(failover) 모드를 변경하려면**  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     }  )  
  
     여기서  
  
    -   *group_name*은 가용성 그룹의 이름입니다.  
  
    -   { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
         변경할 가용성 그룹을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스 주소를 지정합니다. 이 주소의 구성 요소는 다음과 같습니다.  
  
         *system_name*  
         독립 실행형 서버 인스턴스가 있는 컴퓨터 시스템의 NetBIOS 이름입니다.  
  
         *FCI_network_name*  
         대상 서버 인스턴스가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 파트너(FCI)인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 액세스하는 데 사용되는 네트워크 이름입니다.  
  
         *instance_name*  
         대상 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스 이름입니다. 기본 서버 인스턴스의 경우 *instance_name*은 선택 사항입니다.  
  
     이러한 매개 변수에 대한 자세한 내용은 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)을 참조하세요.  
  
     *MyAG* 가용성 그룹의 주 복제본에 입력된 다음 예는 *COMPUTER01*컴퓨터의 기본 서버 인스턴스에 있는 가용성 복제본에서 장애 조치(failover) 모드를 자동 장애 조치(failover)로 변경합니다.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 복제본의 장애 조치(failover) 모드를 변경하려면**  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
2.  **Set-SqlAvailabilityReplica** cmdlet을 **FailoverMode** 매개 변수와 함께 사용합니다. 복제본을 자동 장애 조치(failover)로 설정할 때는 **AvailabilityMode** 매개 변수를 사용하여 복제본을 동기-커밋 가용성 모드로 변경해야 할 수 있습니다.  
  
     예를 들어 다음 명령은 `MyReplica` 가용성 그룹의 `MyAg` 복제본이 동기-커밋 가용성 모드를 사용하고 자동 장애 조치(failover)를 지원하도록 수정합니다.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경에서 **Get-Help** cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## 참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [장애 조치(failover) 및 장애 조치(failover) 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  