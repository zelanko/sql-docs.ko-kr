---
title: 시스템 뷰를 사용 하 여 모니터링
description: 이 문서에서는 분석 플랫폼 시스템 어플라이언스를 모니터링 하는 데 사용할 수 있는 시스템 뷰를 나열 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1979d5e698747e6104f7e743108cc1553de702e5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400951"
---
# <a name="monitor-the-appliance-with-system-views---analytics-platform-system"></a>시스템 뷰-분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링
이 문서에서는 SQL Server PDW를 모니터링 하는 데 사용할 수 있는 시스템 뷰를 나열 합니다.  
  
## <a name="to-monitor-the-appliance-by-using-system-views"></a>시스템 뷰를 사용 하 여 어플라이언스를 모니터링 하려면  
SQL Server PDW에는 어플라이언스 상태, 상태 및 성능에 대 한 자세한 정보를 얻을 수 있는 포괄적인 시스템 뷰가 포함 되어 있습니다. 이 표에서는 각 모니터링 기능에 사용할 수 있는 시스템 뷰에 대 한 링크를 제공 합니다.  
  
![PDW 시스템 뷰 경고](./media/monitor-the-appliance-by-using-system-views/PDW_system_views_alerts.png "PDW_system_views_alerts")  
  
|||  
|-|-|  
|**Information Type**|**관련 시스템 뷰**|  
|기기의 전체 상태|[sys. dm_pdw_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)|  
|경고|[sys.pdw_health_alerts](../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)|  
|어플라이언스 구성 요소 및 해당 상태|[sys.pdw_health_component_groups](../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)<br /><br />[sys.pdw_health_components](../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)<br /><br />[sys.pdw_health_component_properties](../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)<br /><br />[sys.pdw_health_component_status_mappings](../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)<br /><br />[sys. dm_pdw_nodes](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)|  
|요청 모니터링 (쿼리, 로드, 백업 및 복원 포함)|[sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)<br /><br />[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)<br /><br />[sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)<br /><br />[sys. dm_pdw_sql_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)<br /><br />[sys. dm_pdw_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)<br /><br />[sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)<br /><br />[sys. dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)<br /><br />[sys. pdw_distributions](../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)|  
|로드, 백업 및 복원에 대 한 추가 정보를 모니터링 합니다.|[sys. pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)<br /><br />[sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)<br /><br />[sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)|  
|OS 수준 로그 및 성능 정보|[sys.dm_pdw_os_performance_counters](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)<br /><br />[sys.dm_pdw_os_event_logs](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)<br /><br />[sys. dm_pdw_os_threads](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)|  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
