---
title: "Always On 가용성 그룹에 대한 SQL Server 인스턴스 구성(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
caps.latest.revision: "18"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c340172f3eb35155c4760567ae424392de595e42
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹에 대한 서버 인스턴스 구성(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 지원할 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 인스턴스 구성 요구 사항에 대한 정보를 제공합니다.  
  
> [!IMPORTANT]  
>  WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]필수 구성 사항 및 제한 사항에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
 **항목 내용**  
  
-   [용어 및 정의](#TermsAndDefinitions)  
  
-   [Always On 가용성 그룹을 지원하도록 서버 인스턴스를 구성하려면](#ConfigSI)  
  
-   [관련 태스크](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="TermsAndDefinitions"></a> 용어 및 정의  
 [Always On 가용성 그룹](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. *가용성 그룹* 은 함께 장애 조치(Failover)되는 사용자 데이터베이스( *가용성 데이터베이스*라고 함)의 불연속 집합에 대한 장애 조치(Failover) 환경을 지원합니다.  
  
 가용성 복제본  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 관리하는 가용성 그룹 인스턴스화입니다. 가용성 복제본에는 *주 복제본* 과 1-4개의 *보조 복제본*이라는 두 가지 유형이 있습니다. 지정된 가용성 그룹에 대한 가용성 복제본을 호스팅하는 서버 인스턴스는 단일 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 다른 노드에 있어야 합니다.  
  
 [데이터베이스 미러링 끝점](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 SQL Server는 SQL Server 개체인 끝점을 사용하여 네트워크를 통해 통신할 수 있습니다. 데이터베이스 미러링 및/또는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에 참여하려면 서버 인스턴스에 특수 전용 끝점이 필요합니다. 서버 인스턴스의 모든 미러링 및 가용성 그룹 연결은 동일한 데이터베이스 미러링 끝점을 사용합니다. 데이터베이스 미러링 끝점은 다른 서버 인스턴스로부터 이러한 연결을 받는 데만 사용되는 특별한 용도의 끝점입니다.  
  
##  <a name="ConfigSI"></a> Always On 가용성 그룹을 지원하도록 서버 인스턴스를 구성하려면  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하려면 서버 인스턴스가 가용성 그룹을 호스팅하는 WSFC 장애 조치(Failover) 클러스터의 노드에 있어야 하고, [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 이 설정되어 있어야 하며, 데이터베이스 미러링 끝점을 보유하고 있어야 합니다.  
  
1.  하나 이상의 가용성 그룹에 참여할 모든 서버 인스턴스에서 Always On 가용성 그룹 기능을 사용하도록 설정합니다. 특정 서버 인스턴스에서는 특정 가용성 그룹에 대한 단일 가용성 복제본만 호스팅할 수 있습니다.  
  
2.  서버 인스턴스에 데이터베이스 미러링 끝점이 있는지 확인합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **Always On 가용성 그룹을 사용하도록 설정하려면**  
  
-   [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **데이터베이스 미러링 끝점이 있는지 여부를 확인하려면**  
  
-   [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
 **데이터베이스 미러링 끝점을 만들려면**  
  
-   [Always On 가용성 그룹에 대한 데이터베이스 미러링 끝점 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 끝점의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [Always On - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](http://blogs.msdn.com/b/psssql/)  
  
-   **비디오:**  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 1부: 차세대 고가용성 솔루션 소개](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 2부: Always On을 사용하여 중요 업무용 고가용성 솔루션을 구축](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대한 Microsoft 백서](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Always On 가용성 그룹: 상호 운용성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
