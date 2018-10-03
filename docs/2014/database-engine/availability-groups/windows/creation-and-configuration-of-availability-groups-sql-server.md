---
title: 가용성 그룹 만들기 및 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 60cff891ed49fcc97238d77a43a5155d2042b05c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149823"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>가용성 그룹의 생성 및 구성(SQL Server)
  이 섹션의 항목에서는 단일 WSFC 장애 조치(Failover) 클러스터 내의 여러 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스에 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 구현을 배포하는 방법에 대해 설명합니다.  
  
 첫 번째 가용성 그룹을 만들기 전에 다음 항목의 정보를 숙지하는 것이 좋습니다.  
  
 [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 이 항목에서는 컴퓨터의 사전 요구 사항, 제한 사항 및 권장 사항과 WSFC 노드, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스, 가용성 그룹, 복제본 및 데이터베이스에 대해 설명합니다. 이 항목에는 보안 고려 사항에 대한 정보도 포함되어 있습니다.  
  
 [AlwaysOn 가용성 그룹 시작 &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 서버 인스턴스 구성, 가용성 그룹 만들기, 클라이언트 연결을 위한 가용성 그룹 구성, 가용성 그룹 관리 및 가용성 그룹 모니터링 단계에 대한 정보를 포함합니다.  
  
 
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **다음에 대한 서버 인스턴스를 구성하려면 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [데이터베이스 미러링 끝점의 AlwaysOn 가용성 그룹 만들기 &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&amp;#40;Transact-SQL&amp;#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&amp;#40;Transact-SQL&amp;#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **AlwaysOn 가용성 그룹 구성을 시작 하려면**  
  
-   [AlwaysOn 가용성 그룹 시작 &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **새 가용성 그룹을 만들고 구성하려면**  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&amp;#40;SQL Server&amp;#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [자동 장애 조치 (AlwaysOn 가용성 그룹)에 대 한 상태 제어 유연한 장애 조치 정책 구성](configure-flexible-automatic-failover-policy.md)  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [AlwaysOn 보조 데이터베이스에서 데이터 이동 시작 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리&#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **문제를 해결하려면**  
  
-   [AlwaysOn 가용성 그룹 구성 문제 해결 (SQL Server) 삭제](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [실패 한 파일 추가 작업 문제 해결 &#40;AlwaysOn 가용성 그룹&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [AlwaysON-HADRON 학습 시리즈: HADRON 작업자 풀 사용 가능 데이터베이스](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](http://blogs.msdn.com/b/psssql/)  
  
-   **비디오:**  
  
     [Microsoft SQL Server 코드 이름된 "Denali" AlwaysOn 시리즈, 1 부: 차세대 고가용성 솔루션 소개](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름된 "Denali" AlwaysOn 시리즈, 파트 2: AlwaysOn을 사용 하 여 중요 업무용 고가용성 솔루션 빌드](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [Microsoft SQL Server AlwaysOn 솔루션 가이드 고가용성 및 재해 복구](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대한 Microsoft 백서](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 관리&#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [AlwaysOn 가용성 그룹 (SQL Server)를 사용 하 여 운영 문제에 대 한 AlwaysOn 정책](always-on-policies-for-operational-issues-always-on-availability.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹: 상호 운용성 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
  
