---
title: 새 가용성 그룹 대화 상자 사용(SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 1b0a6421-fbd4-4bb4-87ca-657f4782c433
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c589ac9755be006f5521f942e6bf1e19ea6e6a6e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602613"
---
# <a name="use-the-new-availability-group-dialog-box-sql-server-management-studio"></a>새 가용성 그룹 대화 상자 사용(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 **의** 새 가용성 그룹 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 사용하도록 설정된 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다. *가용성 그룹* 은 단일 단위로 장애 조치(Failover)될 사용자 데이터베이스 집합과 장애 조치(Failover)를 지원하는 장애 조치(Failover) 파트너 집합( *가용성 복제본*이라고 함)을 정의합니다.  
  
> [!NOTE]  
>  가용성 그룹에 대한 개요를 보려면 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#PrerequisitesRestrictions)  
  
     [제한 사항](#Limitations)  
  
     [보안](#Security)  
  
-   **가용성 그룹을 만드는 데 사용되는 도구:**  [새 가용성 그룹 대화 상자](#SSMSProcedure)  
  
-   **후속 작업:**  [새 가용성 그룹 대화 상자를 사용하여 가용성 그룹을 만든 후](#FollowUp)  
  
> [!NOTE]  
>  가용성 그룹을 만드는 다른 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [관련 작업](#RelatedTasks)을 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
 가용성 그룹을 처음 만들어 보는 경우 이 섹션을 먼저 읽는 것이 좋습니다.  
  
###  <a name="PrerequisitesRestrictions"></a> 필수 구성 요소  
  
-   가용성 그룹을 만들기 전에 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 동일한 WSFC 장애 조치(Failover) 클러스터 내의 다른 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는지 확인합니다. 또한 각 서버 인스턴스가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하도록 설정되어 있고 다른 모든 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 사전 요구 사항을 충족하는지 확인합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
-   가용성 그룹을 만들기 전에 가용성 복제본을 호스팅하는 모든 서버 인스턴스에 완전하게 기능하는 데이터베이스 미러링 엔드포인트가 있는지 확인하세요. 자세한 내용은 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)을 참조하세요.  
  
-   **새 가용성 그룹** 대화 상자를 사용하려면 가용성 복제본을 호스팅하는 서버 인스턴스의 이름을 알고 있어야 합니다. 또한 새 가용성 그룹에 추가할 모든 데이터베이스의 이름을 알고 있어야 하며 이러한 데이터베이스는 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다. 잘못된 값을 입력하면 새 가용성 그룹이 작동하지 않습니다.  
  
###  <a name="Limitations"></a> 제한 사항  
 **새 가용성 그룹** 대화 상자에서는 다음과 같은 작업을 수행할 수 없습니다.  
  
-   가용성 그룹 수신기를 만듭니다.  
  
-   보조 복제본을 가용성 그룹에 조인할 수 없습니다.  
  
-   초기 데이터 동기화를 수행할 수 없습니다.  
  
 이러한 구성 작업에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [후속 작업: 가용성 그룹을 만든 후](#FollowUp)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> 새 가용성 그룹 대화 상자(SQL Server Management Studio) 사용  
 **가용성 그룹을 만들려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 이름을 클릭합니다.  
  
2.  **Always On 고가용성** 노드를 확장합니다.  
  
3.  **가용성 그룹** 노드를 마우스 오른쪽 단추로 클릭하고 **새 가용성 그룹** 명령을 선택합니다.  
  
4.  이 명령을 실행하면 **새 가용성 그룹** 대화 상자가 열립니다.  
  
5.  **일반** 페이지의 **가용성 그룹 이름** 필드에 새 가용성 그룹의 이름을 입력합니다. 이 이름은 WSFC 클러스터의 모든 가용성 그룹에서 고유한 올바른 SQL Server 식별자여야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  
  
6.  **가용성 데이터베이스** 표에서 **추가** 를 클릭하고 이 가용성 그룹에 포함할 로컬 데이터베이스 이름을 입력합니다. 추가할 모든 데이터베이스에 대해 이 동작을 반복합니다. **확인**을 클릭하면 지정된 데이터베이스가 가용성 그룹에 속하기 위한 사전 요구 사항을 충족하는지 여부가 확인됩니다. 이러한 필수 조건에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
7.  **가용성 데이터베이스** 표에서 **추가** 를 클릭하여 보조 복제본을 호스팅할 서버 인스턴스 이름을 입력합니다. 이 대화 상자에서는 해당 인스턴스에 연결하려고 시도하지 않습니다. 잘못된 서버 이름을 지정하면 보조 복제본이 추가되지만 이 복제본에는 연결할 수 없습니다.  
  
    > [!TIP]  
    >  복제본을 추가했지만 호스트 서버 인스턴스에 연결할 수 없는 경우 해당 복제본을 제거하고 새 복제본을 추가합니다. 자세한 내용은 [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md) 및 [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)를 참조하세요.  
  
8.  대화 상자의 **페이지 선택** 창에서 **백업 기본 설정**을 클릭합니다. 그런 다음 **백업 기본 설정** 페이지에서 복제본 역할에 따라 백업을 실행할 위치를 지정하고 이 가용성 그룹에 대한 가용성 복제본을 호스팅할 각 서버 인스턴스에 백업 속성을 할당합니다. 자세한 내용은 [가용성 그룹 속성: 새 가용성 그룹&#40;일반 페이지&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-backup-preferences-page.md)을 참조하세요.  
  
9. 가용성 그룹을 만들려면 **확인**을 클릭합니다. 이렇게 하면 지정된 데이터베이스가 사전 요구 사항을 충족하는지 여부가 확인됩니다.  
  
     가용성 그룹을 만들지 않고 대화 상자를 종료하려면 **취소**를 클릭합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 새 가용성 그룹 대화 상자를 사용하여 가용성 그룹을 만든 후  
  
-   가용성 그룹의 보조 복제본을 호스팅하는 각 서버 인스턴스에 차례로 연결하여 다음 단계를 완료해야 합니다.  
  
    1.  보조 복제본을 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
    2.  각 주 데이터베이스와 해당 트랜잭션 로그의 현재 백업을 복원합니다(RESTORE WITH NORECOVERY 사용). 자세한 내용은 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
    3.  새로 준비된 각 보조 데이터베이스를 즉시 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
-   새 가용성 그룹에 대해 가용성 그룹 수신기를 만드는 것이 좋습니다. 이렇게 하려면 현재 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다. 자세한 내용은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **가용성 그룹 및 복제본 속성을 구성하려면**  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치(failover)의 상태 제어&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **가용성 그룹 구성을 완료하려면**  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **가용성 그룹을 만드는 다른 방법**  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
 **Always On 가용성 그룹을 사용하도록 설정하려면**  
  
-   [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **데이터베이스 미러링 엔드포인트를 구성하려면**  
  
-   [Always On 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Always On 가용성 그룹 구성 문제를 해결하려면**  
  
-   [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
