---
title: 가용성 그룹 모니터링(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 1793032a72ae1dd150caa5ddd1739f7f5620bce1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62790199"
---
# <a name="monitoring-of-availability-groups-sql-server"></a>가용성 그룹 모니터링(SQL Server)
  AlwaysOn 가용성 그룹의 속성 및 상태를 모니터링하려면 다음 도구를 사용할 수 있습니다.  
  
|도구|간단한 설명|링크|  
|----------|-----------------------|-----------|  
|SQL Server용 System Center 모니터링 팩|SQL Server용 모니터링 팩(SQLMP)은 가용성 그룹, 가용성 복제본 및 IT 관리자의 가용성 데이터베이스를 모니터링하기 위한 권장 솔루션입니다. 특히 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 과 관련된 모니터링 기능은 다음과 같습니다.<br /><br /> 수백 개 컴퓨터 간의 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스의 자동 검색 기능 이 기능을 사용하면 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인벤토리를 쉽게 추적할 수 있습니다.<br /><br /> 완전한 기능의 System Center Operations Manager(SCOM) 경고 및 티켓 부여. 이러한 기능은 보다 빠른 문제 해결을 위한 세부 지식을 제공합니다.<br /><br /> PBM(정책 기반 관리)을 사용한 AlwaysOn 상태 모니터링에 대한 사용자 정의 확장.<br /><br /> 상태는 가용성 데이터베이스에서 가용성 복제본으로 롤업됩니다.<br /><br /> System Center 운영 관리자 콘솔로부터 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 관리하는 사용자 정의 작업.|모니터링 팩(SQLServerMP.msi) 및 *System Center Operations Manager용 SQL Server 관리 팩 가이드* (SQLServerMPGuide.doc)를 다운로드하려면 다음을 참조하세요.<br /><br /> [SQL Server용 System Center 모니터링 팩](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 카탈로그 및 동적 관리 뷰는 가용성 그룹과 해당 복제본, 데이터베이스, 수신기 및 WSFC 클러스터 환경에 대한 풍부한 정보를 제공합니다.|[가용성 그룹 모니터링&#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**개체 탐색기 정보** 창에는 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 호스팅된 가용성 그룹에 대한 기본 정보가 표시됩니다.<br /><br /> 팁:  이 창을 사용 하 여 여러 가용성 그룹, 복제본 또는 데이터베이스를 선택 하 고 선택한 개체;에서 일상적인 관리 태스크 수행 예를 들어 가용성 그룹에서 여러 가용성 복제본 또는 데이터베이스를 제거 합니다.|[개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**속성** 대화 상자에서는 가용성 그룹, 복제본 또는 수신기의 속성을 보고 필요한 경우 해당 값을 변경할 수 있습니다.|[가용성 그룹 속성 보기&#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)<br /><br /> [가용성 복제본 속성 보기&#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)<br /><br /> [가용성 그룹 수신기 속성 보기&#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)|  
|시스템 모니터|**SQLServer:Availability Replica** 성능 개체에는 가용성 복제본에 대한 정보를 보고하는 성능 카운터가 포함됩니다.|[SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|시스템 모니터|**SQLServer:Database Replica** 성능 개체에는 지정된 보조 복제본의 보조 데이터베이스에 대한 정보를 보고하는 성능 카운터가 포함됩니다.<br /><br /> SQL Server의 **SQLServer:Databases** 개체에는 특히 트랜잭션 로그 작업을 모니터링하는 성능 카운터가 포함됩니다. 가용성 데이터베이스에서 트랜잭션 로그 작업 모니터링과 관련 된 다음 카운터 같습니다. **Log Flush Write Time (ms)** , **Log Flushes/sec**, **Log Pool Cache Misses/sec**, **Log Pool Disk Reads/sec** 및 **Log Pool Requests/sec** 카운터를 사용합니다.|[SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md) 및 [SQL Server, Databases 개체](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [AlwaysOn 상태 모델 파트 1--상태 모델 아키텍처](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx)  
  
     [AlwaysOn 상태 모델 파트 2--상태 모델 확장](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
     [PowerShell-1 부를 사용 하 여 AlwaysOn 상태 모니터링: 기본 Cmdlet 개요](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)  
  
     [PowerShell-2 부를 사용 하 여 AlwaysOn 상태 모니터링: 고급 Cmdlet 사용](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)  
  
     [PowerShell-3 부를 사용 하 여 AlwaysOn 상태 모니터링: 간단한 모니터링 애플리케이션](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)  
  
     [PowerShell-4 부를 사용 하 여 AlwaysOn 상태 모니터링: SQL Server 에이전트와의 통합](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **백서:**  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql)   
 [AlwaysOn 가용성 그룹 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions)   
 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치 정책&#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)   
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [자동 페이지 복구 &#40;가용성 그룹 및 데이터베이스 미러링&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
