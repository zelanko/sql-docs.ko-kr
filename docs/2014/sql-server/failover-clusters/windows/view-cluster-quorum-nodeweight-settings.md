---
title: 클러스터 쿼럼 NodeWeight 설정 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07db329a7ba6cb65e5beb94d34f90d1e55582915
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367785"
---
# <a name="view-cluster-quorum-nodeweight-settings"></a>클러스터 쿼럼 NodeWeight 설정 보기
  이 항목에서는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터의 각 멤버 노드에 대한 NodeWeight 설정을 보는 방법에 대해 설명합니다. NodeWeight 설정은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 재해 복구 및 다중 서브넷 시나리오를 지원하기 위한 쿼럼 투표 동안 사용됩니다.  
  
-   **시작 하기 전에:**  [필수 구성 요소](#Prerequisites), [보안](#Security)  
  
-   **쿼럼 NodeWeight 설정을 보려면:** [TRANSACT-SQL을 사용 하 여](#TsqlProcedure), [Powershell을 사용 하 여](#PowerShellProcedure), [Cluster.exe 사용](#CommandPromptProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 이 기능은 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 이상 버전에서만 지원됩니다.  
  
> [!IMPORTANT]  
>  NodeWeight 설정을 사용하려면 WSFC 클러스터의 모든 서버에 다음 핫픽스를 적용해야 합니다.  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]에서 쿼럼 투표가 없는 클러스터 노드를 구성하는 데 사용할 수 있는 핫픽스  
  
> [!TIP]  
>  이 핫픽스가 설치되어 있지 않은 경우 이 항목의 예는 NodeWeight에 대해 빈 값이나 NULL 값을 반환합니다.  
  
###  <a name="Security"></a> 보안  
 사용자는 WSFC 클러스터의 각 노드에 대한 로컬 Administrators 그룹의 멤버인 도메인 계정이어야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 설정을 보려면  
  
1.  클러스터의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  [sys].[dm_hadr_cluster_members] 뷰를 쿼리합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예제에서는 시스템 뷰를 쿼리하여 해당 인스턴스의 클러스터에 있는 모든 노드에 대한 값을 반환합니다.  
  
```tsql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="PowerShellProcedure"></a> Powershell 사용  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 설정을 보려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 commandlet을 사용할 수 있도록 `FailoverClusters` 모듈을 가져옵니다.  
  
3.  `Get-ClusterNode` 개체를 사용하여 클러스터 노드 개체의 컬렉션을 반환합니다.  
  
4.  클러스터 노드 속성을 읽기 가능한 형식으로 출력합니다.  
  
### <a name="example-powershell"></a>예(Powershell)  
 다음 예제에서는 "Cluster001"이라는 클러스터의 노드 속성 일부를 출력합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Cluster.exe 사용  
  
> [!NOTE]  
>  cluster.exe 유틸리티는 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 릴리스에서 더 이상 사용되지 않습니다.  이후 개발에는 PowerShell과 장애 조치(failover) 클러스터링을 함께 사용하세요.  cluster.exe 유틸리티는 Windows Server의 다음 릴리스에서 제거될 예정입니다. 자세한 내용은 [Cluster.exe 명령을 장애 조치(failover) 클러스터용 Windows PowerShell Cmdlet에 매핑](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)을 참조하십시오.  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 설정을 보려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 명령 프롬프트를 시작합니다.  
  
2.  **cluster.exe** 를 사용하여 노드 상태 및 NodeWeight 값을 반환합니다.  
  
### <a name="example-clusterexe"></a>예(Cluster.exe)  
 다음 예제에서는 "Cluster001"이라는 클러스터의 노드 속성 일부를 출력합니다.  
  
```ms-dos  
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>관련 항목  
 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [클러스터 쿼럼 NodeWeight 설정 구성](configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)   
 [태스크 기준으로 나열된 Windows PowerShell의 장애 조치(failover) 클러스터 Cmdlet](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
