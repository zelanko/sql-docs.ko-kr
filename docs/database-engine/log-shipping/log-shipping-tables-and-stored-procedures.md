---
title: "로그 전달 테이블 및 저장 프로시저 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- secondary servers [SQL Server]
- monitor servers [SQL Server]
- log shipping [SQL Server], system tables
- log shipping [SQL Server], stored procedures
- primary servers [SQL Server]
ms.assetid: 03420810-4c38-4c0c-adf0-913eb044c50a
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4021966a60d51ad5a622f127f9c3d26d477d4ab8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="log-shipping-tables-and-stored-procedures"></a>로그 전달 테이블 및 저장 프로시저
  이 항목에서는 로그 전달 구성과 관련된 모든 테이블과 저장된 프로시저에 대해 설명합니다. 모든 로그 전달 테이블은 각 서버의 **msdb** 에 저장됩니다. 아래의 표에서는 로그 전달 구성에서 서버에 사용된 테이블 및 저장 프로시저를 설명합니다.  
  
## <a name="primary-server-tables"></a>주 서버 테이블  
  
|테이블|설명|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)|경고 작업 ID를 저장합니다. 이 테이블은 원격 모니터 서버가 구성되지 않았으면 주 서버에서만 사용됩니다.|  
|[log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)|이 주 서버와 관련된 로그 전달 작업에 대한 오류 정보를 저장합니다.|  
|[log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)|이 주 서버와 관련된 로그 전달 작업에 대한 기록 세부 정보를 저장합니다.|  
|[log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)|이 주 데이터베이스에 대한 하나의 모니터 레코드를 저장합니다.|  
|[log_shipping_primary_databases](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)|지정된 서버의 주 데이터베이스에 대한 구성 정보를 포함합니다. 주 데이터베이스마다 한 행을 저장합니다.|  
|[log_shipping_primary_secondaries](../../relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql.md)|주 데이터베이스를 보조 데이터베이스로 매핑합니다.|  
  
## <a name="primary-server-stored-procedures"></a>주 서버 저장 프로시저  
  
|저장 프로시저|설명|  
|----------------------|-----------------|  
|[sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)|백업 작업, 로컬 모니터 레코드 및 원격 모니터 레코드를 포함하여 로그 전달 구성에 대한 주 데이터베이스를 설정합니다.|  
|[sp_add_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md)|기존 주 데이터베이스에 보조 데이터베이스 이름을 추가합니다.|  
|[sp_change_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)|로컬 및 원격 모니터 레코드를 포함하여 주 데이터베이스 설정을 변경합니다.|  
|[sp_cleanup_log_shipping_history](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)|보존 기간을 기준으로 로컬과 모니터에서 기록을 정리합니다.|  
|[sp_delete_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)|로컬 및 원격 기록과 백업 작업을 포함하여 주 데이터베이스의 로그 전달을 제거합니다.|  
|[sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md)|주 데이터베이스에서 보조 데이터베이스 이름을 제거합니다.|  
|[sp_help_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)|주 데이터베이스 설정을 검색하고 **log_shipping_primary_databases** 및 **log_shipping_monitor_primary** 테이블의 값을 표시합니다.|  
|[sp_help_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)|주 데이터베이스의 보조 데이터베이스 이름을 검색합니다.|  
|[sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)|지정된 로그 전달 에이전트에 대한 최신 정보로 새로 고칩니다.|  
  
## <a name="secondary-server-tables"></a>보조 서버 테이블  
  
|테이블|설명|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)|경고 작업 ID를 저장합니다. 이 테이블은 원격 모니터 서버가 구성되지 않았으면 보조 서버에서만 사용됩니다.|  
|[log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)|이 보조 서버와 관련된 로그 전달 작업에 대한 오류 정보를 저장합니다.|  
|[log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)|이 보조 서버와 관련된 로그 저장 작업에 대한 기록 세부 정보를 저장합니다.|  
|[log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)|이 보조 서버와 관련된 보조 데이터베이스마다 하나의 모니터 레코드를 저장합니다.|  
|[log_shipping_secondary](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)|지정된 서버의 보조 데이터베이스에 대한 구성 정보를 포함합니다. 보조 ID마다 한 행을 저장합니다.|  
|[log_shipping_secondary_databases](../../relational-databases/system-tables/log-shipping-secondary-databases-transact-sql.md)|지정된 보조 데이터베이스에 대한 구성 정보를 저장합니다. 보조 데이터베이스마다 한 행을 저장합니다.|  
  
> [!NOTE]  
>  지정된 주 데이터베이스에 대한 동일한 보조 서버의 보조 데이터베이스는 **log_shipping_secondary** 테이블의 설정을 공유합니다. 하나의 보조 데이터베이스에 대한 공유 설정이 변경되면 모든 보조 데이터베이스에 대한 설정이 변경됩니다.  
  
## <a name="secondary-server-stored-procedures"></a>보조 서버 저장 프로시저  
  
|저장 프로시저|설명|  
|----------------------|-----------------|  
|[sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)|로그 전달에 대한 보조 데이터베이스를 설정합니다.|  
|[sp_add_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql.md)|지정된 주 데이터베이스에 대한 보조 서버에서 주 정보를 설정하고, 로컬 및 원격 모니터 링크를 추가하며, 복사본을 만들고 작업을 복원합니다.|  
|[sp_change_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)|로컬 및 원격 모니터 레코드를 포함하여 보조 데이터베이스 설정을 변경합니다.|  
|[sp_change_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-primary-transact-sql.md)|원본 및 대상 디렉터리와 파일 보존 기간 같은 보조 데이터베이스 설정을 변경합니다.|  
|[sp_cleanup_log_shipping_history](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)|보존 기간을 기준으로 로컬과 모니터에서 기록을 정리합니다.|  
|[sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)|보조 데이터베이스, 로컬 기록 및 원격 기록을 제거합니다.|  
|[sp_delete_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-primary-transact-sql.md)|보조 서버에서 지정한 주 서버에 대한 정보를 제거합니다.|  
|[sp_help_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)|**log_shipping_secondary**, **log_shipping_secondary_databases**및 **log_shipping_monitor_secondary** 테이블에서 보조 데이터베이스 설정을 검색합니다.|  
|[sp_help_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)|이 저장 프로시저는 보조 서버에서 지정된 주 데이터베이스의 설정을 검색합니다.|  
|[sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)|지정된 로그 전달 에이전트에 대한 최신 정보로 새로 고칩니다.|  
  
## <a name="monitor-server-tables"></a>모니터 서버 테이블  
  
|테이블|설명|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)|경고 작업 ID를 저장합니다.|  
|[log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)|로그 전달 작업에 대한 오류 정보를 저장합니다.|  
|[log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)|로그 전달 작업에 대한 기록 세부 정보를 저장합니다.|  
|[log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)|이 모니터 서버와 관련된 주 데이터베이스마다 하나의 모니터 레코드를 저장합니다.|  
|[log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)|이 모니터 서버와 관련된 보조 데이터베이스마다 하나의 모니터 레코드를 저장합니다.|  
  
## <a name="monitor-server-stored-procedures"></a>모니터 서버 저장 프로시저  
  
|저장 프로시저|설명|  
|----------------------|-----------------|  
|[sp_add_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql.md)|로그 전달 경고 작업이 아직 생성되지 않았으면 하나를 생성합니다.|  
|[sp_delete_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)|관련된 주 데이터베이스가 없으면 로그 전달 경고 작업을 제거합니다.|  
|[sp_help_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql.md)|경고 작업의 작업 ID를 반환합니다.|  
|[sp_help_log_shipping_monitor_primary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)|**log_shipping_monitor_primary** 테이블에서 지정한 주 데이터베이스에 대한 모니터 레코드를 반환합니다.|  
|[sp_help_log_shipping_monitor_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)|**log_shipping_monitor_secondary** 테이블에서 지정한 보조 데이터베이스에 대한 모니터 레코드를 반환합니다.|  
  
  
