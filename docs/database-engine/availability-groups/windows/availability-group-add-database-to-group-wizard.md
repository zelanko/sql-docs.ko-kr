---
title: 가용성 그룹 - 그룹 마법사에 데이터베이스 추가 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e836fb404f71d1e2a37a7ab91353b4734aa50484
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34769289"
---
# <a name="availability-group---add-database-to-group-wizard"></a>가용성 그룹 - 그룹 마법사에 데이터베이스 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  가용성 그룹에 데이터베이스 추가 마법사를 사용하여 기존 Always On 가용성 그룹에 하나 이상의 데이터베이스를 손쉽게 추가할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 데이터베이스를 추가하는 방법은 [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)를 참조하세요.  
  
 **항목 내용:**  
  
-   **시작하기 전 주의 사항:**  
  
     [사전 요구 사항 및 제한 사항](#Prerequisites)  
  
     [보안](#Security)  
  
-   **데이터베이스를 추가하려면:**  [가용성 그룹에 데이터베이스 추가 마법사 사용(SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹에 데이터베이스를 추가한 적이 없는 경우 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)를 참조하세요.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소, 제한 사항 및 권장 사항  
  
-   현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
-   **전체 초기 데이터 동기화를 사용하기 위한 사전 요구 사항**  
  
    -   모든 데이터베이스 파일 경로는 가용성 그룹에 대한 복제본을 호스팅하는 모든 서버 인스턴스에서 동일해야 합니다.  
  
    -   보조 복제본을 호스팅하는 서버 인스턴스에 주 데이터베이스 이름이 없을 수 있습니다. 즉, 새 보조 데이터베이스가 아직 없을 수 있습니다.  
  
    -   마법사에서 백업을 만들고 액세스하려면 네트워크 공유를 지정해야 합니다. 주 복제본의 경우 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 시작하는 데 사용되는 계정은 네트워크 공유에 대한 읽기 및 쓰기 파일 시스템 권한이 있어야 합니다. 보조 복제본에 대한 계정은 네트워크 공유에 대한 읽기 권한이 있어야 합니다.  
  
     마법사를 사용하여 전체 초기 데이터 동기화를 수행할 수 없는 경우에는 보조 데이터베이스를 수동으로 준비해야 합니다. 마법사를 실행하기 전이나 후에 이 작업을 수행할 수 있습니다. 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)에서 AlwaysOn 가용성 그룹을 만들고 구성하는 방법을 설명합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> 가용성 그룹에 데이터베이스 추가 마법사 사용(SQL Server Management Studio)  
 **가용성 그룹에 데이터베이스 추가 마법사를 사용하려면**  
  
1.  개체 탐색기에서 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  데이터베이스를 추가할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **데이터베이스 추가** 명령을 선택합니다. 이 명령은 가용성 그룹에 데이터베이스 추가 마법사를 시작합니다.  
  
4.  **데이터베이스 선택** 페이지에서 하나 이상의 데이터베이스를 선택합니다. 자세한 내용은 [데이터베이스 선택 페이지&#40;새 가용성 그룹 마법사 및 데이터베이스 추가 마법사&#41;](../../../database-engine/availability-groups/windows/select-databases-page-new-availability-group-wizard-and-add-database-wizard.md)를 참조하세요.  
  
     데이터베이스에 데이터베이스 마스터 키가 들어 있는 경우 데이터베이스 마스터 키에 대한 암호를 **암호** 열에 입력합니다.  
  
5.  **초기 데이터 동기화 선택** 페이지에서 새 보조 복제본을 만들고 가용성 그룹에 조인할 방법을 선택합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **전체**  
  
         현재 환경이 초기 데이터 동기화 자동 시작을 위한 요구 사항을 충족하는 경우에 이 옵션을 선택합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소, 제한 사항 및 권장 사항](#Prerequisites)을 참조하세요.  
  
         **전체**를 선택한 후 가용성 그룹을 만들면 마법사에서 모든 주 데이터베이스와 해당 트랜잭션 로그를 네트워크 공유에 백업하고 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 백업을 복원하려고 시도합니다. 그런 다음 모든 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
         **모든 복제본에서 액세스할 수 있는 공유 네트워크 위치 지정:** 필드에서 복제본을 호스팅하는 모든 서버 인스턴스에 읽기/쓰기 액세스 권한이 있는 백업 공유를 지정합니다. 로그 백업이 로그 백업 체인의 일부입니다. 로그 백업 파일을 적절히 저장합니다.  
  
        > [!IMPORTANT]  
        >  필요한 파일 시스템 권한에 대한 자세한 내용은 이 항목의 앞부분에 나오는 [필수 구성 요소](#Prerequisites)를 참조하세요.  
  
    -   **조인만**  
  
         보조 복제본을 호스팅할 서버 인스턴스에서 보조 데이터베이스를 수동으로 준비하는 경우 이 옵션을 선택할 수 있습니다. 마법사에서 기존 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
    -   **초기 데이터 동기화 건너뛰기**  
  
         주 데이터베이스의 로그 백업과 사용자 데이터베이스를 사용하려는 경우 이 옵션을 선택합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
     자세한 내용은 [초기 데이터 동기화 페이지 선택&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md)을 참조하세요.  
  
6.  **기존 보조 복제본에 연결** 페이지에서 이 가용성 그룹에 대한 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 모두 동일한 사용자 계정의 서비스로 실행 중인 경우 **모든 연결**을 클릭합니다. 다른 계정에서 서비스로 실행 중인 서버 인스턴스가 있는 경우 각 서버 인스턴스 이름의 오른쪽에 있는 개별 **연결** 단추를 클릭합니다.  
  
     자세한 내용은 [기존 보조 복제본 페이지로 연결&#40;복제본 추가 마법사: 데이터베이스 추가 마법사&#41;](../../../database-engine/availability-groups/windows/connect-to-existing-secondary-replicas-page.md)을 참조하세요.  
  
7.  **유효성 검사** 페이지에서는 이 마법사에서 지정한 값이 새 가용성 그룹 마법사의 요구 사항을 충족하는지 여부를 확인합니다. 변경하려면 **이전** 을 클릭하여 이전 마법사 페이지로 돌아가서 하나 이상의 값을 변경하면 됩니다. **다음**을 클릭하여 **유효성 검사** 페이지로 돌아가서 **유효성 검사 다시 실행**을 클릭합니다.  
  
     자세한 내용은 [유효성 검사 페이지&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/validation-page-always-on-availability-group-wizards.md)를 참조하세요.  
  
8.  **요약** 페이지에서 새 가용성 그룹에 대한 선택 사항을 확인합니다. 변경하려면 **이전** 을 클릭하여 관련 페이지로 돌아갑니다. 변경 후에는 **다음** 을 클릭하여 **요약** 페이지로 돌아갑니다.  
  
     자세한 내용은 [요약 페이지&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/summary-page-always-on-availability-group-wizards.md)를 참조하세요.  
  
     선택이 완료되었으면 필요에 따라 스크립트를 클릭하여 마법사에서 실행할 단계에 대한 스크립트를 만들 수 있습니다. 새 가용성 그룹을 만들어 구성하려면 **마침**을 클릭합니다.  
  
9. **진행률** 페이지에 가용성 그룹을 만들기 위한 단계(끝점 구성, 가용성 그룹 만들기 및 가용성 그룹에 보조 복제본 조인)의 진행 상태가 표시됩니다.  
  
     자세한 내용은 [진행률 페이지&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/progress-page-always-on-availability-group-wizards.md)를 참조하세요.  
  
10. 이러한 단계가 완료되면 **결과** 페이지에 각 단계의 결과가 표시됩니다. 단계가 모두 성공하면 새 가용성 그룹이 완전히 구성됩니다. 단계에서 오류가 발생한 경우 구성을 수동으로 완료해야 할 수 있습니다. 주어진 오류의 원인에 대한 자세한 내용을 보려면 **결과** 열에서 연결된 "오류" 링크를 클릭합니다.  
  
     마법사가 완료되면 **닫기** 를 클릭하여 종료합니다.  
  
     자세한 내용은 [결과 페이지&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md)를 참조하세요.  
  
11. 모든 보조 데이터베이스에서 초기 데이터 동기화가 자동으로 시작되지 않은 경우 아직 조인되지 않은 모든 보조 데이터베이스를 구성해야 합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)   
 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
  
