---
title: 가용성 그룹 시작
description: Always On 가용성 그룹을 지원하고 가용성 그룹을 만들고 관리하고 모니터링하는 SQL Server 인스턴스를 구성하는 단계에 대해 알아봅니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: reference
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], about
ms.assetid: 33f2f2d0-79e0-4107-9902-d67019b826aa
author: cawrites
ms.author: chadam
ms.openlocfilehash: 64dbc41027229f1904cf653a46c9015ca54d2c8c
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584297"
---
# <a name="getting-started-with-always-on-availability-groups"></a>Always On 가용성 그룹 시작
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 지원하도록 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스를 구성하고, 가용성 그룹을 만들고 관리하고 모니터링하기 위한 단계를 소개합니다.  
  
  
##  <a name="recommended-reading"></a><a name="RecommendedReading"></a> 권장 참조 항목  
 가용성 그룹을 처음 만드는 경우 다음 항목을 먼저 읽는 것이 좋습니다.  
  
-   [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
-   [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
##  <a name="configuring-an-instance-of-sql-server-to-support-always-on-availability-groups"></a><a name="ConfigSI"></a> Configuring an Instance of SQL Server to Support Always On Availability Groups  
  
|단계|링크|  
|----------|-----------|  
|**[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용하도록 설정합니다.** 가용성 그룹에 참여할 모든 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 기능을 사용하도록 설정해야 합니다.<br /><br /> **사전 요구 사항:**  호스트 컴퓨터는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드여야 합니다.<br /><br /> 다른 필수 조건에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 사용하도록 설정합니다.|[Always On 가용성 그룹 활성화 및 비활성화](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)|  
|**데이터베이스 미러링 엔드포인트를 만듭니다(없는 경우).** 각 서버 인스턴스에 [데이터베이스 미러링 엔드포인트](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)가 있는지 확인합니다. 서버 인스턴스는 이 엔드포인트를 사용하여 다른 서버 인스턴스에서의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 연결을 수신합니다.|데이터베이스 미러링 엔드포인트가 있는지 여부를 확인하려면 <br />                    [sys.database_mirroring_endpoints](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)<br /><br /> **Windows 인증의 경우**  데이터베이스 미러링 엔드포인트를 만들려면 다음을 사용합니다.<br /><br /> [새 가용성 그룹 마법사](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [SQL Server PowerShell](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)<br /><br /> **인증서 인증의 경우** 데이터베이스 미러링 엔드포인트를 만드는 데 사용되는 도구:[Transact-SQL](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
##  <a name="creating-and-configuring-a-new-availability-group"></a><a name="ConfigAG"></a> Creating and Configuring a New Availability Group  
  
|단계|링크|  
|----------|-----------|  
|**가용성 그룹을 만듭니다.** 가용성 그룹에 추가할 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 가용성 그룹을 만듭니다.<br /><br /> 최소한, 가용성 그룹을 만들 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 초기 주 복제본을 만듭니다. 1~4개의 보조 복제본을 지정할 수 있습니다. 가용성 그룹 및 복제본 속성에 대한 자세한 내용은 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)을 참조하세요.<br /><br /> 또한 [가용성 그룹 수신기](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)를 만드는 것이 좋습니다.<br /><br /> **사전 요구 사항:**  지정된 가용성 그룹의 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 단일 WSFC 클러스터의 개별 노드에 있어야 합니다. 유일한 예외는 다른 WSFC 클러스터로 마이그레이션되는 동안 가용성 그룹이 일시적으로 두 클러스터에 걸쳐 있는 경우입니다.<br /><br /> 다른 필수 조건에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 사용하도록 설정합니다.|가용성 그룹을 만들려면 다음 도구 중 하나를 사용합니다.<br /><br /> [새 가용성 그룹 마법사](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)<br /><br /> [SQL Server PowerShell](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)|  
|**보조 복제본을 가용성 그룹에 조인할 수 없습니다.** 보조 복제본을 호스팅하는 각 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 인스턴스에 연결한 다음 로컬 보조 복제본을 가용성 그룹에 조인합니다.|[가용성 그룹에 보조 복제본 조인](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> 팁: 새 가용성 그룹 마법사를 사용하는 경우 이 단계가 자동으로 수행됩니다.|  
|**보조 데이터베이스를 준비합니다.** 보조 복제본을 호스팅하는 각 서버 인스턴스에서 RESTORE WITH NORECOVERY를 사용하여 주 데이터베이스의 백업을 복원합니다.|[보조 데이터베이스 수동 준비](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)<br /><br /> 팁: 새 가용성 그룹 마법사는 보조 데이터베이스를 자동으로 준비할 수 있습니다. 자세한 내용은 [초기 데이터 동기화 페이지 선택&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md)에서 "전체 초기 데이터 동기화를 사용하기 위한 필수 조건"을 참조하세요.|  
|**가용성 그룹에 보조 데이터베이스를 조인합니다.** 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 각 로컬 보조 데이터베이스를 가용성 그룹에 조인합니다. 가용성 그룹을 조인하면 지정된 보조 데이터베이스가 해당 주 데이터베이스와의 데이터 동기화를 시작합니다.|[가용성 그룹에 보조 데이터베이스 조인](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)<br /><br /> 팁: 모든 보조 복제본에 모든 보조 데이터베이스가 있는 경우 새 가용성 그룹 마법사가 이 단계를 수행할 수 있습니다.|  
|**가용성 그룹 수신기를 만듭니다.**  이 단계는 가용성 그룹을 만드는 중 가용성 그룹 수신기를 아직 만들지 않은 경우에 필요합니다.|[가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|**애플리케이션 개발자에 수신기의 DNS 이름을 제공합니다.**  개발자가 연결 요청을 가용성 그룹 수신기에 연결하기 위해서는 연결 문자열에 이 DNS 이름을 지정해야 합니다. 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)를 참조하세요.|"후속 작업: 가용성 그룹 수신기를 만든 후"([가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)에서)|  
|**백업 작업 위치를 구성합니다.**  보조 데이터베이스에서 백업을 수행하려면 자동화된 백업 기본 설정을 고려하는 백업 작업 스크립트를 만들어야 합니다. 가용성 그룹의 가용성 복제본을 호스팅하는 각 서버 인스턴스에서 가용성 그룹의 각 데이터베이스에 대해 스크립트를 만듭니다.|"후속 작업: 보조 복제본에 백업을 구성한 후"([가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)에서)|  
  
##  <a name="managing-availability-groups-replicas-and-databases"></a><a name="ManageAGsEtc"></a> Managing Availability Groups, Replicas, and Databases  
  
> [!NOTE]  
>  가용성 그룹 및 복제본 속성에 대한 자세한 내용은 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)을 참조하세요.  
  
 기존 가용성 그룹 관리에는 다음 태스크 중 하나 이상이 포함됩니다.  
  
|Task|링크|  
|----------|----------|  
|가용성 그룹의 [유연한 장애 조치(failover) 정책](./configure-flexible-automatic-failover-policy.md) 을 수정하여 자동 장애 조치를 수행해야 하는 상태를 제어합니다. 이 정책은 자동 장애 조치가 가능한 경우에만 유효합니다.|[가용성 그룹의 유연한 장애 조치(failover) 정책 구성](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)|  
|일반적으로 *강제 장애 조치(failover)* 라고 하는 강제 수동 장애 조치(failover)(데이터가 손실될 수 있음)나 계획된 수동 장애 조치(failover)를 수행합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.|[계획된 수동 장애 조치(failover) 수행](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br /> [강제 수동 장애 조치(failover) 수행](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)|  
|미리 정의된 일련의 정책을 사용하여 가용성 그룹과 해당 복제본 및 데이터베이스의 상태를 확인합니다.|[정책 기반 관리를 사용하여 가용성 그룹 상태 보기](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)<br /><br /> [Always On 그룹 대시보드 사용](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)|  
|보조 복제본을 추가하거나 제거합니다.|[보조 복제본 추가](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [보조 복제본 제거](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|가용성 데이터베이스를 일시 중지하거나 다시 시작합니다. 보조 데이터베이스를 일시 중지하면 다시 시작할 때까지 현재 시점의 상태로 유지됩니다.|[데이터베이스 일시 중지](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)<br /><br /> [데이터베이스 다시 시작](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)|  
|데이터베이스를 추가하거나 제거합니다.|[데이터베이스 추가](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)<br /><br /> [보조 데이터베이스 제거](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [주 데이터베이스 제거](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)|  
|가용성 그룹 수신기를 다시 구성하거나 만듭니다.|[가용성 그룹 수신기 만들기 또는 구성](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|가용성 그룹을 삭제합니다.|[가용성 그룹 삭제](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)|  
|파일 추가 작업의 문제를 해결합니다. 이 단계는 주 데이터베이스와 보조 데이터베이스의 파일 경로가 다른 경우에 필요합니다.|[실패한 파일 추가 작업 문제 해결](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|  
|가용성 복제본 속성을 변경합니다.|[가용성 모드 변경](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)<br /><br /> [장애 조치(failover) 모드 변경](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)<br /><br /> [백업 우선 순위(및 자동화된 백업 기본 설정) 구성](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)<br /><br /> [읽기 전용 액세스 구성](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)<br /><br /> [읽기 전용 라우팅 구성](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)<br /><br /> [세션 제한 시간 변경](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)|  
  
##  <a name="monitoring-availability-groups"></a><a name="MonitorAGsEtc"></a> Monitoring Availability Groups  
 Always On 가용성 그룹의 속성 및 상태를 모니터링하려면 다음 도구를 사용할 수 있습니다.  
  
|도구|간략한 설명|링크|  
|----------|-----------------------|-----------|  
|SQL Server용 System Center 모니터링 팩|SQL Server용 모니터링 팩(SQLMP)은 가용성 그룹, 가용성 복제본 및 IT 관리자의 가용성 데이터베이스를 모니터링하기 위한 권장 솔루션입니다. 특히 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 과 관련된 모니터링 기능은 다음과 같습니다.<br /><br /> 수백 개 컴퓨터 간의 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스의 자동 검색 기능 이 기능을 사용하면 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인벤토리를 쉽게 추적할 수 있습니다.<br /><br /> 완전한 기능의 System Center Operations Manager(SCOM) 경고 및 티켓 부여. 이러한 기능은 보다 빠른 문제 해결을 위한 세부 지식을 제공합니다.<br /><br /> PBM(정책 기반 관리)을 사용한 Always On 상태 모니터링에 대한 사용자 정의 확장.<br /><br /> 상태는 가용성 데이터베이스에서 가용성 복제본으로 롤업됩니다.<br /><br /> System Center 운영 관리자 콘솔로부터 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 관리하는 사용자 정의 작업.|모니터링 팩(SQLServerMP.msi) 및 *System Center Operations Manager용 SQL Server 관리 팩 가이드* (SQLServerMPGuide.doc)를 다운로드하려면 다음을 참조하세요.<br /><br /> [SQL Server용 System Center 모니터링 팩](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 카탈로그 및 동적 관리 뷰는 가용성 그룹과 해당 복제본, 데이터베이스, 수신기 및 WSFC 클러스터 환경에 대한 풍부한 정보를 제공합니다.|[가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**개체 탐색기 정보** 창에는 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 호스팅된 가용성 그룹에 대한 기본 정보가 표시됩니다.<br /><br /> 팁: 이 창을 사용하여 여러 가용성 그룹, 복제본 또는 데이터베이스를 선택하고 선택한 개체에 대한 일상적인 관리 태스크를 수행합니다(예: 가용성 그룹에서 여러 가용성 복제본 또는 데이터베이스 제거).|[개체 탐색기 정보를 사용하여 가용성 그룹 모니터링](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**속성** 대화 상자에서는 가용성 그룹, 복제본 또는 수신기의 속성을 보고 필요한 경우 해당 값을 변경할 수 있습니다.|[가용성 그룹 속성](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)<br /><br /> [가용성 복제본 속성](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)<br /><br /> [가용성 그룹 수신기 속성](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)|  
|시스템 모니터|**SQLServer:Availability Replica** 성능 개체에는 가용성 복제본에 대한 정보를 보고하는 성능 카운터가 포함됩니다.|[SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|시스템 모니터|**SQLServer:Database Replica** 성능 개체에는 지정된 보조 복제본의 보조 데이터베이스에 대한 정보를 보고하는 성능 카운터가 포함됩니다.<br /><br /> SQL Server의 **SQLServer:Databases** 개체에는 특히 트랜잭션 로그 작업을 모니터링하는 성능 카운터가 포함됩니다. 가용성 데이터베이스에서 트랜잭션 로그 작업 모니터링과 관련된 카운터는 **Log Flush Write Time (ms)** , **Log Flushes/sec**, **Log Pool Cache Misses/sec**, **Log Pool Disk Reads/sec** 및 **Log Pool Requests/sec** 입니다.|[SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [SQL Server, Databases 개체](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   **동영상-Always On 소개:**  [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 1부: 차세대 고가용성 솔루션 소개](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
-   **동영상 - Always On 심층 탐구:**  [Microsoft SQL Server 코드 이름 “Denali” Always On 시리즈, 2부: Always On을 사용하여 중요 업무용 고가용성 솔루션을 구축](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
-   **블로그:**  [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 서버 인스턴스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 Transact-SQL 문 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)   
 [Always On 가용성 그룹에 대한 PowerShell Cmdlet 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
