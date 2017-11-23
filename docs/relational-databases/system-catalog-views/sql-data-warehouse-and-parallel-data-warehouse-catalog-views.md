---
title: "SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
caps.latest.revision: "5"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a88d2a82ec01c51fce68340fb7570b47f7d21922
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-data-warehouse-and-parallel-data-warehouse-catalog-views"></a>SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  이 항목에서는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 카탈로그 뷰.  
  
 모든 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 카탈로그 뷰 시작 **sys.pdw**합니다.  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 카탈로그 뷰  
 다음 카탈로그 뷰는 둘 다에 적용 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
 [sys.pdw_column_distribution_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [sys.pdw_database_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [sys.pdw_distributions &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [sys.pdw_index_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_dictionaries &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_row_groups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_segments &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [sys.pdw_nodes_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [sys.pdw_nodes_indexes &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [sys.pdw_nodes_partitions &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [sys.pdw_nodes_pdw_physical_databases &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [sys.pdw_nodes_tables &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state(Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [sys.pdw_table_distribution_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [sys.pdw_table_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)  
  
## <a name="includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]카탈로그 뷰  
 다음 카탈로그 뷰를 적용할 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 만:  
  
 [sys.pdw_diag_event_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [sys.pdw_diag_events &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [sys.pdw_diag_sessions &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [sys.pdw_health_alerts &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [sys.pdw_health_component_groups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [sys.pdw_health_component_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [sys.pdw_health_component_status_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [sys.pdw_health_components &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
