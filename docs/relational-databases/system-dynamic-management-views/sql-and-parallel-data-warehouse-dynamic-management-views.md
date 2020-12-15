---
description: SQL 및 병렬 데이터 웨어하우스 동적 관리 뷰
title: SQL 및 병렬 데이터 웨어하우스 동적 관리 뷰
ms.custom: seo-dt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: e1735fa9e8b8ad6a85648b21aab1ba9aa21062b2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466884"
---
# <a name="sql-and-parallel-data-warehouse-dynamic-management-views"></a>SQL 및 병렬 데이터 웨어하우스 동적 관리 뷰
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

이 항목에서는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dmv (동적 관리 뷰)를 나열 합니다.  
  
 모든 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dmv는 **sys.dm_pdw** 로 시작 합니다.  
  
## <a name="sssdw-and-sspdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 동적 관리 뷰  
 다음 동적 관리 뷰는 및에 모두 적용 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
 [Transact-sql&#41;sys.dm_pdw_dms_cores &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_dms_external_work &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_dms_workers &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_errors &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_exec_connections &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_exec_requests &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_exec_sessions &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_hadoop_operations &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_lock_waits &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_nodes &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_nodes_database_encryption_keys &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_os_threads &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_request_steps &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_resource_waits &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_sql_requests &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_sys_info &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_wait_stats &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_waits &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)

## <a name="sssdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 동적 관리 뷰 
 다음 동적 관리 뷰는에만 적용 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .
 
[Transact-sql&#41;sys.dm_pdw_nodes_exec_query_plan &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-plan-transact-sql.md)  

[Transact-sql&#41;sys.dm_pdw_nodes_exec_query_profiles &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-profiles-transact-sql.md)  

[Transact-sql&#41;sys.dm_pdw_nodes_exec_query_statistics_xml &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-statistics-xml-transact-sql.md)  

[sys.dm_pdw_nodes_exec_sql 텍스트 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-sql-text-transact-sql.md)  

[Transact-sql&#41;sys.dm_pdw_nodes_exec_text_query_plan &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-text-query-plan-transact-sql.md)

 [transact-sql&#41;sys.dm_workload_management_workload_groups_stats &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) (미리 보기)

## <a name="sspdw-dynamic-management-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 동적 관리 뷰  
 다음 동적 관리 뷰는에만 적용 됩니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
 [Transact-sql&#41;sys.dm_pdw_component_health_active_alerts &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_component_health_alerts &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_component_health_status &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_diag_processing_stats &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-diag-processing-stats-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_network_credentials &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_node_status &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-node-status-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_os_event_logs &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_os_performance_counters &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_query_stats_xe &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-transact-sql.md)  
  
 [Transact-sql&#41;sys.dm_pdw_query_stats_xe_file &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-file-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
