---
title: 'Always On 가용성 그룹: 상호 운용성(SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8df86f981a6c9f77a474a5f381117d549aab6590
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Always On 가용성 그룹: 상호 운용성(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 다른 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]기능과의 상호 운용성에 대해 설명합니다.  
  
##  <a name="Interop"></a> Always On 가용성 그룹과 상호 운용하는 기능  
 다음 표에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 과 상호 운용하는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]기능이 나와 있습니다. **추가 정보** 열의 링크는 해당 기능에 대해 상호 운용성 고려 사항이 있음을 나타냅니다.  
  
|기능|추가 정보|  
|-------------|----------------------|  
|변경 데이터 캡처|[복제, 변경 내용 추적, 변경 데이터 캡처 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|변경 내용 추적|[복제, 변경 내용 추적, 변경 데이터 캡처 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|포함된 데이터베이스|[Always On 가용성 그룹에 포함된 데이터베이스&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|  
|데이터베이스 암호화|[Always On 가용성 그룹이 있는 암호화된 데이터베이스&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|데이터베이스 스냅숏|[Always On 가용성 그룹이 있는 데이터베이스 스냅숏&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM 및 FileTable|[Always On 가용성 그룹의 FILESTREAM 및 FileTable&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|전체 텍스트 검색|참고: 전체 텍스트 인덱스는 Always On 보조 데이터베이스와 동기화됩니다.|  
|로그 전달|[로그 전달에서 Always On 가용성 그룹으로 마이그레이션하기 위한 필수 조건&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|RBS(Remote Blob Store)|[RBS&#40;Remote Blob Store&#41; 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|복제|[Always On 가용성 그룹에 대한 복제 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Always On 게시 데이터베이스 유지 관리&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [복제, 변경 내용 추적, 변경 데이터 캡처 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [복제 구독자 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Always On 가용성 그룹이 포함된 Analysis Services](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|읽기 전용 보조 복제본을 보고 데이터 원본으로 사용하고 주 읽기/쓰기 주 복제본에 대한 부하를 줄일 수 있습니다.<br /><br /> [Always On 가용성 그룹이 포함된 Reporting Services&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Service Broker|[Always On 가용성 그룹이 포함된 Service Broker&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server 에이전트||  
  
##  <a name="restrictions"></a> 제한 사항이 있는 Always On 가용성 그룹과 상호 운용하는 기능  
 다음 기능은 특정 제한 사항이 있는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 와(과) 상호 운용합니다. 자세한 내용은 연결된 항목을 참조하세요.  
  
-   데이터베이스 간 트랜잭션/분산 트랜잭션([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 및 Windows Server 2016) - 자세한 내용은 [Always On 가용성 그룹에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션과 데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)을 참조하세요.  
  
##  <a name="NoInterop"></a> Always On 가용성 그룹과 상호 운용하는 기능  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 다음 기능과 상호 운용되지 않습니다.  
  
-   데이터베이스 미러링. 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)를 참조하세요.  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [마이그레이션 가이드: 이전 클러스터링 및 미러링 배포에서 SQL Server 2012 장애 조치(Failover) 클러스터링 및 가용성 그룹으로 마이그레이션](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](http://blogs.msdn.com/b/psssql/)  
  
-   **백서:**  
  
     [마이그레이션 가이드: 데이터베이스 미러링 및 로그 전달을 조합하는 이전 배포에서 Always On 가용성 그룹으로 마이그레이션](http://msdn.microsoft.com/library/jj635217)  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대한 Microsoft 백서](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
