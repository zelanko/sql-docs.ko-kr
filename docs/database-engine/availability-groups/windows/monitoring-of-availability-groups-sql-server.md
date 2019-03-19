---
title: 가용성 그룹을 모니터링하는 도구
description: 'Always On 가용성 그룹의 성능 및 상태를 모니터링하는 데 사용할 수 있는 다양한 도구에 대한 참조입니다. '
ms.custom: seodec18
ms.date: 06/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0cf0478f63ab98bda9bf13a7cc5bad0f98bd1795
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973122"
---
# <a name="tools-to-monitor-always-on-availability-groups"></a>"Always On 가용성 그룹을 모니터링하는 도구"
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 가용성 그룹의 속성 및 상태를 모니터링하려면 다음 도구를 사용할 수 있습니다.  
  
|도구|간단한 설명|링크|  
|----------|-----------------------|-----------|  
|SQL Server용 System Center 모니터링 팩|SQL Server용 모니터링 팩(SQLMP)은 가용성 그룹, 가용성 복제본 및 IT 관리자의 가용성 데이터베이스를 모니터링하기 위한 권장 솔루션입니다. 특히 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 과 관련된 모니터링 기능은 다음과 같습니다.<br /><br /> 수백 개 컴퓨터 간의 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스의 자동 검색 기능 이 기능을 사용하면 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인벤토리를 쉽게 추적할 수 있습니다.<br /><br /> 완전한 기능의 System Center Operations Manager(SCOM) 경고 및 티켓 부여. 이러한 기능은 보다 빠른 문제 해결을 위한 세부 지식을 제공합니다.<br /><br /> PBM(정책 기반 관리)을 사용한 Always On 상태 모니터링에 대한 사용자 정의 확장.<br /><br /> 상태는 가용성 데이터베이스에서 가용성 복제본으로 롤업됩니다.<br /><br /> System Center 운영 관리자 콘솔로부터 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 관리하는 사용자 정의 작업.|모니터링 팩(SQLServerMP.msi) 및 *System Center Operations Manager용 SQL Server 관리 팩 가이드* (SQLServerMPGuide.doc)를 다운로드하려면 다음을 참조하세요.<br /><br /> [SQL Server용 System Center 모니터링 팩](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 카탈로그 및 동적 관리 뷰는 가용성 그룹과 해당 복제본, 데이터베이스, 수신기 및 WSFC 클러스터 환경에 대한 풍부한 정보를 제공합니다.|[가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**개체 탐색기 정보** 창에는 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 호스팅된 가용성 그룹에 대한 기본 정보가 표시됩니다.<br /><br /> **\*\* 팁 \*\*** 이 창을 사용하여 여러 가용성 그룹, 복제본 또는 데이터베이스를 선택하고 선택한 개체에 대한 일상적인 관리 태스크를 수행합니다(예: 가용성 그룹에서 여러 가용성 복제본 또는 데이터베이스 제거).|[개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**속성** 대화 상자에서는 가용성 그룹, 복제본 또는 수신기의 속성을 보고 필요한 경우 해당 값을 변경할 수 있습니다.|-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)<br />-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)<br />-   [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)|  
|시스템 모니터|**SQLServer:Availability Replica** 성능 개체에는 가용성 복제본에 대한 정보를 보고하는 성능 카운터가 포함됩니다.|[SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|시스템 모니터|**SQLServer:Database Replica** 성능 개체에는 지정된 보조 복제본의 보조 데이터베이스에 대한 정보를 보고하는 성능 카운터가 포함됩니다.<br /><br /> SQL Server의 **SQLServer:Databases** 개체에는 특히 트랜잭션 로그 작업을 모니터링하는 성능 카운터가 포함됩니다. 가용성 데이터베이스에서 트랜잭션 로그 작업 모니터링과 관련된 카운터는 **Log Flush Write Time (ms)**, **Log Flushes/sec**, **Log Pool Cache Misses/sec**, **Log Pool Disk Reads/sec** 및 **Log Pool Requests/sec** 카운터를 사용합니다.|[SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md) 및 [SQL Server, Databases 개체](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [Always On 상태 모델 파트 1 -- 상태 모델 아키텍처](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/08/the-alwayson-health-model-part-1-health-model-architecture/)  
  
     [Always On 상태 모델 파트 2 -- 상태 모델 확장](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/)  
  
     [PowerShell을 사용하여 Always On 상태 모니터링 - 1부: 기본 Cmdlet 개요](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
     [PowerShell을 사용하여 Always On 상태 모니터링 - 2부: 고급 Cmdlet 사용](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
     [PowerShell을 사용하여 Always On 상태 모니터링 - 3부: 간단한 모니터링 애플리케이션](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
     [PowerShell을 사용하여 Always On 상태 모니터링 - 4부: SQL Server 에이전트와의 통합](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.microsoft.com/psssql/)  
  
-   **백서:**  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Always On 가용성 그룹 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치(Failover) 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [자동 페이지 복구&#40;가용성 그룹: 데이터베이스 미러링&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
