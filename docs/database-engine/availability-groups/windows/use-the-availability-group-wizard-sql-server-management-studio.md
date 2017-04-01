---
title: "가용성 그룹 마법사 사용(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.newagwizard.f1"
  - "sql13.swb.newavgroupwiz.f1"
helpviewer_keywords: 
  - "새 가용성 그룹 마법사, 가용성 복제본"
  - "가용성 그룹 [SQL Server], 마법사"
  - "가용성 그룹 [SQL Server], 만들기"
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 45
---
# 가용성 그룹 마법사 사용(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 새 가용성 그룹 마법사를 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 AlwaysOn 가용성 그룹을 만들고 구성하는 방법을 설명합니다. *가용성 그룹* 은 단일 단위로 장애 조치(Failover)될 사용자 데이터베이스 집합과 장애 조치(Failover)를 지원하는 장애 조치(Failover) 파트너 집합( *가용성 복제본*이라고 함)을 정의합니다.  
  
> [!NOTE]  
>  가용성 그룹에 대한 소개는 [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소, 제한 사항 및 권장 사항](#Prerequisites)  
  
     [보안](#Security)  
  
-   **가용성 그룹을 만들고 구성하려면** [새 가용성 그룹 마법사(SQL Server Management Studio)](#RunAGwiz)를 사용합니다.  
  
> [!NOTE]  
>  새 가용성 그룹 마법사 대신 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell cmdlet을 사용할 수도 있습니다. 자세한 내용은 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md) 또는 [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)를 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹을 처음 만들어 보는 경우 이 섹션을 먼저 읽는 것이 좋습니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소, 제한 사항 및 권장 사항  
 대부분의 경우 새 가용성 그룹 마법사를 사용하여 가용성 그룹을 만들고 구성하는 데 필요한 모든 태스크를 완료할 수 있습니다. 그러나 일부 태스크를 수동으로 완료해야 할 수 있습니다.  
  
-   가용성 그룹을 만들기 전에 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 동일한 WSFC 장애 조치(Failover) 클러스터 내의 다른 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는지 확인합니다. 또한 각 서버 인스턴스가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]의 기타 모든 필수 구성 요소를 충족하는지도 확인합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)을 참조하세요.  
  
-   가용성 복제본을 호스팅하도록 선택한 서버 인스턴스가 도메인 사용자 계정으로 실행되고 있고 아직 데이터베이스 미러링 끝점을 가지고 있지 않은 경우, 마법사가 끝점을 만들고 서버 인스턴스 서비스 계정에 CONNECT 권한을 부여할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스와 같은 기본 제공 계정이나 비도메인 계정으로 실행 중인 경우에는 사용자가 끝점 인증을 위한 인증서를 사용해야 하며 마법사를 통해 서버 인스턴스에 대한 데이터베이스 미러링 끝점을 만들 수는 없습니다. 이 경우 새 가용성 그룹 마법사를 시작하기 전에 수동으로 데이터 미러링 끝점을 만드는 것이 좋습니다.  
  
     **데이터베이스 미러링 끝점에 대한 인증서를 사용하려면**  
  
     [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [데이터베이스 미러링 끝점에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)는 가용성 그룹에 따라 AlwaysOn 자동 장애 조치(Failover)를 지원하지 않으므로 FCI에서 호스팅하는 모든 가용성 복제본은 수동 장애 조치(Failover)에 대해서만 구성될 수 있습니다.  
  
-   **마법사를 사용하여 전체 초기 데이터 동기화를 수행하기 위한 필수 구성 요소**  
  
    -   모든 데이터베이스 파일 경로는 가용성 그룹에 대한 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다.  
  
    -   보조 복제본을 호스팅하는 서버 인스턴스에 주 데이터베이스 이름이 없을 수 있습니다. 즉, 새 보조 데이터베이스가 아직 없을 수 있습니다.  
  
    -   마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
        > [!IMPORTANT]  
        >  로그 백업이 로그 백업 체인의 일부입니다. 로그 백업 파일을 적절히 저장합니다.  
  
     마법사를 사용하여 전체 초기 데이터 동기화를 수행할 수 없는 경우에는 보조 데이터베이스를 수동으로 준비해야 합니다. 마법사를 실행하기 전이나 후에 이 작업을 수행할 수 있습니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 가용성 그룹 마법사에서 데이터베이스 미러링 끝점을 관리할 수 있도록 하려면 CONTROL ON ENDPOINT 권한도 필요합니다.  
  
##  <a name="RunAGwiz"></a> 새 가용성 그룹 마법사 사용  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  새 가용성 그룹 마법사를 시작하려면 **새 가용성 그룹 마법사** 명령을 선택합니다.  
  
4.  이 마법사를 처음 실행하는 경우 **소개** 페이지가 나타납니다. 다음부터 이 페이지를 건너뛰려면 **이 페이지를 다시 표시 안 함**을 클릭합니다. 이 페이지를 읽은 후 **다음**을 클릭합니다.  
  
5.  **가용성 그룹 이름 지정** 페이지에서 **가용성 그룹 이름** 필드에 새 가용성 그룹의 이름을 입력합니다. 이 이름은 WSFC 장애 조치(Failover) 클러스터와 도메인 전체에서 고유하고 유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 식별자여야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  
  
6.  **데이터베이스 선택** 페이지의 표에 *가용성 데이터베이스*로 적합한 연결된 서버 인스턴스의 사용자 데이터베이스가 나열됩니다. 나열된 데이터베이스 중 새 가용성 그룹에 참여할 데이터베이스를 하나 이상 선택합니다. 이러한 데이터베이스가 초기 *주 데이터베이스*가 됩니다.  
  
     나열된 각 데이터베이스의 **크기** 열에 데이터베이스 크기(알려진 경우)가 표시됩니다. **상태** 열에는 지정된 데이터베이스가 가용성 데이터베이스에 대한 [필수 구성 요소](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)를 충족하는지 여부가 표시됩니다. 필수 구성 요소가 충족되지 않는 경우 데이터베이스가 부적합한 이유(예: 전체 복구 모델을 사용하지 않는 경우)를 설명하는 간략한 상태 설명이 나타납니다. 자세한 내용을 보려면 상태 설명을 클릭하세요.  
  
     데이터베이스를 적합하도록 변경한 경우 **새로 고침** 을 클릭하여 데이터베이스 표를 업데이트합니다.  
  
     데이터베이스에 데이터베이스 마스터 키가 들어 있는 경우 데이터베이스 마스터 키에 대한 암호를 **암호** 열에 입력합니다.  
  
7.  **복제본 선택** 페이지에서 새 가용성 그룹에 대해 하나 이상의 복제본을 지정하고 구성합니다. 이 페이지에는 네 개의 탭이 있습니다. 다음 표에서는 이러한 탭을 보여 줍니다. 자세한 내용은 [복제본 페이지 지정&#40;새 가용성 그룹 마법사: 복제본 추가 마법사&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 항목을 참조하세요.  
  
    |탭|간단한 설명|  
    |---------|-----------------------|  
    |**복제본**|이 탭에서는 보조 복제본을 호스팅할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 각 인스턴스를 지정할 수 있습니다. 현재 연결된 서버 인스턴스가 주 복제본을 호스팅해야 합니다.|  
    |**끝점**|기존 데이터베이스 미러링 끝점을 확인하고, 서비스 계정에서 Windows 인증을 사용하는 서버 인스턴스에 이 끝점이 없는 경우 끝점을 자동으로 만들려면 이 탭을 사용합니다.<br /><br /> 참고: 서버 인스턴스가 도메인 사용자 계정이 아닌 계정으로 실행 중인 경우 마법사를 계속하려면 먼저 서버 인스턴스를 수동으로 변경해야 합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.|  
    |**백업 기본 설정**|가용성 그룹 전체에 대한 백업 기본 설정과 개별 가용성 복제본에 대한 백업 우선 순위를 지정하려면 이 탭을 사용합니다.|  
    |**수신기**|이 탭을 사용하여 가용성 그룹 수신기를 만들 수 있습니다. 기본적으로 마법사는 수신기를 만들지 않습니다.|  
  
8.  **초기 데이터 동기화 선택** 페이지에서 새 보조 복제본을 만들고 가용성 그룹에 조인할 방법을 선택합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **전체**  
  
         현재 환경이 초기 데이터 동기화 자동 시작을 위한 요구 사항을 충족하는 경우에 이 옵션을 선택합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소, 제한 사항 및 권장 사항](#Prerequisites)을 참조하세요.  
  
         **전체**를 선택한 후 가용성 그룹을 만들면 마법사에서 모든 주 데이터베이스와 해당 트랜잭션 로그를 네트워크 공유에 백업하고 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 백업을 복원합니다. 그런 다음 모든 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
         **모든 복제본에서 액세스할 수 있는 공유 네트워크 위치 지정:** 필드에서 복제본을 호스팅하는 모든 서버 인스턴스에 읽기/쓰기 액세스 권한이 있는 백업 공유를 지정합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
    -   **조인만**  
  
         보조 복제본을 호스팅할 서버 인스턴스에서 보조 데이터베이스를 수동으로 준비하는 경우 이 옵션을 선택할 수 있습니다. 마법사에서 기존 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
    -   **초기 데이터 동기화 건너뛰기**  
  
         주 데이터베이스의 로그 백업과 사용자 데이터베이스를 사용하려는 경우 이 옵션을 선택합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)을 참조하세요.  
  
9. **유효성 검사** 페이지에서는 이 마법사에서 지정한 값이 새 가용성 그룹 마법사의 요구 사항을 충족하는지 여부를 확인합니다. 변경하려면 **이전** 을 클릭하여 이전 마법사 페이지로 돌아가서 하나 이상의 값을 변경합니다. **다음**을 클릭하여 **유효성 검사** 페이지로 돌아가서 **유효성 검사 다시 실행**을 클릭합니다.  
  
10. **요약** 페이지에서 새 가용성 그룹에 대한 선택 사항을 확인합니다. 변경하려면 **이전** 을 클릭하여 관련 페이지로 돌아갑니다. 변경 후에는 **다음** 을 클릭하여 **요약** 페이지로 돌아갑니다.  
  
    > [!IMPORTANT]  
    >  새 가용성 복제본을 호스팅할 서버 인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정이 로그인으로 존재하지 않는 경우 새 가용성 그룹 마법사에서 로그인을 만들어야 합니다. **요약** 페이지에 만들 로그인에 대한 정보가 표시됩니다. **마침**을 클릭하면 SQL Server 서비스 계정에 대해 이 로그인이 만들어지고 로그인에 CONNECT 권한이 부여됩니다.  
  
     선택이 완료되었으면 필요에 따라 **스크립트** 를 클릭하여 마법사에서 실행할 단계에 대한 스크립트를 만들 수 있습니다. 새 가용성 그룹을 만들어 구성하려면 **마침**을 클릭합니다.  
  
11. **진행률** 페이지에 가용성 그룹을 만들기 위한 단계(끝점 구성, 가용성 그룹 만들기 및 가용성 그룹에 보조 복제본 조인)의 진행 상태가 표시됩니다.  
  
12. 이러한 단계가 완료되면 **결과** 페이지에 각 단계의 결과가 표시됩니다. 단계가 모두 성공하면 새 가용성 그룹이 완전히 구성됩니다. 어느 단계에서라도 오류가 발생하는 경우 수동으로 구성을 완료하거나 실패한 단계에 대해 마법사를 사용해야 합니다. 주어진 오류의 원인에 대한 자세한 내용을 보려면 **결과** 열에서 연결된 "오류" 링크를 클릭합니다.  
  
     마법사가 완료되면 **닫기** 를 클릭하여 종료합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 그룹 구성을 완료하려면**  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **가용성 그룹을 만드는 다른 방법**  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
 **Always On 가용성 그룹을 사용하도록 설정하려면**  
  
-   [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **데이터베이스 미러링 끝점을 구성하려면**  
  
-   [Always On 가용성 그룹에 대한 데이터베이스 미러링 끝점 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database mirroring - always on availability groups- powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 끝점에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [가용성 복제본 추가 또는 수정 시 끝점 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify endpoint url - adding or modifying availability replica.md)  
  
 **Always On 가용성 그룹 구성 문제를 해결하려면**  
  
-   [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [Always On - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](http://blogs.msdn.com/b/sqlAlways%20On/)  
  
     [CSS SQL Server 엔지니어 블로그](http://blogs.msdn.com/b/psssql/)  
  
-   **비디오:**  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 1부: 차세대 고가용성 솔루션 소개](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 2부: Always On을 사용하여 중요 업무용 고가용성 솔루션을 구축](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대한 Microsoft 백서](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## 참고 항목  
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)  
  
  