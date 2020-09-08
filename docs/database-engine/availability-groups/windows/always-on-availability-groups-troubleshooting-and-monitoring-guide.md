---
title: 가용성 그룹 모니터링 및 문제 해결 가이드
description: Always On 가용성 그룹에 있는 몇 가지 일반적인 문제를 모니터링하고 해결하는 데 도움이 되는 콘텐츠의 인덱스입니다.
ms.custom: seo-lt-2019
ms.date: 05/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 8d6d9954-ff6b-4e58-882e-eff0174f0d07
author: rothja
ms.author: jroth
ms.openlocfilehash: 096e416b5abaf7e6c148cba469cd4f7453be092e
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480488"
---
# <a name="monitor-and-troubleshoot-availability-groups"></a>가용성 그룹 모니터링 및 문제 해결
 이 가이드에서는 Always On 가용성 그룹 모니터링 및 가용성 그룹의 일반적인 문제 중 일부의 문제 해결을 시작하도록 돕습니다. 원래 콘텐츠 뿐만 아니라 다른 곳에서 게시된 유용한 정보의 방문 페이지를 제공합니다. 이 가이드는 가용성 그룹의 넓은 영역에서 발생할 수 있는 모든 문제를 완벽하게 논의할 수 없지만 근본 원인 분석 및 문제 해결의 올바른 방향을 안내할 수 있습니다. 
 
 가용성 그룹은 통합된 기술이기 때문에 발생하는 많은 문제는 데이터베이스 시스템에서 다른 문제의 증상일 수 있습니다. 몇 가지 문제는 일시 중지되는 가용성 데이터베이스와 같은 가용성 그룹 내의 설정에 의해 발생합니다. 다른 문제는 SQL Server 설정, 데이터베이스 파일 배포 및 사용 가능성에 관련되지 않은 시스템 성능 문제와 같은 다른 측면의 SQL Server 문제를 포함할 수 있습니다. 여전히 다른 문제가 네트워크 I/O, TCP/IP, Active Directory 및 WSFC(Windows Server 장애 조치(failover) 클러스터링) 문제와 같은 SQL Server 외부에 있을 수 있습니다. 종종 가용성 그룹, 복제본 또는 데이터베이스에서 발생하는 문제는 근본 원인을 파악하는 여러 기술을 해결하는 데 필요합니다.  
  
  
##  <a name="troubleshooting-scenarios"></a><a name="BKMK_SCENARIOS"></a> 문제 해결 시나리오  
 다음 표는 가용성 그룹에 대한 일반적인 문제 해결 시나리오에 대한 링크를 포함합니다. 구성, 클라이언트 연결, 장애 조치(failover) 및 성능과 같은 해당 시나리오 유형에 의해 분류되어 있습니다.  
  
|시나리오|시나리오 유형|Description|  
|--------------|-------------------|-----------------|  
|[Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)|구성|가용성 그룹에 대한 서버 인스턴스를 구성하는 것과 관련된 일반적인 문제를 해결하는 데 유용한 정보를 제공합니다. 가용성 그룹을 사용할 수 없거나, 계정이 잘못 구성되거나, 데이터베이스 미러링 엔드포인트가 없거나, 엔드포인트에 액세스할 수 없거나(SQL Server 오류 1418), 네트워크 액세스 권한이 없거나, 데이터베이스 조인 명령이 실패(SQL Server 오류 35250)하는 경우가 일반적인 구성 문제에 해당합니다.|  
|[실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|구성|파일 추가 작업으로 인해 보조 데이터베이스가 일시 중단되고 NOT SYNCHRONIZING 상태가 되었습니다.|  
|[다중 서브넷 환경에서 가용성 그룹 수신기에 연결할 수 없음](https://support.microsoft.com/kb/2792139/en-us)|클라이언트 연결|가용성 그룹 수신기를 구성한 후 수신기를 ping하거나 애플리케이션에서 연결할 수 없습니다.|  
|[실패 자동 장애 조치(failover) 문제 해결](https://support.microsoft.com/kb/2833707)|장애 조치|자동 장애 조치(failover)가 성공적으로 완료되지 않았습니다.|  
|[문제 해결: 가용성 그룹 초과 RTO](troubleshoot-availability-group-exceeded-rto.md)|성능|데이터 손실 없이 자동 장애 조치(failover) 또는 계획된 수동 장애 조치 후 장애 조치 시간이 RTO를 초과합니다. 또는 동기 커밋 보조 복제본(예: 자동 장애 조치(failover) 파트너)의 장애 조치 시간을 예측할 때 RTO 초과를 발견할 수 있습니다.|  
|[문제 해결: 가용성 그룹 초과 RPO](troubleshoot-availability-group-exceeded-rpo.md)|성능|강제 수동 장애 조치(failover)를 수행한 후 데이터 손실이 RPO보다 많습니다. 또는 비동기 커밋 보조 복제본의 잠재적 데이터 손실을 계산할 때 RPO 초과를 발견합니다.|  
|[문제 해결: 보조 복제본에 반영되지 않은 주 복제본의 변경 내용](troubleshoot-primary-changes-not-reflected-on-secondary.md)|성능|클라이언트 애플리케이션에서 주 복제본에 대한 업데이트를 성공적으로 완료하지만 보조 복제본 쿼리는 변경 내용이 반영되지 않았음을 보여줍니다.|  
|[문제 해결: Always On 가용성 그룹을 사용하여 높은 HADR_SYNC_COMMIT 대기 유형](https://blogs.msdn.microsoft.com/sql_server_team/troubleshooting-high-hadr_sync_commit-wait-type-with-always-on-availability-groups/)|성능|HADR_SYNC_COMMIT가 비정상적으로 긴 경우 데이터 이동 흐름 또는 보조 복제본 로그 강화에 성능 문제가 있습니다.|  

##  <a name="useful-tools-for-troubleshooting"></a><a name="BKMK_TOOLS"></a> 문제 해결에 유용한 도구  
 가용성 그룹을 구성 또는 실행하는 경우 다양한 도구는 서로 다른 유형의 문제를 진단하는 데 유용합니다. 다음 표에서 도구에 대한 유용한 정보에 대한 링크를 제공합니다.  
  
|도구|Description|  
|----------|-----------------|  
|[Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)|알기 쉬운 인터페이스에서 한 눈에 보이는 가용성 그룹의 상태 보기를 보고합니다.|  
|[Always On 정책](always-on-policies.md)|Always On 대시보드에서 사용합니다.|  
|[SQL Server 오류 로그&#40;Always On 가용성 그룹&#41;](sql-server-error-log-always-on-availability-groups.md)|가용성 그룹, 복제본 및 데이터베이스에 대한 로그 상태 전환 이벤트, 다른 Always On 구성 요소의 상태 및 Always On 오류|  
|[CLUSTER.LOG&#40;Always On 가용성 그룹&#41;](cluster-log-always-on-availability-groups.md)|가용성 그룹 리소스의 상태 전환을 포함하는 로그 클러스터 이벤트와 SQL Server 리소스 DLL의 이벤트 및 오류|  
|[Always On 상태 진단 로그](always-on-health-diagnostics-log.md)|[sp_server_diagnostics에서 WSFC 클러스터(SQL Server resource DLL)로 보고되는 로그 SQL Server 상태&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)|  
|[동적 관리 뷰 및 시스템 카탈로그 뷰&#40;Always On 가용성 그룹&#41;](dynamic-management-views-and-system-catalog-views-always-on-availability-groups.md)|구성, 성능 상태 및 성능 메트릭과 같은 가용성 그룹에 대한 정보를 보고합니다.|  
|[Always On 확장 이벤트](always-on-extended-events.md)|가용성 그룹의 자세한 진단을 제공하고 근본 원인 분석에 유용합니다.|  
|[Always On 대기 유형](always-on-wait-types.md)|가용성 그룹에 대한 대기 유형을 제공하고 성능 조정에 유용합니다.|  
|Always On 성능 카운터|가용성 그룹 작업 모니터링은 시스템 모니터에 반영되고 성능 튜닝에 유용합니다. 자세한 내용은 [SQL Server, 가용성 복제본](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 및 [SQL Server, 데이터베이스 복제본](~/relational-databases/performance-monitor/sql-server-database-replica.md)을 참조하세요.|  
|[Always On 링 버퍼](always-on-ring-buffers.md)|내부 진단에 대해 SQL Server 시스템 내에서 경고를 기록하고 가용성 그룹과 관련된 문제를 디버깅하는 데 사용할 수 있습니다.|  
  
##  <a name="monitoring-availability-groups"></a><a name="BKMK_MONITOR"></a> 가용성 그룹 모니터링  
 가용성 그룹의 문제를 해결하는 이상적인 시간은 문제가 자동 또는 수동인지 장애 조치(failover)가 필요하기 전입니다. 이는 가용성 그룹의 성능 메트릭을 모니터링하고 가용성 복제본이 SLA(서비스 수준 계약) 경계 밖에서 수행되는 경우 경고를 보내 수행할 수 있습니다. 예를 들어 동기 보조 복제본에 예상된 장애 조치(failover) 시간을 증가시키는 성능 문제가 있는 경우 자동 장애 조치(failover)가 발생하고 장애 조치(failover) 시간이 복구 시간 목표를 초과하는 것을 발견할 때까지 기다리지 않으려 합니다.  
  
 가용성 그룹은 고가용성 및 재해 복구 솔루션이므로 모니터링하는 가장 중요한 성능 메트릭은 RTO(복구 시간 목표)에 영향을 주는 예상된 장애 조치(failover) 시간 및 RPO(복구 지점 목표)에 영향을 주는 재해의 잠재적 데이터 손실입니다. SQL Server에서 지정된 시간에 노출하는 데이터에서 이러한 메트릭을 수집할 수 있으므로 실제 오류 이벤트가 발생하기 전에 시스템의 HADR(고가용성 및 재해 복구) 기능에서 문제의 경고를 받을 수 있습니다. 따라서 가용성 그룹의 데이터 동기화 프로세스를 숙지하고 그에 따라 메트릭을 수집하는 것이 중요합니다.  
  
 이 아래 표는 가용성 그룹 솔루션의 상태를 모니터링하는 데 도움이 될 수 있는 항목으로 안내합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[Always On 가용성 그룹에 대한 성능 모니터링](monitor-performance-for-always-on-availability-groups.md)|가용성 그룹에 대한 데이터 동기화 프로세스, 흐름 제어 게이트 및 가용성 그룹을 모니터링할 때 유용한 메트릭을 설명하고 RTO 및 RPO 메트릭을 수집하는 방법을 보여줍니다.|  
|[가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)|가용성 그룹 모니터링을 위한 도구의 정보를 제공합니다.|  
|[Always On 상태 모델, 파트 1: 상태 모델 아키텍처](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-1-health-model-architecture)|Always On 상태 모델의 개요를 제공합니다.|  
|[Always On 상태 모델, 파트 2: 상태 모델 확장](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)|Always On 상태 모델을 사용자 지정하고 Always On 대시보드를 사용자 지정하여 추가 정보를 표시하는 방법을 보여줍니다.|  
|[PowerShell을 사용하여 Always On 상태 모니터링, 1부: 기본 cmdlet 개요](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview)|가용성 그룹의 상태를 모니터링하는 데 사용할 수 있는 Always On PowerShell cmdlet의 기본적인 개요를 제공합니다.|  
|[PowerShell을 사용하여 Always On 상태 모니터링, 2부: 고급 cmdlet 사용](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage)|가용성 그룹의 상태를 모니터링하는 Always On PowerShell cmdlet의 고급 사용에 대한 정보를 제공합니다.|  
|[PowerShell을 사용하여 Always On 상태 모니터링, 3부: 간단한 모니터링 애플리케이션](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application)|애플리케이션을 사용하여 가용성 그룹을 자동으로 모니터링하는 방법을 보여줍니다.|  
|[PowerShell을 사용하여 Always On 상태 모니터링, 4부: SQL Server 에이전트와의 통합](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent)|SQL Server 에이전트를 사용하여 가용성 그룹 모니터링을 통합하고 문제가 발생하는 경우 적절한 대상에 대한 알림을 구성하는 방법에 대한 정보를 제공합니다.|  

## <a name="next-steps"></a>다음 단계  
 [SQL Server Always On 팀 블로그](https://docs.microsoft.com/archive/blogs/sqlalwayson/)   
 [CSS SQL Server 엔지니어 블로그](https://docs.microsoft.com/archive/blogs/psssql/)  
  
  
