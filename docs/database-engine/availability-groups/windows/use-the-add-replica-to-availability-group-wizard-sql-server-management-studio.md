---
title: SSMS의 마법사를 사용하여 가용성 그룹에 복제본 추가 - SQL Server
ms.description: Add a replica to an Always On availability group using the wizard found in SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a89678fd2964e528ed09a38184fc295e0c955d98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013557"
---
# <a name="add-a-replica-to-your-always-on-availability-group-using-the-availability-group-wizard-in-sql-server-management"></a>SQL Server management의 가용성 그룹 마법사를 사용하여 Always On 가용성 그룹에 복제본 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **가용성 그룹에 복제본 추가 마법사**를 사용하여 기존 Always On 가용성 그룹에 새 보조 복제본을 추가할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 가용성 그룹에 보조 복제본을 추가하는 방법은 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)를 참조하세요.  
    
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹에 가용성 복제본을 추가한 적이 없는 경우 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)의 "서버 인스턴스" 섹션과 "가용성 그룹 및 복제본" 섹션을 참조하세요.  
  
##  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   보조 복제본을 추가하기 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 호스트 인스턴스가 기존 복제본과 동일한 WSFC(Windows Server 장애 조치 클러스터)에 있지만 다른 클러스터 노드에 있는지 확인합니다. 또한 이 서버 인스턴스가 다른 모든 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 사전 요구 사항과 일치하는지도 확인합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)를 참조하세요.  
  
-   가용성 복제본을 호스팅하도록 선택한 서버 인스턴스가 도메인 사용자 계정으로 실행되고 있고 아직 데이터베이스 미러링 엔드포인트를 가지고 있지 않은 경우, 마법사가 엔드포인트를 만들고 서버 인스턴스 서비스 계정에 CONNECT 권한을 부여할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스와 같은 기본 제공 계정이나 비도메인 계정으로 실행 중인 경우에는 사용자가 엔드포인트 인증을 위한 인증서를 사용해야 하며 마법사를 통해 서버 인스턴스에 대한 데이터베이스 미러링 엔드포인트를 만들 수는 없습니다. 이 경우 가용성 그룹에 복제본 추가 마법사를 시작하기 전에 데이터 미러링 엔드포인트를 수동으로 만드는 것이 좋습니다.  
  
     **데이터베이스 미러링 엔드포인트에 대한 인증서를 사용하려면**  
  
     [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **전체 초기 데이터 동기화를 사용하기 위한 사전 요구 사항**  
  
    -   모든 데이터베이스 파일 경로는 가용성 그룹에 대한 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다.  
  
    -   보조 복제본을 호스팅하는 서버 인스턴스에 주 데이터베이스 이름이 없을 수 있습니다. 즉, 새 보조 데이터베이스가 아직 없을 수 있습니다.  
  
    -   마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
     마법사를 사용하여 전체 초기 데이터 동기화를 수행할 수 없는 경우에는 보조 데이터베이스를 수동으로 준비해야 합니다. 마법사를 실행하기 전이나 후에 이 작업을 수행할 수 있습니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 Always On 가용성 그룹에 보조 데이터베이스를 조인하는 방법에 대해 설명합니다.  
   
## <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
 가용성 그룹에 복제본 추가 마법사에서 데이터베이스 미러링 엔드포인트를 관리할 수 있도록 하려면 CONTROL ON ENDPOINT 권한도 필요합니다.  
  
##  <a name="SSMSProcedure"></a> 복제본을 가용성 그룹에 추가 마법사 사용(SQL Server Management Studio)  
 **복제본을 가용성 그룹에 추가 마법사를 사용하려면**  
  
1.  개체 탐색기에서 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  보조 복제본을 추가할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **복제본 추가** 명령을 선택합니다. 그러면 복제본을 가용성 그룹에 추가 마법사가 시작됩니다.  
  
4.  **기존 보조 복제본에 연결** 페이지에서 가용성 그룹의 모든 보조 복제본에 연결합니다. 자세한 내용은 [기존 보조 복제본 페이지로 연결&#40;복제본 추가 마법사: 데이터베이스 추가 마법사&#41;](../../../database-engine/availability-groups/windows/connect-to-existing-secondary-replicas-page.md)를 참조하세요.  
  
5.  **복제본 선택** 페이지에서 가용성 그룹에 대해 하나 이상의 새 보조 복제본을 지정하고 구성합니다. 이 페이지에는 세 개의 탭이 있습니다. 다음 표에서는 이러한 탭을 보여 줍니다. 자세한 내용은 [복제본 페이지 지정&#40;새 가용성 그룹 마법사: 복제본 추가 마법사&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)를 참조하세요.  
  
    |탭|간단한 설명|  
    |---------|-----------------------|  
    |**복제본**|이 탭에서는 새 보조 복제본을 호스팅할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 각 인스턴스를 지정할 수 있습니다.|  
    |**엔드포인트**|이 탭에서는 각 새 보조 복제본에 대한 기존 데이터베이스 미러링 엔드포인트(있는 경우)를 확인할 수 있습니다. 이 엔드포인트가 서버 계정에서 Windows 인증을 사용하는 서버 인스턴스에 없는 경우 마법사가 엔드포인트를 자동으로 만들도록 시도합니다.<br /><br /> <br /><br /> 참고: 서버 인스턴스가 도메인 사용자 계정이 아닌 계정으로 실행 중인 경우 마법사를 계속하려면 먼저 서버 인스턴스를 수동으로 변경해야 합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.|  
    |**백업 기본 설정**|이 탭에서는 현재 설정을 수정하려는 경우 가용성 그룹 전체에 대한 백업 기본 설정을 지정하고 개별 가용성 복제본에 대한 백업 우선 순위를 지정할 수 있습니다.|  
  
6.  선택한 복제본이 데이터베이스 마스터 키가 있는 데이터베이스를 포함하는 경우 **암호** 열의 데이터베이스 마스터 키에 암호를 입력합니다. **상태** 열은 데이터베이스 마스터 키가 있는 데이터베이스에 대한 **암호 필요** 를 나타냅니다. **다음**은 **암호** 열에 올바른 암호를 입력할 때까지 회색으로 표시됩니다. 암호를 입력한 후 **새로 고침**을 클릭합니다. 암호를 올바르게 입력하면 상태 열에 **암호 입력됨**이 표시되고, **다음**을 사용할 수 있게 됩니다.  
  
7.  **초기 데이터 동기화 선택** 페이지에서 새 보조 복제본을 만들고 가용성 그룹에 조인할 방법을 선택합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **전체**  
  
         현재 환경이 초기 데이터 동기화 자동 시작을 위한 요구 사항을 충족하는 경우에 이 옵션을 선택합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 조건, 제한 사항 및 권장 사항](#Prerequisites)을 참조하세요.  
  
         **전체**를 선택한 후 가용성 그룹을 만들면 마법사에서 모든 주 데이터베이스와 해당 트랜잭션 로그를 네트워크 공유에 백업하고 새 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 백업을 복원합니다. 그런 다음 모든 새 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
         **모든 복제본에서 액세스할 수 있는 공유 네트워크 위치 지정:** 필드에서 복제본을 호스트하는 모든 서버 인스턴스에 읽기/쓰기 액세스 권한이 있는 백업 공유를 지정합니다. 로그 백업이 로그 백업 체인의 일부입니다. 로그 백업 파일을 적절히 저장합니다.  
  
        > [!IMPORTANT]  
        >  필요한 파일 시스템 권한에 대한 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
    -   **조인만**  
  
         새 보조 복제본을 호스팅할 서버 인스턴스에서 보조 데이터베이스를 수동으로 준비하는 경우 이 옵션을 선택할 수 있습니다. 마법사에서 이러한 새 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
    -   **초기 데이터 동기화 건너뛰기**  
  
         주 데이터베이스의 로그 백업과 사용자 데이터베이스를 사용하려는 경우 이 옵션을 선택합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
8.  **유효성 검사** 페이지에서는 이 마법사에서 지정한 값이 가용성 그룹에 복제본 추가 마법사의 요구 사항을 충족하는지 여부를 확인합니다. 변경하려면 **이전** 을 클릭하여 이전 마법사 페이지로 돌아가서 하나 이상의 값을 변경합니다. **다음** 을 클릭하여 **유효성 검사** 페이지로 돌아가서 **유효성 검사 다시 실행**을 클릭합니다.  
  
9. **요약** 페이지에서 새 가용성 그룹에 대한 선택 사항을 확인합니다. 변경하려면 **이전** 을 클릭하여 관련 페이지로 돌아갑니다. 변경 후에는 **다음** 을 클릭하여 **요약** 페이지로 돌아갑니다.  
  
     선택이 완료되었으면 필요에 따라 스크립트를 클릭하여 마법사에서 실행할 단계에 대한 스크립트를 만들 수 있습니다. 새 가용성 그룹을 만들어 구성하려면 **마침**을 클릭합니다.  
  
10. **진행률** 페이지에 가용성 그룹을 만들기 위한 단계(엔드포인트 구성, 가용성 그룹 만들기 및 가용성 그룹에 보조 복제본 조인)의 진행 상태가 표시됩니다.  
  
11. 이러한 단계가 완료되면 **결과** 페이지에 각 단계의 결과가 표시됩니다. 단계가 모두 성공하면 새 가용성 그룹이 완전히 구성됩니다. 단계에서 오류가 발생한 경우 구성을 수동으로 완료해야 할 수 있습니다. 주어진 오류의 원인에 대한 자세한 내용을 보려면 **결과** 열에서 연결된 "오류" 링크를 클릭합니다.  
  
     마법사가 완료되면 **닫기** 를 클릭하여 종료합니다.  
  
> [!IMPORTANT]  
>  복제본을 추가한 후 "후속 작업: [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)의 복제본 추가 후" 섹션을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
