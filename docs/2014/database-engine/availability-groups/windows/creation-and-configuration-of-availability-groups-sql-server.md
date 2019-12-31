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
ms.openlocfilehash: c9858638287876d31733035d1a6bb6d95705708f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228715"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>가용성 그룹의 생성 및 구성(SQL Server)
  이 섹션의 항목에서는 단일 WSFC 장애 조치(Failover) 클러스터 내의 여러 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스에 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 구현을 배포하는 방법에 대해 설명합니다.  
  
 첫 번째 가용성 그룹을 만들기 전에 다음 항목의 정보를 숙지하는 것이 좋습니다.  
  
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 필수 조건, 제한 사항 및 권장 사항&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 이 항목에서는 컴퓨터의 사전 요구 사항, 제한 사항 및 권장 사항과 WSFC 노드, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스, 가용성 그룹, 복제본 및 데이터베이스에 대해 설명합니다. 이 항목에는 보안 고려 사항에 대한 정보도 포함되어 있습니다.  
  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 시작 하기&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 서버 인스턴스 구성, 가용성 그룹 만들기, 클라이언트 연결을 위한 가용성 그룹 구성, 가용성 그룹 관리 및 가용성 그룹 모니터링 단계에 대한 정보를 포함합니다.  
  
 
  
##  <a name="RelatedTasks"></a>관련 태스크  
 **에 대 한 서버 인스턴스를 구성 하려면[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server 사용 및 사용 안 함&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server PowerShell에 대 한 데이터베이스 미러링 끝점을 만듭니다&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Transact-sql&#41;&#40;Windows 인증에 대 한 데이터베이스 미러링 끝점 만들기](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;데이터베이스 미러링 끝점의 아웃 바운드 연결에 대 한 인증서 사용 허용](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **AlwaysOn 가용성 그룹 구성을 시작하려면**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server 시작 하기&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **새 가용성 그룹을 만들고 구성 하려면**  
  
-   [가용성 그룹 마법사를 사용 하 여 SQL Server Management Studio &#40;&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Transact-sql&#41;&#40;가용성 그룹 만들기](create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 &#40;SQL Server PowerShell를 만듭니다&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [새 가용성 그룹 대화 상자를 사용 하 여 SQL Server Management Studio &#40;&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 복제본 &#40;SQL Server를 추가 하거나 수정할 때 끝점 URL을 지정&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [SQL Server&#41;&#40;가용성 그룹 수신기 만들기 또는 구성](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치의 상태 제어(AlwaysOn 가용성 그룹)](configure-flexible-automatic-failover-policy.md)  
  
-   [가용성 복제본에 대 한 백업 구성 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [SQL Server&#41;&#40;가용성 복제본에 대 한 읽기 전용 액세스를 구성 합니다.](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대 한 읽기 전용 라우팅 구성 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [보조 복제본을 가용성 그룹 &#40;SQL Server에 조인&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [AlwaysOn 보조 데이터베이스에서 데이터 이동을 시작 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [가용성 그룹에 대 한 보조 데이터베이스를 수동으로 준비 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [보조 데이터베이스를 가용성 그룹 &#40;SQL Server에 조인&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 데이터베이스에 대 한 로그인 및 작업 관리 SQL Server &#40;&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **문제를 해결 하려면**  
  
-   [삭제 된 SQL Server (AlwaysOn 가용성 그룹 구성) 문제 해결](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [실패 한 파일 추가 작업 문제 해결 AlwaysOn 가용성 그룹 &#40;&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a>관련 내용  
  
-   **블로그**  
  
     [AlwaysON - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **비디오**  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 1부: 차세대 고가용성 솔루션 소개](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 파트 2: AlwaysOn을 사용하여 중요 환경 고가용성 솔루션 빌드](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대 한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 관리 &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [AlwaysOn 가용성 그룹의 작업 문제에 대 한 AlwaysOn 정책 (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)   
 [가용성 그룹 &#40;모니터링 SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹: 상호 운용성(SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
