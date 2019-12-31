---
title: 가용성 그룹 관리(SQL Server) | Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8d826201f44bb666050f5229b4824b5c2198dc0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75229002"
---
# <a name="administration-of-an-availability-group-sql-server"></a>가용성 그룹 관리(SQL Server)
  
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 의 기존 AlwaysOn 가용성 그룹 관리에는 다음 태스크 중 하나 이상이 포함됩니다.  
  
-   기존 가용성 그룹 복제본의 속성 변경(예: 읽기 가능한 보조 복제본 구성을 위한 클라이언트 연결 액세스 변경용), 장애 조치(failover) 모드, 가용성 모드 또는 세션 제한 시간 설정 변경  
  
-   보조 복제본 추가 또는 제거  
  
-   데이터베이스 추가 또는 제거  
  
-   데이터베이스 일시 중단 또는 다시 시작  
  
-   계획된 수동 장애 조치(failover)( *수동 장애 조치(failover)*) 또는 강제 수동 장애 조치(failover)( *강제 장애 조치(failover)*) 수행  
  
-   가용성 그룹 수신기 만들기 또는 구성  
  
-   지정된 가용성 그룹에 대한 [읽기 가능한 보조 복제본](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) 관리 이 태스크에는 보조 역할로 실행하고 읽기 전용 라우팅을 구성할 때 읽기 전용으로 액세스할 하나 이상의 복제본을 구성하는 태스크가 포함됩니다.  
  
-   지정된 가용성 그룹에 대한 [보조 복제본에서의 백업](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) 관리. 이 태스크에는 백업 작업을 실행할 기본 위치를 구성한 다음 백업 작업을 스크립팅하여 백업 기본 설정을 구현하는 태스크가 포함됩니다. 가용성 복제본을 호스팅하는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 가용성 그룹의 모든 데이터베이스에 대한 백업 작업을 스크립팅해야 합니다.  
  
-   가용성 그룹 삭제  
  
-   OS 업그레이드를 위한 AlwaysOn 가용성 그룹의 클러스터 간 마이그레이션  
  
  
##  <a name="RelatedTasks"></a>관련 태스크  
 **기존 가용성 그룹을 구성 하려면**  
  
-   [가용성 그룹 &#40;SQL Server에 보조 복제본을 추가&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본을 제거 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 데이터베이스 추가 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [가용성 그룹에서 보조 데이터베이스를 제거 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 &#40;SQL Server에서 주 데이터베이스를 제거&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [유연한 장애 조치 (failover) 정책을 구성 하 여 자동 장애 조치 (Failover) &#40;AlwaysOn 가용성 그룹의 조건을 제어&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **가용성 그룹을 관리 하려면**  
  
-   [가용성 복제본에 대 한 백업 구성 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [가용성 그룹 &#40;SQL Server의 계획 된 수동 장애 조치 (Failover)를 수행&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치 (Failover)를 수행 하 여 SQL Server &#40;&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 &#40;SQL Server 제거&#41;](remove-an-availability-group-sql-server.md)  
  
 **가용성 복제본을 관리 하려면**  
  
-   [가용성 그룹 &#40;SQL Server에 보조 복제본을 추가&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [보조 복제본을 가용성 그룹 &#40;SQL Server에 조인&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본을 제거 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [가용성 복제본의 가용성 모드를 변경 &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치 (Failover) 모드를 변경 하 여 SQL Server &#40;&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본에 대 한 백업 구성 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [SQL Server&#41;&#40;가용성 복제본에 대 한 읽기 전용 액세스를 구성 합니다.](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대 한 읽기 전용 라우팅 구성 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대 한 세션 제한 시간을 변경 하 &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **가용성 데이터베이스를 관리 하려면**  
  
-   [가용성 그룹에 데이터베이스 추가 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [보조 데이터베이스를 가용성 그룹 &#40;SQL Server에 조인&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 &#40;SQL Server에서 주 데이터베이스를 제거&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 데이터베이스를 제거 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [가용성 데이터베이스 &#40;SQL Server 일시 중단&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [SQL Server&#41;&#40;가용성 데이터베이스를 다시 시작 합니다.](resume-an-availability-database-sql-server.md)  
  
 **가용성 그룹을 모니터링 하려면**  
  
-   [가용성 그룹 &#40;모니터링 SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
 **새 WSFC 클러스터로 가용성 그룹 마이그레이션 (클러스터 간 마이그레이션)을 지원 하려면**  
  
-   [서버 인스턴스의 HADR 클러스터 컨텍스트를 변경 하 &#40;SQL Server&#41;](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [가용성 그룹을 오프 라인 상태로 전환 &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="RelatedContent"></a>관련 내용  
  
-   **블로그**  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **비디오**  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 1부: 차세대 고가용성 솔루션 소개](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 파트 2: AlwaysOn을 사용하여 중요 환경 고가용성 솔루션 빌드](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [SQL Server 2012에 대 한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 서버 인스턴스 구성&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [SQL Server&#41;&#40;가용성 그룹 만들기 및 구성](creation-and-configuration-of-availability-groups-sql-server.md)   
 [활성 보조: 읽기 가능한 보조 복제본 &#40;AlwaysOn 가용성 그룹&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [활성 보조: 보조 복제본에 대 한 백업 &#40;AlwaysOn 가용성 그룹&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치 (Failover) &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server의 운영 문제에 대 한 AlwaysOn 정책&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [가용성 그룹 &#40;모니터링 SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹: &#40;SQL Server 상호 운용성&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 Transact-sql 문 개요&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 PowerShell Cmdlet 개요&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
