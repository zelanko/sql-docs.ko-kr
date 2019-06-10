---
title: 데이터베이스 미러링 모니터링(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
ms.assetid: a7b1b9b0-7c19-4acc-9de3-3a7c5e70694d
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 5bb5ffaab7bf391a50dbfb28be14852a05e83582
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795351"
---
# <a name="monitoring-database-mirroring-sql-server"></a>데이터베이스 미러링 모니터링(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 섹션에서는 데이터베이스 미러링 모니터 및 **sp_dbmmonitor** 시스템 저장 프로시저를 소개하고 **데이터베이스 미러링 모니터 작업**을 포함하는 데이터베이스 미러링 모니터링의 작동 방법에 대해 설명하며 데이터베이스 미러링 세션에 대한 모니터링 정보를 간단하게 설명합니다. 또한 이 섹션에서는 미리 정의된 데이터베이스 미러링 이벤트 집합에 대해 경고 임계값을 정의하는 방법과 데이터베이스 미러링 이벤트에 대해 경고를 설정하는 방법을 소개합니다.  
  
 미러링 세션 중에 미러된 데이터베이스를 모니터링하여 데이터 흐름 여부와 상태를 확인할 수 있습니다. 서버 인스턴스에 있는 하나 이상의 미러된 데이터베이스에 대한 모니터링을 설정하고 관리하려면 데이터베이스 미러링 모니터나 **sp_dbmmonitor** 시스템 저장 프로시저를 사용합니다.  
  
 데이터베이스 미러링 모니터링 작업인 **데이터베이스 미러링 모니터 작업**은 데이터베이스 미러링 모니터와 별개로 백그라운드에서 작동합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 기본적으로 1분마다 **데이터베이스 미러링 모니터 작업** 을 호출하고 작업에서는 미러링 상태를 업데이트하는 저장 프로시저를 호출합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 미러링 세션을 시작하는 경우 **데이터베이스 미러링 모니터 작업** 은 자동으로 생성됩니다. 그러나 ALTER DATABASE *<database_name>* SET PARTNER만 사용하여 미러링을 시작할 경우에는 저장 프로시저를 실행하여 작업을 만들어야 합니다.  
  
 **항목 내용:**  
  
-   [미러링 상태 모니터링](#MonitoringStatus)  
  
-   [미러된 데이터베이스에 대한 추가 정보 원본](#AdditionalSources)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="MonitoringStatus"></a> 미러링 상태 모니터링  
 서버 인스턴스에 있는 하나 이상의 미러된 데이터베이스에 대한 모니터링을 설정하고 관리하려면 데이터베이스 미러링 모니터 서버 또는 **dbmmonitor** 시스템 저장 프로시저를 사용합니다. 미러링 세션 중에 미러된 데이터베이스를 모니터링하여 데이터 흐름 여부와 상태를 확인할 수 있습니다.  
  
 미러된 데이터베이스를 모니터링하면 구체적으로 다음 작업을 수행할 수 있습니다.  
  
-   미러링이 작동하는지 확인합니다.  
  
     기본 상태는 두 서버 인스턴스가 작동하는지, 서버가 연결되어 있는지, 주 서버에서 미러 서버로 로그가 이동하고 있는지를 표시합니다.  
  
-   미러 데이터베이스가 주 데이터베이스와 동기화되고 있는지 여부를 확인합니다.  
  
     성능 우선 모드에서 주 서버는 주 서버에서 미러 서버로 전송해야 하는 보내지 않은 로그 레코드의 백로그를 개발할 수 있습니다. 또한 모든 운영 모드에서 미러 서버는 로그 파일에 기록되었지만 미러 데이터베이스에서 복원해야 하는 복원되지 않은 로그 레코드의 백로그를 개발할 수 있습니다.  
  
-   성능 우선 모드에서 주 서버 인스턴스를 사용할 수 없는 경우 손실된 데이터 양을 확인합니다.  
  
     보내지 않은 트랜잭션 로그(있는 경우)의 양과 손실된 트랜잭션이 주 서버에서 커밋된 시간 간격을 살펴 보면 데이터 손실을 확인할 수 있습니다.  
  
-   현재 성능을 이전 성능과 비교합니다.  
  
     문제가 발생할 경우 데이터베이스 관리자는 미러링 성능 기록을 보고 현재 상태를 이해할 수 있습니다. 기록을 확인함으로써 사용자는 성능 추세를 검색하고 성능 문제의 패턴(예: 네트워크 속도가 느려지는 시간 또는 로그에 입력되는 명령 수가 매우 많은 시간)을 식별할 수 있습니다.  
  
-   미러링 파트너 간의 데이터 흐름 감소 원인을 찾아서 문제를 해결합니다.  
  
-   주요 성능 메트릭에 경고 임계값을 설정합니다.  
  
     새 상태 행에 포함된 값이 임계값을 초과하면 정보 이벤트가 Windows 이벤트 로그로 전송됩니다. 그러면 시스템 관리자가 수동으로 이러한 이벤트를 기반으로 경고를 구성할 수 있습니다. 자세한 내용은 [미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)을 참조하세요.  
  
###  <a name="tools_for_monitoring_dbm_status"></a> 데이터베이스 미러링 상태 모니터링 도구  
 데이터베이스 미러링 모니터나 **sp_dbmmonitorresults** 시스템 저장 프로시저를 사용하여 미러링 상태를 모니터링할 수 있습니다. 두 시스템 관리자, 즉 **sysadmin** 고정 서버 역할의 멤버와 시스템 관리자가 **msdb** 데이터베이스의 **dbm_monitor** 고정 데이터베이스 역할에 추가한 사용자는 모두 이러한 도구를 사용하여 로컬 서버 인스턴스의 모든 미러된 데이터베이스에서 데이터베이스 미러링을 모니터링할 수 있습니다. 이러한 도구를 사용할 때 시스템 관리자가 수동으로 미러링 상태를 새로 고칠 수도 있습니다.  
  
> [!NOTE]  
>  시스템 관리자는 주요 성능 메트릭에 대해 경고 임계값을 구성하고 볼 수도 있습니다. 자세한 내용은 [미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)을 참조하세요.  
  
-   데이터베이스 미러링 모니터  
  
     데이터베이스 미러링 모니터는 시스템 관리자가 상태를 보고 업데이트하며 여러 주요 성능 메트릭에 경고 임계값을 구성할 수 있도록 하는 그래픽 사용자 인터페이스 도구입니다. 또한 **dbm_monitor** 고정 데이터베이스 역할의 멤버는 상태 테이블을 업데이트할 수는 없지만 데이터베이스 미러링 모니터를 사용하여 미러링 상태 테이블의 가장 최근 행을 볼 수 있습니다.  
  
     모니터는 성능 메트릭을 비롯하여 **상태** 탭 페이지에서 선택한 데이터베이스에 대한 상태를 표시합니다. 이 페이지의 내용은 주 서버 인스턴스 및 미러 서버 인스턴스에서 가져옵니다. 주 서버 인스턴스와 미러 서버 인스턴스에 각각 연결하여 상태가 수집되므로 페이지는 비동기적으로 채워집니다. 모니터는 30초 간격으로 상태 테이블을 업데이트합니다. 테이블이 15초 내에 업데이트되지 않고 사용자가 **sysadmin** 고정 서버 역할의 멤버인 경우에만 업데이트에 성공합니다. **상태** 페이지에 표시되는 정보 요약은 이 항목의 뒷부분에 나오는 [데이터베이스 미러링 모니터에 표시되는 상태](#perf_metrics_of_dbm_monitor)를 참조하세요.  
  
     데이터베이스 미러링 모니터 인터페이스에 대한 개요는 [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md)를 참조하세요. 데이터베이스 미러링 모니터를 시작하는 방법은 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)을 참조하세요.  
  
-   시스템 저장 프로시저  
  
     **sp_dbmmonitorresults** 시스템 저장 프로시저를 실행하여 현재 상태를 검색하거나 업데이트할 수도 있습니다. 다른 dbmmonitor 저장 프로시저를 사용하여 서버 인스턴스에 대한 모니터링을 설정하고 모니터링 매개 변수를 변경하며 현재 업데이트 기간을 보고 모니터링을 삭제할 수 있습니다.  
  
     다음 표에서는 데이터베이스 미러링 모니터와 별도로 데이터베이스 미러링 모니터링을 관리하고 사용하기 위한 저장 프로시저를 설명합니다.  
  
    |절차|설명|  
    |---------------|-----------------|  
    |[sp_dbmmonitoraddmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)|서버 인스턴스의 모든 미러된 데이터베이스에 대한 상태 정보를 정기적으로 업데이트하는 작업을 만듭니다.|  
    |[sp_dbmmonitorchangemonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)|데이터베이스 미러링 모니터링 매개 변수의 값을 변경합니다.|  
    |[sp_dbmmonitorhelpmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)|현재 업데이트 기간을 반환합니다.|  
    |[sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)|모니터링한 데이터베이스에 대한 상태 행을 반환하고 프로시저에서 최신 상태를 미리 가져올지 여부를 선택할 수 있도록 합니다.|  
    |[sp_dbmmonitordropmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)|서버 인스턴스의 모든 데이터베이스에 대한 미러링 모니터 작업을 중지하고 삭제합니다.|  
  
     데이터베이스 미러링 모니터의 보조 기능으로 이 **dbmmonitor** 시스템 저장 프로시저를 사용할 수 있습니다. 예를 들어 **sp_dbmmonitoraddmonitoring**을 사용하여 모니터링이 구성된 경우 데이터베이스 미러링 모니터를 사용하여 상태를 볼 수 있습니다.  
  
### <a name="how-monitoring-works"></a>모니터링 작동 방법  
 이 섹션에서는 데이터베이스 미러링 상태 테이블, 데이터베이스 미러링 모니터 작업, 사용자가 데이터베이스 미러링 상태를 모니터링하는 방법, 모니터링 작업을 삭제하는 방법 등에 대해 설명합니다.  
  
#### <a name="database-mirroring-status-table"></a>데이터베이스 미러링 상태 테이블  
 데이터베이스 미러링 상태는 **msdb** 데이터베이스의 문서화되지 않은 내부 데이터베이스 미러링 상태 테이블에 저장됩니다. 이 상태 테이블은 서버 인스턴스에서 미러링 상태가 처음 업데이트될 때 자동으로 생성됩니다.  
  
 상태 테이블은 자동으로 업데이트되거나 시스템 관리자가 수동으로 업데이트할 수 있으며 최소 업데이트 간격은 15초입니다. 최소 간격인 15초는 서버 인스턴스가 상태 요청으로 오버로드되지 않도록 합니다.  
  
 상태 테이블은 데이터베이스 미러링 모니터와 데이터베이스 미러링 모니터 작업(실행 중인 경우)에 의해 자동으로 업데이트됩니다. **데이터베이스 미러링 모니터 작업** 은 기본적으로 1분마다 테이블을 업데이트합니다. 시스템 관리자는 1분에서 120분까지의 업데이트 기간을 지정할 수 있습니다. 반면 데이터베이스 미러링 모니터는 30초마다 자동으로 테이블을 업데이트합니다. 이러한 업데이트에 대해 **데이터베이스 미러링 모니터 작업** 과 데이터베이스 미러링 모니터는 **sp_dbmmonitorupdate**를 호출합니다.  
  
 **sp_dbmmonitorupdate** 는 처음 실행될 때 **msdb** 데이터베이스에 **데이터베이스 미러링 상태** 테이블과 **dbm_monitor** 고정 데이터베이스 역할을 만듭니다. **sp_dbmmonitorupdate** 는 일반적으로 서버 인스턴스의 모든 미러된 데이터베이스에 대한 상태 테이블에 새 행을 삽입하여 미러링 상태를 업데이트합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "데이터베이스 미러링 상태 테이블"을 참조하세요. 또한 이 프로시저는 새 행의 성능 메트릭을 평가하여 현재 보존 기간(기본값: 7일)보다 오래된 행을 자릅니다. 자세한 내용은 [sp_dbmmonitorupdate&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  **sysadmin** 고정 서버 역할의 멤버가 현재 데이터베이스 미러링 모니터를 사용하고 있지 않으면 **데이터베이스 미러링 모니터 작업** 이 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중인 경우에만 상태 테이블이 자동으로 업데이트됩니다.  
  
#### <a name="database-mirroring-monitor-job"></a>데이터베이스 미러링 모니터 작업  
 데이터베이스 미러링 모니터링 작업인 **데이터베이스 미러링 모니터 작업**은 데이터베이스 미러링 모니터와 독립적으로 작동합니다. **데이터베이스 미러링 모니터 작업** 은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 미러링 세션을 시작하는 경우에만 자동으로 생성됩니다. 항상 ALTER DATABASE *database_name* SET PARTNER 명령을 사용하여 미러링을 시작하면 시스템 관리자가 **sp_dbmmonitoraddmonitoring** 저장 프로시저를 실행하는 경우에만 작업이 있습니다.  
  
 **데이터베이스 미러링 모니터 작업** 이 생성되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중일 경우 기본적으로 1분마다 작업이 호출됩니다. 그런 다음 작업에서 **sp_dbmmonitorupdate** 시스템 저장 프로시저를 호출합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 기본적으로 1분마다 **데이터베이스 미러링 모니터 작업** 을 호출하고 작업에서 **sp_dbmmonitorupdate** 를 호출하여 상태 테이블을 업데이트합니다. 시스템 관리자는 **sp_dbmmonitorchangemonitoring** 시스템 저장 프로시저를 사용하여 업데이트 기간을 변경하고 **sp_dbmmonitorchangemonitoring** 시스템 저장 프로시저를 사용하여 현재 업데이트 기간을 볼 수 있습니다. 자세한 내용은 [sp_dbmmonitoraddmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md) 및 [sp_dbmmonitorchangemonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)을 참조하세요.  
  
#### <a name="monitoring-database-mirroring-status-by-system-administrators"></a>데이터베이스 미러링 상태 모니터링(시스템 관리자가 사용하는 경우)  
 **sysadmin** 고정 서버 역할의 멤버는 상태 테이블을 보고 업데이트할 수 있습니다.  
  
-   데이터베이스 미러링 모니터 사용  
  
     시스템 관리자는 데이터베이스 미러링 모니터를 사용할 때 수동으로 **상태** 페이지, 탐색 트리 또는 **기록** 페이지를 새로 고칠 수 있습니다. 이렇게 하면 이전 15초 내에 업데이트되지 않은 경우 상태 테이블도 업데이트됩니다.  
  
     지정된 서버 인스턴스에서 미러링 상태 기록을 보기 위해 시스템 관리자는 **상태** 페이지에서 서버 인스턴스에 대한 **기록** 단추를 클릭할 수도 있습니다. **데이터베이스 미러링 기록** 대화 상자에 기록이 표시됩니다. 여기서 시스템 관리자는 서버 인스턴스의 상태 테이블에 있는 일부 또는 모든 행을 볼 수 있습니다.  
  
     **상태** 페이지 메트릭에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "데이터베이스 미러링 모니터"에 표시되는 성능 메트릭을 참조하세요.  
  
-   **sp_dbmmonitorresults**사용  
  
     시스템 관리자는 **sp_dbmmonitorresults** 시스템 저장 프로시저를 사용하여 상태 테이블을 볼 수 있으며 이전 15초 내에 업데이트되지 않은 경우 필요에 따라 업데이트할 수 있습니다. 이 프로시저는 **sp_dbmmonitorupdate** 프로시저를 호출한 다음 프로시저 호출에서 요청된 양에 따라 기록 행을 하나 이상 반환합니다. 결과 집합의 상태에 대한 자세한 내용은 [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)을 참조하세요.  
  
#### <a name="monitoring-database-mirroring-status-by-dbmmonitor-members"></a>데이터베이스 미러링 상태 모니터링(dbm_monitor 멤버가 사용하는 경우)  
 앞에서 설명한 것처럼 **sp_dbmmonitorupdate** 는 처음 실행될 때 **msdb** 데이터베이스에 **dbm_monitor** 고정 데이터베이스 역할을 만듭니다. **dbm_monitor** 고정 데이터베이스 역할의 멤버는 데이터베이스 미러링 모니터 또는 **sp_dbmmonitorresults** 저장 프로시저를 사용하여 기존 미러링 상태를 볼 수 있습니다. 그러나 이러한 사용자는 상태 테이블을 업데이트할 수 없습니다. 표시되는 상태의 수명을 알아보려면 사용자가 **상태** 페이지에서 **보안 주체 로그 (***\<시간>***)** 및 **미러 로그 (***\<시간>***)** 레이블의 시간을 확인하면 됩니다.  
  
 **dbm_monitor** 고정 데이터베이스 역할의 멤버는 **데이터베이스 미러링 모니터 작업** 을 사용하여 정기적으로 상태 테이블을 업데이트합니다. 작업이 없거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 중지된 경우 상태가 점점 유효하지 않게 되어 미러링 세션의 구성을 더 이상 반영할 수 없습니다. 예를 들어 장애 조치(failover) 후에 파트너가 동일한 역할(주 서버 또는 미러 서버)을 공유하는 것으로 표시되거나 현재 주 서버가 미러 서버로 표시되고 현재 미러 서버가 주 서버로 표시될 수 있습니다.  
  
#### <a name="dropping-the-database-mirroring-monitor-job"></a>데이터베이스 미러링 모니터 작업 삭제  
 데이터베이스 미러링 모니터 작업인 **데이터베이스 미러링 모니터 작업**은 삭제할 때까지 유지됩니다. 시스템 관리자가 모니터링 작업을 관리해야 합니다. **데이터베이스 미러링 모니터 작업**을 삭제하려면 **sp_dbmmonitordropmonitoring**을 사용합니다. 자세한 내용은 [sp_dbmmonitordropmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)을 참조하세요.  
  
###  <a name="perf_metrics_of_dbm_monitor"></a> 데이터베이스 미러링 모니터에 표시되는 상태  
 데이터베이스 미러링 모니터의 **상태** 페이지에는 파트너에 대한 설명과 미러링 세션의 상태가 표시됩니다. 상태에는 장애 조치를 완료하는 데 필요한 시간과 세션이 아직 동기화되지 않은 경우 데이터 손실 가능성을 예상하는 데 도움이 되는 기타 정보와 트랜잭션 로그 상태 같은 성능 메트릭이 포함됩니다. 또한 **상태** 페이지에는 미러링 세션의 상태와 일반적인 정보가 표시됩니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 모니터와 **상태** 페이지에 대한 소개는 이 항목의 앞부분에 나오는 [데이터베이스 미러링 상태 모니터링 도구](#tools_for_monitoring_dbm_status)를 참조하세요.  
  
 다음 섹션에서는 각각에 대해 제공된 내용에 대해 간략하게 설명합니다.  
  
#### <a name="partners"></a>파트너  
 **상태** 페이지에는 각 파트너에 대해 다음 정보가 표시됩니다.  
  
-   서버 인스턴스  
  
     **상태** 행에 해당 상태가 표시되는 서버 인스턴스의 이름입니다.  
  
-   현재 역할  
  
     서버 인스턴스의 현재 역할입니다. 가능한 상태는 다음과 같습니다.  
  
    -   주 서버  
  
    -   미러  
  
-   미러링 상태  
  
     가능한 상태는 다음과 같습니다.  
  
    -   Unknown  
  
    -   동기화 중  
  
    -   동기화됨  
  
    -   일시 중지됨  
  
    -   연결 끊김  
  
-   미러링 모니터 서버 연결  
  
     미러링 모니터 서버의 연결 상태입니다. 가능한 상태는 다음과 같습니다.  
  
    -   Unknown  
  
    -   연결됨  
  
    -   연결 끊김  
  
#### <a name="log-on-the-principal-server"></a>주 서버의 로그  
 **상태** 페이지에는 표시된 시간을 기준으로 주 서버의 로그 상태에 대해 다음 정보가 표시됩니다.  
  
-   보내지 않은 로그  
  
     Send Queue에서 대기 중인 로그의 양(KB)입니다.  
  
-   보내지 않은 가장 오래된 트랜잭션  
  
     Send Queue에 있는 보내지 않은 가장 오래된 트랜잭션의 보존 기간입니다. 이 트랜잭션의 보존 기간은 트랜잭션이 미러 서버 인스턴스에 전송되지 않은 채로 경과된 시간(분)을 나타냅니다. 이 값은 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 됩니다.  
  
-   로그 전송 예상 시간  
  
     주 서버 인스턴스에서 현재 전송 속도를 기반으로 현재 Send Queue에 있는 로그를 미러 서버로 보내는 데 필요한 예상 시간(분)입니다. 로그 전송 실제 시간은 다양하게 나타날 수 있는 들어오는 트랜잭션 속도의 영향을 받습니다. 그러나 **로그 전송 예상 시간** 값은 수동 장애 조치(failover)에 필요한 대략적인 시간을 예상하는 데 유용할 수 있습니다.  
  
-   현재 전송 속도  
  
     트랜잭션이 미러 서버 인스턴스로 전송되는 속도(KB/초)입니다.  
  
-   현재 새 트랜잭션의 속도  
  
     들어오는 트랜잭션이 주 서버의 로그에 들어오는 속도(KB/초)입니다. 미러링 속도가 늦는지, 보통인지 또는 빠른지를 확인하려면 이 값을 **로그 전송 예상 시간** 값과 비교합니다.  
  
#### <a name="log-on-the-mirror-server"></a>미러 서버의 로그  
 **상태** 페이지에는 표시된 시간을 기준으로 미러 서버의 로그 상태에 대해 다음 정보가 표시됩니다.  
  
-   복원되지 않은 로그  
  
     Redo Queue에서 대기 중인 로그의 양(KB)입니다.  
  
-   로그 복원 예상 시간  
  
     현재 Redo Queue에 있는 로그를 미러 데이터베이스에 적용하는 데 필요한 대략적인 시간(분)입니다.  
  
-   현재 복원 속도  
  
     트랜잭션이 미러 데이터베이스로 복원되는 속도(KB/초)입니다.  
  
#### <a name="mirroring-session"></a>미러링 세션  
 또한 **상태** 페이지에는 미러링 세션에 대해 다음 정보가 표시됩니다.  
  
-   미러 커밋 오버헤드  
  
     트랜잭션당 평균 지연 시간(밀리초)입니다(보호 우선 모드에만 해당). 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다.  
  
-   현재 모든 로그 전송 및 복원 예상 시간  
  
     주 서버에서 커밋된 보내지 않은 모든 로그를 전송하고 현재 Redo Queue에 있는 모든 로그를 복원하는 데 필요한 예상 시간입니다. 전송과 복원이 병렬로 실행될 수 있으므로 이 예상 시간은 **로그 전송 예상 시간** 및 **로그 복원 예상 시간** 필드 값의 합계보다 작을 수 있습니다.  
  
-   미러링 모니터 서버 주소  
  
     미러링 모니터 서버 인스턴스의 네트워크 주소입니다. 이 주소 형식에 대한 자세한 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 참조하세요.  
  
-   운영 모드  
  
     데이터베이스 미러링 세션의 운영 모드입니다.  
  
    -   성능 우선(비동기)  
  
    -   자동 장애 조치(Failover)가 없는 보호 우선(동기)  
  
    -   자동 장애 조치(Failover)가 있는 보호 우선(동기)  
  
##  <a name="AdditionalSources"></a> 미러된 데이터베이스에 대한 추가 정보 원본  
 데이터베이스 미러링 모니터 서버와 dbmmonitor 저장 프로시저를 사용하여 미러된 데이터베이스를 모니터링하고 모니터링된 성능 변수에 대해 경고를 설정하는 것 외에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 카탈로그 뷰, 성능 카운터 및 데이터베이스 미러링 이벤트 알림을 제공합니다.  
  
 **섹션 내용**  
  
-   [데이터베이스 미러링 메타데이터](#DbmMetadata)  
  
-   [데이터베이스 미러링 성능 카운터](#DbmPerfCounters)  
  
-   [데이터베이스 미러링 이벤트 알림](#DbmEventNotif)  
  
###  <a name="DbmMetadata"></a> 데이터베이스 미러링 메타데이터  
 각 데이터베이스 미러링 세션은 다음 카탈로그 또는 동적 관리 뷰에 표시된 메타데이터에 설명되어 있습니다.  
  
-   **sys.database_mirroring**  
  
     이 뷰는 서버 인스턴스의 미러된 각 데이터베이스에 대한 데이터베이스 미러링 메타데이터를 표시합니다. 자세한 내용은 [sys.database_mirroring&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)을 참조하세요.  
  
-   **sys.database_mirroring_endpoints**  
  
     **sys.database_mirroring_endpoints** 카탈로그 뷰는 서버 인스턴스의 데이터베이스 미러링 엔드포인트에 대한 정보를 표시합니다. 자세한 내용은 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)를 참조하세요.  
  
-   **sys.database_mirroring_witnesses**  
  
     이 카탈로그 뷰는 서버 인스턴스가 미러링 모니터인 각 세션의 데이터베이스 미러링 메타데이터를 표시합니다. 자세한 내용은 [sys.database_mirroring_witnesses&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)를 참조하세요.  
  
-   **sys.dm_db_mirroring_connections**  
  
     이 동적 관리 뷰는 각 데이터베이스 미러링 네트워크 연결에 대해 하나의 행을 반환합니다.  
  
     자세한 내용은 [sys.dm_db_mirroring_connections&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)를 참조하세요.  
  
###  <a name="DbmPerfCounters"></a> 데이터베이스 미러링 성능 카운터  
 성능 카운터를 사용하면 데이터베이스 미러링 성능을 모니터링할 수 있습니다. 예를 들어 **Transaction Delay** 카운터를 사용하면 데이터베이스 미러링이 주 서버의 성능에 영향을 주는지 여부를 알 수 있고 **Redo Queue** 와 **Log Send Queue** 카운터를 사용하면 미러 데이터베이스가 주 데이터베이스와 동기화가 제대로 이루어지는지 알 수 있습니다. **Log Bytes Sent/sec** 카운터를 사용하면 초당 보낸 로그의 양을 모니터링할 수 있습니다.  
  
 각 파트너의 성능 모니터에서 성능 카운터는 데이터베이스 미러링 성능 개체(**SQLServer:Database Mirroring**)에서 사용할 수 있습니다. 자세한 내용은 [SQL Server, Database Mirroring Object](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)을(를) 참조하세요.  
  
 **성능 모니터를 시작하려면**  
  
-   [시스템 모니터 시작&#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
###  <a name="DbmEventNotif"></a> 데이터베이스 미러링 이벤트 알림  
 이벤트 알림은 특별한 종류의 데이터베이스 개체입니다. 이벤트 알림은 다양한 Transact-SQL DDL(데이터 언어 정의) 문과 SQL 추적 이벤트에 대한 응답으로 실행되며 서버 및 데이터베이스 이벤트에 대한 정보를 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스로 보냅니다.  
  
 데이터베이스 미러링에 대해 사용할 수 있는 이벤트는 다음과 같습니다.  
  
-   **Database Mirroring State Change** 이벤트 클래스  
  
     미러된 데이터베이스의 미러링 상태가 변경되었음을 나타냅니다. 자세한 내용은 [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)을 참조하세요.  
  
-   **Audit Database Mirroring Login** 이벤트 클래스  
  
     데이터베이스 미러링 전송 보안과 관련된 감사 메시지를 보고합니다. 자세한 내용은 [Audit Database Mirroring Login Event Class](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [미러된 데이터베이스의 상태 보기&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
 **저장 프로시저**  
  
-   [sp_dbmmonitoraddmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [서버 이벤트용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
