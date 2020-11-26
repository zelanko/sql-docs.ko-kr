---
title: 클러스터 쿼럼 NodeWeight 설정 구성
description: Windows Server 장애 조치(failover) 클러스터의 멤버 노드에 대한 NodeWeight 설정을 구성하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
author: cawrites
ms.author: chadam
ms.openlocfilehash: c422c1fe6b4b0810cc6e151eda6944fc6cc45b0f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96121133"
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>클러스터 쿼럼 NodeWeight 설정 구성
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터의 멤버 노드에 대한 NodeWeight 설정을 구성하는 방법에 대해 설명합니다. NodeWeight 설정은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 재해 복구 및 다중 서브넷 시나리오를 지원하기 위한 쿼럼 투표 동안 사용됩니다.  
  
-   **시작하기 전에:**  [필수 구성 요소](#Prerequisites), [보안](#Security)  
  
-   **쿼럼 NodeWeight 설정을 보려면 다음을 사용합니다.** [PowerShell 사용](#PowerShellProcedure), [Cluster.exe 사용](#CommandPromptProcedure)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="before-you-start"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 이 기능은 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 이상 버전에서만 지원됩니다.  
  
> [!IMPORTANT]  
>  NodeWeight 설정을 사용하려면 WSFC 클러스터의 모든 서버에 다음 핫픽스를 적용해야 합니다.  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]에서 쿼럼 투표가 없는 클러스터 노드를 구성하는 데 사용할 수 있는 핫픽스  
  
> [!TIP]  
>  이 핫픽스가 설치되어 있지 않은 경우 이 항목의 예는 NodeWeight에 대해 빈 값이나 NULL 값을 반환합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 사용자는 WSFC 클러스터의 각 노드에 대한 로컬 Administrators 그룹의 멤버인 도메인 계정이어야 합니다.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Powershell 사용  
  
##### <a name="to-configure-nodeweight-settings"></a>NodeWeight 설정을 구성하려면  
  
1.  **관리자 권한으로 실행** 을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 commandlet을 사용할 수 있도록 `FailoverClusters` 모듈을 가져옵니다.  
  
3.  `Get-ClusterNode` 개체를 사용하여 클러스터의 각 노드에 대한 `NodeWeight` 속성을 설정합니다.  
  
4.  클러스터 노드 속성을 읽기 가능한 형식으로 출력합니다.  
  
### <a name="example-powershell"></a>예(Powershell)  
 다음 예제에서는 NodeWeight 설정을 변경하여 "AlwaysOnSrv1" 노드에 대한 쿼럼 투표를 제거한 다음, 클러스터의 모든 노드에 대한 설정을 출력합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv1"  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="using-clusterexe"></a><a name="CommandPromptProcedure"></a> Cluster.exe 사용  
  
> [!NOTE]  
>  cluster.exe 유틸리티는 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 릴리스에서 더 이상 사용되지 않습니다.  이후 개발에는 PowerShell과 장애 조치(failover) 클러스터링을 함께 사용하세요.  cluster.exe 유틸리티는 Windows Server의 다음 릴리스에서 제거될 예정입니다. 자세한 내용은 [Cluster.exe 명령을 장애 조치(failover) 클러스터용 Windows PowerShell Cmdlet에 매핑](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)을 참조하세요.  
  
##### <a name="to-configure-nodeweight-settings"></a>NodeWeight 설정을 구성하려면  
  
1.  **관리자 권한으로 실행** 을 통해 승격된 명령 프롬프트를 시작합니다.  
  
2.  **cluster.exe** 를 사용하여 `NodeWeight` 값을 설정합니다.  
  
### <a name="example-clusterexe"></a>예(Cluster.exe)  
 다음 예제에서는 NodeWeight 값을 변경하여 “Cluster001” 클러스터의 “AlwaysOnSrv1” 노드에 대한 쿼럼 투표를 제거합니다.  
  
```ms-dos  
cluster.exe Cluster001 node AlwaysOnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [장애 조치(Failover) 클러스터에 대한 이벤트 및 로그 보기](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 장애 조치(Failover) 클러스터 Cmdlet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461045(v=technet.10))  
  
## <a name="see-also"></a>참고 항목  
 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [클러스터 쿼럼 NodeWeight 설정 보기](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [태스크 기준으로 나열된 Windows PowerShell의 장애 조치(failover) 클러스터 Cmdlet](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
