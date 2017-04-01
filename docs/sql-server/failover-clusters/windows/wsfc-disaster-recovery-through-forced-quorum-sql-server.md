---
title: "강제 쿼럼을 통해 WSFC 재해 복구(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "가용성 그룹 [SQL Server], WSFC 클러스터"
  - "쿼럼 [SQL Server], AlwaysOn 및 WSFC 쿼럼"
  - "장애 조치(Failover) 클러스터링 [SQL Server], AlwaysOn 가용성 그룹"
ms.assetid: 6cefdc18-899e-410c-9ae4-d6080f724046
caps.latest.revision: 21
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 20
---
# 강제 쿼럼을 통해 WSFC 재해 복구(SQL Server)
  쿼럼 실패는 일반적으로 시스템 관련 재해나, 지속적인 통신 오류 또는 WSFC 클러스터의 여러 노드와 관련된 잘못된 구성으로 인해 발생합니다.  쿼럼 실패에서 복구하려면 수동 개입이 필요합니다.  
  
-   **시작하기 전 주의 사항:**  [필수 구성 요소](#Prerequisites), [보안](#Security)  
  
-   **강제 쿼럼 절차를 통해 WSFC 재해 복구** [강제 쿼럼 절차를 통해 WSFC 재해 복구](#Main)  
  
-   [관련 태스크](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 강제 쿼럼 절차는 쿼럼 실패 전에 정상 상태의 쿼럼이 있었다고 가정합니다.  
  
> [!WARNING]  
>  사용자는 Windows Server 장애 조치(Failover) 클러스터링, WSFC 쿼럼 모델, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 환경의 특정 배포 구성에 대한 개념 및 상호 작용에 대해 잘 알고 있어야 합니다.  
>   
>  자세한 내용은 [SQL Server의 WSFC(Windows Server 장애 조치(failover) 클러스터링)](http://msdn.microsoft.com/library/hh270278\(v=SQL.110\).aspx), [WSFC 쿼럼 모드 및 투표 구성(SQL Server)](http://msdn.microsoft.com/library/hh270280\(v=SQL.110\).aspx)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
 사용자는 WSFC 클러스터의 각 노드에 대한 로컬 Administrators 그룹의 멤버인 도메인 계정이어야 합니다.  
  
##  <a name="Main"></a> 강제 쿼럼 절차를 통해 WSFC 재해 복구  
 클러스터는 그 구성에 따라 노드 수준의 내결함성을 보장할 수 없기 때문에 쿼럼 실패가 발생하면 WSFC 클러스터의 클러스터형 서비스, SQL Server 인스턴스 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]이 모두 오프라인 상태로 설정됩니다.  쿼럼 실패란 WSFC 클러스터의 정상적인 투표 노드가 더 이상 쿼럼 모델을 충족하지 않음을 의미합니다. 일부 노드는 완전히 실패했을 수 있고 나머지 일부 노드는 WSFC 서비스만 종료했으며 쿼럼과의 통신 기능이 손실되었다는 점을 제외하고는 정상일 수 있습니다.  
  
 WSFC 클러스터를 다시 온라인 상태로 전환하려면 기존 구성에서 쿼럼 실패의 근본 원인을 해결하고 필요한 경우 영향을 받은 데이터베이스를 복구해야 하며 실패에서 살아남은 클러스터 토폴로지를 반영하도록 WSFC 클러스터의 나머지 노드를 다시 구성해야 합니다.  
  
 클러스터를 오프라인 상태로 전환한 보안 장치를 무시하기 위해 WSFC 클러스터 노드에서 *강제 쿼럼* 절차를 수행할 수 있습니다.  이 경우 클러스터에서 쿼럼 투표 검사가 일시 중지되어 클러스터의 모든 노드에서 WSFC 클러스터 리소스 및 SQL Server를 다시 온라인 상태로 전환할 수 있습니다.  
  
 이 유형의 재해 복구 프로세스에는 다음 단계가 포함됩니다.  
  
#### 쿼럼 실패에서 복구하려면  
  
1.  **실패의 범위 확인.** 응답하지 않는 가용성 그룹 또는 SQL Server 인스턴스, 온라인 상태이며 재해 발생 후 사용이 가능한 클러스터 노드를 식별하고 Windows 이벤트 로그와 SQL Server 시스템 로그를 검토합니다.  필요한 경우 향후 분석을 위해 조사한 데이터와 시스템 로그를 보존해야 합니다.  
  
    > [!TIP]  
    >  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 응답 인스턴스에서는 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md) DMV(동적 관리 뷰)를 쿼리하여 로컬 서버 인스턴스에서 가용성 복제본을 처리하는 가용성 그룹의 상태 정보를 가져올 수 있습니다.  
  
2.  **단일 노드에서 강제 쿼럼을 수행하여 WSFC 클러스터 시작.** WSFC 클러스터 서비스가 종료된 노드 이외의 노드 중에서 구성 요소 오류 수가 가장 적은 노드를 파악합니다.  이 노드가 대부분의 다른 노드와 통신할 수 있는지 확인합니다.  
  
     이 노드에서 강제 쿼럼 절차를 수행하여 수동으로 클러스터를 온라인 상태로 전환합니다.  데이터 손실 위험을 최소화하려면 가용성 그룹 주 복제본을 마지막으로 호스팅한 노드를 선택합니다.  
  
     자세한 내용은  [쿼럼 없이 WSFC 클러스터 강제 시작](http://msdn.microsoft.com/library/hh270275\(v=SQL.110\).aspx)을 참조하세요.  
  
    > [!NOTE]  
    >  강제 쿼럼 설정은 클러스터 전반에 영향을 주어 논리적 WSFC 클러스터가 과반수의 투표를 확보하고 자동으로 정상 쿼럼 작업 모드로 전환될 때까지 쿼럼 검사를 차단합니다.  
  
3.  **각 정상 노드에서 한 번에 하나씩 WSFC 서비스 시작.** 다른 노드에서 클러스터 서비스를 시작할 때는 강제 쿼럼 옵션을 지정할 필요가 없습니다.  
  
     각 노드에서 WSFC 서비스가 온라인 상태로 전환되면 서비스는 다른 정상 노드와 협상하여 새 클러스터 구성 상태를 동기화합니다.  이 작업은 마지막으로 알려진 클러스터 상태 해결과 관련된 경합 상태를 방지하기 위해 한 번에 한 노드에서 수행되어야 합니다.  
  
    > [!WARNING]  
    >  시작하는 각 노드가 새로 온라인 상태로 전환된 다른 노드와 통신할 수 있는지 확인하세요.  다른 노드에서 WSFC 서비스를 비활성화하는 것이 좋습니다.  그렇지 않으면 쿼럼 노드 집합이 둘 이상 만들어져 분리 장애(split-brain) 시나리오가 발생할 수 있습니다. 1단계에서 조사한 내용이 정확하면 이러한 일이 발생하지 않습니다.  
  
4.  **새 쿼럼 모드 및 노드 투표 구성 적용.** 쿼럼을 강제로 실행하여 클러스터의 모든 노드를 성공적으로 다시 시작했으며 쿼럼 실패의 근본 원인을 해결한 경우 원래 쿼럼 모드 및 노드 투표 구성을 변경할 필요가 없습니다.  
  
     그렇지 않은 경우에는 새로 복구한 클러스터 노드와 가용성 복제본 토폴로지를 평가하여 각 노드의 쿼럼 모드 및 투표 수 할당을 적절히 변경해야 합니다. 복구되지 않은 노드의 경우 오프라인으로 설정하거나 해당 노드의 투표 수를 0으로 설정해야 합니다.  
  
    > [!TIP]  
    >  이때 클러스터의 노드 및 SQL Server 인스턴스 수는 정상 작동할 때의 수로 복원된 것으로 나타나지만  정상 상태의 쿼럼은 아직 없을 수도 있습니다.  장애 조치(failover) 클러스터 관리자, SQL Server Management Studio의 Always On 대시보드 또는 적절한 DMV를 사용하여 쿼럼이 복원되었는지 확인하세요.  
  
5.  **필요한 경우 가용성 그룹 데이터베이스 복제본 복구.** 가용성 그룹 데이터베이스 이외 데이터베이스는 일반 SQL Server 시작 프로세스의 일부로 자체적으로 복구되고 온라인 상태로 전환되어야 합니다.  
  
     주 복제본, 동기 보조 복제본, 비동기 보조 복제본의 순서로 가용성 그룹 복제본을 다시 온라인 상태로 전환하여 데이터 손실 위험 및 복구 시간을 최소화할 수 있습니다.  
  
6.  **실패한 구성 요소 복구 또는 교체 후 클러스터에 대해 유효성 검사 다시 수행.** 이제 초기 재해 및 쿼럼 실패에서 복구했으므로 실패한 노드를 복구 또는 교체하고 관련 WSFC 및 Always On 구성을 적절히 조정해야 합니다.  여기에는 가용성 그룹 복제본을 삭제하고, 노드를 클러스터에서 제거하고, 노드에서 소프트웨어를 정리하고 다시 설치하는 작업이 포함될 수 있습니다.  
  
     실패한 가용성 복제본을 모두 복구하거나 제거해야 합니다.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 가용성 복제본의 마지막으로 알려진 가장 오래된 시점 이후의 트랜잭션 로그를 자르지 않습니다.   실패한 복제본을 복구하거나 가용성 그룹에서 제거하지 않으면 트랜잭션 로그 크기가 계속 증가하여 다른 복제본의 트랜잭션 로그 공간이 부족해질 수 있습니다.  
  
    > [!NOTE]  
    >  가용성 그룹 수신기가 WSFC 클러스터에 있을 때 WSFC 구성 유효성 검사 마법사를 실행하면 마법사가 다음과 같이 잘못된 경고 메시지를 생성합니다.  
    >   
    >  “네트워크 이름 'Name:<network_name>'의 RegisterAllProviderIP 속성이 1로 설정되어 있습니다. 현재 클러스터 구성에서는 이 값을 0으로 설정해야 합니다.”  
    >   
    >  이 메시지는 무시하세요.  
  
7.  **필요한 경우 4단계 반복.** 이 작업의 목표는 정상적인 작동을 위해 적절한 수준의 내결함성 및 고가용성을 다시 설정하는 데 있습니다.  
  
8.  **RPO/RTO 분석 실시.** SQL Server 시스템 로그, 데이터베이스 타임스탬프 및 Windows 이벤트 로그를 분석하여 실패의 근본 원인을 파악하고 실제 복구 지점 및 복구 시간 방법을 문서화해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [쿼럼 없이 WSFC 클러스터 강제 시작](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 보기](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 구성](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20AlwaysOn%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [장애 조치(Failover) 클러스터에 대한 이벤트 및 로그 보기](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 장애 조치(Failover) 클러스터 Cmdlet](http://technet.microsoft.com/library/ee461045.aspx)  
  
## 참고 항목  
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  