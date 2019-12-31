---
title: SQL Server (Always On 가용성 그룹)에 대 한 서버 인스턴스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3dcd239c782f53ec11970e94f89e5acfac982785
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228810"
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹에 대한 서버 인스턴스 구성(SQL Server)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 를 지원할 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]인스턴스 구성 요구 사항에 대한 정보를 제공합니다.  
  
> [!IMPORTANT]  
>  WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 필수 조건 및 제한 사항에 대한 자세한 내용은 [AlwaysOn 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
 
  
##  <a name="TermsAndDefinitions"></a>용어 및 정의  
  
 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. *가용성 그룹* 은 함께 장애 조치 (failover) 되는 사용자 데이터베이스의 불연속 집합 ( *가용성 데이터베이스*라고 함)에 대 한 장애 조치 (failover) 환경을 지원 합니다.  
  
 가용성 복제본  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 관리하는 가용성 그룹 인스턴스화입니다. 가용성 복제본에는 *주 복제본* 과 1-4개의 *보조 복제본*이라는 두 가지 유형이 있습니다. 지정된 가용성 그룹에 대한 가용성 복제본을 호스팅하는 서버 인스턴스는 단일 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 다른 노드에 있어야 합니다.  
  
 [데이터베이스 미러링 끝점](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 SQL Server는 SQL Server 개체인 엔드포인트를 사용하여 네트워크를 통해 통신할 수 있습니다. 데이터베이스 미러링 및/또는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 참여하려면 서버 인스턴스에 특수 전용 엔드포인트가 필요합니다. 서버 인스턴스의 모든 미러링 및 가용성 그룹 연결은 동일한 데이터베이스 미러링 엔드포인트를 사용합니다. 데이터베이스 미러링 엔드포인트는 다른 서버 인스턴스로부터 이러한 연결을 받는 데만 사용되는 특별한 용도의 엔드포인트입니다.  
  
##  <a name="ConfigSI"></a>AlwaysOn 가용성 그룹을 지원 하도록 서버 인스턴스를 구성 하려면  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하려면 서버 인스턴스가 가용성 그룹을 호스팅하는 WSFC 장애 조치(Failover) 클러스터의 노드에 있어야 하고, [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]이 설정되어 있어야 하며, 데이터베이스 미러링 엔드포인트를 보유하고 있어야 합니다.  
  
1.  하나 이상의 가용성 그룹에 참여할 모든 서버 인스턴스에서 AlwaysOn 가용성 그룹 기능을 사용하도록 설정합니다. 특정 서버 인스턴스에서는 특정 가용성 그룹에 대한 단일 가용성 복제본만 호스팅할 수 있습니다.  
  
2.  서버 인스턴스에 데이터베이스 미러링 엔드포인트가 있는지 확인합니다.  
  
##  <a name="RelatedTasks"></a>관련 태스크  
 **AlwaysOn 가용성 그룹을 사용하도록 설정하려면**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server 사용 및 사용 안 함&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **데이터베이스 미러링 끝점이 있는지 여부를 확인 하려면**  
  
-   [database_mirroring_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **데이터베이스 미러링 끝점을 만들려면**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server PowerShell에 대 한 데이터베이스 미러링 끝점을 만듭니다&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Transact-sql&#41;&#40;Windows 인증에 대 한 데이터베이스 미러링 끝점 만들기](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;데이터베이스 미러링 끝점의 아웃 바운드 연결에 대 한 인증서 사용 허용](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
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
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 필수 조건, 제한 사항 및 권장 사항&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [데이터베이스 미러링 끝점은 SQL Server을 &#40;&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 가용성 그룹: 상호 운용성 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [장애 조치 (Failover) 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [WSFC&#41;를 사용 하 여 Windows Server 장애 조치 (Failover) 클러스터링 &#40;SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [AlwaysOn 장애 조치 (Failover) 클러스터 인스턴스](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
