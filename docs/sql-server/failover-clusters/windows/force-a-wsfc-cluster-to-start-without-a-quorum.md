---
title: 쿼럼 없이 WSFC 클러스터 강제 시작
description: 쿼럼 없이 Windows Server 장애 조치(failover) 클러스터링 클러스터 노드를 강제로 시작합니다. 이 작업은 데이터를 복구하고 고가용성을 다시 설정하는 데 필요할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: 4a121375-7424-4444-b876-baefa8fe9015
author: cawrites
ms.author: chadam
ms.openlocfilehash: c1de5f07aa692b0d268d3e41a1b8dda554ea0280
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96121068"
---
# <a name="force-a-wsfc-cluster-to-start-without-a-quorum"></a>쿼럼 없이 WSFC 클러스터 강제 시작
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터 노드를 쿼럼 없이 강제로 시작하는 방법에 대해 설명합니다.  이 기능은 재해 복구 및 다중 서브넷 시나리오에서 데이터를 복구하고 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 고가용성을 완전히 다시 설정하는 데 필요할 수 있습니다.  
  
-   **시작하기 전에:**  [권장 사항](#Recommendations), [보안](#Security)  
  
-   **다음을 사용하여 쿼럼 없이 클러스터 강제 시작:**  [장애 조치(failover) 클러스터 관리자 사용](#FailoverClusterManagerProcedure), [Powershell 사용](#PowerShellProcedure), [Net.exe 사용](#CommandPromptProcedure)  
  
-   **후속 작업:**  [후속 작업: 쿼럼 없이 클러스터를 강제로 시작한 후의 작업](#FollowUp)  
  
##  <a name="before-you-start"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
 명시적으로 지정된 경우를 제외하고 이 항목의 절차는 WSFC 클러스터의 노드에서 실행할 경우에 유효합니다.  그러나 쿼럼 없이 강제로 시작할 노드에서 이러한 단계를 실행하면 보다 나은 결과를 얻고 네트워킹 문제를 방지할 수 있습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 사용자는 WSFC 클러스터의 각 노드에 대한 로컬 Administrators 그룹의 멤버인 도메인 계정이어야 합니다.  
  
##  <a name="using-failover-cluster-manager"></a><a name="FailoverClusterManagerProcedure"></a> 장애 조치(Failover) 클러스터 관리자 사용  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>쿼럼 없이 클러스터를 강제로 시작하려면  
  
1.  장애 조치(Failover) 클러스터 관리자를 열고 온라인으로 강제 전환할 클러스터 노드에 연결합니다.  
  
2.  **동작** 창에서 **클러스터 강제 시작** 을 클릭하고 **예. 클러스터를 강제로 시작** 을 클릭합니다.  
  
3.  왼쪽 창의 **장애 조치(Failover) 클러스터 관리자** 트리에서 클러스터 이름을 클릭합니다.  
  
4.  요약 창에서 현재 **쿼럼 구성** 값이  **경고: 클러스터가 ForceQuorum 상태에서 실행 중입니다.** 인지 확인합니다.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Powershell 사용  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>쿼럼 없이 클러스터를 강제로 시작하려면  
  
1.  **관리자 권한으로 실행** 을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 commandlet을 사용할 수 있도록 `FailoverClusters` 모듈을 가져옵니다.  
  
3.  `Stop-ClusterNode` 를 사용하여 클러스터 서비스가 중지되었는지 확인합니다.  
  
4.  `Start-ClusterNode` 와 `-FixQuorum` 을 사용하여 클러스터 서비스를 강제로 시작합니다.  
  
5.  `Get-ClusterNode` 와 `-Propery NodeWieght = 1` 을 사용하여 노드가 쿼럼의 투표 멤버가 되도록 하는 값을 설정합니다.  
  
6.  클러스터 노드 속성을 읽기 가능한 형식으로 출력합니다.  
  
### <a name="example-powershell"></a>예(Powershell)  
 다음 예제에서는 쿼럼 없이 Always OnSrv02 노드 클러스터 서비스를 강제로 시작하고 `NodeWeight = 1`로 설정한 다음 새 강제 시작 노드의 클러스터 노드 상태를 열거합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "Always OnSrv02"  
Stop-ClusterNode -Name $node  
Start-ClusterNode -Name $node -FixQuorum  
  
(Get-ClusterNode $node).NodeWeight = 1  
  
$nodes = Get-ClusterNode -Cluster $node  
$nodes | Format-Table -property NodeName, State, NodeWeight  
  
```  
  
##  <a name="using-netexe"></a><a name="CommandPromptProcedure"></a> Net.exe 사용  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>쿼럼 없이 클러스터를 강제로 시작하려면  
  
1.  원격 데스크톱을 사용하여 온라인으로 강제 전환할 클러스터 노드에 연결합니다.  
  
2.  **관리자 권한으로 실행** 을 통해 승격된 명령 프롬프트를 시작합니다.  
  
3.  **net.exe** 를 사용하여 로컬 클러스터 서비스가 중지되었는지 확인합니다.  
  
4.  **net.exe** 와 `/forcequorum` 을 사용하여 로컬 클러스터 서비스를 강제로 시작합니다.  
  
### <a name="example-netexe"></a>예(Net.exe)  
 다음 예에서는 쿼럼 없이 노드 클러스터 서비스를 강제로 시작하고 `NodeWeight = 1`로 설정한 다음 새 강제 시작 노드의 클러스터 노드 상태를 열거합니다.  
  
```ms-dos  
net.exe stop clussvc  
net.exe start clussvc /forcequorum  
```  
  
##  <a name="follow-up-after-forcing-cluster-to-start-without-a-quorum"></a><a name="FollowUp"></a> 후속 작업: 쿼럼 없이 클러스터를 강제로 시작한 후의 작업  
  
-   다른 노드를 다시 온라인으로 전환하려면 먼저 NodeWeight 값을 다시 계산하고 다시 구성하여 새 쿼럼을 올바르게 생성해야 합니다. 그러지 않으면 클러스터가 다시 오프라인으로 전환될 수 있습니다.  
  
     자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
-   이 항목의 절차에서는 계획되지 않은 쿼럼 오류가 발생한 경우 WSFC 클러스터를 다시 온라인으로 전환하는 단계만 설명합니다.  추가 단계를 통해 다른 WSFC 클러스터 노드가 새 쿼럼 구성에 방해가 되지 않도록 할 수도 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , 데이터베이스 미러링, 로그 전달 등의 다른 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]기능에는 데이터를 복구하고 고가용성을 완전히 다시 설정하기 위한 후속 동작도 필요할 수 있습니다.  
  
     **자세한 내용은 다음을 참조하세요.**  
  
     [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
     [데이터베이스 미러링 세션에 서비스 강제 수행&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
  
     [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [장애 조치(Failover) 클러스터에 대한 이벤트 및 로그 보기](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 장애 조치(Failover) 클러스터 Cmdlet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461045(v=technet.10))  
  
## <a name="see-also"></a>참고 항목  
 [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [클러스터 쿼럼 NodeWeight 설정 구성](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [태스크 기준으로 나열된 Windows PowerShell의 장애 조치(failover) 클러스터 Cmdlet](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
